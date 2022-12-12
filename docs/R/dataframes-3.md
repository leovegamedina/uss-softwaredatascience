---
layout: default
title: tidyr
parent: Dataframes con Tidyverse
grand_parent: Unidad 1 - Estructura de Datos en R
permalink: /docs/R/dataframes/dataframes-3/
nav_order: 3
---

# <img src="/uss-softwaredatascience/assets/images/tidyr.png" width="40"> tidyr


Jenny Bryan afirmó que ***los datos de clases son como osos de peluche y los datos reales son como un oso grizzley con sangre de salmón goteando por la boca***. En esencia, estaba llegando al punto de que, a menudo, cuando aprendemos cómo realizar un enfoque de modelado en el salón de clases, los datos utilizados se proporcionan en un formato que se incorpora adecuadamente a la herramienta de modelado elegida. En la realidad, los conjuntos de datos son desordenados y ***cada conjunto de datos desordenado es desordenado a su manera***.

El concepto de `tidy data` fue establecido por Hadley Wickham y **representa una forma estandarizada de vincular la estructura de un conjunto de datos (su diseño físico) con su semántica (su significado)**. El objetivo siempre debe ser obtener un conjunto de datos en una forma ordenada que consiste en:

1. Cada variable forma una columna.
2. Cada observación forma una fila.
3. Cada tipo de unidad de observación forma una tabla.

## De Wide a Long!

Hay ocasiones en las que nuestros datos se consideran `amplios (wide)` o `no apilados (unstacked)` y un atributo/variable de interés común se distribuye entre las columnas. Para reformatear los datos de modo que estos atributos comunes se reúnan como una sola variable, la función de `pivot_longer()` tomará varias columnas y las colapsará en pares clave-valor, duplicando todas las demás columnas según sea necesario.

```r
library(dplyr) # I'm using dplyr just to create the data frame with tbl_df()

wide <- tbl_df(read.table(header = TRUE, text = "
 Group Year Qtr.1 Qtr.2 Qtr.3 Qtr.4
 1 2006 15 16 19 17
 1 2007 12 13 27 23
 1 2008 22 22 24 20
 1 2009 10 14 20 16
 2 2006 12 13 25 18
 2 2007 16 14 21 19
 2 2008 13 11 29 15
 2 2009 23 20 26 20
 3 2006 11 12 22 16
 3 2007 13 11 27 21
 3 2008 17 12 23 19
 3 2009 14 9 31 24
"))
```

Este dato se considera `wide` ya que la variable tiempo (representada en trimestres [Qtr.]) está estructurada de manera que cada trimestre representa una variable.

```r
library(tidyr)

long <- wide %>% pivot_longer(cols = Qtr.1:Qtr.4, names_to = "Quarter", values_to = "Revenue")
# note, for brevity, I only show the first 15 observations
head(long, 15)
## # A tibble: 15 x 4
##    Group  Year Quarter Revenue
##    <int> <int> <chr>     <int>
##  1     1  2006 Qtr.1        15
##  2     1  2007 Qtr.1        12
##  3     1  2008 Qtr.1        22
##  4     1  2009 Qtr.1        10
##  5     2  2006 Qtr.1        12
##  6     2  2007 Qtr.1        16
##  7     2  2008 Qtr.1        13
##  8     2  2009 Qtr.1        23
##  9     3  2006 Qtr.1        11
## 10     3  2007 Qtr.1        13
## 11     3  2008 Qtr.1        17
## 12     3  2009 Qtr.1        14
## 13     1  2006 Qtr.2        16
## 14     1  2007 Qtr.2        13
## 15     1  2008 Qtr.2        22
```

Otras maneras de hacer lo mismo serian:

```r
wide %>% pivot_longer(cols = c(-Group, -Year), names_to = "Quarter", values_to = "Revenue")
wide %>% pivot_longer(cols = 3:6, names_to = "Quarter", values_to = "Revenue")
wide %>% pivot_longer(cols = c(Qtr.1, Qtr.2, Qtr.3, Qtr.4), names_to = "Quarter", values_to = "Revenue")
```

## De Long a Wide!

También hay momentos en los que debemos convertir datos de formato wide en datos de formato long. Como complemento de la función de pivot_longer(), la función `pivot_wider()` distribuye un par clave-valor en varias columnas.

```r
back2wide <- long %>% pivot_wider(names_from = Quarter, values_from = Revenue)
back2wide
## # A tibble: 12 x 6
##    Group  Year Qtr.1 Qtr.2 Qtr.3 Qtr.4
##    <int> <int> <int> <int> <int> <int>
##  1     1  2006    15    16    19    17
##  2     1  2007    12    13    27    23
##  3     1  2008    22    22    24    20
##  4     1  2009    10    14    20    16
##  5     2  2006    12    13    25    18
##  6     2  2007    16    14    21    19
##  7     2  2008    13    11    29    15
##  8     2  2009    23    20    26    20
##  9     3  2006    11    12    22    16
## 10     3  2007    13    11    27    21
## 11     3  2008    17    12    23    19
## 12     3  2009    14     9    31    24
```

## Separando Una Columna en Multiples Columnas!

Supongamos que tenemos el sigueinte dataframe como ejemplo:

```r
messy_df
## # A tibble: 4 x 4
##   Grp_Ind Yr_Mo    City_State       Extra_variable
##   <chr>   <chr>    <chr>            <chr>         
## 1 1.a     2006_Jan Dayton (OH)      XX01person_1  
## 2 1.b     2006_Feb Grand Forks (ND) XX02person_2  
## 3 1.c     2006_Mar Fargo (ND)       XX03person_3  
## 4 2.a     2007_Jan Rochester (MN)   XX04person_4  
```

Utilizamos la funcion `separate()` para separar una columna en multiples.

```r
# separate Grp_Ind column into two variables named "Grp" & "Ind"
messy_df %>% separate(col = Grp_Ind, into = c("Grp", "Ind"))
## # A tibble: 4 x 5
##   Grp   Ind   Yr_Mo    City_State       Extra_variable
##   <chr> <chr> <chr>    <chr>            <chr>         
## 1 1     a     2006_Jan Dayton (OH)      XX01person_1  
## 2 1     b     2006_Feb Grand Forks (ND) XX02person_2  
## 3 1     c     2006_Mar Fargo (ND)       XX03person_3  
## 4 2     a     2007_Jan Rochester (MN)   XX04person_4  

# default separater is any non alpha-numeric character but you can specify the specific character to separate at
messy_df %>% separate(col = Extra_variable, into = c("X", "Y"), sep = "_")
## # A tibble: 4 x 5
##   Grp_Ind Yr_Mo    City_State       X          Y    
##   <chr>   <chr>    <chr>            <chr>      <chr>
## 1 1.a     2006_Jan Dayton (OH)      XX01person 1    
## 2 1.b     2006_Feb Grand Forks (ND) XX02person 2    
## 3 1.c     2006_Mar Fargo (ND)       XX03person 3    
## 4 2.a     2007_Jan Rochester (MN)   XX04person 4    

# you can keep the original column that you are separating
messy_df %>% separate(col = Grp_Ind, into = c("Grp", "Ind"), remove = FALSE)
## # A tibble: 4 x 6
##   Grp_Ind Grp   Ind   Yr_Mo    City_State       Extra_variable
##   <chr>   <chr> <chr> <chr>    <chr>            <chr>         
## 1 1.a     1     a     2006_Jan Dayton (OH)      XX01person_1  
## 2 1.b     1     b     2006_Feb Grand Forks (ND) XX02person_2  
## 3 1.c     1     c     2006_Mar Fargo (ND)       XX03person_3  
## 4 2.a     2     a     2007_Jan Rochester (MN)   XX04person_4 
```

## Combinando Multiples Columnas en Una Columna!

De manera similar, hay momentos en los que nos gustaría combinar los valores de dos variables. Como complemento a separate(), la función `unite()` es una función conveniente para unir múltiples valores de variables en uno.

```r
expenses <- tbl_df(read.table(header = TRUE, text = "
 Year Month Day Expense
 2015 01 01 500
 2015 02 05 90
 2015 02 22 250
 2015 03 10 325
"))

# default separator when uniting is "_"
expenses %>% unite(col = "Date", c(Year, Month, Day))
## # A tibble: 4 x 2
##   Date      Expense
##   <chr>       <int>
## 1 2015_1_1      500
## 2 2015_2_5       90
## 3 2015_2_22     250
## 4 2015_3_10     325

# specify sep argument to change separator
expenses %>% unite(col = "Date", c(Year, Month, Day), sep = "-")
## # A tibble: 4 x 2
##   Date      Expense
##   <chr>       <int>
## 1 2015-1-1      500
## 2 2015-2-5       90
## 3 2015-2-22     250
## 4 2015-3-10     325
```

## Otras funciones

Tomemos como ejemplo el siguiente dataframe:

```r
expenses <- tbl_df(read.table(header = TRUE, text = "
 Dept Year Month Day Cost
 A 2015 01 01 $500.00
 NA NA 02 05 $90.00
 NA NA 02 22 $1,250.45
 NA NA 03 NA $325.10
 B NA 01 02 $260.00
 NA NA 02 05 $90.00
", stringsAsFactors = FALSE)) 
```

Podemos usar la funcion `fill()` para rellenar los datos faltantes.

```r
expenses %>% fill(Dept, Year)
## # A tibble: 6 x 5
##   Dept   Year Month   Day Cost     
##   <chr> <int> <int> <int> <chr>    
## 1 A      2015     1     1 $500.00  
## 2 A      2015     2     5 $90.00   
## 3 A      2015     2    22 $1,250.45
## 4 A      2015     3    NA $325.10  
## 5 B      2015     1     2 $260.00  
## 6 B      2015     2     5 $90.00   
```

Por otro lado, tenemos la funcion `replace_na()` para reemplazar faltantes con un valor predeterminado.

```r
expenses %>% replace_na(replace = list(Day = "unknown"))
## # A tibble: 6 x 5
##   Dept   Year Month Day     Cost     
##   <chr> <int> <int> <chr>   <chr>    
## 1 A      2015     1 1       $500.00  
## 2 NA       NA     2 5       $90.00   
## 3 NA       NA     2 22      $1,250.45
## 4 NA       NA     3 unknown $325.10  
## 5 B        NA     1 2       $260.00  
## 6 NA       NA     2 5       $90.00   
```

Adicionalmente, podemos secuenciar distintas funciones de tidyr con el operador pipe, dado que este ya viene integrado con el package.

```r
a_mess <- tbl_df(read.table(header = TRUE, text = "
 Dep_Unt Year Q1 Q2 Q3 Q4
 A.1 2006 15 NA 19 17
 B.1 NA 12 13 27 23
 A.2 NA 22 22 24 20
 B.2 NA 12 13 25 18
 A.1 2007 16 14 21 19
 B.2 NA 13 11 16 15
 A.2 NA 23 20 26 20
 B.2 NA 11 12 22 16
"))

a_mess %>%
  fill(Year) %>%
  pivot_longer(names_to = "Quarter", values_to = "Cost", cols = Q1:Q4) %>%
  separate(Dep_Unt, into = c("Dept", "Unit")) %>%
  replace_na(replace = list(Cost = 17))
## # A tibble: 32 x 5
##    Dept  Unit   Year Quarter  Cost
##    <chr> <chr> <int> <chr>   <dbl>
##  1 A     1      2006 Q1         15
##  2 A     1      2006 Q2         17
##  3 A     1      2006 Q3         19
##  4 A     1      2006 Q4         17
##  5 B     1      2006 Q1         12
##  6 B     1      2006 Q2         13
##  7 B     1      2006 Q3         27
##  8 B     1      2006 Q4         23
##  9 A     2      2006 Q1         22
## 10 A     2      2006 Q2         22
## # ... with 22 more rows
```

Aca pueden ver el cheatsheet del paquete:

[![](/uss-softwaredatascience/assets/images/tidyr_image.png)](https://github.com/leovegamedina/uss-softwaredatascience/blob/main/assets/images/tidyr.pdf)