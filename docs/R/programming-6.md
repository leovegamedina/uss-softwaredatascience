---
layout: default
title: Operadores Lógicos
parent: Programación
grand_parent: Unidad 1 - Estructura de Datos en R
permalink: /docs/R/programming/programming-6/
nav_order: 6
---

# Operadores Lógicos

Los operadores lógicos en <img src="/uss-softwaredatascience/assets/images/r.svg" width="20"> se utilizan principalmente en condiciones `If` o `Loops`. Los operadores relacionales en <img src="/uss-softwaredatascience/assets/images/r.svg" width="20"> se usan comúnmente para verificar la ***relación entre dos variables***.

- Si la relación es verdadera, entonces devuelve el booleano `True`.
- Si la relación es falsa, devuelve el booleano `False`.

La siguiente tabla muestra todos los operadores relacionales en <img src="/uss-softwaredatascience/assets/images/r.svg" width="20"> con ejemplos.

| Operador    | Operación              | Ejemplo                    |
|:------------|:-----------------------|:---------------------------|
| >           | Mayor estricto         | 25 > 14 returns `True`     |
| <           | Menor estricto         | 25 < 14 returns `False`    |
| >=          | Mayor o igual          | 25 >= 14 returns `True`    |
| <=          | Menor o igual          | 25 <= 14 return `False`    |
| ==          | Igual                  | 25 == 14 returns `False`   |
| !=          | Distinto de            | 25 != 14 returns `True`    |
| !x          | No x (negación)        |     |
| x &#124; y       | x OR y                 |     |
| x & y       | x AND y                |     |
| xor(x, y)   | OR exclusivo           |     |
| isTRUE(x)   | Prueba TRUE de x       |     |

Lo siguiente proporciona una descripción general visual de los operadores lógicos que utilizan diagramas de Venn. `x` se refiere al círculo izquierdo, `y` al círculo derecho.

![](/uss-softwaredatascience/assets/images/transform-logical.png)

{: .note-title }
> Funciones de comparacion
>
> Tambien para los casos en donde queremos comparar igualdad, tenemos dos funciones `identical()` y `all.equal()`. El primero mide la ***igualdad exacta*** entre dos variables, mientras que la segunda mide la ***igualdad cercana***, es decir, acepta un grado de tolerancia entre las variables.