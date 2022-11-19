---
layout: default
title: Factors/Category
parent: Data Types
grand_parent: Unidad 1 - Estructura de Datos en R
permalink: /docs/R/data-types/data-types-4/
nav_order: 4
---

# Factors/Category

Los factores son variables en <img src="/uss-softwaredatascience/assets/images/r.svg" width="20">, que toman un número limitado de valores diferentes; tales variables a menudo se denominan ***variables categóricas***. Uno de los usos más importantes de los factores es el modelamiento estadístico; dado que las variables categóricas entran en modelos estadísticos como `lm` y `glm` de manera diferente a las variables continuas, el almacenamiento de datos como factores asegura que las funciones de modelado tratarán dichos datos correctamente. Uno puede pensar en un factor como un vector entero donde cada entero tiene una **etiqueta**. De hecho, los factores se construyen sobre vectores enteros utilizando dos atributos: el `class()` ***factor***, que hace que se comporten de manera diferente a los vectores enteros regulares, y los `levels()`, que define el conjunto de valores permitidos.

## Creando Factores

Los objetos factor se pueden crear con la función `factor()`:

```r
# create a factor string
gender <- factor(c("male", "female", "female", "male", "female"))
gender
## [1] male female female male female
## Levels: female male

# inspect to see if it is a factor class
class(gender)
## [1] "factor"

# show that factors are just built on top of integers
typeof(gender)
## [1] "integer"

# See the underlying representation of factor
unclass(gender)
## [1] 2 1 1 2 1
## attr(,"levels")
## [1] "female" "male"

# what are the factor levels?
levels(gender)
## [1] "female" "male"

# show summary of counts
summary(gender)
## female male
## 3 2 
```

Si tenemos un vector de cadenas de caracteres o números enteros, podemos convertirlo fácilmente en factores:

```r
group <- c("Group1", "Group2", "Group2", "Group1", "Group1")
str(group)
## chr [1:5] "Group1" "Group2" "Group2" "Group1" "Group1"

# convert from characters to factors
as.factor(group)
## [1] Group1 Group2 Group2 Group1 Group1
## Levels: Group1 Group2
```

## Ordenando Factores

Al crear un factor, podemos controlar el orden de los niveles usando el argumento `levels`:

```r
# when not specified the default puts order as alphabetical
gender <- factor(c("male", "female", "female", "male", "female"))
gender
## [1] male female female male female
## Levels: female male

# specifying order
gender <- factor(c("male", "female", "female", "male", "female"),
                levels = c("male", "female"))
gender
## [1] male female female male female
## Levels: male female 
```

También podemos crear factores ordinales en los que se desea un orden específico usando el argumento `ordered = TRUE`.

```r
ses <- c ("low", "middle", "low", "low", "low", "low", "middle", "low", "middle",
 "middle", "middle", "middle", "middle", "high", "high", "low", "middle",
 "middle", "low", "high")
# create ordinal levels
ses <- factor(ses, levels = c("low", "middle", "high"), ordered = TRUE)
ses
## [1] low middle low low low low middle low middle middle
## [11] middle middle middle high high low middle middle low high
## Levels: low < middle < high

# you can also reverse the order of levels if desired
factor(ses, levels = rev(levels(ses)))
## [1] low middle low low low low middle low middle middle
## [11] middle middle middle high high low middle middle low high
## Levels: high < middle < low
```

## Eliminando Levels

Cuando desee descartar niveles de factores no utilizados, usamos `droplevels()`:

```r
ses2 <- ses[ses != "middle"]

# lets say you have no observations in one level
summary(ses2)
## low middle high
## 8 0 3

# you can drop that level if desired
droplevels(ses2)
## [1] low low low low low low high high low low high
## Levels: low < high 
```

> {: .highlight }
  Se recomienda que puedan revisar el paquete  [`plyr`](https://cran.r-project.org/web/packages/plyr/plyr.pdf) ya que esta fuera del scope del curso, pero tiene una ***gran capacidad de hacer manipulacion de factores (como `plyr::revalue()`) y funciones adicionales***.