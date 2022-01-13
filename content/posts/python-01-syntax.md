---
title: "Python 01 Syntax"
date: 2022-01-13T06:21:39-06:00
author : "El Señor Robot"
cover : "/cover01.png"
tags : ["python", "01", "syntax", "PEP8"]
keywords : ["python", "syntax", "pep8"]
description : ""
showFullContent : false
readingTime : false
draft: false

---

## Python 01 - Syntax.

Que tal, este es uno de los primeros post para el tutorial de Python, los cuales los podrás encontrar como post individuales y también lo colocare en [Menú](/pages/python) para que los puedas tener todos de manera accesible sin tener que buscar.

Un poco de Python :
Fue creado por Guido van Rossum y lo publico por primera vez el 20 de febrero de 1991, la versión actual de python es 3.9 y el lenguaje es usado en muchos ámbitos como:
- Desarrollo web
- Ciencia de datos
- Inteligencia artificial
- Empresarial, educativo.
- Scraping
- Desarrollo de vídeo juegos.

*[tranquilo, se que ya quieres escribir tu primera linea de código con `print("Hola, mundo!!")`, pero seria bueno iniciar por lo mas esencial, como lo es la sintaxis básica, ¿Bueno, pero y a mi de que me sirve la sintaxis, si solo es código?. Es importante porque te servirá para escribir código más legible, ayuda a la hora de nombrar variables, el numero máximo de caracteres por linea, como y porque comentar tu código, por mencionar algunas. Todo esto esta incluido en [PEP8](https://www.python.org/dev/peps/pep-0008/)]*

Si te es complicado recordar todo esto puedes utilizar algunas herramientas, por ejemplo en [vscode](https://code.visualstudio.com/) o [sublime text](https://www.sublimetext.com/) puedes instalar el paquete **AutoPEP8** (yo uso sublime text, puedes usar el de tu elección), en sublime text me basta con hacer `ctrl + 8` para que me abra otro pestaña y me muestre los errores o bien con `ctrl + shift + 8` realiza los cambios directamente en el archivo, otro mas es instalar con `pip3 install autopep8` y usarlo desde la linea de comando con un archivo de python así: `autopep8 mi_archivo.py -v -i` y tratara de solucionar los errores dentro del archivo.

## Organización.
El usar lineas en blanco puede ayudar a tener un código mas legible ya que tener mucho texto de manera continua puede llegar a ser confuso.

- **Rodear las funcione y clases con 2 lineas en blanco**: esto quiere decir que cada que escribamos nuestras funciones o clases hay que dejar 2 lineas en blanco por arriba y por debajo.
- **Dejar una linea en blanco entre cada método de instancia**: para que sea mas claro, los métodos de instancia son las funciones `def` dentro de una clase.
- **Dejar una linea en blanco para agrupar pasos similares**: si estamos escribiendo código de un proceso en especifico podemos delimitar ciertos pasos con una linea en blanco.

```python
class Ejemplo1:
    def prueba1():
        pass

    def prueba2():
    	pass


class Ejemplo2:
	def test1():
		pass

	def test2():
		passs

```

Como puedes observar en el ejemplo de arriba, hay 2 lineas en blanco entre cada clase `class` pero las funciones `def` solo uno. Si las funciones estan así, si deben de llevar doble linea en blanco:
```python
def fuera1():
	pass


def fuera2():
	pass

```

---
**NOTA**
Siempre en cualquier archivo python debe colocarse una linea en blanco al final, de hecho te recomendaría que si estas en algún edito de texto como vscode o sublime text e instalaste el paquete **AUTOPEP8**, hagas la prueba y veas como ajusta tu código según la guía **PEP8**, recuerda usar la combinación `ctrl + shift + 8` para ver el resultado directamente en el archivo.
---

## Separar con una linea fragmentos de código.
Supongamos que estamos trabajando con un archivo y después realizamos otra operación sobre el mismo archivo, podríamos hacer algo así:
```python
import csv

with open(file, 'r') as f:
	reader = csv.reader(f)
	registros = [n for n in reader]

	if registros[5] not in 'este valor':
		print(registros)
```

Como puedes ver,primero importamos el modulo, abrimos un archivo y después dejamos una linea en blanco para separar el código y realizar uno paso condicional, al fin de cuentas estamos realizando una acción concreta pero el dividir el código lo hace mas simple y lógico a simple vista.

## Espacios en blanco.
PEP8 nos ayuda a saber donde y como utilizar los espacio al momento de declarar variables o usar operadores dentro de nuestro código.

Usar espacio al realizar asignaciones o declarar variables:
```python
# uso correcto
x = 5

# uso incorrecto
x=5
```

En funciones con argumentos por defecto, no se deben dejar espacio, tampoco debe haber espacio dentro del paréntesis a menos que sea para separar argumentos:
```python
def funcion(phone=3):
	pass

def funcion2(argumento1, argumento2):
	pass

```
*[si, si, se que deje solo un espacio entre cada función, cuando deberían de ser 2, es intencional, para que con la practica no solo analices tu código, sino también el de los demás.]*

Agrupación por orden de ejecucion:
```python
if n > 0 and n % 2 == 0:
	print(n)

if n>0 and n%2==0:
	print(n)

```

Puedes usar los 2 ejemplos de arriba pero evita combinarlos de la siguiente manera:
```python
if n>0 and n % 2 == 0:
	print(n)

```

Los espacio en blanco no se deben usar en listas, diccionarios, tuplas o sets, solo si es para dividir elementos:
```python
lista = [1, 2, 3]
diccionario = {"nombre": "eliot", "edad": 33}
```

Otro punto importe, es no tratar de alinear las variables al declararlas:
```python
# correcto
uno = 10
otro_var = 33

# incorrecto
uno =      10
otro_var = 33
```

## Indentación del código.
tal vez hayas notado que python no utiliza llaves {} en cada bloque de código como por ejemplo **C++**:
```c++
#include <iostream>
 
int main () 
{
    std::cout << "Hola, mundo";
    return 0;
}
```

En su lugar usa la indentacion, indica un determinado bloque de código, el cual se representa usando 4 espacios o tabulador, hay que tener cuidado con este ultimo, primero porque python recomienda 4 espacio y si llegáramos a usar un tab en otro editor de texto, este pude usar un numero de tabulación diferente. Supongamos que usamos un tabulador de 6 y se nos ocurre solo borrar 2 espacios para dejarlo en 4, python puede marcar error, de igual manera evita mezclar espacios y tabulador, si el editor lo permite, configura el tabulador en 4 o de lo contrario utiliza 4 espacio.
```python
for i in range(34):
	print(i)
```

Indentar lineas de código muy largas para evitar mas de 79 caracteres:
```python
def identar_linea(argumento1, argumento2, argumento3,
				  argumento4, argumento5):
	pass

# puedes usar \ para acortar condiciones:
for i in a and\
	i not in r:
	print(...)

# o con la ayuda de paréntesis:
for (i in a and
	i not in r):
	print(...)
```

Realmente no sucede nada si no indentas lineas muy largas como una lista o argumentos dentro de una función, pero ayudan mucho para evitar hacer scroll a la derecha o cuando se trabaja con divisiones en algún editor.

## Tamaño de las lineas.
Es recomendable limitar el tamaño de las lineas a 79 caracteres, por otro lado para los *docstring* y comentarios usar 72 caracteres.

```python
# para romper una linea que no sea posible dividir puedes usar \

import csv

with open(r'/file/dir_other_file/dir1/dir_dir_dir/file_file.csv', 'r') as file,\
	open(r'archivo_de_salida/salida.txt', 'w', newline='') as salida:

	lector = csv.reader(file)
	escritor = csv.writer(salida)

	for e in lector:
		escritor.writerow(e)
```

## Palabras reservadas en Python.
Las palabras reservadas como su nobre lo dice, están reservadas para ser usadas solo por python y se pide que jamas se utilicen para nombrar o asignar variables. Podemos ver todas las palabras reservadas de la siguiente forma:
```python
import keyword

for palabras_reservadas in keyword.kwlist:
	print(palabras_reservadas)

# aqui están todas si quieres evitar escribir lo de arriba.
False      class      finally    is         return
None       continue   for        lambda     try
True       def        from       nonlocal   while
and        del        global     not        with
as         elif       if         or         yield
assert     else       import     pass
break      except     in         raise
```
lo puedes escribir en el IDLE de python si te encuentras en windows y presionar `F5` o crear un archivo .py.

Para nombrar variables evita hacerlo con espacios y en su lugar usa `_`:
```python
# Algunos ejemplos de como nombrar variables

esto_es_una_variable
EstoEsUnaVariable

# para funciones, solo pueden ser en minúsculas y separadas por guión
def esto_es_una_funcion():
	pass

# para clases siempre la primera letra debe ser en mayúscula sin guiones y la 
# segunda palabra también debe comenzar en mayúscula.

class Empleados:
	pass

class EmpleadosTi:
	class
```

Los nombres de los módulos (tus archivos python) deben nombrarse asi `mimodulo.py` o `mi_modulo.py`. 

Para importar módulos, deben de importarse uno por linea si es que son módulos diferentes:
```python
# correcto
import csv
import time

# incorrecto
import time, csv

# si pertenecen a una misma librería se pueden pasar en la misma linea
from time import time, sleep

# y en lugar de importar todos los módulos, es mejor importar solo los necesarios

# incorrecto

from Collections import *

# correcto

from Collections import Counter
```

## Comentarios.
Los comentarios son una forma de realizar anotaciones o describir nuestro código para darle seguimiento y que los demás puedan saber de que se trata el código, para esto tenemos 2 formas de hacerlo:
```python
# comentario de una sola linea
# aunque puedes añadir otra linea colocando una almohadilla

"""
comentario multi linea utilizando tripe comilla doble " o simple ', con esto
puedes documentar una área de código que requiera cierto nivel de explicación. 
"""

```

No hay que confundir los comentarios con los *docstring*, un comentario se utiliza para aumentar la legibilidad, compresión del código y solo son visibles o accesibles desde dentro del código, mientras que, un *docstring* es muy similar a un comentario, pues utiliza triple comilla doble `"`, pero este es de gran ayuda en clases y funciones, ya que permiten añadir una descripción de que hace o como funciona cada objeto.

```python
# esto es un comentario de una sola linea

"""
comentario de varias lineas
para documentar o añadir ayuda a los programadores externos
"""

def prueba(a:int, b:float) -> int:
	""""Función que recibe 2 argumentos de tipo entero"""
	pass
    


class DocExample:
    """Explicación de la clase""""
	pass
```

Los *docstring* que como ya lo pudiste notar, se tiene que declaran con triple comilla doble `"` y deben estar justo debajo de la clase y de su función, para acceder a estos métodos lo hacemos de la siguiente manera `help(prueba)`, lo que es, la palabra reservada help y dentro de los paréntesis el nombre de la función o de la clase.