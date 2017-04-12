# SCHEMAS

És el contenedor de taulas, un esquemes està format per :

 + Vistas
 + Índices
 + sequencias
 + tipos de datos
 + operadores
 + Funnciones
 
 > Normalmente se trabaja con el esquema public o un esquema para una nueva base de datos
 
 crear un schema nou:
 
 ```sql
  CREATE SCHEMA [name];
 ```
 Important donar pemisos a esquemes per als roles que hi hagin de interactuar

 ```sql
GRANT USAGE ON SCHEMA nombreschema TO nombrerole;
GRANT CREATE ON SCHEMA nombreschema TO nombrerole;
 ```
 Per crear una taula en un esquema
 ```sql
CREATE TABLE miscschema.mitabla (..);
 ```
 A partir d'ara quan volem accedir a una taula necessitem dir-li l'esquema al davant `nom_esquema.nom_taula`

 Modificar esquemes
 ```sql
 ALTER SCHEMA [esquema] RENAME TO [nou_esquema];
 DROP SCHEMA [esquema];
 ```
 Per canviar una taula d'esquema
 ```sql
ALTER TABLE [esquema].[taula] SET SCHEMA [nou_esquema];
 ```
# TABLESPACES

Abans de començar necessitem donar permisos a postgres a la carpeta

```bash
sudo mkdir /path
sudo chown postgres:postgres /path/to/directory
```
```sql
CREATE TABLESPACE [nom_tablespace] OWNER postgres LOCATION `/path/to/directory’;
```
per crear una taula en un tablespace especific:
```sql
CREATE TABLE [taula] (...) TABLESPACE [space1];
```

