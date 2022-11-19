---
layout: default
title: While Loop
parent: Control Statements
grand_parent: Unidad 1 - Estructura de Datos en R
permalink: /docs/R/control-statements/control-statements-3/
nav_order: 3
---

# While Loop

Los bucles `while` comienzan probando una condición. Si es cierto, entonces ejecutan la sentencia. Una vez que se ejecuta la declaración, la condición se prueba de nuevo, y así sucesivamente, hasta que la condición sea falsa, después de lo cual el bucle sale. Se considera una mejor práctica incluir un objeto de contador para realizar un seguimiento de las iteraciones totales.

```r
# syntax of while loop
counter <- 1

while(test_expression) {
    statement
    counter <- counter + 1
} 
```

{: .important-title }
> **for** vs **while**
>
> La principal diferencia entre un ciclo `for` y un ciclo `while` es: un ciclo for se usa cuando se conoce el número de iteraciones que se debe ejecutar un código mientras que un ciclo while se usa cuando no se conoce el número de iteraciones.

## Ejercicios

1. Escriba un bucle `while()` que imprima la variable `i` que se incrementa de 2 a 5, omitiendo el valor 3.