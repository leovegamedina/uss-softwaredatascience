---
layout: default
title: dplyr
parent: Dataframes con Tidyverse
grand_parent: Unidad 1 - Estructura de Datos en R
permalink: /docs/R/dataframes/dataframes-4/
nav_order: 4
---

# <img src="/uss-softwaredatascience/assets/images/dplyr.png" width="40"> dplyr

La transformación de los datos es una parte básica de la manipulación de datos. Esto puede incluir filtrar, resumir y ordenar los datos por diferentes medios. Esto también incluye la combinación de conjuntos de datos dispares, la creación de nuevas variables y muchas otras tareas de manipulación. Para los siguientes ejkemplos usaremos el siguiente dataset:

```r
##   Division      State   X1980    X1990    X2000    X2001    X2002    X2003    X2004    X2005    X2006    X2007    X2008    X2009    X2010    X2011
## 1        6    Alabama 1146713  2275233  4176082  4354794  4444390  4657643  4812479  5164406  5699076  6245031  6832439  6683843  6670517  6592925
## 2        9     Alaska  377947   828051  1183499  1229036  1284854  1326226  1354846  1442269  1529645  1634316  1918375  2007319  2084019  2201270
## 3        8    Arizona  949753  2258660  4288739  4846105  5395814  5892227  6071785  6579957  7130341  7815720  8403221  8726755  8482552  8340211
## 4        7   Arkansas  666949  1404545  2380331  2505179  2822877  2923401  3109644  3546999  3808011  3997701  4156368  4240839  4459910  4578136
## 5        9 California 9172158 21485782 38129479 42908787 46265544 47983402 49215866 50918654 53436103 57352599 61570555 60080929 58248662 57526835
## 6        8   Colorado 1243049  2451833  4401010  4758173  5151003  5551506  5666191  5994440  6368289  6579053  7338766  7187267  7429302  7409462
```

Cuando se trabaja con un marco de datos considerable, a menudo deseamos evaluar solo variables específicas. La función `select()` nos permite seleccionar y/o renombrar variables.

```r
sub.exp <- expenditures %>% select(Division, State, X2007:X2011)
head(sub.exp)  # for brevity only display first 6 rows
##   Division      State    X2007    X2008    X2009    X2010    X2011
## 1        6    Alabama  6245031  6832439  6683843  6670517  6592925
## 2        9     Alaska  1634316  1918375  2007319  2084019  2201270
## 3        8    Arizona  7815720  8403221  8726755  8482552  8340211
## 4        7   Arkansas  3997701  4156368  4240839  4459910  4578136
## 5        9 California 57352599 61570555 60080929 58248662 57526835
## 6        8   Colorado  6579053  7338766  7187267  7429302  7409462

# select all variables that start with "X"
head(expenditures %>% select(starts_with("X")))

##     X1980    X1990    X2000    X2001    X2002    X2003    X2004    X2005  X2006    X2007    X2008    X2009    X2010    X2011
## 1 1146713  2275233  4176082  4354794  4444390  4657643  4812479  5164406  5699076  6245031  6832439  6683843  6670517  6592925
## 2  377947   828051  1183499  1229036  1284854  1326226  1354846  1442269  1529645  1634316  1918375  2007319  2084019  2201270
## 3  949753  2258660  4288739  4846105  5395814  5892227  6071785  6579957  7130341  7815720  8403221  8726755  8482552  8340211
## 4  666949  1404545  2380331  2505179  2822877  2923401  3109644  3546999  3808011  3997701  4156368  4240839  4459910  4578136
## 5 9172158 21485782 38129479 42908787 46265544 47983402 49215866 50918654 53436103 57352599 61570555 60080929 58248662 57526835
## 6 1243049  2451833  4401010  4758173  5151003  5551506  5666191  5994440  6368289  6579053  7338766  7187267  7429302  7409462

# de-select variables by using "-" prior to name or function
expenditures %>% select(-X1980:-X2006)
expenditures %>% select(-starts_with("X"))
```

Para renombrar variables con `select()`, podemos hacerlo de las siguientes 2 maneras y adicional podemos usar la funcion `rename()` de esta forma:

```r
# select and rename a single column
expenditures %>% select(Yr_1980 = X1980)

# select and rename the multiple variables with an "X" prefix:
expenditures %>% select(Yr_ = starts_with ("X"))

# keep all variables and rename a single variable
expenditures %>% rename(`2011` = X2011)
```

El filtrado de datos es una tarea común para identificar/seleccionar observaciones en las que una variable en particular coincide con un valor/condición específicos.

```r
sub.exp %>% filter(Division == 3)
##   Division     State    X2007    X2008    X2009    X2010    X2011
## 1        3  Illinois 20326591 21874484 23495271 24695773 24554467
## 2        3   Indiana  9497077  9281709  9680895  9921243  9687949
## 3        3  Michigan 17013259 17053521 17217584 17227515 16786444
## 4        3      Ohio 18251361 18892374 19387318 19801670 19988921
## 5        3 Wisconsin  9029660  9366134  9696228  9966244 10333016
```

{: .note-title }
> Nota
>
> Aca podemos aplicar filtros con multiples operadores logicos, para revisar cuales son pueden ver la seccion ***Operadores Logicos*** del curso.

Por ejemplo, podemos filtrar por la División 3 y los gastos en 2011 que superaron los USD 10B. Esto da como resultado que Indiana, que se encuentra en la División 3, quede excluida ya que sus gastos fueron < USD 10B.

```r
# Raw census data are in units of $1,000
sub.exp %>% filter(Division == 3, X2011 > 10000000)  
##   Division     State    X2007    X2008    X2009    X2010    X2011
## 1        3  Illinois 20326591 21874484 23495271 24695773 24554467
## 2        3  Michigan 17013259 17053521 17217584 17227515 16786444
## 3        3      Ohio 18251361 18892374 19387318 19801670 19988921
## 4        3 Wisconsin  9029660  9366134  9696228  9966244 10333016
```

A menudo, las observaciones se anidan dentro de grupos o categorías y nuestro objetivo es realizar análisis estadísticos tanto a nivel de observación como a nivel de grupo. La función `group_by()` nos permite crear estas agrupaciones categóricas. La función `group_by()` es una función ***silenciosa*** en la que no se realiza ninguna manipulación observable de los datos como resultado de la aplicación de la función.

```r
group.exp <- sub.exp %>% group_by(Division)
head(group.exp)
## Source: local data frame [6 x 7]
## Groups: Division
## 
##   Division      State    X2007    X2008    X2009    X2010    X2011
## 1        6    Alabama  6245031  6832439  6683843  6670517  6592925
## 2        9     Alaska  1634316  1918375  2007319  2084019  2201270
## 3        8    Arizona  7815720  8403221  8726755  8482552  8340211
## 4        7   Arkansas  3997701  4156368  4240839  4459910  4578136
## 5        9 California 57352599 61570555 60080929 58248662 57526835
## 6        8   Colorado  6579053  7338766  7187267  7429302  7409462
```

Para desagrupar utilizamos la funcion `ungroup()`.

Obviamente, el objetivo de toda esta manipulacion de datos es poder realizar un análisis estadístico de nuestros datos. La función `summarise()` nos permite realizar la mayoría de las estadísticas de resumen cuando realizamos análisis de datos exploratorios.

```r
sub.exp %>% summarise(Mean_2011 = mean(X2011))
##   Mean_2011
## 1  10513678

sub.exp %>% summarise(Min = min(X2011, na.rm=TRUE),
                     Median = median(X2011, na.rm=TRUE),
                     Mean = mean(X2011, na.rm=TRUE),
                     Var = var(X2011, na.rm=TRUE),
                     SD = sd(X2011, na.rm=TRUE),
                     Max = max(X2011, na.rm=TRUE),
                     N = n())

##       Min  Median     Mean         Var       SD      Max  N
## 1 1049772 6527404 10513678 1.48619e+14 12190938 57526835 50
```

Esta información es útil, pero poder comparar estadísticas de resumen en múltiples niveles es cuando realmente comienza a recopilar información. Aquí es donde entra en juego la función `group_by()`. Primero, agrupemos por división y veamos cómo se comparan las diferentes regiones en 2010 y 2011.

```r
sub.exp %>%
        group_by(Division)%>% 
        summarise(Mean_2010 = mean(X2010, na.rm=TRUE),
                  Mean_2011 = mean(X2011, na.rm=TRUE))
## Source: local data frame [9 x 3]
## 
##   Division Mean_2010 Mean_2011
## 1        1   5121003   5222277
## 2        2  32415457  32877923
## 3        3  16322489  16270159
## 4        4   4672332   4672687
## 5        5  10975194  11023526
## 6        6   6161967   6267490
## 7        7  14916843  15000139
## 8        8   3894003   3882159
## 9        9  15540681  15468173
```

Ahora estamos empezando a ver algunas diferencias. ¿Qué tal si comparamos estados dentro de una División? Podemos comenzar a aplicar múltiples funciones que hemos aprendido hasta ahora para obtener el promedio de 5 años para cada estado dentro de la División 3.

```r
sub.exp %>%
        pivot_longer(names_to = "Year", values_to = "Expenditure", cols = X2007:X2011) %>%   # this turns our wide data to a long format
        filter(Division == 3) %>%                    # we only want to compare states within Division 3
        group_by(State) %>%                          # we want to summarize data at the state level
        summarise(Mean = mean(Expenditure),
                  SD = sd(Expenditure))

## Source: local data frame [5 x 3]
## 
##       State     Mean        SD
## 1  Illinois 22989317 1867527.7
## 2   Indiana  9613775  238971.6
## 3  Michigan 17059665  180245.0
## 4      Ohio 19264329  705930.2
## 5 Wisconsin  9678256  507461.2
```

La funcion summarise() contiene funcion built-in para aplicar:

- Center: `mean()`, `median()`
- Spread: `sd()`, `IQR()`, `mad()`
- Range: `min()`, `max()`, `quantile()`
- Position: `first()`, `last()`, `nth()`,
- Count: `n()`, `n_distinct()`
- Logical: `any()`, `all()`

A veces deseamos ver las observaciones en orden de rango para una(s) variable(s) en particular. La función arrange() nos permite ordenar los datos por variables en orden ascendente o descendente.

```r
sub.exp %>%
        group_by(Division)%>% 
        summarise(Mean_2010 = mean(X2010, na.rm=TRUE),
                  Mean_2011 = mean(X2011, na.rm=TRUE)) %>%
        arrange(Mean_2011)

## Source: local data frame [9 x 3]
## 
##   Division Mean_2010 Mean_2011
## 1        8   3894003   3882159
## 2        4   4672332   4672687
## 3        1   5121003   5222277
## 4        6   6161967   6267490
## 5        5  10975194  11023526
## 6        7  14916843  15000139
## 7        9  15540681  15468173
## 8        3  16322489  16270159
## 9        2  32415457  32877923

sub.exp %>%
        group_by(Division)%>% 
        summarise(Mean_2010 = mean(X2010, na.rm=TRUE),
                  Mean_2011 = mean(X2011, na.rm=TRUE)) %>%
        arrange(desc(Mean_2011))

## Source: local data frame [9 x 3]
## 
##   Division Mean_2010 Mean_2011
## 1        2  32415457  32877923
## 2        3  16322489  16270159
## 3        9  15540681  15468173
## 4        7  14916843  15000139
## 5        5  10975194  11023526
## 6        6   6161967   6267490
## 7        1   5121003   5222277
## 8        4   4672332   4672687
## 9        8   3894003   3882159
```

A menudo, queremos crear una nueva variable que sea una función de las variables actuales en nuestro dataframe o simplemente queremos agregar una nueva variable que sea externa a nuestras variables existentes. La función `mutate()` nos permite agregar nuevas variables mientras conservamos las variables existentes.

```r
inflation_adj <- join.exp %>% mutate(Adj_Exp = Expenditure/Inflation)
head(inflation_adj)

##   Division      State Year Expenditure  Annual Inflation  Adj_Exp
## 1        6    Alabama 2007     6245031 207.342 0.9030811  6915249
## 2        9     Alaska 2007     1634316 207.342 0.9030811  1809711
## 3        8    Arizona 2007     7815720 207.342 0.9030811  8654505
## 4        7   Arkansas 2007     3997701 207.342 0.9030811  4426735
## 5        9 California 2007    57352599 207.342 0.9030811 63507696
## 6        8   Colorado 2007     6579053 207.342 0.9030811  7285119

rank_exp <- inflation_adj %>% 
        filter(Year == 2010) %>%
        arrange(desc(Adj_Exp)) %>%
        mutate(Rank = 1:length(Adj_Exp))
head(rank_exp)

##   Division      State Year Expenditure  Annual Inflation  Adj_Exp Rank
## 1        9 California 2010    58248662 218.056 0.9497461 61330774    1
## 2        2   New York 2010    50251461 218.056 0.9497461 52910417    2
## 3        7      Texas 2010    42621886 218.056 0.9497461 44877138    3
## 4        3   Illinois 2010    24695773 218.056 0.9497461 26002501    4
## 5        2 New Jersey 2010    24261392 218.056 0.9497461 25545135    5
## 6        5    Florida 2010    23349314 218.056 0.9497461 24584797    6

inflation_adj %>%
        filter(State == "Ohio") %>%
        mutate(Perc_Chg = (Adj_Exp-lag(Adj_Exp))/lag(Adj_Exp))

##   Division State Year Expenditure  Annual Inflation  Adj_Exp     Perc_Chg
## 1        3  Ohio 2007    18251361 207.342 0.9030811 20210102           NA
## 2        3  Ohio 2008    18892374 215.303 0.9377553 20146378 -0.003153057
## 3        3  Ohio 2009    19387318 214.537 0.9344190 20747992  0.029862103
## 4        3  Ohio 2010    19801670 218.056 0.9497461 20849436  0.004889357
## 5        3  Ohio 2011    19988921 224.939 0.9797251 20402582 -0.021432441

perc.of.whole <- inflation_adj %>%
        filter(Year == 2011) %>%
        arrange(desc(Adj_Exp)) %>%
        mutate(Perc_of_Total = Adj_Exp/sum(Adj_Exp),
               Cum_Perc = cumsum(Perc_of_Total)) %>%
        select(-Expenditure, -Annual, -Inflation)       
head(perc.of.whole, 8)

##   Division        State Year  Adj_Exp Perc_of_Total  Cum_Perc
## 1        9   California 2011 58717324    0.10943237 0.1094324
## 2        2     New York 2011 52575244    0.09798528 0.2074177
## 3        7        Texas 2011 43751346    0.08154005 0.2889577
## 4        3     Illinois 2011 25062609    0.04670957 0.3356673
## 5        5      Florida 2011 24364070    0.04540769 0.3810750
## 6        2   New Jersey 2011 24128484    0.04496862 0.4260436
## 7        2 Pennsylvania 2011 23971218    0.04467552 0.4707191
## 8        3         Ohio 2011 20402582    0.03802460 0.5087437
```

Tambien otras funcion que tiene dplyr, son las funciones de `join()`. Esta cuenta con las siguientes:

- `inner_join(x, y, by = NULL)`: Incluye solo filas en x e y que tengan un valor coincidente.
- `left_join(x, y, by = NULL)`: Incluye todo x y las filas correspondientes de y.
- `right_join(x, y, by = NULL)`: Incluye todo y y las filas correspondientes de x.
- `full_join(x, y, by = NULL)`: Incluye tanto x como y.
- `semi_join(x, y, by = NULL)`: Incluye filas de x que coincidan con y pero solo mantiene las columnas de x.
- `anti_join(x, y, by = NULL)`: Opuesto a semi_join().