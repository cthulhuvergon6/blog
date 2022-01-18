---
title: "Python 02 Nombrando Variables"
date: 2022-01-18T14:27:29-06:00
author : "El Señor Robot"
cover : "/cover02.png"
tags : ["python", "02", "variables", "comentarios"]
keywords : ["python", "variables"]
description : ""
showFullContent : false
readingTime : false
draft: false

---

## Python 02 - Nombrando variables.

En este segundo post aprenderemos como nombrar y utilizar correctamente las variables.

## ¿Qué es una variable en python?
Un variable podría ser una palabra a la que le asignas un valor o una lista vacía para añadirle valores, entonces un valor siempre estará asociado a una variable.

## Nombrar variables.
La sintaxis básica seria, `nombre_de_la_variable = valor`, el valor puede ser un string `str`, entero `int`, decimal `float`, lista, sets, tuplas, diccionario, por nombrar algunos.
- Deben comenzar por una letra o guión bajo `_`.
- El uso de palabras reservadas esta prohibido.
- Usar nombres descriptivos.
- Deben estar escritas en minúsculas y separadas por `_`.
- Las constantes deben ser en mayúsculas y separadas con `_`:
un detalle con las constantes es que realmente en python no existen, si bien las constantes son para declarar variables que no van a cambiar con el tiempo y que por defecto no se pueden modificar, la cosa es que en python si las puedes modificar, pero si ves o declaras una constante deberías evitar modificarla, ya que tiene su motivo de existir dentro del programa.

```python
# ejemplo de nombrar variables

# correcto
nombre_de_mi_variable
palabra
registro_8
_mi_variable
CONSTANTE

# incorrecto, no pueden iniciar con `.`, `-` o numero al inicio
-variable
23variable
.palabra

# ejemplos prácticos
cadena = 'esto es una palabra' # recuerda que puedes usar comilla simple o doble

# puedes mezclar las comillas para resaltar algun valor o palabra
cadena = 'Esto es una "gran palabra"'

entero = 13 # entero
decimal = 13.15 # float

# las literales es lo mismo que una variable pero es directamente descriptivo

color_rojo = 'red'

# para ver los resultado con la ayuda de print()

print(color_rojo)

# puedes asignar el resultado de otras variables

a = 20
b = 15
resultado = a + b
print(resultado)

# declarar una lista con valores predeterminados

lista = [1, 2, 3, 4, 5]

```

Si estas en la terminal o usas el IDLE de python puedas usar la función `type()`, la cual pasándole un argumento, en este caso el nombre de cualquiera de las variables que haya declarado, te mostrara el tipo de clase de la variable.
```python
# tenemos dos formas de hacerlo

print(type(cadena))

# o solo

type(cadena)
type(entero)
type(decimal)

# también podemos hacer lo siguiente

print(type(cadena) is str) # devuelve True
print(type(entero) is int) # True
print(type(decimal) is float) # True

# otra opción que puedes usar

print(type([]) is list) # True
```

## Asignación múltiple ó desempaquetado de tuplas.

## Asignación múltiple.
Es muy similar a lo que ya hicimos en unos pasos más arriba, pero con la asignación múltiple podemos asignar múltiples variables al mismo tiempo sobre una misma linea. La asignación múltiple puede ser usada en cualquier iterable (cadenas, listas, tuplas, sets y diccionarios).

```python
# crearemos 3 variables y les asignaremos un valor

cadena, entero, decimal = 'palabra', 300, 193.12

# desde cli o IDLE basta con escribir la variable y dar enter para ver el 
# resultado, en editores de texto hay que usar print(variable)

# también podemos usarlo con cadenas
a, b = 'Hi' # a = 'H' y b = 'i'
# el uso de paréntesis `()` es opcional

(a), (b) = 'Hi'

```

En el ejemplo de arriba declaramos 3 variables en la misma linea y les asignamos un valor sobre la misma linea, como ya te diste cuenta, les asigna el valor respetando la posición. De haber declarado solo 2 variables obtendríamos un error, ya que se debe declarar por igual el numero de variables por el numero de elementos en el iterable.

También podemos utilizar la asignación mutile con estructuras de datos como listas, sets, tuplas y diccionarios.
```python
# asignación múltiple en estructura de datos

manzana, platano, uva = ['manzana', 'platano', 'uva']

# con listas, tuplas y sets, la asignación múltiple es igual, pero en diccionarios
# es diferente.
user = {'nombre':'elliot', 'edad': 30}

# de esta manera solo obtienes las key (claves)
nombre, edad = user

# para obtener los valores necesitamos la función values()
nombre, edad = user.values()

# si estas en una versión de python 3.6 o menor puede que hayas notado que
# la asignación no mantuvo el orden esperado y es que solo a partir de python
# 3.7 los diccionarios mantiene el orden a como fueron creados, por es misma
# razón en otras versiones menores los valores no pueden ser los esperados

# incluso lo podemos usar en la funcion format(), con esto evitamos acceder
# a todos los elementos por su indice

elementos = ['hoja', 'vaso', 'agua', 'python']

print('{},{},{},{}'.format(*elementos))

```

## Desempaquetado.
Es lo mismo que la asignación múltiple, pero como su nombre lo dice, nos permite desempaquetar elementos de una variable con elementos ya declarados.
```python
# desempaquetar una lista

lista = [1,2,3,4]
uno, dos, tres, cuatro = lista

# podemos realizar un desempaquetado haciendo uso del bucle for

for uno, dos, tres, cuatro in lista:
	print(uno, dos, tres, cuatro)

# para usar un for dentro de un diccionario seria así

for key, value in diccionario.items():
	print(key, value)

```

*[Se que hay elementos que un desconoces como las estructuras de datos o el bucle for, pero no te apures, solo son ejemplos y en los siguientes post entraremos mas a detalle en cada uno de ellos.]*

## Asignar múltiples valores a una sola variable.

Como vimos podemos asignar valores a múltiples variables declaradas, pero que pasa si tengo 10 elementos y solo 2 variables, pero a una de ellas deseo asignarle una cantidad predeterminada de elementos?.
```python
lista = [1,2,3,4,5,6,7,8,9]
# en a solo asignamos 3 elementos, mientras que b se lleva los demás
a = lista[0:3] # [1, 2, 3]
b = lista[3:] # [4, 5, 6, 7, 8, 9]

# en este caso hicimos uso de slices o cortes

```

## Uso de `*` como alternativa a cortes *(los corte o rebanadas las veremos en las listas)*.

El uso de `*` permite que al colocarlo junto y antes de la variable se le asignen múltiples elementos. Veamos un par de ejemplos.
```python
lista = [1,2,3,4,5,6,7,8,9]

a, *b = lista

# donde `a` solo obtendria `1` y `b` `2,3,4,5,6,7,8,9`

inicio, *medio, fin = lista

# quedaría así `inicio[1]`, `medio[2,3,4,5,6,7,8]` y `fin[9]`

# que a su vez seria similar a:
lista_anidada = [[1,2,3], [4,5,6], [7,8,9]]

a, b, c = lista_anidada

# donde cada variable obtiene una lista
# `a = [1,2,3]`, `b = [4,5,6]` y `c[7,8,9]`

# suponiendo que quisiéramos desempaquetar los elementos de una lista anidada
a, [b,c,d], e = lista_anidada

# a y e obtiene una lista mientras que b, c y d obtiene solo un elemento
# `a = [1,2,3]`, `b=4`, `c=5`, `d=6` y `e = [7,8,9]` 
```

---
NOTA: 
Todo esto que escribo es con la intención de pasar todas mis notas sobre python para que puedan ser de ayuda, no soy experto en python y reconozco que pueden haber un par de errores, ya que también me encuentro aprendiendo más cosas sobre este lenguaje de programación tan amplio. Recuerda poner en practica todo lo que veas aquí o en cualquier otro lado, la practica hace al maestro.
---

*[Este blog es ajeno a cualquier partido político del "Bienestar". Saludos a la canica]*