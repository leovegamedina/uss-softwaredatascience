---
layout: default
title: For Loop
parent: Control Statements
grand_parent: Unidad 1 - Estructura de Datos en R
permalink: /docs/R/control-statements/control-statements-2/
nav_order: 2
---

# For Loop

El bucle `for` se utiliza para ejecutar instrucciones de código repetitivas durante un número determinado de veces. La sintaxis general esta definida, donde **i** es el contador y como **i** asume cada valor secuencial definido, el código en el cuerpo se ejecutará para ese **i-ésimo** valor.

```r
# syntax of for loop
for(i in 1:100) {
    <do stuff here with i>
} 
```

Por ejemplo, el siguiente ciclo `for` itera a través de cada valor (2010, 2011,…, 2016) y realiza las funciones de `paste` y `print` dentro de las llaves.

```r
for(i in 2010:2016){
    output <- paste ("The year is", i)
    print (output)
}
## [1] "The year is 2010"
## [1] "The year is 2011"
## [1] "The year is 2012"
## [1] "The year is 2013"
## [1] "The year is 2014"
## [1] "The year is 2015"
## [1] "The year is 2016"
```

Si desea realizar el bucle `for` pero tiene las salidas combinadas en un vector u otra estructura de datos, puede iniciar la estructura de datos de salida antes del bucle `for`. Por ejemplo, si queremos combinar las salidas anteriores en un solo vector **x**, podemos iniciar **x** primero y luego agregar la salida del bucle `for` a **x**.

```r
x <- NULL

for(i in 2010:2016) {
    output <- paste ("The year is", i)
    x <- append(x, output)
}
x
## [1] "The year is 2010" "The year is 2011" "The year is 2012" "The year is 2013"
## [5] "The year is 2014" "The year is 2015" "The year is 2016"
```

Sin embargo, una lección importante que aprender es que <img src="/uss-softwaredatascience/assets/images/r.svg" width="20"> no es eficiente para hacer crecer los objetos de datos. Una práctica más eficiente es iniciar un vector (u otra estructura de datos) del tamaño correcto y llenar los elementos.

```r
x <- vector(mode = “numeric”, length = 7)
counter <- 1

for(i in 2010:2016) {
    output <- paste ("The year is", i)
    x[counter] <- output
    counter <- counter + 1
}
x
## [1] "The year is 2010" "The year is 2011" "The year is 2012" "The year is 2013"
## [5] "The year is 2014" "The year is 2015" "The year is 2016"
```

## Ejercicios

1. Escriba un programa para escribir del 1 al 30 con la condición de que salte todos los múltiplos de 3.

```r
for(i in 1:30){
  if(i%%3 == 0){
    next
  }
  print(i)
}
## [1] 1
## [1] 2
## [1] 4
## [1] 5
## [1] 7
## [1] 8
## [1] 10
## [1] 11
## [1] 13
## [1] 14
## [1] 16
## [1] 17
## [1] 19
## [1] 20
## [1] 22
## [1] 23
## [1] 25
## [1] 26
## [1] 28
## [1] 29
```

1. Escriba un bucle repeat() que imprima todos los números pares del 2 al 10, incrementando el
variable i comenzando con la inicialización de `i <- 0` fuera del bucle.

```r
i <- 0
repeat{
  i <- i + 2
  print(i)
  if(i == 10){
    break
  }
}
## [1] 2
## [1] 4
## [1] 6
## [1] 8
## [1] 10
```

1. Escriba un ciclo anidado, donde el ciclo for() externo incrementa `a` 3 veces, y el ciclo for() interno incrementa `b` 3 veces. La instrucción `break` sale del bucle for() interno después de 2 incrementos. El bucle anidado imprime los valores de las variables, `a` y `b`.

```r
for(a in 1:3){
  for(b in 1:3){
    print(c(a, b))
    if (b == 2){
      break
    }
  }
}
## [1] 1 1
## [1] 1 2
## [1] 2 1
## [1] 2 2
## [1] 3 1
## [1] 3 2
```

1. Considere la siguiente serie que se usa para aproximar la función `sin(x)`:

$$ sin(x) = \sum_{k=0}^{\infty}{\dfrac{(-1)^k}{(2k+1!)}x^{2k+1}} = x - \dfrac{x^3}{3!} + \dfrac{x^5}{5!} - \dfrac{x^7}{7!} + ...$$

Escribe un bucle for para aproximar `sin(x)`. Pruebe diferentes números de términos, `n=5,10,50,100`. Compara tu bucle con la función `sin()`.

```r
val = 1
sin = 0
n = 5

for(i in 0:n){
  neg_term = (-1) ** i
  den = factorial(2 * i + 1)
  x_power = val ** (2 * i + 1)
  calc = (neg_term / den) * x_power
  sin = sin + calc
}
print(sin)
## [1] 0.841471
print(sin(val))
## [1] 0.841471
```