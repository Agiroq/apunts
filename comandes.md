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
` PRIMARY KEY	`*Clau Primaria*
`NOT NULL`	*No es pot deixar buit*
`DEFAULT [value]` *Valor per defecte*

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
```


DB COMMANNDS
============
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
INSERT INTO [taula] (atr1, atr2, ...) VALUES ([atr1], [atr2], ...); 	-- *insertar* nova tupla
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



```sql
SELECT pais, to_char(fecha, 'month') AS month, date_part('day', fecha)AS day, date_part('hour', fecha) AS hora
FROM visitas
ORDER BY 2, 3, 4;

```
