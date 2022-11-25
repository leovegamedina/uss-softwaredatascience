---
layout: default
title: Vectores, Sequencias, Listas y Matrices
parent: Arreglos
grand_parent: Unidad 1 - Estructura de Datos en R
permalink: /docs/R/arrays/arrays-1/
nav_order: 1
---

# Vectores

Un vector es simplemente una lista de elementos que son del mismo tipo. Para combinar la lista de elementos en un vector, utilizamos la función `c()` y separamos los elementos con una coma.

```r
# Vector of strings
fruits <- c("banana", "apple", "orange")
fruits
## [1] "banana" "apple" "orange"
```

Ademas, se pueden crear vectores logicos.

```r
# Vector of logical values
log_values <- c(TRUE, FALSE, TRUE, FALSE)
log_values
## [1] TRUE FALSE TRUE FALSE
```

Para averiguar cuántos elementos tiene un vector, usamos la función `length()`:

```r
fruits <- c("banana", "apple", "orange")
length(fruits)
## [1] 3
```

Para ordenar elementos en un vector alfabética o numéricamente, usamos la función `sort()`:

```r
fruits <- c("banana", "apple", "orange", "mango", "lemon")
numbers <- c(13, 3, 5, 7, 20, 2)

sort(fruits)  # Sort a string
sort(numbers) # Sort numbers
## [1] "apple" "banana" "lemon" "mango" "orange"
## [1] 2 3 5 7 13 20
```

Podemos acceder a los elementos del vector consultando su número de índice entre corchetes `[]`. El primer elemento tiene índice 1, el segundo elemento tiene índice 2, y así sucesivamente:

```r
fruits <- c("banana", "apple", "orange")

# Access the first item (banana)
fruits[1]
## [1] "banana"
```

También podemos acceder a varios elementos haciendo referencia a diferentes posiciones de índice con la función `c()`:

```r
fruits <- c("banana", "apple", "orange", "mango", "lemon")

# Access the first and third item (banana and orange)
fruits[c(1, 3)]
## [1] "banana" "orange"
```

También podemos usar números de índice negativos para acceder a todos los elementos excepto a los especificados:

```r
fruits <- c("banana", "apple", "orange", "mango", "lemon")

# Access all items except for the first item
fruits[c(-1)]
## [1] "apple" "orange" "mango" "lemon"
```

Para cambiar el valor de un elemento específico, consultmamos el número de índice:

```r
fruits <- c("banana", "apple", "orange", "mango", "lemon")

# Change "banana" to "pear"
fruits[1] <- "pear"

# Print fruits
fruits
## [1] "pear" "apple" "orange" "mango" "lemon"
```

# Secuencias

## Especificación de números dentro de una secuencia

Para especificar explícitamente números en una secuencia, puede usar el operador `:` para especificar todos los números enteros entre dos números especificados o la función combine `c()` para especificar explícitamente todos los números en la secuencia.

```r
# create a vector of integers between 1 and 10
1:10
## [1] 1 2 3 4 5 6 7 8 9 10

# create a vector consisting of 1, 5, and 10
c(1, 5, 10)
## [1] 1 5 10

# save the vector of integers between 1 and 10 as object x
x <- 1:10
x
## [1] 1 2 3 4 5 6 7 8 9 10
```

## Generación de secuencias regulares

Una generalización de `:` es la función `seq()`, que genera una secuencia de números con una progresión aritmética específica.

```r
seq(from, to, by, length.out, along.with)
```

- `from` = numero inical de la sequencia.
- `to` = numero final de la sequencia.
- `by` = es el incremento de la sequencia dada. Es calculada como ***((to-from) /(length.out-1))***.
- `length.out` = decide el largo total de la sequencia.
- `along.with` = entrega una sequencia con el mismo largo al vector indicado.

```r
# generate a sequence of numbers from 1 to 21 by increments of 2
seq(from = 1, to = 21, by = 2)
## [1] 1 3 5 7 9 11 13 15 17 19 21

# generate a sequence of numbers from 1 to 21 that has 15 equal incremented numbers
seq(0, 21, length.out = 15)
## [1] 0.0 1.5 3.0 4.5 6.0 7.5 9.0 10.5 12.0 13.5 15.0 16.5
## [13] 18.0 19.5 21.0

# generate a sequence of numbers from 1 to 25 that has the same lenght that y
y <- c(5,10,15,20)
seq(1, 25, along.with = y)
## [1] 1 9 17 25
```

La función `rep()` nos permite repetir convenientemente constantes específicas en vectores largos. Esta función permite repeticiones cotejadas y no cotejadas.

```r
# replicates the values in x a specified number of times
rep(1:4, times = 2)
## [1] 1 2 3 4 1 2 3 4

# replicates the values in x in a collated fashion
rep(1:4, each = 2)
## [1] 1 1 2 2 3 3 4 4
```

# Listas

Una lista en <img src="/uss-softwaredatascience/assets/images/r.svg" width="20"> puede contener muchos tipos de datos diferentes dentro de ella. Una lista es una colección de datos ordenados y modificables.

Para crear una lista, usamos la función `list()`:

```r
# List of strings
thislist <- list("apple", "banana", "cherry")

# Print the list
thislist4
## [[1]]
## [1] "apple"
## 
## [[2]]
## [1] "banana"
## 
## [[3]]
## [1] "cherry"
```

Podemos acceder a los elementos de la lista consultando su número de índice, entre paréntesis. El primer elemento tiene índice 1, el segundo elemento tiene índice 2, y así sucesivamente:

```r
thislist <- list("apple", "banana", "cherry")

thislist[1]
## [[1]]
## [1] "apple"
```

Para cambiar el valor de un elemento específico, referenciamos al número de índice:

```r
thislist <- list("apple", "banana", "cherry")
thislist[1] <- "blackcurrant"

# Print the updated list
thislist
## [[1]]
## [1] "blackcurrant"
## 
## [[2]]
## [1] "banana"
## 
## [[3]]
## [1] "cherry"
```

Para averiguar si un elemento específico está presente en una lista, usamos el operador `%in%`.

```r
thislist <- list("apple", "banana", "cherry")

"apple" %in% thislist
## [1] TRUE
```

Para agregar un elemento al final de la lista, usamos la función `append()`:

```r
thislist <- list("apple", "banana", "cherry")

append(thislist, "orange")
## [[1]]
## [1] "apple"
## 
## [[2]]
## [1] "banana"
## 
## [[3]]
## [1] "cherry"
## 
## [[4]]
## [1] "orange"
```

Puede especificar un rango de índices especificando dónde comenzar y dónde terminar el rango, usando el operador `:`:

```r
thislist <- list("apple", "banana", "cherry", "orange", "kiwi", "melon", "mango")

(thislist)[2:5]
## [[1]]
## [1] "banana"
## 
## [[2]]
## [1] "cherry"
## 
## [[3]]
## [1] "orange"
## 
## [[4]]
## [1] "kiwi"
```

Podemos recorrer los elementos de la lista usando un bucle `for`:

```r
thislist <- list("apple", "banana", "cherry")

for (x in thislist) {
  print(x)
}
## [1] "apple"
## [1] "banana"
## [1] "cherry"
```

Hay varias formas de unir o concatenar dos o más listas. La forma más común es usar la función `c()`, que combina dos elementos:

```r
list1 <- list("a", "b", "c")
list2 <- list(1,2,3)
list3 <- c(list1,list2)

list3
## [[1]]
## [1] "a"
## 
## [[2]]
## [1] "b"
## 
## [[3]]
## [1] "c"
## 
## [[4]]
## [1] 1
## 
## [[5]]
## [1] 2
## 
## [[6]]
## [1] 3
```

# Matrices

Una matriz es un conjunto de datos bidimensional con columnas y filas. Una columna es una representación vertical de datos, mientras que una fila es una representación horizontal de datos.

Podemos crear una matriz con la función `matrix()`. Especificamos los parámetros `nrow` y `ncol` para obtener la cantidad de filas y columnas:

```r
# Create a matrix
thismatrix <- matrix(c(1,2,3,4,5,6), nrow = 3, ncol = 2)

# Print the matrix
thismatrix
##      [,1] [,2]
## [1,]    1    4
## [2,]    2    5
## [3,]    3    6
```

Podemos acceder a los elementos usando `[]` corchetes. El primer número **1** entre corchetes especifica la posición de la fila, mientras que el segundo número **2** especifica la posición de la columna:

```r
thismatrix <- matrix(c("apple", "banana", "cherry", "orange"), nrow = 2, ncol = 2)

thismatrix[1, 2]
## [1] "cherry"
```

Se puede acceder a toda la fila si especifica una coma ***después*** del número entre paréntesis. Se puede acceder a toda la columna si especifica una coma ***antes*** del número entre paréntesis:

```r
thismatrix <- matrix(c("apple", "banana", "cherry", "orange"), nrow = 2, ncol = 2)

thismatrix[2,]
## [1] "banana" "orange"

thismatrix[,2]
## [1] "cherry" "orange"
```

Podemos acceder a más de una fila/columna si usamos la función `c()`:

```r
thismatrix <- matrix(c("apple", "banana", "cherry", "orange","grape", "pineapple", "pear", "melon", "fig"), nrow = 3, ncol = 3)

thismatrix[c(1,2),]
##      [,1]     [,2]     [,3]   
## [1,] "apple"  "orange" "pear" 
## [2,] "banana" "grape"  "melon"

thismatrix[, c(1,2)]
##      [,1]     [,2]       
## [1,] "apple"  "orange"   
## [2,] "banana" "grape"    
## [3,] "cherry" "pineapple"
```

Usamos la función `cbind()` para agregar columnas adicionales y `rbind()` para agregar filas adicionales en una matriz.

```r
thismatrix <- matrix(c("apple", "banana", "cherry", "orange","grape", "pineapple", "pear", "melon", "fig"), nrow = 3, ncol = 3)

newmatrix1 <- cbind(thismatrix, c("strawberry", "blueberry", "raspberry"))

# Print the new matrix
newmatrix1
##      [,1]     [,2]        [,3]    [,4]        
## [1,] "apple"  "orange"    "pear"  "strawberry"
## [2,] "banana" "grape"     "melon" "blueberry" 
## [3,] "cherry" "pineapple" "fig"   "raspberry" 

newmatrix2 <- rbind(thismatrix, c("strawberry", "blueberry", "raspberry"))

# Print the new matrix
newmatrix2
##      [,1]         [,2]        [,3]       
## [1,] "apple"      "orange"    "pear"     
## [2,] "banana"     "grape"     "melon"    
## [3,] "cherry"     "pineapple" "fig"      
## [4,] "strawberry" "blueberry" "raspberry"
```

Para averiguar si un elemento específico está presente en una matriz, usamos el operador `%in%`:

```r
thismatrix <- matrix(c("apple", "banana", "cherry", "orange"), nrow = 2, ncol = 2)

"apple" %in% thismatrix
## [1] TRUE
```

Usamos la función `dim()` para encontrar el número de filas y columnas y usamos la función `length()` para encontrar la dimensión `n x m` de una matriz:

```r
thismatrix <- matrix(c("apple", "banana", "cherry", "orange"), nrow = 2, ncol = 2)

dim(thismatrix)
## [1] 2 2

length(thismatrix)
## [1] 4
```

Podemos recorrer una matriz usando un bucle `for`. El ciclo comenzará en la primera fila, moviéndose hacia la derecha:

```r
thismatrix <- matrix(c("apple", "banana", "cherry", "orange"), nrow = 2, ncol = 2)

for (rows in 1:nrow(thismatrix)) {
  for (columns in 1:ncol(thismatrix)) {
    print(thismatrix[rows, columns])
  }
}
## [1] "apple"
## [1] "cherry"
## [1] "banana"
## [1] "orange"
```

Nuevamente, podemos usar la función `rbind()` o `cbind()` para combinar dos o más matrices juntas:

```r
# Combine matrices
Matrix1 <- matrix(c("apple", "banana", "cherry", "grape"), nrow = 2, ncol = 2)
Matrix2 <- matrix(c("orange", "mango", "pineapple", "watermelon"), nrow = 2, ncol = 2)

# Adding it as a rows
Matrix_Combined <- rbind(Matrix1, Matrix2)
Matrix_Combined

# Adding it as a columns
Matrix_Combined <- cbind(Matrix1, Matrix2)
Matrix_Combined

##     [,1]     [,2]        
## [1,] "apple"  "cherry"    
## [2,] "banana" "grape"     
## [3,] "orange" "pineapple" 
## [4,] "mango"  "watermelon"
##      [,1]     [,2]     [,3]     [,4]        
## [1,] "apple"  "cherry" "orange" "pineapple" 
## [2,] "banana" "grape"  "mango"  "watermelon"
```