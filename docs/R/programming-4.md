---
layout: default
title: Printing
parent: Programación
grand_parent: Unidad 1 - Estructura de Datos en R
permalink: /docs/R/programming/programming-4/
nav_order: 3
---

# Printing

Los metodos mas comunes para imprimir son:

- `print()`: impresión genérica
- `noquote()`: imprimir sin comillas
- `cat()`: concatenar e imprimir sin comillas
- `sprintf()`: un envoltorio para la función en C `sprintf`, que devuelve un vector de caracteres que contiene una combinación formateada de texto y valores de variables

La función de impresión primaria en <img src="/uss-softwaredatascience/assets/images/r.svg" width="20"> es `print()`

```r
x <- "learning to print strings"
# basic printing
print(x)
## [1] "learning to print strings"

# print without quotes
print(x, quote = FALSE)
## [1] learning to print strings

noquote (x)
## [1] learning to print strings
```

Una alternativa a imprimir una cadena sin comillas es usar `noquote()`

```r
noquote(x)
## [1] learning to print strings
```

Otra función muy útil es `cat()` que nos permite concatenar objetos e imprímalos en la pantalla o en un archivo. El resultado de salida es muy similar a `noquote()`; sin embargo, `cat()` no imprime el indicador de línea numérico. Como resultado, `cat()` puede ser útil para imprimir respuestas bien formateadas para los usuarios.

```r
# basic printing (similar to noquote)
cat(x)
## learning to print strings

# combining character strings
cat(x, "in R")
## learning to print strings in R

# basic printing of alphabet
cat(letters)
## a b c d e f g h i j k l m n o p q r s t u v w x y z

# specify a separator between the combined characters
cat(letters, sep = "-")
## a-b-c-d-e-f-g-h-i-j-k-l-m-n-o-p-q-r-s-t-u-v-w-x-y-z

# collapse the space between the combine characters
cat(letters, sep = "")
## abcdefghijklmnopqrstuvwxyz
```

También puede formatear el ancho de línea para imprimir cadenas largas usando el argumento `fill`:

```r
x <- "Today I am learning how to print strings."
y <- "Tomorrow I plan to learn about textual analysis."
z <- "The day after I will take a break and drink a beer."
cat(x, y, z, fill = 0)
## Today I am learning how to print strings. Tomorrow I plan to learn about textual analysis. The day after I will take a break and drink a beer.

cat(x, y, z, fill = 5)
## Today I am learning how to print strings.
## Tomorrow I plan to learn about textual analysis.
## The day after I will take a break and drink a beer. 
```

`sprintf()` es una función de impresión útil para un control preciso de la salida. Para sustituir en una cadena o variable de cadena, use `%s`:

```r
x <- "print strings"
# substitute a single string/variable
sprintf("Learning to %s in R", x)
## [1] "Learning to print strings in R"

# substitute multiple strings/variables
y <- "in R"
sprintf("Learning to %s %s", x, y)
## [1] "Learning to print strings in R" 
```

Para números enteros, use `%d`:

```r
version <- 3
# substitute integer
sprintf("This is R version:%d", version)
## [1] "This is R version:3"

# print with leading spaces
sprintf("This is R version:%4d", version)
## [1] "This is R version: 3"

# can also lead with zeros
sprintf("This is R version:%04d", version)
## [1] "This is R version:0003"
```

Para números flotantes, use `%f` para notación estándar y `%e` o `%E` para notación exponencial:

```r
sprintf ("%f", pi) # '%f' indicates 'fixed point' decimal notation
## [1] "3.141593"

sprintf ("%.3f", pi) # decimal notation with 3 decimal digits
## [1] "3.142"

sprintf ("%1.0f", pi) # 1 integer and 0 decimal digits
## [1] "3"

sprintf ("%5.1f", pi) # decimal notation with 5 total decimal digits and only 1 to the right of the decimal point
## [1] " 3.1"

sprintf ("%e", pi) # exponential decimal notation 'e'
## [1] "3.141593e+00"

sprintf ("%E", pi) # exponential decimal notation 'E'
## [1] "3.141593E+00" 
```