---
layout: default
title: Instalación
parent: Unidad 1 - Estructura de Datos en R
nav_order: 2
---

# Instalación de <img src="/uss-softwaredatascience/assets/images/r.svg" width="40">

Primero, debemos descargar e instalar <img src="/uss-softwaredatascience/assets/images/r.svg" width="20"> desde el repositorio de `CRAN` (Comprehensive R Archive Network). 

{: .note-title }
> Recomendación
>
> Es altamente recomendable instalar la distribucion binaria precompilada para tu OS.

Para descargar, sigue las siguientes instrucciones:

1. Ve a [https://cran.r-project.org/](https://cran.r-project.org/).

Para OS Windows ❖:
{:style="counter-reset:step-counter 2"}
1. Cliquea en la opción `Download R for Windows`.
1. Cliquea en la opción `base`.
1. Elije la opción `Download R-X.X.X for Windows`
1. Sigue las instrucciones del instalador.

Para macOSX <img src="/uss-softwaredatascience/assets/images/apple.svg" width="15">:
{:style="counter-reset:step-counter 2"}
1. Cliquea en la opción `Download R for macOS`.
1. Cliquea en la opción para tu `OSX` que termina en la extensión `.pkg`.
1. Sigue las instrucciones del instalador.

# Instalación de <img src="/uss-softwaredatascience/assets/images/rstudio.svg" width="90"> (IDE)

Ahora, podemos descargar <img src="/uss-softwaredatascience/assets/images/rstudio.svg" width="40"> IDE (Integrated Development Environment), una poderosa interfase de usuario de <img src="/uss-softwaredatascience/assets/images/r.svg" width="20">.

{: .warning-title }
> Instalación previa de <img src="/uss-softwaredatascience/assets/images/r.svg" width="20">
>
> Se debe procurar que la instalación de <img src="/uss-softwaredatascience/assets/images/r.svg" width="20"> este bien ejecutada para poder utilizar <img src="/uss-softwaredatascience/assets/images/rstudio.svg" width="40">, ya que este último utiliza <img src="/uss-softwaredatascience/assets/images/r.svg" width="20"> como compilador.

1. Ve a [https://www.rstudio.com/products/rstudio/download/](https://www.rstudio.com/products/rstudio/download/).
1. Elige la opción `Free`.
1. Cliquea en la opción `DOWNLOAD RSTUDIO FOR ...`, deberia reconocer automaticamente el OS. En caso de no hacerlo, puedes elegir el instalador en la sección `All Installers`.
1. Sigue las instrucciones del instalador.

# Entendiendo la Consola de <img src="/uss-softwaredatascience/assets/images/rstudio.svg" width="90">

En la consola de <img src="/uss-softwaredatascience/assets/images/rstudio.svg" width="40"> es donde todo pasa. Existen 4 ventanas fundamentales, cada una con su proposito.

![](/uss-softwaredatascience/assets/images/rstudio.png)

## 1. Code Editor

Aqui es donde tus scripts son mostrados. Existen multiples archivos de scripts, pero el más básico es el archivo `.R`. Para crear un nuevo archivo usa el menú **File → New File**. Para abrir un archivo existente, puedes usar el menú **File → Open File…**, o bien, **Recent Files** para seleccionar los archivos recientemente abiertos.

El editor de codigos incluye una variedad de caracteristicas que mejoran la productividad tales como  `syntax highlighting`, `code completion`, `edicion multiple` y `find/replace`.

## 2. R Console

Acá puedes codificar directamente en la ventana pero no quedará guardado el codigo. Es recomendable utilizar esta ventana cuando quieres simplemente ejecutar algún calculo. También acá es donde verás tus `outputs` cuando ejecutes algún script.

## 3. Workspace Environment

Workspace Environment captura cualquier objetivo definido por el usuario (`vecotres`, `matrices`, `dataframes`, `listas`, `funciones`, etc.). Cuando guardas tus sesiones de <img src="/uss-softwaredatascience/assets/images/r.svg" width="20">, estas son las componentes en conjunto con los scripts que seran guardadas en tu directorio de trabajo (`working directory`), el cual es la ruta por defecto para todos los archivos de entrada y salida (I/O). Para obtener o setar tu working directory puedes usar los comandos `getwd()` y `setwd()` en la consola.

{: .note-title }
> Nota
>
> Puedes tipear cualquier comentario en tu script de <img src="/uss-softwaredatascience/assets/images/r.svg" width="20"> usando el simbolo `#`.

```r
# returns path for the current working directory
getwd()
# set the working directory to a specified directory
setwd(directory_name)
```

El workspace environment tambien lista los objetos definidos por el usuario tales como vectores, matrices, dataframes, etc. Para identificar o remover estos objetos en tu actual ambiente de <img src="/uss-softwaredatascience/assets/images/r.svg" width="20"> puedes usar:

```r
# list all objects
ls()
# identify if an R object with a given name is present
exists("object_name")
# remove defined object from the environment
rm("object_name")
# you can remove multiple objects by using the c() function
rm(c("object1", "object2"))
# basically removes everything in the working environment -- use with caution!
rm(list = ls())
```

Tambien puedes ver tus comandos previos en tu workspace environment cliqueando el tab `History`, o bien en la consola:

```r
# list all objects
# default shows 25 most recent commands
history()
# show 100 most recent commands
history(100)
# show entire saved history
history(Inf) 
```

Adicional a esto, puedes guardar y cargar tus `workspaces`. Estos quedaran con la extensión `.Rdata`.

```r
# save all items in workspace to a .RData file
save.image()
# save specified objects to a .RData file
save(object1, object2, file = "myfile.RData")
# load workspace into current session
load("myfile.RData")
```

{: .important-title }
> Importante: Guardar en otro working directory
>
> Nota que guardando el `workspace` sin especificar el 	`working directory` hara que por defecto guarde en el directorio actual. Puedes especificar donde quieres guardar el `.RData` al incluir el path: 
```r
save(object1, object2, file = "/users/name/folder/myfile.RData")
```

## 4. Miscelaneos

Esta ventana contiene multiples tabs. El tab `Files` te permite ver cuales archivos estan disponibles en tu working directory. El tab `Plots` mostrará cualquier visualizacion que es producida por tu codigo. El tab `Packages` listará todos los paquetes descargados en tu computadora y tambien los que estan cargados en tu sesión. Finalmente el tab `Help` te permite buscar topicos en los que necesites ayuda y tambien despliega cualquier respuesta de ayuda.

# Ayuda General

Para levantar los recursos de ayuda general puedes usar:

```r
# provides general help links
help.start()
# searches the help system for documentation matching a given character string
help.search ("text") 
```

Para ayuda en funciones que esten instaladas en tu computador:

```r
# provides details for specific function
help(functionname)
# provides same information as help(functionname)
?functionname
# provides examples for said function
example(functionname) 
```

{: .important-title }
> Importante
>
> `help()` y `?` solo funcionan con funciones de paquetes cargados en la sesion. Si quieres ver detalles de funciones en un paquete que esta instalado en tu computador pero no se encuentra cargado en tu sesión puedes usar:
```r
help(functionname, package = "packagename")
# another option
help(packagename::functionname)
```

Por otro lado, puedes obtener ayuda de los siguientes recursos:

- **RSiteSearch("key phrase")**: busca por la frase clave en el sitio web de R Project [http://search.r-project.org/](http://search.r-project.org/)
- **Stack Overflow**: sitio de Q&A orientado a programación [http://stackoverflow.com/questions/tagged/r](http://stackoverflow.com/questions/tagged/r)
- **Cross Validated**: sitio de Q&A orientado a analisis estadistico [http://stats.stackexchange.com/questions/tagged/r](http://stats.stackexchange.com/questions/tagged/r)