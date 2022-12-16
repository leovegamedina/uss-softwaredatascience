---
layout: default
title: Control Statements
parent: Unidad 2 - Estructuras de Datos en Python
nav_order: 3
---

# if Statements

La instrucción `if` se utiliza para la ejecución condicional:

```python
if condition:
    # body of if statement
```

```python
if_stmt ::=  "if" assignment_expression ":" suite
             ("elif" assignment_expression ":" suite)*
             ["else" ":" suite]
```

Selecciona exactamente una de las suites evaluando las expresiones una por una hasta que se encuentra que una es verdadera; luego se ejecuta esa suite (y no se ejecuta ni evalúa ninguna otra parte de la instrucción if). Si todas las expresiones son falsas, se ejecuta el conjunto de la cláusula else, si está presente.

```python
x = int(input("Please enter an integer: "))
## Please enter an integer: 42
if x < 0:
    x = 0
    print('Negative changed to zero')
elif x == 0:
    print('Zero')
elif x == 1:
    print('Single')
else:
    print('More')

## More
```

Puede haber cero o más partes `elif`, y la parte else es opcional. La palabra clave `elif` es la abreviatura de `else if` y es útil para evitar una sangría excesiva. Una secuencia `if... elif... elif...` es un sustituto de las sentencias switch o case que se encuentran en otros idiomas.

Si está comparando el mismo valor con varias constantes, o verificando tipos o atributos específicos, también puede encontrar útil la declaración `match`.

# match Statements

Una declaración `match` toma una expresión y compara su valor con patrones sucesivos dados como uno o más bloques de casos. Solo se ejecuta el primer patrón que coincide y también puede extraer componentes (elementos de secuencia o atributos de objeto) del valor en variables.

La forma más simple compara un valor de sujeto con uno o más literales:

```python
def http_error(status):
    match status:
        case 400:
            return "Bad request"
        case 404:
            return "Not found"
        case 418:
            return "I'm a teapot"
        case _:
            return "Something's wrong with the internet"
```

Puede combinar varios literales en un solo patrón usando `|` ("o"):

```python
case 401 | 403 | 404:
    return "Not allowed"
```

# for Statements

La declaración `for` se usa para iterar sobre los elementos de una secuencia (como una cadena, una tupla o una lista) u otro objeto iterable:

```python
for val in sequence:
    # statement(s)
```

```python
for_stmt ::=  "for" target_list "in" starred_list ":" suite
              ["else" ":" suite]
```

La expresión starred_list se evalúa una vez; debería producir un objeto iterable. Se crea un iterador para ese iterable. Luego, el primer elemento proporcionado por el iterador se asigna a la lista de destino utilizando las reglas estándar para las asignaciones y se ejecuta el conjunto. Esto se repite para cada elemento proporcionado por el iterador. Cuando se agota el iterador, se ejecuta la suite en la cláusula else, si está presente, y el ciclo termina.

```python
numbers = [1, 5, 43, 2, 7, 9, 19, 10]
target = 100

for number in numbers:
    if number == target:
        print("Target found, escaping the loop")
        break
else:
    print("Target not found. The loop ran through all the numbers.")
```

Una declaración `break` ejecutada en la primera suite termina el ciclo sin ejecutar la suite de la cláusula else. Una declaración `next` ejecutada en la primera suite salta el resto de la suite y continúa con el siguiente elemento, o con la cláusula else si no hay ningún elemento siguiente.

```python
# Measure some strings:
words = ['cat', 'window', 'defenestrate']
for w in words:
    print(w, len(w))

## cat 3
## window 6
## defenestrate 12
```

# while Statements

El bucle `while` se ejecuta mientras la condición se mantenga verdadera. En Python, como en C, cualquier valor entero distinto de cero es verdadero; cero es falso. La condición también puede ser una cadena o un valor de lista, de hecho, cualquier secuencia; cualquier cosa con una longitud distinta de cero es verdadera, las secuencias vacías son falsas. Los operadores de comparación estándar se escriben igual que en C: < (menor que), > (mayor que), == (igual a), <= (menor que o igual a), >= (mayor que o igual a) y != (distinto de).

```python
while condition:
    # body of while loop
```

```python
while_stmt ::=  "while" assignment_expression ":" suite
                ["else" ":" suite]
```

Esto prueba repetidamente la expresión y, si es verdadera, ejecuta la primera suite; si la expresión es falsa (que puede ser la primera vez que se prueba), se ejecuta el conjunto de la cláusula else, si está presente, y el ciclo termina.

```python
basket = [
    {'fruit': 'apple', 'qty': 20},
    {'fruit': 'banana', 'qty': 30},
    {'fruit': 'orange', 'qty': 10}
]

fruit = input('Enter a fruit:')

index = 0

while index < len(basket):
    item = basket[index]
    # check the fruit name
    if item['fruit'] == fruit:
        print(f"The basket has {item['qty']} {item['fruit']}(s)")
        found_it = True
        break

    index += 1
else:
    qty = int(input(f'Enter the qty for {fruit}:'))
    basket.append({'fruit': fruit, 'qty': qty})
    print(basket)
```

Una declaración `break` ejecutada en la primera suite termina el ciclo sin ejecutar la suite de la cláusula else. Una declaración `continue` ejecutada en la primera suite salta el resto de la suite y vuelve a probar la expresión.

# break y continue Statements

La sentencia `break`, como en C, sale del bucle for o while más interno.

Las declaraciones de bucle pueden tener una cláusula else; se ejecuta cuando el ciclo termina por agotamiento del iterable (con for) o cuando la condición se vuelve falsa (con while), pero no cuando el ciclo termina con una instrucción break. Esto se ejemplifica con el siguiente bucle, que busca números primos:

```python
for n in range(2, 10):
    for x in range(2, n):
        if n % x == 0:
            print(n, 'equals', x, '*', n//x)
            break
    else:
        # loop fell through without finding a factor
        print(n, 'is a prime number')

## 2 is a prime number
## 3 is a prime number
## 4 equals 2 * 2
## 5 is a prime number
## 6 equals 2 * 3
## 7 is a prime number
## 8 equals 2 * 4
## 9 equals 3 * 3
```

La sentencia continue, también prestada de C, continúa con la siguiente iteración del bucle:

```python
for num in range(2, 10):
    if num % 2 == 0:
        print("Found an even number", num)
        continue
    print("Found an odd number", num)

## Found an even number 2
## Found an odd number 3
## Found an even number 4
## Found an odd number 5
## Found an even number 6
## Found an odd number 7
## Found an even number 8
## Found an odd number 9
```

# pass Statements

La instrucción `pass` no hace nada. Se puede usar cuando se requiere una declaración sintácticamente pero el programa no requiere ninguna acción. Por ejemplo:

```python
while True:
    pass  # Busy-wait for keyboard interrupt (Ctrl+C)
```

`pass` se puede usar como marcador de posición para una función o cuerpo condicional cuando está trabajando en un nuevo código, lo que le permite seguir pensando en un nivel más abstracto. La funcion `pass` se ignora en silencio:

```python
def initlog(*args):
    pass   # Remember to implement this!
```

## Ejercicios:

1. Escriba un programa para imprimir el siguiente patrón numérico usando un bucle.
```python
1 
1 2 
1 2 3 
1 2 3 4 
1 2 3 4 5
```

1. Escriba un programa para aceptar un número de un usuario y calcule la suma de todos los números desde 1 hasta un número dado. Por ejemplo, si el usuario ingresó 10, la salida debería ser 55 (1+2+3+4+5+6+7+8+9+10)
```python
Ingrese numero 10
La suma es:  55
```

1. Escriba un programa para mostrar solo aquellos números de una lista que satisfagan las siguientes condiciones:
El número debe ser divisible por cinco. Si el número es mayor que 150, sáltelo y pase al siguiente número. Si el número es mayor que 500, detenga el ciclo.
```python
numbers = [12, 75, 150, 180, 145, 525, 50]
```

1. Escriba un programa para usar el ciclo for para imprimir el siguiente patrón numérico inverso.
```python
5 4 3 2 1 
4 3 2 1 
3 2 1 
2 1 
1
```

1. La secuencia de Fibonacci es una serie de números. El siguiente número se encuentra sumando los dos números anteriores. Los dos primeros números son 0 y 1. Por ejemplo, 0, 1, 1, 2, 3, 5, 8, 13, 21. El siguiente número en esta serie anterior es 13+21 = 34.
```python
Fibonacci sequence:
0  1  1  2  3  5  8  13  21  34
```

1. Escriba un programa para encontrar el factorial de un número dado.
```python
5! = 5 × 4 × 3 × 2 × 1 = 120
```

1. Invertir un número entero dado.
```python
Dado: 76542
Salida esperada: 24567
```

1. Escriba un programa para calcular la suma de series hasta n término para un x numero. Por ejemplo, si n=5 y x=2, la serie se convertirá en:
```python
2 + 22 + 222 + 2222 + 22222 = 24690
```

