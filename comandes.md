DB COMMANNDS
============
```sql
CREATE DATABASE [name]; -- crear DB
```
DROP DATABASE [name];   -- eliminar DB
```sql
\c [name]		-- connectar a [name]
```
```sql
\d                      -- Mostrar taules
```
* **importar script**
```sql
\i [path]		-- *importar* script
```

TABLE COMMANDS
===============

```sql
\d [table]		-- *mostra atributs* de la taula
```
* **Crear taula**
```sql
CREATE TABLE [nom] ([atribut] [type] [*modifiers*],
		    ...,
		    primary key([atribut]));--defineix atribut pKey	
```
```postgres
CREATE TABLE [nom] (id serial,		/* exemple amb modificadors */	 
		    titol varchar(30),
		    autor NOT NULL DEFAULT 'desconocido',
		    editoraial varchar(20),
		    PRIMARY KEY(id);
```

* **insertar tupla** 
```sql
INSERT INTO [taula] (atr1, atr2, ...) VALUES ([atr1], [atr2], ...); 	-- *insertar* nova tupla
INSERT INTO [taula] VALUES ([atr1],[atr2],...) 				-- insertar tupla
INSERT INTO [taula] ([atr], [atr_amb_default],..) VALUES ([value], default, ...); --insertar quan hi ha un valor **default**
```
* **Seleccionar**
```sql
SELECT * FROM [table];			-- mostra *totes* les entrades *tots* els atributs de [taula]
SELECT [atr1], [atr2], ... FROM [table];	-- *mostra només* [atr1], [atr2], ... de totes les tuples de [taula]
SELECT * FROM [taula] WHERE [atr][comparador][value] -- mostra nomes els que compleixen la *condició*
SELECT [atr] AS [nou nom] FROM [taula]; --AS canvia el nom d'atribut al mostrar-lo
```
* **borrar registres**
```sql
DELETE FROM [table] WHERE [atr][=|>|<|<=|>=|<>][value];	-- Sobretot no oblidar *WHERE*
```
* **editar registres**
```sql
UPDATE [tablbe] SET [atr]=[value] WHERE [atr]=[value];
```
* **afegir comentaris**
```sql
SELECT * FROM [table]; --Comentari a mostrar
SELECT * FROM /*Comentari del codi*/ [table];
```
	
				
* **buidar taula**
```sql
TRUNCATE TABLE taula;
```
***

Alter
======
_agregar/borrar columna, cambiar nom, ..._
* **canvi de nom d'atribut**
```sql
ALTER TABLE [taula] RENAME COLUMN [nom_from] TO [nom_to]; --modifica el nom de l'atribut
```
* **elimina atribut**
```sql
ALTER TABLE [taula] DROP COLUMN [atr]; --borra un atribut
```
* **agrega un atribut**
```sql
ALTER TABLE [taula] ADD COLUMN [nom] [type]; -- agregar columna
```
* **valor per defecte**
```sql
ALTER TABLE [taula] ALTER COLUMN [atribut] SET DEFAULT [false];
```
___
**Tipus de dades**

+ boolean				_y/n, yes/no, 1/0, t/f, true/false_
+ integer				_enter_
+ serial 				_enter autoincremental_
+ float					_decimal_
+ character varyng(n), varchar(n) 	_longitud de 'n' caràcters_
+ character(n), char(n) 		_char de longitud 'n' obligatòria_
+ text, varchar				_longitud variable il.limitada_
___
**Modifiers**
PRIMARY KEY	*Clau Primaria*
NOT NULL	*No es pot deixar buit*
DEFAULT [value] *Valor per defecte*

___
**Comparadors**

= / <> _equal/not equal_
< / >  _less/more than_
<=/ >= _less or equal/more or equal than_
IS/IS NOT _per a valors NULL_

