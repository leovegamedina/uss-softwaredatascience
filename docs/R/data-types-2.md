---
layout: default
title: Double/Float
parent: Data Types
grand_parent: Unidad 1 - Estructura de Datos en R
permalink: /docs/R/data-types/data-types-2/
nav_order: 2
---

# Double/Float ℝ

Los valores decimales/double/floats se denominan `numerics` en <img src="/uss-softwaredatascience/assets/images/r.svg" width="20">. Es el tipo de datos computacional predeterminado. Si asignamos un valor decimal a una variable x de la siguiente manera, x será de tipo numérico.

{: .note-title }
> class() e is.numeric()
>
> Otra manera de saber el tipo de clase de una variable es la funcion `class()`. Es una alternativa a ***`typeof()`***. Además. al igual que ***`is.integer()`***, tambien existe la funcion `is.numeric()` para validar el tipo de dato numeric.

```r
x = 10.5       # assign a decimal value 
x              # print the value of x 
## [1] 10.5 
class(x)       # print the class name of x 
## [1] "numeric"
```

Además, incluso si asignamos un número entero a una variable k, todavía se guarda como un valor numérico.

```r
k = 1 
k              # print the value of k 
## [1] 1 
class(k)       # print the class name of k 
## [1] "numeric"
```

El hecho de que k no sea un número entero se puede confirmar con la función `is.integer()`.

```r
is.integer(k)  # is k an integer? 
## [1] FALSE

is.numeric(k)  # is k a numeric? 
## [1] TRUE
```

Para convertir un tipo de dato integer o character a numeric, podemos usar la funcion `as.numeric()`.

```r
k = 3L
as.numeric(k)  
## [1] 3.0
```