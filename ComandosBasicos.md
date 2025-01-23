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
## Funciones de dominio agregado

### Sintasi
+ COUNT(<expresion>), cuenta el numero de filas en las que aparece(no cuenta las nulas, creo xD)
+ SUM(<expresio>) pues suma,no?(ingora los nulos)
+ AVG(<expresio>) saca la media, no te vas a creer lo  que hace con los nulos!
+ VAR_SAMP(<expresio>) no se que hace xD, luego investigo... 😅
+ STDDEV(<expresio>) desviacio tipicia d'una mostra, ni idea xd
+ MAX(<expresio>) calcula el maximo
+ MIN(<expressio>) calcula el minim
  

Comptar el nombre de clients que tenen el codi postal nul.
```
select count(*)
from client c 
where cp is null
```

Comptar el número de vegades que l'article L76104 entra en les línies de factura, i el número total d'unitats venudes d'aquest article. Només us fa falta la taula LINIA_FAC.

```
select count(*),sum(quant) 
from linia_fac lf 
where cod_a like 'L76104'
```

Traure la mitjana del stock dels articles.
```
select avg(stock) 
from article a 
```

Modificar l'anterior per a tenir en compte els valors nuls, com si foren 0. Us vindrà bé la funció COALESCE que converteix els nuls del primer paràmetre al valor donat com a segon paràmetre (si és diferent de nul, deixa igual el valor). Per tant l'heu d'utilitzar d'aquesta manera: COALESCE(stock,0)
```
select avg(coalesce(stock,0)) 
from article a 
```

Comptar quantes factures té el client 375
```
select count(*) 
from factura f 
where cod_cli = 375
```

Calcular el descompte màxim, el mínim i el descompte mitjà de les factures.
```
select max(dte),min(dte),avg(dte) 
from factura f 
```

## Ejercicios GROUP BY

Pues agrupa los elementos segun se repitan




Comptar el número de pobles de cada província (és suficient traure el codi de la província i el número de pobles).
```
select cod_pro , count(cod_pob) 
from poble p
group by cod_pro 
```

Comptar el nombre de clients en cada poble i codi postal.
```
select cod_pob ,  cp, count(*) 
from client c 
group by cod_pob,cp 
```

Comptar el número de factures de cada venedor a cada client.
```
select cod_ven , cod_cli , count(*)
from factura f 
group by cod_ven ,cod_cli 
```

Comptar el número de factures de cada trimestre. Per a poder traure el trimestre i agrupar per ell (ens val el número de trimestre, que va del 1 al 4), podem utilitzar la funció TO_CHAR(data,'Q').
```
select to_char(data,'Q') ,count(num_f)
from factura f 
group by to_char(data,'Q')
```

Calcular quantes vegades s'ha venut un article, la suma d'unitats venudes, la quantitat màxima i la quantitat mínima.
```
select cod_a ,count(quant),sum(quant),max(quant),min(quant)
from linia_fac lf 
group by cod_a 
```

Comptar el número d'articles de cada categoria i el preu mitjà.
```
select cod_cat ,count(*) , avg(preu)
from article a 
group by cod_cat 
```

Calcular el total de cada factura, sense aplicar descomptes ni IVA. Només ens farà falta la taula LINIES_FAC, i consistirà en agrupar per cada num_f per a calcular la suma del preu multiplicat per la quantitat.
```
select num_f , sum(preu * quant)
from linia_fac lf 
group by num_f 
```

## Ejercicios HAVING
Pues tener y eso





