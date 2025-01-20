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
