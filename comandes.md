##DB--COMMANNDS##

CREATE DATABASE [name]; -> crear DB

DROP DATABASE [name]; 	-> eliminar DB
\c [name]		-> connectar a [name]
\d 			-> Mostrar taules
_importar script_
\i [path]		-> *importar* script

##DB--TABLES##

\d [table]		-> *mostra atributs* de la taula

_insertar tupla_ 
+ INSERT INTO [taula] (atr1, atr2, ...) VALUES ([atr1], [atr2], ...); 	-> *insertar* nova tupla
+ INSERT INTO [taula] VALUES ([atr1],[atr2],...) 			-> *insertar tupla

_Seleccionar_
+ SELECT * FROM [table];			-> mostra *totes* les entrades *tots* els atributs de [taula]
+ SELECT [atr1], [atr2], ... FROM [table];	-> *mostra només* [atr1], [atr2], ... de totes les tuples de [taula]
+ SELECT * FROM [taula] WHERE [atr][=|>|<|<=|>=|<>][value] -> mostra nomes els que compleixen la *condició*

_borrar registres_
+ DELETE FROM [table] WHERE [atr][=|>|<|<=|>=|<>][value];	-> Sobretot no oblidar *WHERE*

_editar registres_
+ UPDATE [tablbe] SET [atr]=[value] WHERE [atr]=[value];


	
				




