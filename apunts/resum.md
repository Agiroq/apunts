### tipus de dades
  * **char**	_n char obligatori_    
  * **varchar(n)** _de 0 a n_    
  * **date** 	'YYYY-MM-DD' defauls    
		'DD-MM-YYYY "SET DATASTYLE 'European';"  	
  * **time** 	'hh:mm:ss'	  	
  * **timestamp**  'YYYY-MM-DD hh:mm:ss'     
  * **timestamptz** 'YYYY-MM-DD hh:mm:ss±tz'    

### modifiers 
  * PRIMARY KEY	*Clau Primaria*    
  * NOT NULL	  
  * DEFAULT [value] *Valor per defecte*    

### Comparadors
  * = / <> _equal/not equal_   
  * < / >  _less/more than_   
  * <=/ >= _less or equal/more or equal than_   
  * IS/IS NOT _per a NULL !!!no usar lògics_   
### Operadors relacionals 
  * AND  |  OR    
  * IN --> ...WHERE [atr] IN ([value],[value],...);   
  * BETWEEN --> ...WHERE [atr] BETWEEN x AND y;   

### COMANDES DDBB

  * **\c** [database]	_connectar a [database]_    
  * **\d**                 	_Mostrar taules_    
  * **\i [path_to_script]**	_**importar** script_    
  * CREATE DATABASE [name];    
  * DROP DATABASE [name];   

### COMANDES TAULA 
* crear taula   
  * CREATE TABLE [nom] ([atribut] [type] [*modifiers*],
		    	...,
/* define PKey */	primary key([atr], [atr2])),
/* define ForeigKey */	CONSTRAINT [FK_name] FOREIGN KEY ([atr_dst]) 
/* on FK references*/	REFERENCES [taula_src] ([atr_src]));	

* insertar tuplas
> INSERT INTO [taula] ([atr], [atr_amb_default],..)   
> VALUES ([value], default, ...); /* quan hi ha valors **default** */
		    |__________________________|	


