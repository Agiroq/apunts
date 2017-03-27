___
POSTGRES BASICS [oficial documentation](https://www.postgresql.org/docs/9.1/static/index.html)
===============
___
DEFINITIONS
===========
### Tipus de dades

tipus | descripció
---|---
 **boolean**		  |  		_y/n, yes/no, 1/0, t/f, true/false_
**integer, int, int4**	|	_enter_
**smallint, int2**	    	|	_enter de fins a 5 digits (-32000/32000)_
**bigint, int8**		|	_desde (-9*10^17/9*10^17)_
**serial/bigserial**	|    		_enter autoincremental int/bigint_
**decimal/numeric(t,d)**	 |   	_**t**=total digits /**d**=total decimalsprecisión_
**float**			   | 	_decimal fins a 6 decimals_
**double precision**	 |   		_decimal fins a 15 xifres_
**character varyng(n), varchar(n)** | 	_longitud de 'n' caràcters_
**character(n), char(n)** 	  |  	_char de longitud 'n' obligatòria_
**text, varchar**	|		_longitud variable il.limitada_
**date** 'YYYY-MM-DD'	 |		_desde 4317A.C. fins 32767D.C._
**date** 'YYYY-MM-DD'	 |		`SET DATETYPE 'European'`
|
**time** 	 'hh:mm:ss'	|	_guarda la hora_
**timestamp**  'YYYY-MM-DD hh:mm:ss' | _data i hora_
**timestamptz**  'YYYY-MM-DD hh:mm:ss±tz' |  	_data i hora *guardael TIME ZONE'*_
___
### Modifiers
` PRIMARY KEY	 `*Clau Primaria*
`NOT NULL	 `*No es pot deixar buit*
`UNIQUE          `*valor únic a la taula*
`DEFAULT [value] ` *Valor per defecte*
``

___
### Comparadors

operador | descripció
 --- | ---
 = / <> | _equal/not equal_
 < / > | _less/more than_
 <=/ >= |_less or equal/more or equal than_
 IS/IS NOT| _per a NULL !!!no usar lògics!!!_
___
### Operadors relacionals

operador | exemple
---|---
 AND	| WHERE [atr]=[value] AND [atr]=[value];
 OR		| WHERE [atr]=[value] AND IS NOT NULL;
 IN		| WHERE [atr] IN ([value], [value], ...);
IN | WHERE [atr] IN (SELECT [atr] FROM [table] WHERE [condición]);
 BETWEEN	| WHERE [atr] BETWEEN [x] AND [y];
___
### Operadors aritmetics
<<<<<<< HEAD

simbol | operacio | simbol |operació
---  | --- | --- | ---
 *     |multiplicació |    /  | divisió
 %     |modul 	       |        |
 +     |suma	       | -      | resta

### Funcions
**Concatenar cadenes**
```sql
SELECT ( [atr] || 'string' || [atr] ||...) AS [header_name] FROM [taula];
	      ----        ----
	    concatena    concat
```
**Funcions amb strings**
```sql
char_length([varchar]) 		/* length */
upper([string]) 		/* posar en majúscules */
lower([string])			/* posar en minúscules */
position( '[char]' IN [string] )/* char position in string */
```
**buscar en Strings**
```sql
SELECT * FROM [taula] WHERE [atr] LIKE '%Jos_';
%   /* de 0-x caracters */
_   /* només un caracter comodí */

```
**Aritmètiques**
```sql
SELECT count(*) FROM [taula] WHERE [condition];	_contar repeticions_
SELECT sum([atr]) FROM [taula];	_Suma valors_
... max([atr])...		_Valor màxim_
... max([atr])...		_valor mínim_
abs([num])			_valor absolut_
round([float])			_arrodoniment_
trunc([float])			_arrod. x truncament_
```
**Data i hora**
```sql
current_date; 	_data actual_
extract([day|week|month|...] from [timestamp]);
=======

simbol | operacio | simbol |operació
---  | --- | --- | ---
 *     |multiplicació |    /  | divisió
 %     |modul 	       |        |
 +     |suma	       | -      | resta

### Format de cadenes
```sql
SELECT ( [atr] || 'string' || [atr] ||...) AS [header_name] FROM [taula];
							----        ----
						concatena    concat
>>>>>>> origin/master
```

**Agrupar**
```sql
SELECT [atr], count(*) FROM [taula] GROUP BY [atr]; _count tuplas ordered by [atr]_
```
**Condicions a grups**
```sql  
SELECT count(*) FROM [taula] GROUP BY [atr_x] HAVING [[atr_X]|count(*)|...] [condició];
```

**Buscar elements sense repeticions**
```sql
SELECT DISTINCT [atr] FROM [taula];
```

### INDEX
 PRO: Permet trobar dades de manera més ràpida.
 CON: Major consum de l'espai i la inserció i borrat son més lens
 * *Primary key*
 * *Index*
 * *Unique index*

```sql
CREATE INDEX [ind_name] ON [table] ([atr]); -- agrega un indexat
```

``sql
CREATE UNIQUE INDEX [idx_name] ON [taula] ([atr]); --agrega idx únic
```

```sql
DROP INDEX [name];
```



DB COMMANNDS
============
**log to postgresql as postgres user**
```bash
sudo -u postgres psql
```

```sql
CREATE DATABASE [name]; crear DB
```

```sql
DROP DATABASE [name];   eliminar DB
```
```sql
\c [name]		connectar a [name]
```
```sql
\d               Mostrar taules
```
```sql
\i [path]		importar script
```

TABLE COMMANDS
===============

```sql
\d [table]		mostra atributs de la taula
```
**Crear taula**
```sql
CREATE TABLE [nom] ([atribut] [type] [*modifiers*],
				...,
				primary key([atr], [atr2]));--defineix atribut/s clau
```
```sql
CREATE TABLE [nom] (id serial,		/* exemple amb modificadors */
				titol varchar(30),
				autor NOT NULL DEFAULT 'desconocido',
				editoraial varchar(20),
				PRIMARY KEY(id);
```
**buidar taula**
```sql
TRUNCATE TABLE taula;
```
**insertar tupla**
```sql
INSERT INTO [taula] (atr1, atr2, ...) VALUES ([value1], [value2], ...); -- *insertar* nova tupla
INSERT INTO [taula] VALUES ([atr1],[atr2],...) 				-- insertar tupla
INSERT INTO [taula] ([atr], [atr_amb_default],..) VALUES ([value], default, ...); --insertar quan hi ha un valor **default**
```
**borrar registres**
```sql
DELETE FROM [table] WHERE [atr][=|>|<|<=|>=|<>][value];	-- Sobretot no oblidar *WHERE*
```
**editar registres**
```sql
UPDATE [table] SET [atr]=[value] WHERE [atr]=[value];
```
**afegir comentaris**
```sql
SELECT * FROM [table]; --Comentari a mostrar
SELECT * FROM /*Comentari del codi*/ [table];
```
**Seleccionar**
```sql
SELECT * FROM [table];			-- mostra *totes* les entrades *tots* els atributs de [taula]
SELECT [atr1], [atr2], ... FROM [table];	-- *mostra només* [atr1], [atr2], ... de totes les tuples de [taula]
SELECT * FROM [taula] WHERE [atr][comparador][value] -- mostra nomes els que compleixen la *condició*
SELECT [atr] AS [nou nom] FROM [taula]; --AS canvia el nom d'atribut al mostrar-lo
```
**Ordenar**
```sql
SELECT * FROM [taula] ORDER BY [atr] ASC, [atr] DESC;
```

***

[ALTER documentation](https://www.postgresql.org/docs/9.1/static/sql-altertable.html)
======
_agregar/borrar columna, cambiar nom, ..._

```sql
ALTER TABLE [taula] **action**
####actions
* **canvi de nom d'atribut**
```sql
... RENAME COLUMN [nom_from] TO [nom_to]; --modifica el nom de l'atribut
```
**elimina atribut**
```sql
... DROP COLUMN [atr]; --borra un atribut
```
**agrega un atribut**
```sql
... ADD COLUMN [nom] [type] ~ [modifier]; -- agregar columna
```
**valor per defecte**
```sql
... ALTER COLUMN [atribut] SET DEFAULT [false];
```
**definir primary key**
```sql
... ADD PRIMARY KEY ([atr]);
```
**eliminar primary key modifier**
```sql
... DROP CONSTRAINT nomTaula_pkey;
```
**definir/eliminar NOT NULL**
```sql
... [SET | DROP] NOT NULL;
```
**asignar restriccions a un atribut (CHECK)**
```sql
ALTER TABLE [taula] ADD CONSTRAINT [nom_restricció] CHECK ([atr][condició]);
```
___

Relacions
=========
**definir primary key**
```sql
ALTER TABLE [taula] ADD PRIMARY KEY ([atr]);
```
**eliminar primary key modifier**
```sql
ALTER TABLE [taula] DROP CONSTRAINT nomTaula_pkey;
```
**Crear una tabla con una foreign key**
```sql
CREATE TABLE [name](OrderID serial primary key, PersonID int,
/* asignem pkey */  PRIMARY KEY(OrderID),
/* definim fkey */  CONSTRAINT FK_PersonOrder FOREIGN KEY (PersonID) REFERENCES Persons(PersonID);
```
**Eliminar una foreign key**
```sql
ALTER TABLE [taula] DROP CONSTRAINT [nom_de_la_foreing_key];
```

**Agregar una foreing key a una taula**
```sql
ALTER TABLE [taula] ADD CONSTRAINT [name] FOREIGN KEY ([atr_fk]) REFERENCES [taula_origen] ([atr_origen]);
```

**Agregar restriccions**
```sql
ALTER TABLE [name] ADD CONSTRAINT [const_name] UNIQUE (columns);
```


### INNER JOIN
**Consulta entre taules relacionades**
```sql
SELECT * FROM [taula_principal] INNER JOIN [taula_connectada] ON [taula_pri].[atr]= [taula_conn].[atr];
SELECT [taula].[atr_ambigu], [atr] FROM [taula_principal] INNER JOIN [taula_connectada] ON [taula_pri].[atr]= [taula_conn].[atr];
	-----------------
	       |____atributs amb ambigüetats necessites definir en quina taula esta.
SELECT * FROM [taula_principal] INNER JOIN [taula_connectada] ON [taula_pri].[atr]= [taula_conn].[atr], INNER JOIN [taula]...;
```

### LEFT
```sql
SELECT [table].[atr], ... FROM [L_table] LEFT JOIN [R_table] ON [R_table].[FK]=[L_table].[PK]; 
```
### RIGHT
```sql
SELECT [table].[atr], ... FROM [L_table] RIGHT JOIN [R_table] ON [R_table].[FK]=[L_table].[PK]; 
```
### FULL OUTER
```sql
SELECT  [table].[atr], ... FROM [L_table] FULL JOIN [R_table] ON [R_table].[FK]=[L_table].[PK];
```
### CROSS JOIN [table_A]*[table_B]
```sql
SELECT * FROM [table_A] CROSS JOIN [table_B];
```
### UNION/UNION ALL
s'utilitza per fer consultes de varies consultes
NO/SI repeteix duplicats a la sortida !!!
```sql
SELECT * FROM [taula] UNION ~ALL SELECT * FROM [taula];
```	

VISTES
======
És com guardar una consulta a la cual e pot cridar més tard  

 * Ocultar informació a l'usuari
 * Aplica permisos/restriccions a les vistes
 * Millorar-ne el rendimen (automatitzar consultes).

## Vistes

**crear una vista**
```sql
CREATE VIEW [nom] AS SELECT ...; -- Crear una vista
```
**veure una vista**
```sql
SELECT * FROM [view];
```
**Borrar vista**
```sql
DROP VIEW [nom];
```

**Accions a les taules a través de la vista**
```sql
DELETE FROM [vista] WHERE [condició];
```

## Vistes materialitzades
A més a més, es guarden com a taula en la vase de dades


