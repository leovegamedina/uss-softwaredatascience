---
layout: default
title: Funciones Numéricas y Estadisticas
parent: Programación
grand_parent: Unidad 1 - Estructura de Datos en R
permalink: /docs/R/programming/programming-7/
nav_order: 7
---

# Funciones Numéricas y Estadisticas

En <img src="/uss-softwaredatascience/assets/images/r.svg" width="20">, de manera nativa contamos con las siguientes funciones numéricas:

| Función                                              | Descripción                       |
|:-----------------------------------------------------|:----------------------------------|
| abs(x)                                               | Valor Absoluto                    |
| sqrt(x)                                              | Raíz Cuadrada                     |
| ceiling(x)                                           | Redondeo hacia arriba             |
| floor(x)                                             | Redondeo hacia abajo              |
| round(x, digits=n)                                   | Redondeo                          |
| cos(x), sin(x), tan(x), acos(x), cosh(x), acosh(x)   | Funciones trigonométricas         |
| log(x)                                               | Logaritmo Natural                 |
| log(10, base = n)                                    | Logaritmo base n                  |
| log2(x)                                              | Logaritmo base 2                  |
| log10(x)                                             | Logaritmo base 10                 | 
| exp(x)                                               | Funcion Exponencial               |

Adicionalmente <img src="/uss-softwaredatascience/assets/images/r.svg" width="20"> posee una lista de funciones estadísticas. Estos tienen en común que pueden tener el argumento `na.rm`, que está establecido en ***FALSE*** de forma predeterminada. Esto nos permite lidiar con los valores faltantes (na = no disponible). Si se establece en falso, no se eliminan.

| Función                                              | Descripción                       |
|:-----------------------------------------------------|:----------------------------------|
| mean(x, na.rm = FALSE)                               | Media                             |
| sd(x)                                                | Desviación Estandar               |
| var(x)                                               | Varianza                          |
| median(x)                                            | Mediana                           |
| quantile(x, probs)                                   | Quantiles de x                    |
| sum(x)                                               | Suma                              |
| min(x)                                               | Mínimo                            |
| max(x)                                               | Máximo                            |
| range(x)                                             | Rango                             |
| scale(x, center = TRUE, scale = TRUE)                | Escalamiento                      | 
| sample(x, size, replace = FALSE, prob)               | Muestra                           |