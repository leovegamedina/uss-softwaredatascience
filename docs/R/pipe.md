---
layout: default
title: Operador Pipe
parent: Unidad 1 - Estructura de Datos en R
nav_order: 10
---

# Operador Pipe

Eliminar la duplicación es un principio importante a tener en cuenta con nuestro código; sin embargo, igualmente importante es mantener nuestro código ***eficiente*** y ***legible***. La eficiencia a menudo se logra aprovechando funciones y declaraciones de control en nuestro código. Sin embargo, la eficiencia también incluye la eliminación de la creación y el almacenamiento de objetos innecesarios que a menudo resultan cuando se intenta que el código sea más legible, claro y explícito. En consecuencia, escribir código que sea simple, legible y eficiente a menudo se considera contradictorio.

Por esta razón, el paquete `magrittr` es una herramienta poderosa para tener en su conjunto de herramientas de gestión de datos.

La función principal proporcionada por el paquete magrittr es `%>%` , o lo que se llama el operador `pipe`. Este operador reenviará un valor, o el resultado de una expresión, a la siguiente llamada/expresión de función.

```r
filter (data, variable == numeric_value)    # option 1
data %>% filter(variable == numeric_value)  # option 2
```

Para ver la ventaja evidente de eficiencia en codigo, podemos revisar el siguiente ejemplo:

```r
# Nested Option
arrange(
    summarize(
        group_by(
            filter(mtcars, carb > 1),
            cyl
            ),
        Avg_mpg = mean(mpg)
        ),
    desc(Avg_mpg)
)
## Source: local data frame [3 x 2]
##
## cyl Avg_mpg
## (dbl) (dbl)
## 1 4 25.90
## 2 6 19.74
## 3 8 15.10 
```

```r
# Multiple Object Option
a <- filter(mtcars, carb > 1)
b <- group_by(a, cyl)
c <- summarise(b, Avg_mpg = mean(mpg))
d <- arrange(c, desc(Avg_mpg))
print(d)
## Source: local data frame [3 x 2]
##
## cyl Avg_mpg
## (dbl) (dbl)
## 1 4 25.90
## 2 6 19.74
## 3 8 15.10 
```

```r
# %>% Option
mtcars %>%
    filter(carb > 1) %>%
    group_by(cyl) %>%
    summarise(Avg_mpg = mean(mpg)) %>%
    arrange(desc(Avg_mpg))
## Source: local data frame [3 x 2]
##
## cyl Avg_mpg
## (dbl) (dbl)
## 1 4 25.90
## 2 6 19.74
## 3 8 15.10 
```

Dado que <img src="/uss-softwaredatascience/assets/images/r.svg" width="20"> es un lenguaje de programación funcional, lo que significa que todo lo que hacemos se basa básicamente en funciones, podemos usar el operador pipe para alimentar casi cualquier llamada de argumento. Por ejemplo, podemos conectarnos a una función de regresión lineal `lm()` y luego obtener el resumen de los parámetros de regresión.

```r
mtcars %>%
    filter(carb > 1) %>%
    lm(mpg ~ cyl + hp, data = .) %>%
    summary()
##
## Call:
## lm(formula = mpg ~ cyl + hp, data = .)
##
## Residuals:
## Min 1Q Median 3Q Max
## -4.6163 -1.4162 -0.1506 1.6181 5.2021
##
## Coefficients:
## Estimate Std. Error t value Pr(>|t|)
## (Intercept) 35.67647 2.28382 15.621 2.16e-13 ***
## cyl -2.22014 0.52619 -4.219 0.000353 ***
## hp -0.01414 0.01323 -1.069 0.296633
## ---
## Signif. codes: 0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
##
## Residual standard error: 2.689 on 22 degrees of freedom
## Multiple R-squared: 0.7601, Adjusted R-squared: 0.7383
## F-statistic: 34.85 on 2 and 22 DF, p-value: 1.516e-07
```

{: .note-title }
> NOTA
>
> En este caso le indicamos de la siguiente forma `datos = .` a la función lm(), para que entienda que se trabaja con el set de datos de la funcion anterior en el pipe.

`magrittr` también ofrece algunos operadores pipe alternativos. Algunas funciones, como las funciones de plotting, harán que termine la cadena. El operador `tee` (`%T>%`) nos permite continuar con las funciones que normalmente provocan la terminación.

```r
# inserting %T>% allows you to plot and perform the functions that
# follow the plotting function
mtcars %>%
    filter (carb > 1) %>%
    extract (, 1:4) %T>%
    plot () %>%
    summary ()
```
<img src="/uss-softwaredatascience/assets/images/plotting_tee.png" width="550">

```r
## mpg cyl disp hp
## Min. :10.40 Min. :4.00 Min. : 75.7 Min. : 52.0
## 1st Qu.:15.20 1st Qu.:6.00 1st Qu.:146.7 1st Qu.:110.0
## Median :17.80 Median :8.00 Median :275.8 Median :175.0
## Mean :18.62 Mean :6.64 Mean :257.7 Mean :163.7
## 3rd Qu.:21.00 3rd Qu.:8.00 3rd Qu.:351.0 3rd Qu.:205.0
## Max. :30.40 Max. :8.00 Max. :472.0 Max. :335.0
```

El operador de asignación compuesta `%<>%` se usa para actualizar un valor primero canalizándolo en una o más expresiones y luego asignando el resultado. El uso de `%<>%` realizará las funciones a la derecha de `%<>%` y guardará los cambios que estas funciones realizan en la variable o dataframe llamado a la izquierda de `%<>%`.

```r
# we can square root mpg and save this change using %<>%
mtcars$mpg %<>% sqrt
head(mtcars)
##                        mpg cyl disp  hp drat    wt  qsec vs am gear carb
## Mazda RX4         4.582576   6  160 110 3.90 2.620 16.46  0  1    4    4
## Mazda RX4 Wag     4.582576   6  160 110 3.90 2.875 17.02  0  1    4    4
## Datsun 710        4.774935   4  108  93 3.85 2.320 18.61  1  1    4    1
## Hornet 4 Drive    4.626013   6  258 110 3.08 3.215 19.44  1  0    3    1
## Hornet Sportabout 4.324350   8  360 175 3.15 3.440 17.02  0  0    3    2
## Valiant           4.254409   6  225 105 2.76 3.460 20.22  1  0    3    1
```

El operador de exposición `%$%` es útil cuando desea canalizar un dataframe, que puede contener muchas columnas, en una función que solo se aplica a algunas de las columnas.

```r
# regular piping results in an error
mtcars %>%
    subset(vs == 0) %>%
    cor(mpg, wt)
## Error in pmatch(use, c("all.obs", "complete.obs", "pairwise.complete.obs", : object 'wt' not found

# using %$% allows you to specify variables of interest
mtcars %>%
    subset(vs == 0) %$%
    cor(mpg, wt)
## [1] -0.830671 
```