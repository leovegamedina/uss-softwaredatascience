---
layout: default
title: Repeat/Break/Next
parent: Control Statements
grand_parent: Unidad 1 - Estructura de Datos en R
permalink: /docs/R/control-statements/control-statements-4/
nav_order: 4
---

# Repeat/Break/Next

## Repeat Loop

Un bucle `repeat` se utiliza para iterar sobre un bloque de código varias veces. No hay una expresión de prueba en un bucle de repetición para finalizar o salir del bucle. Más bien, debemos poner una declaración de condición explícitamente dentro del cuerpo del ciclo y usar la función `break` para salir del ciclo. Si no lo hace, se producirá un bucle infinito.

```r
# syntax of repeat loop
counter <- 1
repeat {
    statement
    if(test_expression){
        break
 }
    counter <- counter + 1
} 
```

Por ejemplo, supongamos que queremos extraer valores aleatoriamente de una distribución uniforme entre 1 y 25. Además, queremos continuar extrayendo valores aleatoriamente hasta que nuestra muestra contenga al menos cada valor entero entre 1 y 25; sin embargo, no nos importa si hemos obtenido un valor en particular varias veces. El siguiente código repite los sorteos aleatorios de valores entre 1 y 25 (que redondeamos). Luego incluimos una declaración `if` para verificar si todos los valores entre 1 y 25 están presentes en nuestra muestra. Si es así, usamos la instrucción `break` para salir del bucle. Si no, agregamos a nuestro `counter` y dejamos que el ciclo se repita hasta que se encuentre que la declaración condicional es verdadera. Luego podemos verificar el objeto `counter` para evaluar cuántas iteraciones se requirieron para alcanzar nuestro requisito condicional.

```r
counter <- 1
x <- NULL

repeat {
    x <- c(x, round(runif(1, min = 1, max = 25)))
    if(all(1:25 %in% x)){
        break
 }
    counter <- counter + 1
}

counter
## [1] 102
x
## [1] 14  4  5 17 17 10 14 13  5 24  5 24 10 18 11  6  9 13 24 22 21 13 19 10 16 24 10 19 24  5 19  4 19  3
## [35] 13  4 16 13 10 12 19 18  2 15 18 19 15 25 13  4  7 13 18 21 14 10 23 20  9  1  3  3  7  5 18 16 10 17
## [69] 13 20 17 17 18  6 13  5 18 24  5  1 14 12 23 23  5 24  5 10 24 22  6 17 14 10 16 14  1  2 18  5  2  8
```

## Break Function

La función `break` se utiliza para salir de un bucle inmediatamente, independientemente de la iteración en la que se encuentre el bucle. Las funciones `break` generalmente están integradas en una declaración `if` en la que se evalúa una condición, si es **TRUE**, salen del ciclo, si es **FALSE**, continúan con el ciclo. En una situación de bucle anidado, donde hay un bucle dentro de otro bucle, esta declaración sale del bucle más interno que se está evaluando.

```r
x <- 1:5

for (i in x) {
    if (i == 3){
        break
 }
    print (i)
}
## [1] 1
## [1] 2  
```

## Next Function

La siguiente declaración es útil cuando queremos omitir la iteración actual de un bucle sin terminarlo. Al encontrar `next`, el analizador <img src="/uss-softwaredatascience/assets/images/r.svg" width="20"> omite la evaluación adicional y comienza la siguiente iteración del ciclo.

```r
x <- 1:5

for (i in x) {
    if (i == 3){
        next
}
    print (i)
}
## [1] 1
## [1] 2
## [1] 4
## [1] 5   
```

{: .highlight }
> {: .opaque }
> Se recomienda que puedan revisar dado que se encuentran fuera del scope del curso:
> <div markdown="block">
> {: .warning }
> - [apply](https://www.rdocumentation.org/packages/base/versions/3.6.2/topics/apply): returns a vector or array or list of values obtained by applying a function to margins of an array or matrix.
- [lapply](https://www.rdocumentation.org/packages/base/versions/3.6.2/topics/lapply): returns a list of the same length as X, each element of which is the result of applying `FUN` to the corresponding element of X.
- [sapply](https://www.rdocumentation.org/packages/base/versions/3.6.2/topics/lapply): is a user-friendly version and wrapper of `lapply` by default returning a vector, matrix or, if `simplify = "array"`, an array if appropriate, by applying `simplify2array()`.
- [tapply](https://www.rdocumentation.org/packages/base/versions/3.6.2/topics/tapply): apply a function to each cell of a ragged array, that is to each (non-empty) group of values given by a unique combination of the levels of certain factors.
- [mapply](https://www.rdocumentation.org/packages/base/versions/3.6.2/topics/mapply): is a multivariate version of `sapply`. mapply applies `FUN` to the first elements of each `…` argument, the second elements, the third elements, and so on. Arguments are recycled if necessary.
- [rapply](https://www.rdocumentation.org/packages/base/versions/3.6.2/topics/rapply): is a recursive version of `lapply` with flexibility in how the result is structured `(how = "..")`.
- [vapply](https://www.rdocumentation.org/packages/base/versions/3.6.2/topics/lapply): is similar to `sapply`, but has a pre-specified type of return value, so it can be safer (and sometimes faster) to use.
> </div>