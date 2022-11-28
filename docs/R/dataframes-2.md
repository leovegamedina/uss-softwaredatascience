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

