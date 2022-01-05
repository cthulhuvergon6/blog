+++
title = "Crear un blog con hugo, github y netlify"
date = "2022-01-04T05:09:51-06:00"
author = "El Señor Robot"
authorTwitter = ""
cover = ""
tags = ["blog", "hugo", "github", "netlify", "linux", "ssh"]
keywords = ["netlify", "github", "hugo", "linux", "crear"]
description = ""
showFullContent = false
readingTime = false
+++


Bien, pues en esta primera entrega les mostrare el proceso de como hice mi blog con la ayuda de [Hugo](https://gohugo.io/), [github](github.com) y [netlify](netlify.com).


El proceso lo realice en mi servidor de escritorio (carisimo), es un equipo muy básico como del 2000 que me ayuda para este tipo de proyectos (es mi todo terreno), el equipo no cuenta con monitor por lo cual recurriremos a una poderosa herramienta [ssh](https://es.wikipedia.org/wiki/Secure_Shell), pero no te preocupes, el proceso es idéntico si lo realizas desde tu equipo local (osea, el que estas usando en este momento).

Pongamos manos a la obra (la carne al asador, por eso de los amigos regios), comencemos con una introducción básica sobre las herramientas que utilizaremos.

En primer lugar tenemos a **Hugo**: Es un framework para la creación de sitios estáticos de propósito general, el cual esta basado en la arquitectura JAMstack, en pocas palabras podrás generar un sitio web estático que solo es alimentado por texto, imágenes, archivos .css y javascript, pero no por eso deja de ser potente o poco visual, al contrario.

**Github**: es una plataforma para almacenar tu código en la “nube”, github utiliza el control de versiones *[git](https://git-scm.com/)*, con lo cual una vez registrado en la plataforma podrás cargar tu contenido y llevar un control de todo el código, además de poder tenerlo en cualquier equipo y compartirlo con los demás.

**Netlify**: es una plataforma que nos va a permitir automatizar nuestros proyectos web estáticos, cuando nosotros carguemos el contenido a github, netlify se encargara de las tareas de integración y despliegue, dándonos como resultado un sitio web en linea, la plataforma cuenta con un plan gratuito el cual permite cargar solo un sitio y una url como la siguiente mi-sitio.netlify.app, pero nos otorga sitios HTTPS de manera gratuita por lo cual nos podremos evitar el generar certificados. Ya con esto evadimos muchos problemas como lo son de, disponer de un host, un dominio web, publicar nuestra web desde un equipo que se encuentra detras de NAT y tener que estar generando certificados, aunque let’s encrypt ayuda mucho en estos casos.

Si, lo se, ya me extendí, *"pero si venia a ver como crear mi sitio web gratis y mostrarle a mi novi@ mi primer post con un **hola, mundo!**"*, no te mientas por favor, además, ¿quien se va a tomar todo este tiempo para explicarte casi con lujo de detalle? (si, con uno que otro dato un poco errado), bien, continuemos.

Por ultimo pero no menos importante **SSH**: secure shell, es una herramienta que permite acceder a un servidor mediante un canal seguro, el cual se encarga de cifrar la conexión haciéndola invisible para cualquier fisgón, no solo te permite conectarte a un servidor, son muchas más, las cuales dejaremos para otro post.

Viene lo bueno, como yo me encuentro en otro equipo diferente al cual realizare todo el procedimiento requeriré hacer unos cuantos movimientos antes; conectarme por ssh a mi equipo (adicional podremos realizar un ` apt update && apt upgrade`, abrir el puerto ` 1313` con ufw ya que hugo lo necesitar para lanzar la pagina de manera local). Correcto lancemos la conexión `ssh -L 1313:127.0.0.1:1313 miusuario@192.168.0.50` (al final lleva la bandera `-p` para el puerto, pero como yo lo tengo en el puerto por defecto, `22`, no es necesario ponerlo, solo si decides cambiar el puerto de escucha en tu servidor ssh). *"Ey, momento!!!, se que puedo acceder a un equipo con ssh de la siguiente manera ssh usario@ip, pero tú acabas de poner `-L 1313:127.0.0.1:1313`, ke es eso!?".*

Estas en lo correcto mi pequeño saltamontes y excelente pregunta, la bandera `-L` nos permite crear un túnel para traer un servicio que se ejecuta en un servidor remoto y lanzarlo en nuestro equipo como si estuviéramos en local, donde `1313:` es el puerto de mi equipo, con `127.0.0.1` le decimos que lo queremos de manera local y después `:1313` que es el puerto del equipo remoto, no notaras diferencia alguna al realizar la conexión. Siguiente paso, dar permisos y abrir el puerto `1313`, en Debian hay que escribir `su`, para pasar a modo *root/administrador*, en distros basadas en ubuntu basta con un `sudo ufw allow 1313`, instalar hugo por primer vez `sudo apt install hugo -y` (la bandera `-y` omite la confirmación por tecla), esperamos termine la instalación y después validamos con `hugo version`, el cual mostrara la versión de hugo, en caso de recibir algun error hay que revisar dependencias o realizar un update del equipo.

Ya contamos con lo esencial, ahora nos moveremos al directorio donde tendremos nuestro proyecto, crearemos un directorio y lanzaremos `hugo new site nombre_del_proyecto` para crear un directorio donde hugo colocara todos los archivos necesarios.

## Crear directorio hugo.
[![asciicast](https://asciinema.org/a/imTTB4dq3uhuQrp73yTrNrSkV.svg)](https://asciinema.org/a/imTTB4dq3uhuQrp73yTrNrSkV)

*No le encontré la forma de hacer que se reproduzcan los vídeos desde la pagina, ustedes disculparan*

Como pudimos ver ya tenemos el esqueleto de nuestro proyecto, por el momento nos centraremos en un par de directorios y un archivo: config.toml, content, static y themes. El archivo config.toml contendra la configuraciones como el tema, el lenguaje, el menu, por mencionar alguno. Veamos que contiene actualmente, `nano config.toml`:

![configtoml](/config.png "Contenido del archivo")

Como podemos ver el archivo no tiene mucho contenido, en la primera linea tenemos `baseURL = "http://example.org/"`, cuando ejecutemos el sitio localmente no tendremos problema con esto, pero una vez que lo despleguemos con netlify hay que cambiar la url por la que nos proporcione el sitio u obtendremos un error, después tenemos `languageCode = "en-us"` es el lenguaje del sitio y lo podemos cambiar según la región donde estemos por el momento es irrelevante y por ultimo `title = "My New Hugo Site"` este titulo es el que se muestra en las pestañas del navegador. 

**Content**, como recién creamos el esqueleto del proyecto algunos directorios no contienen nada, pero este directorio contendrá un directorio *posts/* el cual como su nombre lo dice, almacenara los posts en formato `Markdown .md` y sea crean de la siguiente manera `hugo new posts/nombre-del-post.md`, (no es necesario pasarle el directorio *content*, hugo por si solo se encarga de eso), también contendrá otro directorio *pages/*, este directorio almacenara las paginas o secciones como por ejemplo los enlaces de menú y se crea de una manera muy similar `hugo new pages/about.md`, *"pero, apoco puedo lanzar mi sitio solo creando archivos Markdown, si son solo texto muy simple y caracteres extraños!?"*, si, y es que cuando tengamos nuestro primer post creado bastara con lanzar en la terminal `hugo -D` este comando creara un nuevo directorio *public/* ya con los archivos transformados en *.html*,y si queremos ver el resultado ejecutamos `hugo server -D` y en nuestro navegador preferido escribimos `localhost:1313`. **KABUM!!! magia, hijo.**

**Static**: este directorio es para colocar, por ejemplo las imágenes y se incrustan en Markdown de la siguiente manera ![imagen](/imagen.jpeg “nombre que muestra al pasar el puntero por encima”), una vez más no es necesario pasarle el static/file.jpg ya que hugo se encarga de enrutar todo.

Procedamos a crear un primer post y ver el resultado, *“Espera, no vas a explicar el directorio de themes/ y echarte un rollo mundial?”*, si, pero lo dejamos para el próximo post, mentira, pero quería aclarar un par de puntos, primero que nada hay que clonar un tema de tu gusto de la siguiente pagina oficial de [hugo](https://themes.gohugo.io/), la manera recomendada de hacerlo es así (pero antes que  nada hay que hacer un `git init`, tal como lo marca la documentación oficial) `git submodule add -f https://github.com/panr/hugo-theme-hello-friend.git themes/hello-friend`, si no se añada un tema antes, cuando carguemos el sitio con `hugo server -d` no obtendremos ningún resultado, solo una pagina en blanco, bien, una vez clonado el tema hay que añadirlo al archivo config.toml con `nano config.toml` y al final colocar `theme = “hello friend”` (el nombre viene siendo el nombre del  directorio como se guardo al momento de clonarlo, puedes elegir uno diferente) y ahora si podemos crear el primer post con `hugo new posts/prueba.md`, tendremos un archivo como este:

![configtoml](/prueba.png "Contenido de prueba.md")

Como puedes ver ya añadí algo de texto, para darle formato recuerda usar la sintaxis de Markdown, ahora hay que generar los archivos estáticos, como lo mencione en un texto más arriba, con `hugo -D` se creara el directorio *static/* y los archivos transformados a *.html*, hecho todo lo anterior procedemos a ejecutar `hugo server -D` y podremos ver nuestro sitio en funcionamiento:

Proceso para generar los archivos estáticos y levantar el servicio en local:

[![asciicast](https://asciinema.org/a/4HlRuLHLhRgcTK1oVOMwm8YNA.svg)](https://asciinema.org/a/4HlRuLHLhRgcTK1oVOMwm8YNA)

Resultado: 
![configtoml](/sitio_de_prueba.png "Contenido del archivo")

"*Que tal, eh!?, ahora corre con tu “novi@” y con toda la familia para mostrarles tu creación y para lanzarte de lleno a todas esas ofertas laborales, ya eres todo un taquero programador master races 60k.
Ey, no tan rápido, aun nos falta cargar nuestro proyecto a github, hacer nuestro primer git push y desplegarlo con netlify."*

Como ya se supone debimos haber hecho un `git init` pasaremos a lo siguiente y si no lo has hecho aun lo puedes realizar ahora mismo (recuerda que todo eso se hará dentro del directorio principal, en mi caso dentro de my-blog), después iremos a nuestra cuenta de github y crearemos un nuevo repositorio:

Nuevo repo:
![repo_](/new_repo.png "creación del repositorio")

Nos deberá mostrar algo como esto:
![copy_](/repo_conf.png)

en mi caso me da la opción con *ssh* porque yo añadí una llave para enlazar mi cuenta sin la necesidad de escribir a cada momento mi user y pass (eso también lo veremos en otro post), copiado el enlace haremos lo siguiente: un `git add .`  (no olvides el punto al final), `git remote add origin git@github.com:cthulhuvergon6/mi-primer-blog.git`, `git commit -m “mi primer blog”` y `git push -u origin` master.

Proceso:
[![asciicast](https://asciinema.org/a/s6JSOszJ0I7Z9enqjykGyBjGJ.svg)](https://asciinema.org/a/s6JSOszJ0I7Z9enqjykGyBjGJ)

Al recargar la pagina deberíamos obtener algo como esto:
![copy_](/push_p.png)



