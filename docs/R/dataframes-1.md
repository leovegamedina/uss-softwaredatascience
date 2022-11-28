---
layout: default
title: readr
parent: Dataframes con Tidyverse
grand_parent: Unidad 1 - Estructura de Datos en R
permalink: /docs/R/dataframes/dataframes-1/
nav_order: 1
---

# <img src="/uss-softwaredatascience/assets/images/readr.png" width="40"> readr 

El objetivo de `readr` es proporcionar una forma rápida y sencilla de leer datos rectangulares de archivos delimitados, como valores separados por comas (CSV) y valores separados por tabuladores (TSV). Está diseñado para analizar muchos tipos de datos que se encuentran en la naturaleza, al tiempo que proporciona un informe de problemas informativo cuando el análisis conduce a resultados inesperados.

Para leer un conjunto de datos rectangular con readr, se combinan dos piezas: una función que analiza las líneas del archivo en campos individuales y otra de especificación de columna.

Eset admite los siguientes formatos de archivo con estas funciones `read_*()`:

- `read_csv()`: comma-separated values (CSV) files.
- `read_tsv()`: tab-separated values (TSV) files.
- `read_delim()`: delimited files (CSV and TSV are important special cases).
- `read_fwf()`: fixed-width files.
- `read_table()`: whitespace-separated files.
- `read_log()`: web log files.

Para revisar las especificaciones de las columnas podemos usar la funcion `spec()`:

```r
chickens <- read_csv(readr_example("chickens.csv"))
spec(chickens)
#> cols(
#>   chicken = col_character(),
#>   sex = col_character(),
#>   eggs_laid = col_double(),
#>   motto = col_character()
#> )
```
Por otro lado, si es que necesitamos cargar el dataset con las columnas en su tipo de dato correspondiente, podemos usar las siguientes funciones para forzar el tipo de dato a traves del parametro `col_types`. Los tipos de datos disponibles para modificar son los siguientes:

- `col_logical()` - "l"
- `col_integer()` - "i"
- `col_double()` - "d"
- `col_number()` - "n"
- `col_character()` - "c"
- `col_factor(levels, ordered = FALSE)` - "f"
- `col_datetime(format = "")` - "T"
- `col_date(format = "")` - "D"
- `col_time(format = "")` - "t"
- `col_skip()` - "-", "_" ***(ignora la columna cuando se lee el archivo)***
- `col_guess()` - "?" ***(analiza usando el tipo "mejor" basado en la entrada)***

```r
chickens <- read_csv(
  readr_example("chickens.csv"),
  col_types = cols(
    chicken   = col_character(),
    sex       = col_factor(levels = c("rooster", "hen")),
    eggs_laid = col_integer(),
    motto     = col_character()
  )
)
chickens
#> # A tibble: 5 × 4
#>   chicken                 sex     eggs_laid motto                               
#>   <chr>                   <fct>       <int> <chr>                               
#> 1 Foghorn Leghorn         rooster         0 That's a joke, ah say, that's a jok…
#> 2 Chicken Little          hen             3 The sky is falling!                 
#> 3 Ginger                  hen            12 Listen. We'll either die free chick…
#> 4 Camilla the Chicken     hen             7 Bawk, buck, ba-gawk.                
#> 5 Ernie The Giant Chicken rooster         0 Put Captain Solo in the cargo hold.
```

En el caso que queramos guardar el dataframe, podemos utilizar multiples funciones de la familia `format_*()` y `write_*()`:

Convierte dataframes a un string delimitado:

- `format_delim()`: se puede espicificar un delimitador.
- `format_csv()`: utiliza el formato csv (,).
- `format_csv2()`: utiliza el formato de csv2 (;).
- `format_tsv()`: utiliza el formato tsv.

Guarda dataframes en archivos delimitados:

- `write_delim()`: se puede espicificar un delimitador.
- `write_csv()`: utiliza el formato csv (,).
- `write_csv2()`: utiliza el formato de csv2 (;).
- `write_excel_csv()`: utiliza el formato csv (,) para guardar en archivo excel (.xlsx).
- `write_excel_csv2()`: utiliza el formato csv2 (;) para guardar en archivo excel (.xlsx).
- `write_tsv()`: utiliza el formato tsv.

Aca pueden ver el cheatsheet del paquete:

[![](/uss-softwaredatascience/assets/images/readr_image.png)](https://github.com/leovegamedina/uss-softwaredatascience/blob/main/assets/images/datacamp.png)