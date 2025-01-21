# Comandos basicos de SQL! 🤓
Estructura completa:
```
SELECT [DISTINCT] <columnes>
  [ INTO <clàusula> ]
    FROM <clàusula>
  [ WHERE <clàusula> ]
  [ GROUP BY <clàusula> ]
  [ HAVING <clàusula> ]
  [ ORDER BY <clàusula> ]
  [ LIMIT num1 OFFSET num2 ]
```



Sacar toda la info de una tabla
```
select *
from nombreTabla
```
Sacar solo algunos datos de la tabla
```
select  cp, nom ,adreca
from venedor v 
```
Sacar algunos datos y modificar un dato de la tabla(En este ejemplo incrementar un 5% el precio)
```
select  cod_a , descrip , preu , preu *1.05
from article a 
```
### Concatenar
Funcion __concat()__

### Primera letra mayuscula
Funcion __initcap()__

Sacar algunos datos en una misma columna y formateado(concatenar e iniciales en mayusculas)
```
select  concat(initcap( nom),'. ', adreca,' (',cp,')') 
from client
```
Sacar datos con un alias
__as__
```
select  num_f as "Número Factura", data, cod_ven as "Codi Venedor"
from factura f 
```
```
select  cod_a as "Codi Article", descrip as descripcio, stock_min  as "Stock mínimm", cod_cat as "Codif Categoria"
from article a 
```
### Clausula __WHERE__
```
WHERE<condicio> AND/OR/NOT <condicio>
```
Operadores para hacer comparaciones en las condiciones:

+ < <= = > >= >                <> (!=) (distinto)
+ BETWEEN  valor1 AND valor2 (valores entre ambos valores)
+ IN  si el valor amb què es compara està en la llista de valors (entre parèntesis i valors separats per comes)
+ LIKE se usa con caracteres comodin %(equivale a 0 o mas caracteres, el que sea), _(equivale a 1 caracter, el que sea)
+ IS[NOT]
  
### Como se escriven las constantes
+ constantes __numericas__ van con . decimal y sin comillas
+ constantes __alfanumericas__(TEXTO) van entre comillas simples '
+ las __fechas__ tambien entre comillas simples
+ el valor __nulo__ se escrive   NULL

## Ejercicios WHERE
Sacar clientes de la ciudad que tiene codigo 12309
```
select *
from client c 
where cp = 12425
```

### Trabajar con fechas!

La funcion to_char(data,'DD-MM-YYYY')
Estructura :  TO_CHAR(NOW(),'format')

Ponemos primera la fecha y despues el formato en quela queremos.

### La funcion like
Nos sirve para sacar los valores que sean igual al que pongamos.


Sacar las facturas del mes de marzo de 2015
```
select *
from factura f 
where to_char(data,'MM-YYYY') like '03-2015'
```

Sacar articulos de la categoria BjcOlimpia amb un stock entre 2 y 7 unidades.
```
select *
from  article a 
where cod_cat like 'BjcOlimpia' and stock between 2 and 7
```

### FUncion is NULL
Nos sirve para comprobar si es nulo

Traure tots els clients que no tenen introduït el codi postal.
```
select*
from client
where cp is NULL
```
(6.11)
Traure tots els articles amb el stock introduït però que no tenen introduït el stock mínim.
```
select *
from  article a 
where stock is not null and stock_min is null
```
Traure tots els clients, el primer cognom dels quals és VILLALONGA.
```
select *
from  client c 
where nom like 'VILLALONGA%'
```
 Modificar l'anterior per a traure tots els que són VILLALONGA de primer o de segon cognom.

 El simbolo % equivale a 0 o muchos caracteres
```
select *
from  client c 
where nom like '%VILLALONGA%'
```
Modificar l'anterior per a traure tots els que no són VILLALONGA ni de primer ni de segon cognom.
```
select *
from  client c 
where nom not like '%VILLALONGA%'
```
Traure els articles "Pulsador" (la descripció conté aquesta paraula), el preu dels quals oscila entre 2 i 4 € i dels quals tenim un stock estrictament major que el stock mínim.
```
select *
from article a 
where descrip like '%Pulsador%' and preu between 2 and 4 and stock > stock_min
```

