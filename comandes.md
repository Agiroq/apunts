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
		    primary key([atr], [atr2]));--defineix atribut/s clau	
```
```postgres
CREATE TABLE [nom] (id serial,		/* exemple amb modificadors */	 
		    titol varchar(30),
		    autor NOT NULL DEFAULT 'desconocido',
		    editoraial varchar(20),
		    PRIMARY KEY(id);
```
* **buidar taula**
```sql
TRUNCATE TABLE taula;
```
* **insertar tupla** 
```sql
INSERT INTO [taula] (atr1, atr2, ...) VALUES ([atr1], [atr2], ...); 	-- *insertar* nova tupla
INSERT INTO [taula] VALUES ([atr1],[atr2],...) 				-- insertar tupla
INSERT INTO [taula] ([atr], [atr_amb_default],..) VALUES ([value], default, ...); --insertar quan hi ha un valor **default**
```

* **borrar registres**
```sql
DELETE FROM [table] WHERE [atr][=|>|<|<=|>=|<>][value];	-- Sobretot no oblidar *WHERE*
```
* **editar registres**
```sql
UPDATE [table] SET [atr]=[value] WHERE [atr]=[value];
```
* **afegir comentaris**
```sql
SELECT * FROM [table]; --Comentari a mostrar
SELECT * FROM /*Comentari del codi*/ [table];
```
* **Seleccionar**
```sql
SELECT * FROM [table];			-- mostra *totes* les entrades *tots* els atributs de [taula]
SELECT [atr1], [atr2], ... FROM [table];	-- *mostra només* [atr1], [atr2], ... de totes les tuples de [taula]
SELECT * FROM [taula] WHERE [atr][comparador][value] -- mostra nomes els que compleixen la *condició*
SELECT [atr] AS [nou nom] FROM [taula]; --AS canvia el nom d'atribut al mostrar-lo
```

* **Ordenar**
```sql
SELECT * FROM [taula] ORDER BY [atr] ASC, [atr] DESC;
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
ALTER TABLE [taula] ADD COLUMN [nom] [type] ~ [modifier]; -- agregar columna
```
* **valor per defecte**
```sql
ALTER TABLE [taula] ALTER COLUMN [atribut] SET DEFAULT [false];
```
* **definir primary key**
```sql
ALTER TABLE [taula] ADD PRIMARY KEY ([atr]);
```
* **eliminar modificador**
```sql
ALTER TABLE [taula] DROP CONSTRAINT nomTaula_pkey
```
___
**Tipus de dades**

+ boolean				_y/n, yes/no, 1/0, t/f, true/false_
+ integer, int, int4			_enter_
+ smallint, int2			_enter de fins a 5 digits (-32000/32000)_
+ bigint, int8				_desde (-9*10^17/9*10^17)_	
+ serial/bigserial			_enter autoincremental int/bigint_
+ decimal/numeric(t,d)			_**t**=total digits /**d**=total decimalsprecisión_
+ float					_decimal fins a 6 decimals_
+ double precision			_decimal fins a 15 xifres_
+ character varyng(n), varchar(n) 	_longitud de 'n' caràcters_
+ character(n), char(n) 		_char de longitud 'n' obligatòria_
+ text, varchar				_longitud variable il.limitada_
___
**Modifiers**
+ PRIMARY KEY	*Clau Primaria*
+ NOT NULL	*No es pot deixar buit*
+ DEFAULT [value] *Valor per defecte*

___
**Comparadors**

+ = / <> _equal/not equal_
+ < / >  _less/more than_
+ <=/ >= _less or equal/more or equal than_
+ IS/IS NOT _per a valors NULL_
___
**Operadors relacionals**
+ AND		ex-| WHERE [atr]=[value] AND [atr]=[value]
+ OR		ex-| WHERE [atr]=[value] AND IS NOT NULL
+ IN		ex-| WHERE [atr] IN ([value], [value], ...
*  '-----------¬ex-| WHERE [atr] IN (SELECT [atr] FROM [table] WHERE [condición])
+ BETWEEN		ex-| WHERE [atr] BETWEEN x AND y

