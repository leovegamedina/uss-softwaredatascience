---
layout: default
title: Variables y Asignaciones
parent: Programación
grand_parent: Unidad 1 - Estructura de Datos en R
permalink: /docs/R/programming/programming-1/
nav_order: 1
---

# Variables y Asignaciones

El primer operador utilizado es el de `asignamiento`, este se usa para asignar un valor. En <img src="/uss-softwaredatascience/assets/images/r.svg" width="20"> se utiliza el comando `<-` para indicar la asignacion a un objeto. Dicho objeto al que le fue asignado el valor se le llama `variable`. Por ejemplo:

```r
# assignment
x <- 3
# evaluation
x
## [1] 3
```

Adicionalmente, <img src="/uss-softwaredatascience/assets/images/r.svg" width="20"> permite 5 operedores de asignación:

```r
# leftward assignment
x <- value
x = value
x <<- value
# rightward assignment
value -> x
value ->> x 
```

{: .note-title }
> Uso operador de asignamiento
>
> El operador original en <img src="/uss-softwaredatascience/assets/images/r.svg" width="20"> es `<-`, pero en 2001 se incluyo el operador `=`, aunque este ultimo se utiliza mas como asignacion para argumentos de funciones del tipo `f(x=3)`.

Por otro lado, <img src="/uss-softwaredatascience/assets/images/r.svg" width="20"> es un lenguaje de programación es `case sensitive`, es decir, discierne las mayusculas de las minusculas.

```r
x <- 1
y <- 3
z <- 4
x * y * z
## [1] 12
x * Y * z
## Error in eval(expr, envir, enclos): object 'Y' not found
```