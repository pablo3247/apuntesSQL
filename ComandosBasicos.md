# Comandos basicos de SQL! 🤓

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


