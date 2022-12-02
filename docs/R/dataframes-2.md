---
layout: default
title: readxl
parent: Dataframes con Tidyverse
grand_parent: Unidad 1 - Estructura de Datos en R
permalink: /docs/R/dataframes/dataframes-2/
nav_order: 2
---

# <img src="/uss-softwaredatascience/assets/images/readxl.png" width="40"> readxl 

El paquete `readxl` facilita la transferencia de datos de Excel a R. En comparación con muchos de los paquetes existentes (por ejemplo, gdata, xlsx, xlsReadWrite), readxl no tiene dependencias externas, por lo que es fácil de instalar y usar en todos los sistemas operativos. Está diseñado para trabajar con datos tabulares.

readxl admite tanto el formato legacy `.xls` como el formato moderno basado en xml `.xlsx`.

`read_excel()` lee archivos `xls` y `xlsx` y detecta el formato de la extensión.

```r
xlsx_example <- readxl_example("datasets.xlsx")
read_excel(xlsx_example)
#> # A tibble: 150 × 5
#>   Sepal.Length Sepal.Width Petal.Length Petal.Width Species
#>          <dbl>       <dbl>        <dbl>       <dbl> <chr>  
#> 1          5.1         3.5          1.4         0.2 setosa 
#> 2          4.9         3            1.4         0.2 setosa 
#> 3          4.7         3.2          1.3         0.2 setosa 
#> # … with 147 more rows
#> # ℹ Use `print(n = ...)` to see more rows

xls_example <- readxl_example("datasets.xls")
read_excel(xls_example)
#> # A tibble: 150 × 5
#>   Sepal.Length Sepal.Width Petal.Length Petal.Width Species
#>          <dbl>       <dbl>        <dbl>       <dbl> <chr>  
#> 1          5.1         3.5          1.4         0.2 setosa 
#> 2          4.9         3            1.4         0.2 setosa 
#> 3          4.7         3.2          1.3         0.2 setosa 
#> # … with 147 more rows
#> # ℹ Use `print(n = ...)` to see more rows
```

Se puede enumerar los nombres de las hojas con `excel_sheets()`.

```r
excel_sheets(xlsx_example)
#> [1] "iris"   "mtcars"    "chickwts"   "quakes"
```

Se especifica una hoja de trabajo por nombre o número.

```r
read_excel(xlsx_example, sheet = "chickwts")
#> # A tibble: 71 × 2
#>   weight feed     
#>    <dbl> <chr>    
#> 1    179 horsebean
#> 2    160 horsebean
#> 3    136 horsebean
#> # … with 68 more rows
#> # ℹ Use `print(n = ...)` to see more rows

read_excel(xls_example, sheet = 4)
#> # A tibble: 1,000 × 5
#>     lat  long depth   mag stations
#>   <dbl> <dbl> <dbl> <dbl>    <dbl>
#> 1 -20.4  182.   562   4.8       41
#> 2 -20.6  181.   650   4.2       15
#> 3 -26    184.    42   5.4       43
#> # … with 997 more rows
#> # ℹ Use `print(n = ...)` to see more rows
```

Hay varias formas de controlar las celdas que se leen. Se pueden especificar los rangos de distintas maneras al estilo Excel. Adicionalmente, si existen celdas en blanco, se puede setear el argumento `na` con un valor especifico.

```r
read_excel(xlsx_example, n_max = 3)
#> # A tibble: 3 × 5
#>   Sepal.Length Sepal.Width Petal.Length Petal.Width Species
#>          <dbl>       <dbl>        <dbl>       <dbl> <chr>  
#> 1          5.1         3.5          1.4         0.2 setosa 
#> 2          4.9         3            1.4         0.2 setosa 
#> 3          4.7         3.2          1.3         0.2 setosa

read_excel(xlsx_example, range = "C1:E4")
#> # A tibble: 3 × 3
#>   Petal.Length Petal.Width Species
#>          <dbl>       <dbl> <chr>  
#> 1          1.4         0.2 setosa 
#> 2          1.4         0.2 setosa 
#> 3          1.3         0.2 setosa

read_excel(xlsx_example, range = cell_rows(1:4))
#> # A tibble: 3 × 5
#>   Sepal.Length Sepal.Width Petal.Length Petal.Width Species
#>          <dbl>       <dbl>        <dbl>       <dbl> <chr>  
#> 1          5.1         3.5          1.4         0.2 setosa 
#> 2          4.9         3            1.4         0.2 setosa 
#> 3          4.7         3.2          1.3         0.2 setosa

read_excel(xlsx_example, range = cell_cols("B:D"))
#> # A tibble: 150 × 3
#>   Sepal.Width Petal.Length Petal.Width
#>         <dbl>        <dbl>       <dbl>
#> 1         3.5          1.4         0.2
#> 2         3            1.4         0.2
#> 3         3.2          1.3         0.2
#> # … with 147 more rows
#> # ℹ Use `print(n = ...)` to see more rows

read_excel(xlsx_example, range = "mtcars!B1:D5")
#> # A tibble: 4 × 3
#>     cyl  disp    hp
#>   <dbl> <dbl> <dbl>
#> 1     6   160   110
#> 2     6   160   110
#> 3     4   108    93
#> # … with 1 more row
#> # ℹ Use `print(n = ...)` to see more rows

read_excel(xlsx_example, na = "setosa")
#> # A tibble: 150 × 5
#>   Sepal.Length Sepal.Width Petal.Length Petal.Width Species
#>          <dbl>       <dbl>        <dbl>       <dbl> <chr>  
#> 1          5.1         3.5          1.4         0.2 <NA>   
#> 2          4.9         3            1.4         0.2 <NA>   
#> 3          4.7         3.2          1.3         0.2 <NA>   
#> # … with 147 more rows
#> # ℹ Use `print(n = ...)` to see more rows
```

Aca pueden ver el cheatsheet del paquete:

[![](/uss-softwaredatascience/assets/images/readr_image.png)](https://github.com/leovegamedina/uss-softwaredatascience/blob/main/assets/images/readr.pdf)