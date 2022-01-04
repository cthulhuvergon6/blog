+++
title = "Crear Blog con hugo, github y netlify"
date = "2022-01-04T05:09:51-06:00"
author = "El Señor Robot"
authorTwitter = ""
cover = ""
tags = ["blog", "hugo", "github", "netlify", "linux"]
keywords = ["netlify", "github", "hugo", "linux", "crear"]
description = ""
showFullContent = false
readingTime = false
+++


Bien, pues en esta primera entrega les mostrare el proceso de como hice mi blog con la ayuda de [Hugo](https://gohugo.io/), [github](github.com) y [netlify](netlify.com).


El proceso lo realice en mi servidor de escritorio (carisimo), es un equipo muy básico como del 2000 que me ayuda para este tipo de proyectos (es mi todo terreno), el equipo no cuenta con monitor por lo cual recurriremos a una poderosa herramienta [ssh](https://es.wikipedia.org/wiki/Secure_Shell), pero no te preocupes, el proceso es idéntico si lo realizas desde tu equipo local (osea, el que estas usando en este momento).

Pongamos manos a la obra (la carne al asador, por eso de los amigos regios), comencemos con una introducción básica sobre las herramientas que utilizaremos.

En primer lugar tenemos a **Hugo**: Es un framework para la creación de sitios estáticos de propósito general, el cual esta basado en la arquitectura JAMstack, en pocas palabras podrás generar un sitio web estático que solo es alimentado por texto, imágenes, archivos .css y javascript, pero no por eso deja de ser potente o poco visual, al contrario.

**Github**: es una plataforma para almacenar tu codigo en la “nube”, github utiliza el control de versiones *git*, con lo cual una vez registrado en la plataforma podrás cargar tu contenido y llevar un control de todo el código, además de poder tenerlo en cualquier equipo y compartirlo con los demás.

**Netlify**: es una plataforma que nos va a permitir automatizar nuestros proyectos web estáticos, cuando nosotros carguemos el contenido a github, netlify se encargara de las tareas de integración y despliegue, dándonos como resultado un sitio web en linea, la plataforma cuenta con un plan gratuito el cual permite cargar solo un sitio y una url como la siguiente mi-sitio.netlify.app, pero nos otorga sitios HTTPS de manera gratuita por lo cual nos podremos evitar el generar certificados. Ya con esto evadimos muchos problemas como lo son de, disponer de un host, un dominio web, publicar nuestra web desde un equipo que se encuentra detras de NAT y tener que estar generando certificaos, aunque let’s encrypt ayuda mucho en estos casos.

Si, lo se, ya me extendí, *pero si venia a ver como crear mi sitio web gratis y mostrarle a mi novi@ mi primer post con un **hola mundo!***, no te mientas por favor, además, quien se va a tomar todo este tiempo para explicarte casi con lujo de detalle (si, con uno que otro dato un poco errado), bien, continuemos.

Por ultimo pero no menos importante SSH: secure shell, es una herramienta que permite acceder a un servidor mediante un canal seguro, el cual se encarga de cifras la conexión y haciéndola invisible para cualquier fisgón, no solo te permite conectarte a un servidor, son muchas más, las cuales dejaremos para otro post.

Viene lo bueno, como yo me encuentro en otro equipo diferente al cual realizare todo el procedimiento requeriré hacer unos cuantos movimientos antes; conectarme por ssh a mi equipo (adicional podremos realizar un ` apt update && apt upgrade`, abrir el puerto ` 1313` con ufw ya que hugo lo necesitar para lanzar la pagina de manera local). Correcto lancemos la conexión `ssh -L 1313:127.0.0.1:1313 miusuario@192.168.0.50` (al final lleva la bandera `-p` para el puerto, pero como yo lo tengo en el puerto por defecto, `22`, no es necesario ponerlo, solo si decides cambiar el puerto de escucha en tu servidor ssh). *Ey, momento!!!, se que puedo acceder a un equipo con ssh de la siguiente manera ssh usario@ip, pero tú acabas de poner `-L 1313:127.0.0.1:1313`, ke es eso!?.*

Estas en lo correcto mi pequeño saltamontes y excelente pregunta, la bandera `-L` nos permite crear un túnel para traer un servicio que se ejecuta en un servidor remoto y lanzarlo en nuestro equipo como si estuviéramos en local, donde `1313:` es el puerto de mi equipo, con `127.0.0.1` le decimos que lo queremos de manera local y después `:1313` que es el puerto del equipo remoto, no notaras diferencia alguna al realizar la conexión. Siguiente paso, dar permisos y abrir el puerto `1313`, en Debian hay que escribir `su`, para pasar a modo *root/administrador*, en distros basadas en ubuntu basta con un `sudo ufw allow 1313`, instalar hugo por primer vez `sudo apt install hugo -y` (la bandera `-y` omite la confirmación por tecla), esperamos termine la instalación y después validamos con `hugo version`, el cual mostrara la versión de hugo, en caso contrario de recibir algun error, hay que revisar dependencias o realizar un update del equipo.

Ya contamos con lo esencial, ahora nos moveremos al directorio donde tendremos nuestro proyecto, crearemos un directorio y lanzaremos `hugo new site nombre_del_proyecto` para crear un directorio donde hugo colocara todos los archivos necesarios.

## Crear directorio hugo.
[![asciicast](https://asciinema.org/a/imTTB4dq3uhuQrp73yTrNrSkV.svg)](https://asciinema.org/a/imTTB4dq3uhuQrp73yTrNrSkV)

*No le encontré la forma de hacer que se reproduzcan los vídeos desde la pagina, hay disculparan*