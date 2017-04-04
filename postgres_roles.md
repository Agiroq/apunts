ROLS I USUARIS
==============



```sql
CREATE USER [name] PASSWORD 'xxxx'; 	-- crea un usuari nou
DROP USER [name];			-- elimina usuari
CREATE DATABASE [name] WITH OWNER [user];-- crea una db amb propierai
```
 + Per conectar a una base de dades amb propietari com ho fem normalment haríem de crear un usuar UNIX. 
Per conectarnos quant aquest no existeix a UNIX:
_l'usuari necessita tenir 1 o més permisos en aquesta BD_
```sql
psql -U [usuari] -h 127.0.0.1 [db]
```

## LListar usuaris i roles:   
```sql
\du     --llita tots els usuaris
SELECT * FROM pg_shadow; --usuaris amb capacitat de conecció
\dp     --mostra els privilegis asignats a lestaules 
```  
 
## Atributs dels roles


 **Asignem atributs que volem assignar**
```sql
ALTER ROLE [name] WITH [opcio1] [opcio2] ...;
```
 **Treiem  atributs als ROLES**
```sql
ALTER ROLE [name] WITH NO[opcio1] NO[opció2] ...;
                       |--------| |--------|
                        una sola paraula
```
 + **LOGIN**
Quan creem un USER és el mateix que crear un rol amb LOGIN o asignar-l'hi ho:  
```sql 
CREATE ROLE [name] LOGIN; -- = CREATE USER [name];
ALTER ROLE [name] WITH LOGIN;
```

 + **SUPERUSER**
**No és aconsellable crear superusuaris**
```sql
CREATE ROLE [name] SUPERUSER;
ALTER ROLE [name] WITH SUPERUSER;
```

 + **CREATEDB**
crear noves bases de daades

```sql 
CREATE ROLE [name] CREATEDB;
ALTER ROLE [name] WITH CREATEDB;
```

 +  **CREATEROLE**


```sql 
CREATE ROLE [name] CREATEROLE;
ALTER ROLE [name] WITH CREATEROLE;
```

 + **PASSWORD**
Fan servir md5

```sql 
CREATE ROLE [name] PASSWORD 'xxxx';
ALTER ROLE [name] PASSWORD 'xxxx';
```

## Privilegis

 * OWNER te tots els permisos per a una DB 
 
  tipus | de  | privilegis 
  ---|---|---
  CREATE | DELETE | TRUNCATE
  SELECT | INSERT | UPDATE
  REFERENCES |TRIGGER | CONNECT
  TEMPORARY | EXECUTE |USAGE
   
 
Per assignar privilegis;
```sql
GRANT [privilegi] ON [taula] TO [usuari]; -- permisos a taula
GRANT ALL PRIVILEGES ON DATABASE [taula] TO [user];
```
## Grups

Un cop tenim un rol creat aquest es pot usar com a grup.
El que fem quan asignem un "usuari" a un "grup":

```sql
GRANT [grup] TO [role];		--
```
 > _El que no es permet és crear herències cicliques  (grup->role->grup)._  

Per treurel del grup
```sql
REVOQUE [grup] TO [role];	--
```
#### restringir herències
Si volem que un rol no hereti dels altres fem servir **INHERIT |NOINHERIT**
```sql
CREATE ROLE [roleX] NOINHERIT; --aquest rol no hereterà de cap altre rol
GRANT [role] TO [roleX];	-- roleX forma part del grup role, però no hereta els seus privilegis
```

Si volem __restringir__ els permisos d'un role a algun dels roles dels que hereda:
```sql
SET ROLE [grup];	--assigna temporalment privilegis d'un grup al que pertany
```
Per anular la restricció temporal
```sql
SET ROLE joe;
SET ROLE NONE;
RESET ROLE;
```




 