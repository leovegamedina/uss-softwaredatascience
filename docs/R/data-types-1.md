---
layout: default
title: Integers
parent: Data Types
grand_parent: Unidad 1 - Estructura de Datos en R
permalink: /docs/R/data-types/data-types-1/
nav_order: 1
---

# Integers ℤ

Por defecto, cuando una variable numérica , producirá un vector de valores numéricos de doble precisión (`double`). Para crear una variable de enteros se debe especificar explícitamente colocando una `L` directamente después de cada número.

{: .note-title }
> typeof() e is.integer()
>
> Para comprobar si una variable preexistente está formado por valores enteros o dobles, puede usar `typeof()` que le dirá si la variable es un ***double***, ***integer***, ***logical***, o ***character***, o bien, puede usar `is.integer()` para saber si es de tipo ***integer*** entregando un `TRUE` o `FALSE`.

```r
y = 3
y
## [1] 3.0
typeof(y)
## [1] double
is.integer(y)
## [1] FALSE
```
```r
y = 3L
y
## [1] 3
typeof(y)
## [1] integer
is.integer(y)
## [1] TRUE
```

Adicionalmente, podemos convertir un valor numérico en un número entero con la función `as.integer`, y podemos analizar una cadena en busca de valores decimales de la misma manera.

```r
as.integer(3.14)    # coerce a numeric value 
## [1] 3

as.integer("5.27")  # coerce a decimal string 
## [1] 5
```

Por otro lado, es erróneo intentar analizar una cadena **no decimal**.

```r
as.integer("Joe")   # coerce an non-decimal string 
## [1] NA 
Warning message: 
NAs introduced by coercion
```

A menudo, es útil realizar operaciones aritméticas con valores lógicos. Al igual que el lenguaje C, `VERDADERO` tiene el valor **1**, mientras que `FALSO` tiene el valor **0**.

```r
as.integer(TRUE)    # the numeric value of TRUE 
## [1] 1 
as.integer(FALSE)   # the numeric value of FALSE 
## [1] 0
```