---
layout: default
title: Funciones
parent: Unidad 1 - Estructura de Datos en R
nav_order: 7
---

# Funciones

<img src="/uss-softwaredatascience/assets/images/r.svg" width="20"> es un lenguaje de programación funcional, lo que significa que todo lo que haces se basa básicamente en funciones. Sin embargo, pasar del simple uso de funciones preconstruidas a escribir funciones propias es cuando nuestras capacidades realmente comienzan a despegar y nuestro desarrollo/escritura de código adquiere un nuevo nivel de eficiencia. Las funciones nos permiten reducir la duplicación de código al automatizar una tarea generalizada para que se aplique de forma recursiva. Cada vez que nos encuentramos repitiendo una función o copiando y pegando código, hay un buen indicio de que se debe escribir una función para eliminar las redundancias.

Una función es un bloque de código que solo se ejecuta cuando se le invoca. Puede pasar datos, conocidos como `parámetros` o `argumentos`, a una función. Una función puede devolver datos como resultado.

Con la excepción de las funciones primitivas, todas las funciones de <img src="/uss-softwaredatascience/assets/images/r.svg" width="20"> tienen tres partes:
1. `body()`: el código dentro de la función.
1. `formals()`: la lista de argumentos utilizados para llamar a la función.
1. `environment()`: el mapeo de la(s) ubicación(es) de las variables de la función.

Para crear una función, usamos `function()`:

```r
my_function <- function() {
    print("Hello World!")
}
```

Ahora, para invocar una función, usamos el nombre de la función seguido por perentesis, como **my_function()**.

```r
my_function <- function() {
    print("Hello World!")
}

my_function()
## [1] "Hello World!"
```

## Argumentos

Si desea entregar informacion a una función como un `input`, podemos ingresarlos como `argumentos`.

Los `argumentos` se especifican después del nombre de la función, entre paréntesis. Puede agregar tantos argumentos como desee, simplemente sepárelos con una coma.

```r
my_function <- function(fname) {
    paste(fname, "Perez")
}

my_function("Felipe")
my_function("Antonio")
my_function("Sebastian")
## [1] "Felipe Perez"
## [1] "Antonio Perez"
## [1] "Sebastian Perez"
```

{: .important-title }
> ¿**Parámetros** o **Argumentos**?
>
> Los términos `parámetro` y `argumento` se pueden usar para lo mismo: información que se pasa a una función.
>
>Desde la perspectiva de una función:
>
>- Un ***parámetro*** es la **variable** que aparece entre paréntesis en la definición de la función.
>
>- Un ***argumento*** es el **valor** que se envía a la función cuando se llama.

Por defecto, una función debe llamarse con el número correcto de argumentos. Lo que significa que si su función espera 2 argumentos, debe llamar a la función con 2 argumentos, ni más ni menos:

```r
my_function <- function(fname, lname) {
  paste(fname, lname)
}

my_function("Felipe", "Perez")
## [1] "Felipe Perez"
```

{: .warning }
> Esta función espera 2 argumentos y obtiene 1 argumento:
> 
> ```r
> my_function <- function(fname, lname) {
>   paste(fname, lname)
> }
> 
> my_function("Felipe")
> ## Error in paste(fname, lname) : 
> ##   argument "lname" is missing, with no default
> ## Calls: my_function -> paste
> ## Execution halted
> ```

## Valor de Parámetro predeterminado

Cuando definimos una función, podemos indicar un `valor predeterminado` para los parametrós de esta:

```r
my_function <- function(country = "Santiago") {
    paste("I am from", country)
}

my_function("Valdivia")
my_function("Concepcion")
my_function() # will get the default value, which is Santiago
my_function("Puerto Montt")
## [1] "I am from Valdivia"
## [1] "I am from Concepcion"
## [1] "I am from Santiago"
## [1] "I am from Puerto Montt"
```

## Funcion Return

Para permitir que una función devuelva un resultado, use la función `return()`:

```r
my_function <- function(x) {
  return (5 * x)
}

print(my_function(3))
print(my_function(5))
print(my_function(9))
## [1] 15
## [1] 25
## [1] 45
```

## Funciones Anidadas

Hay dos formas de crear una función anidada:

- Llamar a una función dentro de otra función.
- Escribir una función dentro de otra función.

{: .note-title }
> Llamar a una función dentro de otra función:
> 
> ```r
> nested_function <- function(x, y) {
>   a <- x + y
>   return(a)
> }
> 
> nested_function(nested_function(2,2), nested_function(3,3))
> ## [1] 10
> ```
> 
> ***Ejemplo explicado:***
> 
> La función le dice a `x` que sume `y`.
> 
> La primera entrada **nested_function(2,2)** es `x` de la función principal.
> 
> La segunda entrada **nested_function(3,3)** es `y` de la función principal.
> 
> Por lo tanto, la salida es (2+2) + (3+3) = 10.

{: .note-title }
> Escribir una función dentro de otra función:
> 
> ```r
> outer_func <- function(x) {
>   inner_func <- function(y) {
>     a <- x + y
>     return(a)
>   }
>   return (inner_func)
> }
> output <- outer_func(3) # To call the outer_func
> output(5)
> ## [1] 8
> ```
> 
> ***Ejemplo explicado:***
> 
> No puede llamar directamente a la función porque `inner_func` se ha definido (anidado) dentro de `outer_func`.
> 
> Necesitamos llamar a `outer_func` primero para llamar a `inner_func` como segundo paso.
> 
> Cuando guardamos en `output` la funcion `outer_func`, esta lo que hace es dejar en storage el valor `x` (definido como 3) y retorna la funcion `inner_func`, por lo que ahora, a output le podemos ingresar el valor `y` de la funcion `inner_func`.
>
> Al ingresar el valor `y` en `output`, lo que hace es invocar ahora a la funcion `inner_func`, y ejecuta el body de esta, el cual ya teniendo definido los valores de `x` y de `y`, retorna la suma de estos en el valor `a`. Esto hace que devuelva 3 + 5 = 8.

## Recursividad

<img src="/uss-softwaredatascience/assets/images/r.svg" width="20"> también acepta la función recursiva, lo que significa que una **función definida puede llamarse a sí misma**.

La recursividad es un concepto común matemático y de programación. Esto tiene la ventaja de que puede recorrer los datos para llegar a un resultado.

Se debe tener mucho cuidado con la recursividad, ya que puede ser bastante fácil escribir una función que nunca termina, o una que usa cantidades excesivas de memoria o potencia del procesador. Sin embargo, cuando se escribe correctamente, la recursividad puede ser un enfoque de programación muy eficiente y matemáticamente elegante.

```r
tri_recursion <- function(k) {
  if (k > 0) {
    result <- k + tri_recursion(k - 1)
    print(result)
  } else {
    result = 0
    return(result)
  }
}
tri_recursion(6)
## [1] 1
## [1] 3
## [1] 6
## [1] 10
## [1] 15
## [1] 21
```

<img src="/uss-softwaredatascience/assets/images/recursividad.png" width="550">

## Guardado Funciones

Para guardar funciones en R, se puede guardar un script (.R) con la funcion, y luego invocarla con la funcion `source()`. Es importante que el archivo de la función este en el mismo ambiente que el proyecto, sino se tendra que definir la ruta completa en la funcion `source()`.

## Ejercicios

1. Cree una función que calcuale la varianza de un vector, usando la siguiente formula:
$$ Var(x) = \frac{1}{n-1}\sum_{i=0}^{n}{(x_i - \bar{x})^2}$$ 
el vector es: `c(10,8,5,3,12)`

```r
varianza <- function(x, na.rm = TRUE) {
  n <- length(x)
  m <- mean(x, na.rm = TRUE)
  sq_err <- (x - m)^2
  sum(sq_err) / (n - 1)
}
varianza(c(10,8,5,3,12))
## [1] 13.3
var(c(10,8,5,3,12))
## [1] 13.3
```

2. Usando la funcion anterior, calcule la simetría (skew) del mismo vector.
$$ Skew(x) = \frac{\frac{1}{n-2}(\sum_{i=1}^{n}{(x_i - \bar{x})^3})}{Var(x)^{3/2}}$$

```r
skewness <- function(x, na.rm = FALSE) {
  n <- length(x)
  m <- mean(x, na.rm = na.rm)
  v <- var(x, na.rm = na.rm)
  (sum((x - m) ^ 3) / (n - 2)) / v ^ (3 / 2)
}
skewness(c(10,8,5,3,12))
## [1] -0.108857
```

3. Escriba una función que calcule la suma de enteros no negativos con `recursividad`.

```r
sum_digito <- function(x){
  if(x==0){
    return(0)
  }
  else{
    return(x%%10 + sum_digito(as.integer(x/10)))
  }
}
sum_digito(123)
## [1] 6
```

4. Cree una funcion anidada que calcule el factorial de un numero, esta funcion debe cumplir las siguientes condiciones:
  - La funcion factorial se debe calcular con `recursividad`.
  - Si el valor no es entero, debe entregar el mensaje: `"Error! El valor no es un numero"`.
  - Si el valor es negativo, debe entregar el mensaje: `"Error! El numero debe ser no negativo"`.

```r
get_fact <- function(num){
  factorial <- function(num){
    if(num == 0 | num == 1){
      return(1)
    }
    else{
      return(num * factorial(num -1))
    }
  }
  if(is.numeric(num)==FALSE){
    print("Error! El valor no es un numero")
  }
  if(num < 0){
    print("Error! El numero debe ser no negativo")
  }
  return(factorial(num))
}

get_fact(3)
## [1] 6
get_fact('3')
## [1] "Error! El valor no es un numero"
get_fact(-3)
## [1] "Error! El numero debe ser no negativo"
```