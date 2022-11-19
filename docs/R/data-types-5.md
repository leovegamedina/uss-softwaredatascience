---
layout: default
title: Datetimes
parent: Data Types
grand_parent: Unidad 1 - Estructura de Datos en R
permalink: /docs/R/data-types/data-types-5/
nav_order: 5
---

# Datetimes

Los datos del mundo real a menudo se asocian con fechas y horas; sin embargo, manejar las fechas con precisión puede parecer una tarea complicada debido a la variedad de formatos y teniendo en cuenta las diferencias de zona horaria y los años bisiestos. <img src="/uss-softwaredatascience/assets/images/r.svg" width="20"> tiene una variedad de funciones que le permiten trabajar con fechas y horas. Además, paquetes como `lubridate` facilitan el trabajo con fechas y horas.

Para facilitar el trabajo, en este curso veremos directamente las funciones de **lubridate**.

## Obtener fecha y hora actuales

```r
x <- c("2015-07-01", "2015-08-01", "2015-09-01") 
y <- c("07/01/2015", "07/01/2015", "07/01/2015") 

ymd(x)
## [1] "2015-07-01 UTC" "2015-08-01 UTC" "2015-09-01 UTC"

mdy(y)
## [1] "2015-07-01 UTC" "2015-07-01 UTC" "2015-07-01 UTC"
```

Uno de los muchos beneficios del paquete de `lubridate` es que automáticamente reconoce los separadores comunes utilizados al registrar fechas (`"-"`, `"/"`, `"."` y `""`).

| Orden                                     | Función    |
|:------------------------------------------|:-----------|
| year, month, day                          | ymd()      | 
| year, day, month                          | ydm()      | 
| month, day, year                          | mdy()      | 
| day, month, year                          | dmy()      | 
| hour, minute                              | hm()       | 
| hour, minute, second                      | hms()      | 
| year, month, day, hour, minute, second    | ymd_hms()  | 

## Extraer y manipular partes de fechas

Las funciones proporcionadas por `lubridate` para realizar extracción y manipulación de fechas incluyen:

| Componente Fecha    | Accesor    |
|:--------------------|:-----------|
| Year                | year()     | 
| Month               | month()    | 
| Week                | week()     | 
| Day of year         | yday()     | 
| Day of month        | mday()     | 
| Day of week         | wday()     | 
| Hour                | hour()     | 
| Minute              | minute()   | 
| Second              | second()   | 
| Time zone           | tz()       | 

```r
x <- c("2015-07-01", "2015-08-01", "2015-09-01")
year(x)
## [1] 2015 2015 2015
# default is numerical value

month(x)
## [1] 7 8 9

# show abbreviated name
month(x, label = TRUE)
## [1] Jul Aug Sep
## 12 Levels: Jan < Feb < Mar < Apr < May < Jun < Jul < Aug < Sep < … < Dec

# show unabbreviated name
month(x, label = TRUE, abbr = FALSE)
## [1] July August September
## 12 Levels: January < February < March < April < May < June < … < December

wday(x, label = TRUE, abbr = FALSE)
## [1] Wednesday Saturday Tuesday
## 7 Levels: Sunday < Monday < Tuesday < Wednesday < Thursday < … < Saturday
```

## Creación de secuencias de fechas

```r
seq(ymd("2010-1-1"), ymd("2015-1-1"), by = "years")
## [1] "2010-01-01 UTC" "2011-01-01 UTC" "2012-01-01 UTC" "2013- 01- 01 UTC"
## [5] "2014-01-01 UTC" "2015-01-01 UTC"

seq(ymd("2015/1/1"), ymd("2015/12/30"), by = "quarter")
## [1] "2015-01-01 UTC" "2015-04-01 UTC" "2015-07-01 UTC" "2015- 10- 01 UTC"

seq(ymd('2015-09-15'), ymd('2015-09-30'), by = "2 days")
## [1] "2015-09-15 UTC" "2015-09-17 UTC" "2015-09-19 UTC" "2015- 09- 21 UTC"
## [5] "2015-09-23 UTC" "2015-09-25 UTC" "2015-09-27 UTC" "2015- 09- 29 UTC"
```

## Cálculos con fechas

```r
x <- now()
x
## [1] "2015-09-26 10:08:18 EDT"

y <- ymd("2015-09-11")
x > y
## [1] TRUE

x - y
## Time difference of 15.5891 days

y + days(4)
## [1] "2015-09-15 UTC"

x - hours(4)
## [1] "2015-09-26 06:08:18 EDT"TC" "2015- 09- 21 UTC"
## [5] "2015-09-23 UTC" "2015-09-25 UTC" "2015-09-27 UTC" "2015- 09- 29 UTC"
```

> {: .highlight }
  Se recomienda que puedan revisar el paquete  [`lubridate`](https://lubridate.tidyverse.org/reference/index.html) ya que cuenta con muchisimas funciones utiles para hacer manipulacion de datos.