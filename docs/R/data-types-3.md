---
layout: default
title: Strings
parent: Data Types
grand_parent: Unidad 1 - Estructura de Datos en R
permalink: /docs/R/data-types/data-types-3/
nav_order: 3
---

# Strings 🔤

El manejo de cadenas de caracteres a menudo se subestima en el entrenamiento de análisis de datos. El enfoque normalmente permanece en los valores numéricos; sin embargo, el crecimiento en la recopilación de datos también está generando más bits de información integrados en cadenas de caracteres. En consecuencia, el manejo, la limpieza y el procesamiento de cadenas de caracteres se está convirtiendo en un requisito previo en el análisis diario de datos.
{: .text-justify}

## Creando Strings

La forma más básica de crear cadenas es usar comillas y asignar una cadena a un objeto similar a la creación de secuencias numéricas.

```r
a <- "learning to create" # create string a
b <- "character strings" # create string b 
```

La función `paste()` proporciona un medio versátil para crear y construir cadenas. Toma uno o más objetos <img src="/uss-softwaredatascience/assets/images/r.svg" width="20">, los convierte en "carácter" y luego los concatena (pega) para formar una o varias cadenas de caracteres.

```r
# paste together string a & b
paste(a, b) 
## [1] "learning to create character strings"

# paste character and number strings (converts numbers to character class)
paste("The life of", pi)
## [1] "The life of 3.14159265358979"

# paste multiple strings
paste("I", "love", "R")
## [1] "I love R"

# paste multiple strings with a separating character
paste("I", "love", "R", sep = "-")
## [1] "I-love-R"

# use paste0() to paste without spaces btwn characters
paste0("I", "love", "R")
## [1] "IloveR"

# paste objects with different lengths
paste("R", 1:5, sep = "v1.")
## [1] "R v1.1" "R v1.2" "R v1.3" "R v1.4" "R v1.5"
```

{: .note-title }
> is.character()
>
> Al igual que en los otros tipos de datos vistos, tambien tenemos una funcion para revisar si es de tipo character nuestra variable, esta es la funcion `is.character()`

```r
a <- "The life of"
b <- pi

is.character(a)
## [1] TRUE

is.character(b)
## [1] FALSE 
```
## Convirtiendo a Strings

Adicional, tambien contamos con la funcion `as.character()` para convertir a tipo character.

```r
c <- as.character(b)
is.character(c)
## [1] TRUE 
```

{: .note-title }
> toString()
>
> Otra alternativa a *`as.character()`* es la funcion `toString()`, la diferencia radica en que esta última, tiene la capacidad de juntar todos las variables en un solo caracter.

```r
toString(c("Aug", 24, 1980))
## [1] "Aug, 24, 1980" 

as.character(c("Aug", 24, 1980))
## [1] "Aug"  "24"   "1980"
```

## Contando Elementos Strings y Caractéres

Para contar el número de elementos en una cadena, usamos `length()`:

```r
length("How many elements are in this string?")
## [1] 1

length(c("How", "many", "elements", "are", "in", "this", "string?"))
## [1] 7
```

Para contar el número de caracteres en una cadena, usamos `nchar()`:

```r
nchar("How many characters are in this string?")
## [1] 

nchar(c("How", "many", "characters", "are", "in", "this", "string?"))
## [1] 3 4 10 3 2 4 7 
```

## Case Conversion

Para convertir todos los caracteres en mayúsculas a minúsculas, usamos `tolower()`:

```r
x <- "Learning To MANIPULATE strinGS in R"
tolower(x)
## [1] "learning to manipulate strings in r"
```

Para convertir todos los caracteres en minúsculas a mayúsculas, usamos `toupper()`:

```r
toupper(x)
## [1] "LEARNING TO MANIPULATE STRINGS IN R" 
```

## Reemplazo de caracteres simples

Para reemplazar un carácter (o varios caracteres) en una cadena, usamos `chartr()`:

```r
# replace 'A' with 'a'
x <- "This is A string."
chartr(old = "A", new = "a", x)
## [1] "This is a string."

# multiple character replacements
# replace any 'd' with 't' and any 'z' with 'a'
y <- "Tomorrow I plzn do lezrn zbout dexduzl znzlysis."
chartr(old = "dz", new = "ta", y)
## [1] "Tomorrow I plan to learn about textual analysis."
```

{: .warning-title }
> advertencia
>
> Tenga en cuenta que `chartr()` reemplaza todas las letras identificadas por reemplazo, por lo que la única vez que se debe usar es cuando ***se esta seguro de que se quiere cambiar todas las posibles apariciones*** de una letra.

## Extraer/Reemplazar Substrings

Para extraer o reemplazar subcadenas en un vector de caracteres, hay tres funciones básicas en <img src="/uss-softwaredatascience/assets/images/r.svg" width="20"> para usar: `substr()`, `substring()` y `strsplit()`.

El propósito de `substr()` es extraer y reemplazar subcadenas con caracteres de inicio y fin específicos:

```r
alphabet <- paste(LETTERS, collapse = "")

# extract 18th character in string
substr(alphabet, start = 18, stop = 18)
## [1] "R"

# extract 18-24th characters in string
substr(alphabet, start = 18, stop = 24)
## [1] "RSTUVWX"

# replace 19-24th characters with `R`
substr(alphabet, start = 19, stop = 24) <- "RRRRRR"
alphabet
## [1] "ABCDEFGHIJKLMNOPQRRRRRRRYZ" 
```

El propósito de `substring()` es extraer y reemplazar subcadenas con solo un punto de inicio especificado. `substring()` también permite extraer/reemplazar de forma ***recursiva***:

```r
alphabet <- paste(LETTERS, collapse = "")

# extract 18th through last character
substring(alphabet, first = 18)
## [1] "RSTUVWXYZ"

# recursive extraction; specify start position only
substring(alphabet, first = 18:24)
## [1] "RSTUVWXYZ" "STUVWXYZ" "TUVWXYZ" "UVWXYZ" "VWXYZ" "WXYZ"
## [7] "XYZ"

# recursive extraction; specify start and stop positions
substring(alphabet, first = 1:5, last = 3:7)
## [1] "ABC" "BCD" "CDE" "DEF" "EFG" 
```

Para dividir los elementos de una cadena de caracteres, usamos `strsplit()`:

```r
z <- "The day after I will take a break and drink a beer."
strsplit(z, split = " ")
## [[1]]
## [1] "The" "day" "after" "I" "will" "take" "a" "break"
## [9] "and" "drink" "a" "beer."

a <- "Alabama-Alaska-Arizona-Arkansas-California"
strsplit(a, split = "-")
## [[1]]
## [1] "Alabama" "Alaska" "Arizona" "Arkansas" "California" 
```

{: .note-title }
> nota
>
> Tenga en cuenta que la salida de *`strsplit()`* es una lista. Para convertir la salida en un vector simple, usamos `unlist()`:
```r
unlist(strsplit(a, split = "-"))
## [1] "Alabama" "Alaska" "Arizona" "Arkansas" "California" 
```

> {: .highlight }
  Se recomienda que puedan revisar el paquete de tydiverse [`stringr`](https://stringr.tidyverse.org/) ya que esta fuera del scope del curso, pero tiene una ***gran capacidad de hacer manipulacion de strings***.

  > {: .highlight }
  Se recomienda que puedan revisar el ***Capitulo 6*** del libro [Data Wrangling with R. Use R!](https://github.com/leovegamedina/uss-softwaredatascience/blob/main/books/Data%20Wrangling%20with%20R.%20Use%20R!.pdf) donde se enseña el uso de `Regex`, el cual esta fuera del scope del curso.