DB COMMANNDS
============
***
```sql
CREATE DATABASE [name]; -- crear DB
```
DROP DATABASE [name]; 	-- eliminar DB
```sql
\c [name]		-- connectar a [name]
```
```sql
\d 			-- Mostrar taules
```
_importar script_
```sql
\i [path]		-- *importar* script
```

TABLES COMMANDS
===============
***
```sql
\d [table]		-- *mostra atributs* de la taula
```
_Crear taula_
```sql
CREATE TABLE [nom] ([atribut] serial,  		/* Serial és tipus numeric autoincremental 		      */
		    [atr2] varchar(20),		/* Els atributs poden ser de tipus integer, float, varchar... */
		    [atr3] float not null,      /* NOT NULL no deja que el campo quede vacío		      */
		    primary key([atribut]));	
```

_insertar tupla_ 
```sql
INSERT INTO [taula] (atr1, atr2, ...) VALUES ([atr1], [atr2], ...); 	-- *insertar* nova tupla
INSERT INTO [taula] VALUES ([atr1],[atr2],...) 			-- *insertar tupla
```
_Seleccionar_
```sql
SELECT * FROM [table];			-- mostra *totes* les entrades *tots* els atributs de [taula]
SELECT [atr1], [atr2], ... FROM [table];	-- *mostra només* [atr1], [atr2], ... de totes les tuples de [taula]
SELECT * FROM [taula] WHERE [atr][=|>|<|<=|>=|<>][value] -- mostra nomes els que compleixen la *condició*
```
_borrar registres_
```sql
DELETE FROM [table] WHERE [atr][=|>|<|<=|>=|<>][value];	-- Sobretot no oblidar *WHERE*
```
_editar registres_
```sql
UPDATE [tablbe] SET [atr]=[value] WHERE [atr]=[value];
```
_afegir comentaris_
```sql
SELECT * FROM [table]; --Comentari a mostrar
SELECT * FROM /*Comentari del codi*/ [table];
```
	
				




