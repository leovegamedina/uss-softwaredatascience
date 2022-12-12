---
layout: default
title: 📝 Taller 1
parent: Unidad 1 - Estructura de Datos en R
nav_order: 8
---

# Taller 1 📝

A continuacion se mostrara la solucion al Taller 1.

### Actividad 1

```r
binario = 10011010001
fin = nchar(binario)
decimal = 0
mult = 0

for(i in 0:fin){
  n = binario %% 10
  binario = floor(binario / 10)
  mult = n * (2 ^ i)
  decimal = decimal + mult
}

decimal
## [1] 1233
```

### Actividad 2

```r
is_armstrong <- function(v=1:1000){
  armstrong_vec = NULL
  for(i in v){
    sum = 0
    x = i
    while(x != 0){
      n = x %% 10
      x = floor(x / 10)
      power = n ^ 3
      sum = sum + power
    }
    if(sum == i){
      armstrong_vec = append(armstrong_vec, i)
    }
    else{
      next
    }
  }
  return(armstrong_vec)
}

is_armstrong()
## [1]   1 153 370 371 407
```

<iframe src="/uss-softwaredatascience/T01_SDS.pdf" width="100%" height="500px">