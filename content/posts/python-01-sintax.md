---
title: "Python 01 Sintax"
date: 2022-01-12T13:04:01-06:00
draft: true
author : "El Señor Robot"
cover : ""
tags : ["python", "01", "syntax", "PEP8", "post-semanal"]
keywords : ["python syntax", "pep8"]
description : ""
showFullContent : false
readingTime : true
---

## Python 01 - Syntax.

Que tal, este es uno de los primeros post para el tutorial de Python, los cuales los podras encontrar como post individuales y tambien lo colocares en [Menu]() para que los puedas tener todos de manera accesible sin tener que buscar.

Un poco de Python :
Fue creado por Guido van Rossum y lo publico por primera vez el 20 de febrero de 1991,la version actual de python es 3.9 y el lenguaje es usado en muchos ambitos como:
- Desarrollo web
- Ciencia de datos
- Inteligencia artificial
- Emresarial, educativo.
- Scraping
- Desarrollo de video juegos.

*[tranquilo, se que ya quieres escribir tú primera linea de codigo con print("Hola, mundo!!"), pero seria bueno iniciar por lo mas esencial, como lo es la sintaxis basica, ¿Bueno, pero y a mi de que me sirve la sintax, si solo es código?. Es importante porque te serviara para escribir código maás legible, ayuda a la hora de nombrar variables, el numero maximo de caracteres por linea, como y porque comentar tu codigo, por mencionar algunas. Todo esto esta incluido en [PEP8](https://www.python.org/dev/peps/pep-0008/)]*

Si te es complicado recordar todo esto puedes utilizar algunas herramientas, por ejemplo en [vscode](https://code.visualstudio.com/) o [sublime text](https://www.sublimetext.com/) puedes intalar el paquete **AutoPEP8** (yo uso sublime text, pero usar el de tu eleccion), en sublime text me basta con hacer `ctrl + 8` para que me abra otro pestaña y me muestre los errores o bien con `ctrl + shift + 8` realiza los cambios directamente en el archivo, otro mas es instalar con `pip3 install autopep8` y usarlo desde la linea de comando con un archivo de python asi: `autopep8 mi_archivo.py -v -i` y tratara de solucionar los errores dentro del archivo.

## Organización.
El usar lineas en blanco puede ayudar a tener un cógio mas legible ya que tener mucho texto de manera continua puede llegar a ser confuzo.

- **Rodear las funcione y clases con 2 lineas en blanco**: esto quiere decir que cada que escribamos nuestras funciones o clases hay que dejar 2 lineas en blanco por arriba y por debajo.
- **Dejar una linea en blanco entre cada metodo de instancia**: para que sea mas claro, los metodos de instacia son las funciones `def` dentro de una clase.
- **Dejar una linea en blanco para agrupar pasos similares**: si estamos escribiendo codigo de un proceso en especifico podemos delimitar ciertos pasos con una linea en blanco.

```
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

Como puedes observar en este ejemplo, hay 2 lineas en blanco entre cada clase `class` pero las funciones `def` solo uno. Si las funciones estan así, si deben de llevar doble linea en blanco:
```
def fuera1():
	pass


def fuera2():
	pass

```

---
**NOTA**
Siempre en cualquier archivo python debe colocarse una linea en blanco al final, de hecho te recomendaria que si estas en algun edito de texto como vscode o sublime text e instalaste el paquete **AUTOPEP8**, hagas la prueba y veas como ajusta tu codigo segun la guia **PEP8**, recuerda usar la combinacion `ctrl + shift + 8` para ver el resultado directamene en el archivo.
---

## Separar con una linea fragmentos de codigo.
Supongamos que estamos trabajando con un archivo y despues realizamos otra operacion sobre el mismo archivo, podriamos hacer algo así:
```
import csv

with open(file, 'r') as f:
	reader = csv.reader(f)
	registros = [n for n in reader]

	if registros[5] not in 'este valor':
		print(registros)
```

Como puedes ver, abrimos un archivo y despues dejamos una linea en blanco para separar el codigo y realizar uno paso condicional, al fin de cuentas estamos realizando una accion concreta pero el dividir el codigo lo hace mas simple y logico a simple vista.

## Espacios en blanco.
PEP8 no ayuda a saber donde y como utilizar los espacion al momento de declarar variables o usar operadores dentro de nustro codigo.

Usar espacion al realizar asignaciones o declarar variables:
```
# uso correcto
x = 5

# uso incorrecto
x=5
```

En funciones con argumentos por defecto, no se deben dejar espacio, tampoco debe haber espacio dentro del parentesis a menos que sea para separar argumentos:
```
def funcion(phone=3):
	pass

def funcion2(argumento1, argumento2):
	pass

```
*[si, si, se que deje solo un espacion entre cada funcion, cuando deberian de ser 2, es intencional, para que con la practica no solo analizes tu codigo, sino tambien el de los demas.]*

Agrupacion por orden de ejecucion:
```
if n > 0 and n % 2 == 0:
	print(n)

if n>0 and n%2==0:
	print(n)

```

Puedes usar los 2 ejemplos de arriba pero evita combinarlos de la siguiente manera:
```
if n>0 and n % 2 == 0:
	print(n)

```

Los espacion en blanco no se deben usar en listas, diccionarios, tuplas o sets, solo si es para dividir elementos:
```
lista = [1, 2, 3]
diccionario = {"nombre": "eliot", "edad": 33}
```

Otro punto importe, es no tatar de alinear las variables al declararlas:
```
# correcto
uno = 10
otro_var = 33

# incorrecto
uno =      10
otro_var = 33
```

## Identación del código.
tal vez hayas notado que python no utiliza llaves {} en cada bloque de codigo como por ejemplo **C++**:
```
#include <iostream>
 
int main () 
{
    std::cout << "Hola, mundo";
    return 0;
}
```

En su lugar usa la indentacion, indica un determinado bloque de codigo, el cual se representa usando 4 espacios o tabulador, hay que tener cuidado con este ultimo, primero porque python recomienda 4 espacio y si llegaramos a usar un tab en otro editor de texto, este pude usar un numero de tabulacion diferente. Supongoamos que usamos un tabulador de 6 y se nos ocurre solo borrar 2 espacios para dejarlo en 4, python puede marcar error, de igual manera evita convinar espacion y tabulador, si el editor lo permite, configura el tabulador en 4 o de lo contrario utiliza 4 espacio.
```
for i in range(34):
	print(i)
```

Identar lineas de codigo muy largas para evitar mas de 79 caracteres:
```
def identar_linea(argumento1, argumento2, argumento3,
				  argumento4, argumento5):
	pass

# pudes usar \ para acortar condicones:
for i in a and\
	i not in r:
	print(...)

# o con la ayuda de parentesis:
for (i in a and
	i not in r):
	print(...)
```

Realmente no sucede nada si no identas lineas muy largas como una lista o argumentos dentro de una funcion, pero ayudan mucho para evitar hacer scroll a la derecha o cuando se trabaja con divisiones en algun editor.

## Tamaño de las lineas.
Es recomendable limitar el tamaño de las lineas a 79 caracteres, por otro lado para los *docstring* y comentarios usar 72 caracteres.

```
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
Las palabras reservadas como su nobre lo dice, estan reservadas para ser usadas solo por python y se pide que jamas se utilizen para nombrar o asignar variables. Podemos ver todas la s palabras reservadas de la siguiente forma:
```
import keyword

for palabras_reservadas in keyword.kwlist:
	print(palabras_reservadas)

# aqui estan todas si quieres evitar escribir lo de arriba.
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
```
# Algunos ejemplos de como nombrar variables

esto_es_una_variable
EstoEsUnaVariable

# para funciones, solo pueden ser en minuscular y separadas por guion
def esto_es_una_funcion():
	pass

# para clases simpre la primera letra debe ser en mayuscula sin guines y la 
# segunda palabra tambien debe comenzar en mayuscula.

class Empleados:
	pass

class EmpleadosTi:
	class
```

Los nombres de los modulos (tus archivos python) deben nombrarse asi `mimodulo.py` o `mi_modulo.py`. 

Para importar modulos, deben de importarse uno por linea si es que son modulos difertes:
```
# correcto
import csv
import time

# incorrecto
import time, csv

# si pertenecen a una misma libreira se puden pasar en la misma linea
from time import time, sleep

# y en lugar de imortar todos los modulos, es mejor importar solo los necesarios

# incorrecto

from Collections import *

# correcto

from Collections import Counter
```

## Comentarios.
Los comentarios son una forma de realizar anotacones o describir nuestro codigo para darle seguimiento y que los demas puedan saber de que se trata el codigo, para esto tenemos 2 formas de hacerlo:
```
# comentario de una sola linea
# aunque puede sañadir otra linea colocando una almoadilla

"""
comentario multilinea utilizando tripe comilla doblre " o simple '.
con esto puedes domunetar una area de codigo que requiera cierto nivel de explicacion. 
"""

```

No hay que confundir los comentarios con los *docstring*, un comentario se utiliza para aumentar la legibilida, compresion del codigo y solo son visibles o accesibles desde dentro del codigo, mientras que, un *docstring* es muy similar a un comentario, pues utiliza triple comilla doble `"`, pero este es de gran ayuda en clases y funciones, ya que permiten añadir una descripcion de que hace o como funciona cada objeto.

```
# esto es un comentario de una sola linea

"""
comentario de varias lineas
para docuentar o añadir ayuda a los progremadores externos
"""

def prueba(a:int, b:float) -> int:
	""""Funcion que recibe 2 argumentos de tipo entero"""
	pass
    


class DocExample:
    """Explicacion de la clase""""
	pass
```
Los *docstring* que como ya lo pudiste notar, se tiene que declaran con triple comilla doble `"` y deben estar justo debajo de la clase y de su funcion, para acceder a estos metodos lo hacemos de la siquiente manera `help(prueba)`, lo que es, la palabra reservada help y dentro de los parentesis el nombre de la funcion o de la clase.
