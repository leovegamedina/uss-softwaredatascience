---
layout: default
title: Packages
parent: Unidad 1 - Estructura de Datos en R
nav_order: 3
---

# Packages en <img src="/uss-softwaredatascience/assets/images/r.svg" width="40">

En R, la unidad fundamental de codigo compartible es el `package`. Al dia de hoy existen mas de 8.000 paquetes disponibles en **CRAN**, mas una infinidad de paquetes en **Github**.

## Instalación de Paquetes

El primer recurso para instalar paqueterias será CRAN. Para instalar desde aca:

```r
# install packages from CRAN
install.packages ("packagename")
```

Para descargar paquetes por Github:

{: .warning-title }
> uso de devtools
>
> Para poder instalar paquetes desde Github, debemos utilizar la paquetería `devtools`.

```r
# the devtools package provides a simply function to download GitHub packages
install.packages("devtools")
# install package which exists at github.com/username/packagename
devtools::install_github("username/packagename")
```

## Carga de Paquetes

Puedes acceder a las funciones y recursos provistos por el paquete de dos maneras distintas:

```r
# load the package to use in the current R session
library (packagename)
# use a particular function within a package without loading the package
packagename::functionname 
```

## Obtener ayuda en los Paquetes

Para obtener ayuda en los paquetes instalados:

```r
# provides details regarding contents of a package
help(package="packagename")
# see all packages installed
library()
# see packages currently loaded
search()
# list vignettes available for a specific package
vignette(package="packagename")
# view specific vignette
vignette("vignettename")
# view all vignettes on your computer
vignette() 
```