---
layout: default
title: If Statement
parent: Control Statements
grand_parent: Unidad 1 - Estructura de Datos en R
permalink: /docs/R/control-statements/control-statements-1/
nav_order: 1
---

# If Statement

La declaración condicional `if` se usa para probar una expresión. Si `test_expression` es **TRUE**, la declaración se ejecuta. Pero si es **FALSE**, nada
sucede.

```r
# syntax of if statement
if(test_expression){
    statement
} 
```

```r
x <- c(8, 3, -2, 5)

# without curly braces
if(any(x < 0)) print ("x contains negative numbers")
## [1] "x contains negative numbers"

# with curly braces produces same result
if(any(x < 0)){
    print ("x contains negative numbers")
}
## [1] "x contains negative numbers"

# an if statement in which the test expression is FALSE does not produce any output
y <- c(8, 3, 2, 5)

if(any(y < 0)){
    print ("y contains negative numbers")
} 
```

{: .warning-title }
> uso de corchetes
>
> El no uso de corchetes puede inducir errores de codigo si es que se usa ***funciones adicionales*** o ***else*** en el `statement`.
```r
if(any(x < 0))
    print ("x contains negative numbers")
else
    print("x not contains negative numbers")
## [1] "x contains negative numbers"
## > else
## Error: unexpected 'else' in "else"
## >   print("x not contains negative numbers")
## [1] "x not contains negative numbers"
```

# If...else Statement

La sentencia condicional `if...else` se usa para probar una expresión similar a la sentencia if. Sin embargo, en lugar de que no suceda nada si `test_expression` es
**FALSE**, se evaluará la parte ***else*** de la función.

```r
# syntax of if…else statement
if(test_expression) {
    statement 1
} else {
    statement 2
} 
```

```r
# this test results in statement 1 being executed
x <- c(8, 3, -2, 5)

if(any(x < 0)){
    print("x contains negative numbers")
} else{
    print("x contains all positive numbers")
}
## [1] "x contains negative numbers"

# this test results in statement 2 (or the else statement) being executed
y <- c (8, 3, 2, 5)

if(any(y < 0)){
    print("y contains negative numbers")
} else{
    print("y contains all positive numbers")
}
## [1] "y contains all positive numbers"
```

Las declaraciones `if...else` simples, como las anteriores, en las que solo se ejecuta una línea de código en las declaraciones, se pueden escribir de una manera alternativa simplificada. Estas alternativas solo se recomiendan para códigos `if...else` ***muy cortos*** porque pueden volverse difíciles de leer a medida que aumenta la longitud de los caracteres.

```r
x <- c(8, 3, 2, 5)

# alternative 1
if(any(x < 0)) print("x contains negative numbers") else print("x contains all positive numbers")
## [1] "x contains all positive numbers"

# alternative 2 using the ifelse function
ifelse(any(x < 0), "x contains negative numbers", "x contains all positive numbers")
## [1] "x contains all positive numbers" 
```

También podemos ***anidar*** tantas sentencias `if…else` como sean necesarias.

```r
# this test results in statement 1 being executed
x <- 7

if(x >= 10){
    print("x exceeds acceptable tolerance levels")
} else if(x >= 0 & x < 10){
    print("x is within acceptable tolerance levels")
} else {
    print("x is negative")
}
## [1] "x is within acceptable tolerance levels"
```