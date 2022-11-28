---
layout: default
title: Dataframes con Tidyverse
parent: Unidad 1 - Estructura de Datos en R
has_children: true
nav_order: 11
---

# <img src="/uss-softwaredatascience/assets/images/tidyverse.png" width="40"> Dataframes con Tidyverse 

El proceso de análisis de datos siempre conlleva procedimientos de limpieza de los valores que implican realizar eliminación o generación de nuevos datos. Este proceso es relevante ya que sin datos eficientes y veraces todos los procesos posteriores serán erróneos o poco eficaces.

Además, R trabaja en forma preferente con datos tabulados (en forma de tablas) y su formato preferido es el dataframe. Los datos tabulados establecen:

- Cada variable esta almacenada en su propia columna.
- Cada observación esta almacenada en su propia fila.
- Cada tabla corresponde a un tipo de observación.

El análisis de los datos tiene como objetivo extraer información de ello. Por ello se requiere entre otras operaciones: Extraer las variables existentes en el conjunto de datos, Extraer las observaciones preexistentes, Derivar nuevas variables sobre las ya existentes y Cambiar las unidades de las variables.

El paquete Tidyverse provee una serie de herramientas destinadas a facilitar estos procesos.

Tidyverse es una colección de paquetes R diseñados para la ciencia de datos. Todos los paquetes comparten una filosofía de diseño, gramática y estructuras de datos subyacentes. Está compuesto de los siguientes paquetes:

- ***readr***
- ***readxl***
- ***dplyr***
- ***tidyr***
- ggplot2
- tibble
- purr
- stringr
- forcats
- entre otros...