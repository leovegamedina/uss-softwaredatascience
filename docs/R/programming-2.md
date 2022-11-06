---
layout: default
title: Type function
parent: Programación
grand_parent: Unidad 1 - Estructura de Datos en R
permalink: /docs/R/programming/programming-2/
nav_order: 2
---

# Type function

Para obtener el tipo de dato de un valor, variable u objeto en <img src="/uss-softwaredatascience/assets/images/r.svg" width="20">, se usa la función `typeof()` y se inserta el valor/variable como parametro.

La sintaxis para usar la función typeof() para obtener el tipo de datos de la variable x es:

```r
typeof(x)
```

La función devuelve una cadena de caracteres. Los siguientes son algunos de los valores posibles que devuelve la función typeof().

- logical
- integer
- double
- complex
- character
- raw
- list
- NULL
- closure
- special
- builtin
- environment
- S4

Por ejemplo, inicializaremos una variable `x` con un valor de `2.8` y encontraremos su tipo usando la función typeof():

```r
x <- 2.8
typeof(x)
## [1] "double"
```

Ahora, asignemos `x` con `TRUE` y encontremos el tipo de x:

```r
x <- TRUE
typeof(x)
## [1] "logical"
```