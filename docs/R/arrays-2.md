---
layout: default
title: Sequencias de Números Aleatoreos
parent: Arreglos
grand_parent: Unidad 1 - Estructura de Datos en R
permalink: /docs/R/arrays/arrays-2/
nav_order: 2
---

# Sequencias de Números Aleatoreos

La simulación es una práctica común en el análisis de datos. A veces, su análisis requiere la implementación de un procedimiento estadístico que requiere la generación o muestreo de números aleatorios (es decir, simulación de Monte Carlo, muestreo de arranque, etc.). <img src="/uss-softwaredatascience/assets/images/r.svg" width="20"> viene con un conjunto de generadores de números pseudoaleatorios que le permiten simular las distribuciones de probabilidad más comunes, como Uniforme, Normal, Binomial, Poisson, Exponencial y Gamma.

Para cada distribución de probabilidad no uniforme hay cuatro funciones principales disponible para generar números aleatorios, densidad (PDF), densidad acumulada (CDF) y cuantiles. Los prefijos para estas funciones son:

- `r`: generación de números aleatorios.
- `d`: función de masa de densidad o probabilidad (PDF)
- `p`: distribución acumulada (CDF)
- `q`: cuantiles

## Distribución Uniforme

Para generar números aleatorios a partir de una distribución uniforme, puede utilizar la función `runif()`. Alternativamente, puede usar `sample()` para tomar una muestra aleatoria con o sin reemplazos.

```r
# generate n random numbers between the default values of 0 and 1
runif(n)

# generate n random numbers between 0 and 25
runif(n, min = 0, max = 25)

# generate n random numbers between 0 and 25 (with replacement)
sample(0:25, n, replace = TRUE)

# generate n random numbers between 0 and 25 (without replacement)
sample(0:25, n, replace = FALSE) 
```

Por ejemplo, para generar 25 números aleatorios entre los valores 0 y 10:

```r
runif(25, min = 0, max = 10)
## [1] 6.11473003 9.72918761 0.04977565 0.98291110 8.53146606 1.17408103
## [7] 1.09907810 5.83266343 8.04336903 1.70783108 3.13275943 1.28380380
## [13] 8.67087873 8.02653947 7.23398025 4.62386458 3.03617622 6.10895175
## [19] 6.39970018 9.02183043 3.24990736 4.64181107 5.35496769 9.97374324
## [25] 3.30954880 
```

## Distribución Normal

La distribución normal (o gaussiana) es la distribución más común y conocida. Dentro de <img src="/uss-softwaredatascience/assets/images/r.svg" width="20">, las funciones de distribución normal se escriben como `norm()`.

```r
# generate n random numbers from a normal distribution with given mean and standard deviation
rnorm(n, mean = 0, sd = 1)

# generate CDF probabilities for value(s) in vector q
pnorm(q, mean = 0, sd = 1)

# generate quantile for probabilities in vector p
qnorm(p, mean = 0, sd = 1)

# generate density function probabilites for value(s) in vector x
dnorm(x, mean = 0, sd = 1) 
```

Por ejemplo, para generar 25 números aleatorios a partir de una distribución normal con **media = 100** y **desviación estándar = 15**:

```r
x <- rnorm(25, mean = 100, sd = 15)
x
## [1] 97.43216 98.98658 96.43514 73.77727 100.51316 103.11050 111.36823
## [8] 102.09288 101.16769 114.54549 99.28044 97.51866 110.57522 87.85074
## [15] 86.67675 108.95660 88.45750 106.28923 114.22225 80.17450 110.39667
## [22] 96.87112 112.30709 110.54963 93.24365

summary(x)
## Min. 1st Qu. Median Mean 3rd Qu. Max.
## 73.78 96.44 100.50 100.10 110.40 114.50 
```

También puede pasar un vector de valores. Por ejemplo, digamos que desea conocer las probabilidades CDF para cada valor en el vector x creado anteriormente:

```r
pnorm(x, mean = 100, sd = 15)
## [1] 0.43203732 0.47306731 0.40607337 0.04021628 0.51364538 0.58213815
## [7] 0.77573919 0.55548261 0.53102479 0.83390182 0.48086992 0.43430567
## [13] 0.75959941 0.20898424 0.18721209 0.72478191 0.22079836 0.66249503
## [19] 0.82847339 0.09313407 0.75588023 0.41738339 0.79402667 0.75906822
## [25] 0.32620260
```

## Distribución Binomial

Esto se interpreta convencionalmente como el número de éxitos en `size = x` intentos y con `prob = p` probabilidad de éxito:

```r
# generate a vector of length n displaying the number of successes from a trial size = 100 with a probability of success = 0.5
rbinom(n, size = 100, prob = 0.5)

# generate CDF probabilities for value(s) in vector q
pbinom(q, size = 100, prob = 0.5)

# generate quantile for probabilities in vector p
qbinom(p, size = 100, prob = 0.5)

# generate density function probabilites for value(s) in vector x
dbinom(x, size = 100, prob = 0.5) 
```

## Distribución Poisson

La distribución de Poisson es una distribución de probabilidad discreta que expresa la probabilidad de que ocurra un número dado de eventos en un intervalo fijo de tiempo y/o espacio si estos eventos ocurren con una tasa promedio conocida e independientemente del tiempo transcurrido desde el último evento.

```r
# generate a vector of length n displaying the random number of events occurring when lambda (mean rate) equals 4.
rpois(n, lambda = 4)

# generate CDF probabilities for value(s) in vector q when lambda (mean rate) equals 4.
ppois(q, lambda = 4)

# generate quantile for probabilities in vector p when lambda (mean rate) equals 4.
qpois(p, lambda = 4)

# generate density function probabilites for value(s) in vector x when lambda (mean rate) equals 4.
dpois(x, lambda = 4) 
```

## Distribución Exponencial

La distribución de probabilidad exponencial describe el tiempo entre eventos en un proceso de Poisson.

```r
# generate a vector of length n with rate = 1
rexp(n, rate = 1)

# generate CDF probabilities for value(s) in vector q when rate = 4.
pexp(q, rate = 1)

# generate quantile for probabilities in vector p when rate = 4.
qexp(p, rate = 1)

# generate density function probabilites for value(s) in vector xwhen rate = 4.
dexp(x, rate = 1)
```

## Distribución Gamma

La distribución de probabilidad Gamma está relacionada con la distribución Beta y surge naturalmente en procesos para los cuales los tiempos de espera entre eventos distribuidos de Poisson son relevantes.

```r
# generate a vector of length n with shape parameter = 1
rgamma(n, shape = 1)

# generate CDF probabilities for value(s) in vector q when shape parameter = 1.
pgamma(q, shape = 1)

# generate quantile for probabilities in vector p when shape parameter = 1.
qgamma(p, shape = 1)

# generate density function probabilites for value(s) in vector x when shape parameter = 1.
dgamma(x, shape = 1) 
```

## Configuración de semilla para números aleatorios reproducibles

Si desea generar una secuencia de números aleatorios y luego poder reproducir esa misma secuencia de números aleatorios más adelante, puede configurar el generador de semillas de números aleatorios con `set.seed()`.

```r
set.seed (197)
rnorm(n = 10, mean = 0, sd = 1)
## [1] 0.6091700 -1.4391423 2.0703326 0.7089004 0.6455311 0.7290563
## [7] -0.4658103 0.5971364 -0.5135480 -0.1866703

set.seed (197)
rnorm(n = 10, mean = 0, sd = 1)
## [1] 0.6091700 -1.4391423 2.0703326 0.7089004 0.6455311 0.7290563
## [7] -0.4658103 0.5971364 -0.5135480 -0.1866703 
```