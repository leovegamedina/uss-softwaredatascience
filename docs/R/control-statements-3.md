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

```r
n = 2

while(n<6){
  if(n!=3){
    print(n)
  }
  n = n + 1
}
## [1] 2
## [1] 4
## [1] 5
```

2. Convierta numeros decimales a binarios.
<img src="/uss-softwaredatascience/assets/images/decimal_binary.png" width="550">

```r
n = 6
x = c()

while(n/2 != 0){
  x = append(x,n%%2)
  n = as.integer(n/2)
}

print(rev(x))
## [1] 1 1 0
```

3. Encuentre los 10 primeros multiplos de un numero.

```r
n = 4
i = 1

while(i <= 10){
  mul = i*n
  i = i+1
  print(mul)
}
## [1] 4
## [1] 8
## [1] 12
## [1] 16
## [1] 20
## [1] 24
## [1] 28
## [1] 32
## [1] 36
## [1] 40
```

4. Reverse un numero usando while. No puede usar `rev()`.

```r
n = 432
rev = 0

while(n!=0){
  r = n%%10
  rev = rev * 10 + r
  n = as.integer(n/10)
}

print(rev)
## [1] 234
```