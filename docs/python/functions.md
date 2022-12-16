---
layout: default
title: Funciones
parent: Unidad 2 - Estructuras de Datos en Python
nav_order: 4
---

# Funciones

Una definición de función es una sentencia ejecutable. Su ejecución vincula el nombre de la función en el espacio de nombres local actual a un objeto de función (un envoltorio alrededor del código ejecutable de la función). Este objeto de la función contiene una referencia al actual espacio de nombres globales como el espacio de nombres global que se usará cuando se llame a la función.

La definición de la función no ejecuta el cuerpo de la función; esto se ejecuta solo cuando se llama a la función

```python
def <function_name>([<parameters>]):
    <statement(s)>
```

Los componentes de la definición se explican en la siguiente tabla:

| Componente      | Significado                                                                                                |
|-----------------|------------------------------------------------------------------------------------------------------------|
| `def`             | La palabra clave que informa a Python que se está definiendo una función                                   |
| `<function_name>` | Un identificador de Python válido que nombra la función                                                    |
| `<parameters>`    | Una lista opcional de parámetros separados por comas que se pueden pasar a la función                      |
| `:`               | Puntuación que indica el final del encabezado de la función de Python (el nombre y la lista de parámetros) |
| `<statement(s)>`  | Un bloque de sentencias de Python válidas                                                                  |

La sintaxis para llamar a una función de Python es la siguiente:

```python
<function_name>([<arguments>])
```

`<arguments>` son los valores pasados ​​a la función. Corresponden a los `<parameters>` en la definición de la función de Python. Puede definir una función que no tome ningún argumento, pero los paréntesis aún son necesarios. Tanto una definición de la función como una llamada de la función siempre deben incluir paréntesis, incluso si están vacíos.

```python
def fib(n):    # write Fibonacci series up to n
    """Print a Fibonacci series up to n."""
    a, b = 0, 1
    while a < n:
        print(a, end=' ')
        a, b = b, a+b
    print()

# Now call the function we just defined:
fib(2000)
## 0 1 1 2 3 5 8 13 21 34 55 89 144 233 377 610 987 1597
```

## Argument Passing

### Positional Arguments

La forma más sencilla de pasar argumentos a una función de Python es con argumentos posicionales (también llamados argumentos requeridos). En la definición de la función, especifica una lista de parámetros separados por comas dentro de los paréntesis:

```python
def f(qty, item, price):
    print(f'{qty} {item} cost ${price:.2f}')
```

Cuando se llama a la función, especifica una lista correspondiente de argumentos:

```python
f(6, 'bananas', 1.74)
## 6 bananas cost $1.74
```

Los parámetros (qty, item y price) se comportan como variables que se definen localmente en la función. Cuando se llama a la función, los argumentos que se pasan (6, 'bananas' y 1.74) se vinculan a los parámetros en orden, como si se tratara de una asignación de variables:

| Parámetro |   | Argumento |
|-----------|---|-----------|
| qty       | ← | 6         |
| item      | ← | bananas   |
| price     | ← | 1.74      |


Aunque los argumentos posicionales son la forma más sencilla de pasar datos a una función, también ofrecen la menor flexibilidad. Para empezar, el orden de los argumentos en la llamada debe coincidir con el orden de los parámetros en la definición. No hay nada que le impida especificar argumentos posicionales fuera de orden, por supuesto:

```python
f('bananas', 1.74, 6)
## bananas 1.74 cost $6.00
```

Con argumentos posicionales, los argumentos en la llamada y los parámetros en la definición deben coincidir no solo en orden sino también en número. Esa es la razón por la cual los argumentos posicionales también se conocen como argumentos requeridos. No puede omitir ninguno al llamar a la función o incluir parametros extras:

```python
# Too few arguments
f(6, 'bananas')
## Traceback (most recent call last):
##   File "<pyshell#6>", line 1, in <module>
##     f(6, 'bananas')
## TypeError: f() missing 1 required positional argument: 'price'

# Too many arguments
f(6, 'bananas', 1.74, 'kumquats')
## Traceback (most recent call last):
##   File "<pyshell#5>", line 1, in <module>
##     f(6, 'bananas', 1.74, 'kumquats')
## TypeError: f() takes 3 positional arguments but 4 were given
```

### Keyword Arguments

Cuando llama a una función, puede especificar argumentos en la forma `<keyword>`=`<value>`. En ese caso, cada `<keyword>` debe coincidir con un parámetro en la definición de la función de Python. Por ejemplo, la función f() previamente definida se puede llamar con argumentos de palabras clave de la siguiente manera:

```python
f(qty=6, item='bananas', price=1.74)
## 6 bananas cost $1.74
```

Hacer referencia a una palabra clave que no coincide con ninguno de los parámetros declarados genera una excepción:

```python
f(qty=6, item='bananas', cost=1.74)
## Traceback (most recent call last):
##   File "<stdin>", line 1, in <module>
## TypeError: f() got an unexpected keyword argument 'cost'
```

El uso de argumentos de palabras clave elimina la restricción en el orden de los argumentos. Cada argumento de palabra clave designa explícitamente un parámetro específico por nombre, por lo que puede especificarlos en cualquier orden y Python aún sabrá qué argumento va con qué parámetro:

```python
f(item='bananas', price=1.74, qty=6)
## 6 bananas cost $1.74
```

Cuando los argumentos posicionales y de palabra clave están presentes, todos los argumentos posicionales deben ir primero:

```python
f(6, item='bananas', 1.74)
## SyntaxError: positional argument follows keyword argument
```

Una vez que haya especificado un argumento de palabra clave, no puede haber argumentos posicionales a su derecha.

### Default Parameters

Si un parámetro especificado en una definición de función de Python tiene la forma `<name>`=`<value>`, `<valor>` se convierte en un valor predeterminado para ese parámetro. Los parámetros definidos de esta manera se denominan parámetros predeterminados u opcionales. A continuación se muestra un ejemplo de una definición de función con parámetros predeterminados:

```python
def f(qty=6, item='bananas', price=1.74):
    print(f'{qty} {item} cost ${price:.2f}')
```

Cuando se llama a esta versión de f(), cualquier argumento que se omite asume su valor predeterminado:

```python
f(4, 'apples', 2.24)
## 4 apples cost $2.24
f(4, 'apples')
## 4 apples cost $1.74

f(4)
## 4 bananas cost $1.74
f()
## 6 bananas cost $1.74

f(item='kumquats', qty=9)
## 9 kumquats cost $1.74
f(price=2.29)
## 6 bananas cost $2.29
```

### The `return` Statement

Una declaración `return` en una función de Python tiene dos propósitos:

1. Inmediatamente finaliza la función y devuelve el control de ejecución a la persona que llama.
1. Proporciona un mecanismo por el cual la función puede devolver datos a la persona que llama.

```python
def f():
    print('foo')
    print('bar')
    return

f()
## foo
## bar
```

```python
def f():
    return 'foo'

s = f()
s
## 'foo'
```

Cuando no se proporciona ningún valor de retorno, una función de Python devuelve el valor especial de Python `None`. Lo mismo sucede si el cuerpo de la función no contiene ninguna declaración de retorno y la función se cae al final:

```python
def f():
    return

print(f())
## None

def g():
    pass

print(g())
## None
```

`None` es falso cuando se evalúa en un contexto booleano.

Dado que las funciones que salen a través de una declaración de retorno simple o se caen al final devuelven `None`, una llamada a dicha función se puede usar en un contexto booleano:

```python
def f():
    return

def g():
    pass

if f() or g():
    print('yes')
else:
    print('no')
## no  
```

### Argument Tuple Packing

Cuando un nombre de parámetro en una definición de función de Python está precedido por un asterisco (`*`), indica el empaquetamiento de tuplas de argumentos. Todos los argumentos correspondientes en la llamada a la función se empaquetan en una tupla a la que la función puede hacer referencia mediante el nombre de parámetro dado. Aquí hay un ejemplo:

```python
def f(*args):
    print(args)
    print(type(args), len(args))
    for x in args:
        print(x)

f(1, 2, 3)
## (1, 2, 3)        
## <class 'tuple'> 3
## 1
## 2
## 3

f('foo', 'bar', 'baz', 'qux', 'quux')
## ('foo', 'bar', 'baz', 'qux', 'quux')
## <class 'tuple'> 5
## foo
## bar
## baz
## qux
## quux
```

En la definición de f(), la especificación del parámetro `*args` indica empaquetamiento de tuplas. En cada llamada a f(), los argumentos se empaquetan en una tupla a la que la función puede hacer referencia con el nombre `args`. Se puede usar cualquier nombre, pero `args` se elige tan comúnmente que es prácticamente un estándar.

Usando el empaquetado de tuplas, puede definir avg() de esta manera:

```python
def avg(*args):
    total = 0
    for i in args:
        total += i
    return total / len(args)

avg(1, 2, 3)
## 2.0
avg(1, 2, 3, 4, 5)
## 3.0
```
```python
def avg(*args):
    return sum(args) / len(args)

avg(1, 2, 3)
## 2.0
avg(1, 2, 3, 4, 5)
## 3.0
```

### Argument Tuple Unpacking

Una operación análoga está disponible en el otro lado de la ecuación, en una llamada de función de Python. Cuando un argumento en una llamada de función está precedido por un asterisco (*), indica que el argumento es una tupla que debe desempaquetarse y pasarse a la función como valores separados:

```python
def f(x, y, z):
    print(f'x = {x}')
    print(f'y = {y}')
    print(f'z = {z}')

f(1, 2, 3)
## x = 1
## y = 2
## z = 3

t = ('foo', 'bar', 'baz')
f(*t)
## x = foo
## y = bar
## z = baz
```

Aunque este tipo de desempaquetado se llama desempaquetado de tuplas, no solo funciona con tuplas. El operador de asterisco (*) se puede aplicar a cualquier iterable en una llamada de función de Python. Por ejemplo, también se puede descomprimir una lista o un conjunto (set):

```python
a = ['foo', 'bar', 'baz']
type(a)
## <class 'list'>
f(*a)
## x = foo
## y = bar
## z = baz

s = {1, 2, 3}
type(s)
## <class 'set'>
f(*s)
## x = 1
## y = 2
## z = 3
```

### Argument Tuple Unpacking

Python tiene un operador similar, el asterisco doble (`**`), que se puede usar con los parámetros y argumentos de las funciones de Python para especificar el empaquetado y desempaquetado del diccionario. Preceder a un parámetro en una definición de función de Python con un asterisco doble (`**`) indica que los argumentos correspondientes, que se espera que sean pares key = value, deben empaquetarse en un diccionario:

```python
def f(**kwargs):
    print(kwargs)
    print(type(kwargs))
    for key, val in kwargs.items():
        print(key, '->', val)

f(foo=1, bar=2, baz=3)
## {'foo': 1, 'bar': 2, 'baz': 3}
## <class 'dict'>
## foo -> 1
## bar -> 2
## baz -> 3
```

En este caso, los argumentos foo=1, bar=2 y baz=3 se empaquetan en un diccionario al que la función puede hacer referencia con el nombre `kwargs`.

### Argument Dictionary Unpacking

El desempaquetado del diccionario de argumentos es análogo al desempaquetado de tuplas de argumentos. Cuando el doble asterisco (**) precede a un argumento en una llamada de función de Python, especifica que el argumento es un diccionario que se debe desempaquetar, y los elementos resultantes se pasan a la función como argumentos de palabras clave:

```python
def f(a, b, c):
    print(F'a = {a}')
    print(F'b = {b}')
    print(F'c = {c}')

d = {'a': 'foo', 'b': 25, 'c': 'qux'}
f(**d)
## a = foo
## b = 25
## c = qux
```

Piense en `*args` como una lista de argumentos posicionales de longitud variable y en `**kwargs` como una lista de argumentos de palabras clave de longitud variable.

Los tres (parámetros posicionales estándar, *args y **kwargs) se pueden usar en una definición de función de Python. Si es así, entonces deben especificarse en ese orden:

```python
def f(a, b, *args, **kwargs):
    print(F'a = {a}')
    print(F'b = {b}')
    print(F'args = {args}')
    print(F'kwargs = {kwargs}')

f(1, 2, 'foo', 'bar', 'baz', 'qux', x=100, y=200, z=300)
## a = 1
## b = 2
## args = ('foo', 'bar', 'baz', 'qux')
## kwargs = {'x': 100, 'y': 200, 'z': 300}
```

### Keyword-Only Arguments

Se puede definir una función de Python en la versión 3.x para que tome argumentos de solo palabras clave, esta se define con un asterisco (*), con el nombre omitido:

```python
def oper(x, y, *, op='+'):
    if op == '+':
        return x + y
    elif op == '-':
        return x - y
    elif op == '/':
        return x / y
    else:
        return None

oper(3, 4, op='+')
## 7
oper(3, 4, op='/')
## 0.75

oper(3, 4, "I don't belong here")
## Traceback (most recent call last):
##   File "<stdin>", line 1, in <module>
## TypeError: oper() takes 2 positional arguments but 3 were given

oper(3, 4, '+')
## Traceback (most recent call last):
##   File "<stdin>", line 1, in <module>
## TypeError: oper() takes 2 positional arguments but 3 were given
```

El parámetro de argumento variable simple * indica que no hay más parámetros posicionales. Este comportamiento genera mensajes de error apropiados si se especifican mensajes adicionales. Permite que sigan parámetros de solo palabras clave.

### Positional-Only Arguments

A partir de Python 3.8, los parámetros de función también pueden declararse solo posicionales, lo que significa que los argumentos correspondientes deben proporcionarse posicionalmente y no pueden especificarse por palabra clave.

Para designar algunos parámetros como solo posicionales, especifique una barra inclinada (/) en la lista de parámetros de una definición de función. Cualquier parámetro a la izquierda de la barra inclinada (/) debe especificarse posicionalmente. Por ejemplo, en la siguiente definición de función, x e y son parámetros solo posicionales, pero z se puede especificar mediante una palabra clave:

```python
def f(x, y, /, z):
    print(f'x: {x}')
    print(f'y: {y}')
    print(f'z: {z}')

f(1, 2, 3)
## x: 1
## y: 2
## z: 3

f(1, 2, z=3)
## x: 1
## y: 2
## z: 3

f(x=1, y=2, z=3)
## Traceback (most recent call last):
##   File "<stdin>", line 1, in <module>
## TypeError: f() got some positional-only arguments passed as keyword arguments:
## 'x, y'
```

Los designadores positional-only y keyword-only pueden usarse en la misma definición de la función:

```python
def f(x, y, /, z, w, *, a, b):
    print(x, y, z, w, a, b)

f(1, 2, z=3, w=4, a=5, b=6)
## 1 2 3 4 5 6

f(1, 2, 3, w=4, a=5, b=6)
## 1 2 3 4 5 6
```

En este ejemplo:

- `x` e `y` son positional-only.
- `a` y `b` son keyword-only.
- `z` y `w` pueden especificarse posicionalmente o por palabra clave.

### Docstrings

Cuando la primera declaración en el cuerpo de una función de Python es un literal de cadena, se conoce como la cadena de documentación de la función (docstring). Una cadena de documentación se utiliza para proporcionar documentación para una función. Puede contener el propósito de la función, qué argumentos toma, información sobre los valores devueltos o cualquier otra información que crea que sería útil.

El siguiente es un ejemplo de una definición de función con una cadena de documentación:

```python
def avg(*args):
    """Returns the average of a list of numeric values."""
    return sum(args) / len(args)
```

uando se define una cadena de documentación, el intérprete de Python la asigna a un atributo especial de la función llamado `__doc__` o tambien con la funcion `help()`:

```python
print(avg.__doc__)
## Returns the average of a list of numeric values.

help(avg)
## Help on function avg in module __main__:

## avg(*args)
##     Returns the average of a list of numeric values.
```