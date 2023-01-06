---
layout: default
title: Pandas
parent: Unidad 2 - Estructuras de Datos en Python
nav_order: 5
---

# Pandas

Pandas es una biblioteca Python de código abierto que proporciona una herramienta de análisis y manipulación de datos de alto rendimiento utilizando sus poderosas estructuras de datos.

En 2008, el desarrollador Wes McKinney comenzó a desarrollar pandas cuando necesitaba una herramienta flexible y de alto rendimiento para el análisis de datos.
Antes de Pandas, Python se usaba principalmente para la recopilación y preparación de datos, tuvo muy poca contribución al análisis de datos y Pandas resolvio este problema. 

Con Pandas, podemos realizar cinco pasos típicos en el procesamiento y análisis de datos, independientemente del origen de los datos: cargar, preparar, manipular, modelar y analizar.

Pandas se utiliza en una amplia gama de campos, incluidos dominios académicos y comerciales, como finanzas, economía, estadísticas, análisis, etc.

## Instalacion

La distribución estándar de Python no viene incluida con el módulo Pandas. Una alternativa ligera es instalar Pandas utilizando el popular instalador de paquetes de Python, `pip`.

```python
!pip install pandas
```

## Estructuras de datos

Pandas se ocupa de las siguientes tres estructuras de datos:
- Series
- Dataframes
- Panel

Estas estructuras de datos se construyen sobre arreglos Numpy, lo que significa que son rápidas.

### Dimensión y descripción

La mejor manera de pensar en estas estructuras de datos es que la estructura de datos de dimensiones superiores es un contenedor de su estructura de datos de dimensiones inferiores. Por ejemplo, DataFrame es un contenedor de Series, y Panel es un contenedor de DataFrame.

| Data Structure | Dimensions | Description                                                                                                         |
|----------------|------------|---------------------------------------------------------------------------------------------------------------------|
| Series         | 1          | Arreglo homogéneo etiquetado 1D, tamaño inmutable.                                                                  |
| Data Frames    | 2          | Estructura tabular de tamaño mutable etiquetada en 2D general con columnas tipificadas potencialmente heterogéneas. |
| Panel          | 3          | Matriz de tamaño mutable, etiquetada en 3D general.                                                                 |

{: .note-title }
> Nota
>
> Todas las estructuras de datos de Pandas son de valor mutable (se pueden cambiar) y, excepto por las Series, todas son de tamaño mutable. Las Series es de tamaño inmutable.

### Series

Las Series son una matriz unidimensional como estructura con datos homogéneos. 

| 10 | 23 | 56 | 17 | 52 | 61 | 73 | 90 | 26 | 72 |

{: .new-title }
> Puntos Claves
>
> - Datos homogéneos
- Tamaño inmutable
- Valores de datos mutables

### DataFrame

DataFrame es una matriz bidimensional con datos heterogéneos.

| Name   | Age     | Gender | Rating |
|--------|---------|--------|--------|
| Steve  | 32      | Male   | 3.45   |
| Lia    | 28      | Female | 4.6    |
| Vin    | 45      | Male   | 3.9    |
| Katie  | 38      | Female | 2.78   |

| Name   | Age     | Gender | Rating |
|--------|---------|--------|--------|
| String | Integer | String | Float  |

{: .new-title }
> Puntos Claves
>
> - Datos heterogéneos
- Tamaño mutable
- Datos mutables

### Panel

El panel es una estructura de datos tridimensional con datos heterogéneos. Es difícil representar el panel en representación gráfica. Pero un panel se puede ilustrar como un contenedor de DataFrame.

<img src="/uss-softwaredatascience/assets/images/pandas_panel.png" width="800">

{: .new-title }
> Puntos Claves
>
> - Datos heterogéneos
- Tamaño mutable
- Datos mutables

## pandas.Series

Se puede crear una serie de pandas usando el siguiente constructor.

```python
pandas.Series( data, index, dtype, copy)
```

| No. | Parameter & Description                                                                                                                               |
|-----|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1   | `data`                                                                                                                                                  |
|     | Los datos toman varias formas como ndarray, lista, constantes...                                                                                         |
| 2   | `index`                                                                                                                                                 |
|     | Los valores de índice deben ser únicos y modificables, con la misma longitud que los datos. Predeterminado **np.arrange(n)** si no se pasa ningún índice. |
| 3   | `dtype`                                                                                                                                                 |
|     | dtype es para el tipo de datos. Si no hay, se inferirá el tipo de datos                                                                               |
| 4   | `copy`                                                                                                                                                  |
|     | Copiar datos. Predeterminado **Falso**                                                                                                                    |


Se puede crear una serie usando varias entradas como:

- Arrays
- Diccionarios
- Valor escalar o constante

Veamos algunos ejemplos:

***Arrays (ndarray):***
```python
#import the pandas library and aliasing as pd
import pandas as pd
import numpy as np
data = np.array(['a','b','c','d'])
s = pd.Series(data)
print s

## 0   a
## 1   b
## 2   c
## 3   d
## dtype: object
```

***Diccionarios (dict):***
```python
#import the pandas library and aliasing as pd
import pandas as pd
import numpy as np
data = {'a' : 0., 'b' : 1., 'c' : 2.}
s = pd.Series(data)
print s

## a 0.0
## b 1.0
## c 2.0
## dtype: float64
```

***Escalar (scalar):***
```python
#import the pandas library and aliasing as pd
import pandas as pd
import numpy as np
s = pd.Series(5, index=[0, 1, 2, 3])
print s

## 0  5
## 1  5
## 2  5
## 3  5
dtype: int64
```

### Accediendo a datos por posicion

```python
import pandas as pd
s = pd.Series([1,2,3,4,5],index = ['a','b','c','d','e'])

#retrieve the first element
print s[0]

## 1
```

### Accediendo a datos por label

```python
import pandas as pd
s = pd.Series([1,2,3,4,5],index = ['a','b','c','d','e'])

#retrieve a single element
print s['a']

## 1
```

## pandas.DataFrame

Se puede crear un dataframe de pandas usando el siguiente constructor.

```python
pandas.DataFrame(data, index, columns, dtype, copy)
```

| No. | Parameter & Description                                                                                                                              |
|-----|------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1   | `data`                                                                                                                                                 |
|     | Los datos toman varias formas como ndarray, series, mapas, listas, dictados, constantes y también otro DataFrame.                                    |
| 2   | `index`                                                                                                                                                |
|     | Para las etiquetas de fila, el índice que se utilizará para el marco resultante es **np.arange(n)** predeterminado opcional si no se pasa ningún índice. |
| 3   | `columns`                                                                                                                                              |
|     | Para las etiquetas de columna, la sintaxis predeterminada opcional es - **np.arange(n)**. Esto solo es cierto si no se pasa ningún índice.               |
| 4   | `dtype`                                                                                                                                                |
|     | Tipo de datos de cada columna.                                                                                                                       |
| 5   | `copy`                                                                                                                                                 |
|     | Este parámetro se usa para copiar datos, si el valor predeterminado es **Verdadero**.                                                                    |

Se puede crear un dataframe usando varias entradas como:

- Listas
- Diccionarios
- Series
- Numpy ndarrays
- Otro DataFrame

Veamos algunos ejemplos:

***Listas (lists):***
```python
import pandas as pd
data = [1,2,3,4,5]
df = pd.DataFrame(data)
print df

##      0
## 0    1
## 1    2
## 2    3
## 3    4
## 4    5
```

***Diccionarios de Listas (dict of lists/ndarrays):***
```python
import pandas as pd
data = {'Name':['Tom', 'Jack', 'Steve', 'Ricky'],'Age':[28,34,29,42]}
df = pd.DataFrame(data)
print df

##       Age      Name
## 0     28        Tom
## 1     34       Jack
## 2     29      Steve
## 3     42      Ricky
```

***Listas de Diccionarios (lists of dicts):***
```python
import pandas as pd
data = [{'a': 1, 'b': 2},{'a': 5, 'b': 10, 'c': 20}]
df = pd.DataFrame(data)
print df

##     a    b      c
## 0   1   2     NaN
## 1   5   10   20.0
```

***Diccionarios de Series (dicts of series):***
```python
import pandas as pd

d = {'one' : pd.Series([1, 2, 3], index=['a', 'b', 'c']),
   'two' : pd.Series([1, 2, 3, 4], index=['a', 'b', 'c', 'd'])}

df = pd.DataFrame(d)
print df

##       one    two
## a     1.0    1
## b     2.0    2
## c     3.0    3
## d     NaN    4
```

### Seleccion de columna

```python
import pandas as pd

d = {'one' : pd.Series([1, 2, 3], index=['a', 'b', 'c']),
   'two' : pd.Series([1, 2, 3, 4], index=['a', 'b', 'c', 'd'])}

df = pd.DataFrame(d)
print df['one']

## a     1.0
## b     2.0
## c     3.0
## d     NaN
## Name: one, dtype: float64
```

### Adicion de columna

```python
import pandas as pd

d = {'one' : pd.Series([1, 2, 3], index=['a', 'b', 'c']),
   'two' : pd.Series([1, 2, 3, 4], index=['a', 'b', 'c', 'd'])}

df = pd.DataFrame(d)

# Adding a new column to an existing DataFrame object with column label by passing new series

print ("Adding a new column by passing as Series:")
df['three']=pd.Series([10,20,30],index=['a','b','c'])
print df

print ("Adding a new column using the existing columns in DataFrame:")
df['four']=df['one']+df['three']

print df

## Adding a new column by passing as Series:
##      one   two   three
## a    1.0    1    10.0
## b    2.0    2    20.0
## c    3.0    3    30.0
## d    NaN    4    NaN
## 
## Adding a new column using the existing columns in DataFrame:
##       one   two   three    four
## a     1.0    1    10.0     11.0
## b     2.0    2    20.0     22.0
## c     3.0    3    30.0     33.0
## d     NaN    4     NaN     NaN
```

### Eliminacion de columna

```python
# Using the previous DataFrame, we will delete a column
# using del function
import pandas as pd

d = {'one' : pd.Series([1, 2, 3], index=['a', 'b', 'c']), 
   'two' : pd.Series([1, 2, 3, 4], index=['a', 'b', 'c', 'd']), 
   'three' : pd.Series([10,20,30], index=['a','b','c'])}

df = pd.DataFrame(d)
print ("Our dataframe is:")
print df

# using del function
print ("Deleting the first column using DEL function:")
del df['one']
print df

# using pop function
print ("Deleting another column using POP function:")
df.pop('two')
print df

## Our dataframe is:
##       one   three  two
## a     1.0    10.0   1
## b     2.0    20.0   2
## c     3.0    30.0   3
## d     NaN     NaN   4
## 
## Deleting the first column using DEL function:
##       three    two
## a     10.0     1
## b     20.0     2
## c     30.0     3
## d     NaN      4
## 
## Deleting another column using POP function:
##    three
## a  10.0
## b  20.0
## c  30.0
## d  NaN
```

### Seleccion de fila por label

```python
import pandas as pd

d = {'one' : pd.Series([1, 2, 3], index=['a', 'b', 'c']), 
   'two' : pd.Series([1, 2, 3, 4], index=['a', 'b', 'c', 'd'])}

df = pd.DataFrame(d)
print df.loc['b']

## one 2.0
## two 2.0
## Name: b, dtype: float64
```

### Seleccion de fila por posicion

```python
import pandas as pd

d = {'one' : pd.Series([1, 2, 3], index=['a', 'b', 'c']),
   'two' : pd.Series([1, 2, 3, 4], index=['a', 'b', 'c', 'd'])}

df = pd.DataFrame(d)
print df.iloc[2]

## one   3.0
## two   3.0
## Name: c, dtype: float64
```

### Cortar filas

```python
import pandas as pd

d = {'one' : pd.Series([1, 2, 3], index=['a', 'b', 'c']), 
   'two' : pd.Series([1, 2, 3, 4], index=['a', 'b', 'c', 'd'])}

df = pd.DataFrame(d)
print df[2:4]

##    one  two
## c  3.0    3
## d  NaN    4
```

### Adicionar filas

```python
import pandas as pd

df = pd.DataFrame([[1, 2], [3, 4]], columns = ['a','b'])
df2 = pd.DataFrame([[5, 6], [7, 8]], columns = ['a','b'])

df = df.append(df2)
print df

##    a  b
## 0  1  2
## 1  3  4
## 0  5  6
## 1  7  8
```

### Eliminar filas

```python
import pandas as pd

df = pd.DataFrame([[1, 2], [3, 4]], columns = ['a','b'])
df2 = pd.DataFrame([[5, 6], [7, 8]], columns = ['a','b'])

df = df.append(df2)

# Drop rows with label 0
df = df.drop(0)

print df

##   a b
## 1 3 4
## 1 7 8
```

## Funcionalidades Basicas de Series

| No. | Attribute or Method & Description                                             |
|-----|-------------------------------------------------------------------------------|
| 1   | `axes`                                                                          |
|     | Devuelve una lista de las etiquetas del eje de fila                           |
| 2   | `dtype`                                                                         |
|     | Devuelve el dtype del objeto.                                                 |
| 3   | `empty`                                                                         |
|     | Devuelve True si la serie está vacía.                                         |
| 4   | `ndim`                                                                          |
|     | Devuelve el número de dimensiones de los datos subyacentes, por definición 1. |
| 5   | `size`                                                                          |
|     | Devuelve el número de elementos en los datos subyacentes.                     |
| 6   | `values`                                                                        |
|     | Devuelve la Serie como ndarray.                                               |
| 7   | `head()`                                                                        |
|     | Devuelve las primeras n filas.                                                |
| 8   | `tail()`                                                                        |
|     | Devuelve las últimas n filas.                                                 |

```python
import pandas as pd
import numpy as np

#Create a series with 100 random numbers
s = pd.Series(np.random.randn(4))
print s
```


## Funcionalidades Basicas de Dataframe

| Sr.No. | Attribute or Method & Description                                                                               |
|--------|-----------------------------------------------------------------------------------------------------------------|
| 1      | `T`                                                                                                               |
|        | Transpone filas y columnas.                                                                                     |
| 2      | `axes`                                                                                                            |
|        | Devuelve una lista con las etiquetas de eje de fila y las etiquetas de eje de columna como los únicos miembros. |
| 3      | `dtypes`                                                                                                          |
|        | Devuelve los tipos de datos en este objeto.                                                                     |
| 4      | `empty`                                                                                                           |
|        | True si NDFrame está completamente vacío [sin elementos]; si alguno de los ejes tiene longitud 0.               |
| 5      | `ndim`                                                                                                            |
|        | Número de ejes / dimensiones de la matriz.                                                                      |
| 6      | `shape`                                                                                                           |
|        | Devuelve una tupla que representa la dimensionalidad del DataFrame.                                             |
| 7      | `size`                                                                                                            |
|        | Número de elementos en el NDFrame.                                                                              |
| 8      | `values`                                                                                                          |
|        | Representación numpy de NDFrame.                                                                                |
| 9      | `head()`                                                                                                          |
|        | Devuelve las primeras n filas.                                                                                  |
| 10     | `tail()`                                                                                                          |
|        | Devuelve las últimas n filas.                                                                                   |

```python
import pandas as pd
import numpy as np

#Create a Dictionary of series
d = {'Name':pd.Series(['Tom','James','Ricky','Vin','Steve','Smith','Jack']),
   'Age':pd.Series([25,26,25,23,30,29,23]),
   'Rating':pd.Series([4.23,3.24,3.98,2.56,3.20,4.6,3.8])}

#Create a DataFrame
df = pd.DataFrame(d)
print ("Our data series is:")
print df
```

## Estadistica Descriptiva

Una gran cantidad de métodos calculan colectivamente estadísticas descriptivas y otras operaciones relacionadas en un DataFrame. La mayoría de estos son agregaciones como sum(), mean(). En términos generales, estos métodos toman un argumento de eje, al igual que ndarray.{sum, std, ...}, pero el eje se puede especificar por nombre o número entero.

DataFrame − “index” (axis=0, default), “columns” (axis=1)

| No. | Function  | Description                        |
|--------|-----------|------------------------------------|
| 1      | count()   | Número de observaciones no nulas   |
| 2      | sum()     | Suma de valores                    |
| 3      | mean()    | Media de valores                   |
| 4      | median()  | Mediana de Valores                 |
| 5      | mode()    | Moda de valores                    |
| 6      | std()     | Desviación estándar de los valores |
| 7      | min()     | Valor mínimo                       |
| 8      | max()     | Valor máximo                       |
| 9      | abs()     | Valor absoluto                     |
| 10     | prod()    | Producto de Valores                |
| 11     | cumsum()  | Suma acumulativa                   |
| 12     | cumprod() | Producto acumulativo               |

```python
import pandas as pd
import numpy as np

#Create a Dictionary of series
d = {'Name':pd.Series(['Tom','James','Ricky','Vin','Steve','Smith','Jack',
   'Lee','David','Gasper','Betina','Andres']),
   'Age':pd.Series([25,26,25,23,30,29,23,34,40,30,51,46]),
   'Rating':pd.Series([4.23,3.24,3.98,2.56,3.20,4.6,3.8,3.78,2.98,4.80,4.10,3.65])
}

#Create a DataFrame
df = pd.DataFrame(d)
print df
```

La función `describe()` calcula un resumen de estadísticas relacionadas con las columnas de DataFrame.

Esta función proporciona los valores medio, estándar e IQR. Y, la función excluye las columnas de caracteres y el resumen dado sobre las columnas numéricas. `include` es el argumento que se usa para pasar la información necesaria sobre qué columnas se deben considerar para resumir. Toma la lista de valores; por defecto, 'number'.

- `object`: resume las columnas de cadena
- `number`: Resume columnas numéricas
- `all`: resume todas las columnas juntas (no debe pasarlo como un valor de lista)

## Iteraciones

El comportamiento de la iteración básica sobre los objetos Pandas depende del tipo. Al iterar sobre una serie, se considera como una matriz y la iteración básica produce los valores. Otras estructuras de datos, como DataFrame y Panel, siguen la convención similar a un dictado de iterar sobre las claves de los objetos.

En resumen, la iteración básica (para i en el objeto) produce −

- **Serie** − valores
- **DataFrame** − etiquetas de columna
- **Panel** − etiquetas de elementos

Iterar un DataFrame da nombres de columna. Consideremos el siguiente ejemplo para entender lo mismo.

```python
import pandas as pd
import numpy as np
 
N=20
df = pd.DataFrame({
   'A': pd.date_range(start='2016-01-01',periods=N,freq='D'),
   'x': np.linspace(0,stop=N-1,num=N),
   'y': np.random.rand(N),
   'C': np.random.choice(['Low','Medium','High'],N).tolist(),
   'D': np.random.normal(100, 10, size=(N)).tolist()
   })

for col in df:
   print col
```

Para iterar sobre las filas del DataFrame, podemos usar las siguientes funciones:

`iteritems()` - para iterar sobre los pares (clave, valor)
`iterrows()` - iterar sobre las filas como pares (índice, serie)
`itertuples()` - iterar sobre las filas como namedtuples

```python
# iteritems()
import pandas as pd
import numpy as np
 
df = pd.DataFrame(np.random.randn(4,3),columns=['col1','col2','col3'])

for key,value in df.iteritems():
   print key,value
```

```python
# iterrows()
import pandas as pd
import numpy as np

df = pd.DataFrame(np.random.randn(4,3),columns = ['col1','col2','col3'])

for row_index, row in df.iterrows():
   print row_index, row
```

```python
# itertuples()
import pandas as pd
import numpy as np

df = pd.DataFrame(np.random.randn(4,3),columns = ['col1','col2','col3'])

for row in df.itertuples():
    print row
```

## Funciones con Texto

Pandas proporciona un conjunto de funciones de cadena que facilitan la operación con datos de cadena. Lo que es más importante, estas funciones ignoran (o excluyen) los valores faltantes/NaN.

| Sr.No | Function & Description                                                                                              |
|-------|---------------------------------------------------------------------------------------------------------------------|
| 1     | `lower()`                                                                                                             |
|       | Convierte cadenas en Serie/Índice a minúsculas.                                                                     |
| 2     | `upper()`                                                                                                             |
|       | Convierte cadenas en la Serie/Índice a mayúsculas.                                                                  |
| 3     | `len()`                                                                                                               |
|       | Calcula la longitud de la cadena().                                                                                 |
| 4     | `strip()`                                                                                                             |
|       | Ayuda a eliminar los espacios en blanco (incluida la nueva línea) de cada cadena en la Serie/índice de ambos lados. |
| 5     | `split(' ')`                                                                                                          |
|       | Divide cada cadena con el patrón dado.                                                                              |
| 6     | `cat(sep=' ')`                                                                                                        |
|       | Concatena los elementos de serie/índice con el separador dado.                                                      |
| 7     | `get_dummies()`                                                                                                       |
|       | Devuelve el DataFrame con valores One-Hot Encoded.                                                                  |
| 8     | `contains(pattern)`                                                                                                   |
|       | Devuelve un valor booleano True para cada elemento si la subcadena contiene en el elemento, de lo contrario, False. |
| 9     | `replace(a,b)`                                                                                                        |
|       | Reemplaza el valor a con el valor b.                                                                                |
| 10    | `repeat(value)`                                                                                                       |
|       | Repite cada elemento con un número especificado de veces.                                                           |
| 11    | `count(pattern)`                                                                                                      |
|       | Devuelve el recuento de aparición del patrón en cada elemento.                                                      |
| 12    | `startswith(pattern)`                                                                                                 |
|       | Devuelve verdadero si el elemento en la Serie/Índice comienza con el patrón.                                        |
| 13    | `endswith(pattern)`                                                                                                   |
|       | Devuelve verdadero si el elemento en la Serie/Índice termina con el patrón.                                         |
| 14    | `find(pattern)`                                                                                                       |
|       | Devuelve la primera posición de la primera aparición del patrón.                                                    |
| 15    | `findall(pattern)`                                                                                                    |
|       | Devuelve una lista de todas las ocurrencias del patrón.                                                             |
| 16    | `swapcase()`                                                                                                            |
|       | Cambia la caja inferior/superior.                                                                                   |
| 17    | `islower()`                                                                                                           |
|       | Comprueba si todos los caracteres de cada cadena de la Serie/Índice están en minúsculas o no. Devuelve Booleano     |
| 18    | `isupper()`                                                                                                           |
|       | Comprueba si todos los caracteres de cada cadena de la Serie/Índice están en mayúsculas o no. Devuelve booleano.    |
| 19    | `isnumeric()`                                                                                                         |
|       | Comprueba si todos los caracteres de cada cadena de la Serie/Índice son numéricos. Devuelve booleano.               |

```python
import pandas as pd
import numpy as np

s = pd.Series(['Tom', 'William Rick', 'John', 'Alber@t', np.nan, '1234','SteveSmith'])

print s
```

## Indexado y Seleccion de Datos

Pandas ahora admite tres tipos de indexación de ejes múltiples; los tres tipos se mencionan en la siguiente tabla:

| No. | Indexing & Description                       |
|-------|----------------------------------------------|
| 1     | `.loc()`                                       |
|       | basado en etiquetas                          |
| 2     | `.iloc()`                                      |
|       | basado en enteros                            |
| 3     | `.ix()`                                        |
|       | Basados ​​tanto en etiquetas como en enteros |

```python
# .loc()
#import the pandas library and aliasing as pd
import pandas as pd
import numpy as np

df = pd.DataFrame(np.random.randn(8, 4),
index = ['a','b','c','d','e','f','g','h'], columns = ['A', 'B', 'C', 'D'])

# Select few rows for multiple columns, say list[]
print df.loc[['a','b','f','h'],['A','C']]
```

```python
# .iloc()
import pandas as pd
import numpy as np

df = pd.DataFrame(np.random.randn(8, 4), columns = ['A', 'B', 'C', 'D'])

# Slicing through list of values
print df.iloc[[1, 3, 5], [1, 3]]
print df.iloc[1:3, :]
print df.iloc[:,1:3]
```

```python
# .ix()
import pandas as pd
import numpy as np

df = pd.DataFrame(np.random.randn(8, 4), columns = ['A', 'B', 'C', 'D'])

# Integer slicing
print df.ix[:4]
# Index slicing
print df.ix[:,'A']
```

Adicionalmente, podemos seleccionar por etiqueta sin la necesidad de usar .loc() (con uso de listas) o tambien a traves del operador de atributo `.`.

```python
# .ix()
import pandas as pd
import numpy as np

df = pd.DataFrame(np.random.randn(8, 4), columns = ['A', 'B', 'C', 'D'])

# List slicing
print df[['A','C']]
# Attribute operator slicing
print df.A
```

## Agrupacion (Groupby)

Cualquier operación groupby implica una de las siguientes operaciones en el objeto original, ellos son:

- Dividir el objeto
- Aplicar una función
- Combinacion de resultados

En muchas situaciones, dividimos los datos en conjuntos y aplicamos alguna funcionalidad en cada subconjunto. En la funcionalidad de aplicación, podemos realizar las siguientes operaciones:

- `Agregación`: cálculo de una estadística de resumen
- `Transformación`: realizar alguna operación específica del grupo
- `Filtración`: descartar los datos con alguna condición.

```python
#import the pandas library
import pandas as pd

ipl_data = {'Team': ['Riders', 'Riders', 'Devils', 'Devils', 'Kings',
   'kings', 'Kings', 'Kings', 'Riders', 'Royals', 'Royals', 'Riders'],
   'Rank': [1, 2, 2, 3, 3,4 ,1 ,1,2 , 4,1,2],
   'Year': [2014,2015,2014,2015,2014,2015,2016,2017,2016,2014,2015,2017],
   'Points':[876,789,863,673,741,812,756,788,694,701,804,690]}
df = pd.DataFrame(ipl_data)

print df
```

### Separar data en grupos

El objeto Pandas se puede dividir en cualquiera de sus objetos. Hay varias formas de dividir un objeto como:

- obj.groupby('key')
- obj.groupby(['key1','key2'])
- obj.groupby(key, axis=1)

```python
# Split data into groups
print df.groupby('Team') 
# View groups           
print df.groupby('Team').groups
# View multiple groups
print df.groupby(['Team','Year']).groups
```

```python
# Iterating through Groups
grouped = df.groupby('Year')

for name, group in grouped:
   print name
   print group

# Select a Group
grouped = df.groupby('Year')

print grouped.get_group(2014)
```

### Agregación

Una función agregada devuelve un solo valor agregado para cada grupo. Una vez que se crea el grupo por objeto, se pueden realizar varias operaciones de agregación en los datos agrupados.

Una obvia es la agregación a través del método `agg` o equivalente.

```python
# Aggreagation
grouped = df.groupby('Year')
print grouped['Points'].agg(np.mean)

# Attribute Access in Python Pandas
grouped = df.groupby('Team')
print grouped.agg(np.size)

# Multiple Aggregation Functions
grouped = df.groupby('Team')
print grouped['Points'].agg([np.sum, np.mean, np.std])
```

### Transformación

La transformación en un grupo o una columna devuelve un objeto indexado del mismo tamaño que el que se está agrupando. Por lo tanto, la transformación debería devolver un resultado del mismo tamaño que el de un fragmento de grupo.

```python
# Transformations
grouped = df.groupby('Team')
score = lambda x: (x - x.mean()) / x.std() * 10
print grouped.transform(score)
```

### Filtración

La filtración filtra los datos según un criterio definido y devuelve el subconjunto de datos. La función filter() se utiliza para filtrar los datos.

```python
# Filtration
print df.groupby('Team').filter(lambda x: len(x) >= 3)
```

## Join/Merge

Pandas tiene operaciones de unión en memoria de alto rendimiento y con todas las funciones, idiomáticamente muy similares a las bases de datos relacionales como SQL.

Pandas proporciona una sola función, fusionar, como punto de entrada para todas las operaciones estándar de unión de bases de datos entre objetos DataFrame.

```python
pd.merge(left, right, how='inner', on=None, left_on=None, right_on=None,
left_index=False, right_index=False, sort=True)
```

Aquí, se definen los siguientes parámetros:

- `left`: un objeto DataFrame.
- `right`: Otro objeto DataFrame.
- `on`: Columnas (nombres) para unirse. Debe encontrarse en los objetos DataFrame izquierdo y derecho.
- `left_on`: columnas del DataFrame izquierdo para usar como claves. Pueden ser nombres de columna o matrices con una longitud igual a la longitud del DataFrame.
- `right_on`: columnas del DataFrame derecho para usar como claves. Pueden ser nombres de columna o matrices con una longitud igual a la longitud del DataFrame.
- `left_index`: si es verdadero, se usa el índice (etiquetas de fila) del DataFrame izquierdo como su(s) clave(s) de unión. En el caso de un DataFrame con MultiIndex (jerárquico), el número de niveles debe coincidir con el número de claves de combinación del DataFrame derecho.
- `right_index`: el mismo uso que left_index para el DataFrame derecho.
- `how` − Uno de **left**, **right**, **outer**, **inner**. El valor predeterminado es inner.
- `sort` − Ordena el DataFrame resultante por las claves de combinación en orden lexicográfico. El valor predeterminado es Verdadero, el establecimiento en Falso mejorará sustancialmente el rendimiento en muchos casos.

```python
# import the pandas library
import pandas as pd
left = pd.DataFrame({
   'id':[1,2,3,4,5],
   'Name': ['Alex', 'Amy', 'Allen', 'Alice', 'Ayoung'],
   'subject_id':['sub1','sub2','sub4','sub6','sub5']})
right = pd.DataFrame(
   {'id':[1,2,3,4,5],
   'Name': ['Billy', 'Brian', 'Bran', 'Bryce', 'Betty'],
   'subject_id':['sub2','sub4','sub3','sub6','sub5']})
print left
print right
```

```python
# Merge Two DataFrames on a Key
print pd.merge(left,right,on='id')
# Merge Two DataFrames on Multiple Keys
print pd.merge(left,right,on=['id','subject_id'])
```

El argumento `how` para fusionar especifica cómo determinar qué claves se incluirán en la tabla resultante. Si una combinación de teclas no aparece en las tablas izquierda o derecha, los valores en la tabla unida serán NA.

Aquí hay un resumen de las opciones de cómo y sus nombres equivalentes de SQL.

| Merge Method | SQL Equivalent   | Description                |
|--------------|------------------|----------------------------|
| left         | LEFT OUTER JOIN  | Use keys from left object  |
| right        | RIGHT OUTER JOIN | Use keys from right object |
| outer        | FULL OUTER JOIN  | Use union of keys          |
| inner        | INNER JOIN       | Use intersection of keys   |

```python
# Left Join
print pd.merge(left, right, on='subject_id', how='left')
# Right Join
print pd.merge(left, right, on='subject_id', how='right')
# Outer Join
print pd.merge(left, right, how='outer', on='subject_id')
# Inner Join
print pd.merge(left, right, on='subject_id', how='inner')
```

## Plotting

Esta funcionalidad en Series y DataFrame es solo un simple envoltorio alrededor del método plot() de las bibliotecas matplotlib.

```python
import pandas as pd
import numpy as np

df = pd.DataFrame(np.random.randn(10,4),index=pd.date_range('1/1/2000',
   periods=10), columns=list('ABCD'))

df.plot()
```

Los métodos de trazado permiten un puñado de estilos de trazado distintos del trazado de líneas predeterminado. Estos métodos se pueden proporcionar como argumento de palabra clave `kind` para plot(). Estos incluyen:

- `bar` o `barh` para diagramas de barras
- `hist` para histograma
- `box` para boxplot
- `area` para plots de área
- `scatter` para diagramas de dispersión
- `pie` para diagramas de torta

```python
# Barplot
import pandas as pd
import numpy as np

df = pd.DataFrame(np.random.rand(10,4),columns=['a','b','c','d'])

df.plot.bar()
df.plot.bar(stacked=True)     ## Stacked plot
df.plot.barh(stacked=True)    ## Horizontal stacked plot
```

```python
# Histograms
import pandas as pd
import numpy as np

df = pd.DataFrame({'a':np.random.randn(1000)+1,'b':np.random.randn(1000),'c':
np.random.randn(1000) - 1}, columns=['a', 'b', 'c'])

df.plot.hist(bins=20)
```

```python
# Box Plots
import pandas as pd
import numpy as np

df = pd.DataFrame(np.random.rand(10, 5), columns=['A', 'B', 'C', 'D', 'E'])

df.plot.box()
```

```python
# Area Plot
import pandas as pd
import numpy as np

df = pd.DataFrame(np.random.rand(10, 4), columns=['a', 'b', 'c', 'd'])

df.plot.area()
```

```python
# Scatter Plot
import pandas as pd
import numpy as np 


df = pd.DataFrame(np.random.rand(50, 4), columns=['a', 'b', 'c', 'd'])

df.plot.scatter(x='a', y='b')
```

```python
# Pie Chart
import pandas as pd
import numpy as np

df = pd.DataFrame(3 * np.random.rand(4), index=['a', 'b', 'c', 'd'], columns=['x'])

df.plot.pie(subplots=True)
```