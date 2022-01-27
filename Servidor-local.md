Algunas funciones (como cargar archivos externos, por ejemplo) funcionan según lo esperado cuando los archivos son ubicados en línea a través de FTP o SSH. Sin embargo, si estás tratando de revisarlos localmente, verás algún error del tipo "cross-origin" (origen cruzado) en la consola. La solución a esto es usar lo que se conoce como un servidor web local. Este tutorial incluye instrucciones para configurar distintos tipos de servidores web locales en Mac OSX, Windows y Linux.

## Python SimpleHTTPServer (Primera opción)

Si necesitas ejecutar rápidamente un servidor web y no quieres molestarte en configurar apache o algo similar, Python te puede ayudar. Python incluye un servidor HTTP simple. Con la ayuda de este pequeño servidor HTTP puedes transformar cualquier directorio en tu sistema en un directorio de un servidor web. Lo único que necesitas es tener instalado [Python](https://www.python.org/downloads/) (Python ya viene instalado en Mac OS X).

[Tutorial de Python SimpleHTTPServer](https://github.com/lmccart/itp-creative-js/wiki/SimpleHTTPServer)

Escribe en Terminal:
```
python -m SimpleHTTPServer
```

O  escribe esto si estás usando Python 3:
```
python -m http.server
```

A continuación visita `http://localhost:8000` en tu navegador.

Desafortunadamente el servidor simple de Python es muy lento. Cargar una página local a menudo no funcionará y no podrá transmitir video y tendrá problemas con archivos medianos como un mp3 de 8MB, por ejemplo. Sin embargo, será suficiente para cargar la mayoría de los textos, tipografías e imágenes.

## Node http-server (Segunda opción) 

Una alternativa es http-server de node.js. Es mucho más rápido que el servidor simple de Python y requiere un poco de configuración. Solamente 3 simples pasos:

1.  [Descarga e instala node.js](https://nodejs.org/en/download/)
2.  Abre una sesión de terminal 
3.  En OSX/Linux escribe

        sudo npm install -g http-server

    En Windows escribe (quizás necesites abrir la terminal como admin)

        npm install -g http-server
 
¡Listo!

De ahora en adelante basta con hacer `cd` al directorio que tiene los archivos que quieres poner en tu servidor y luego escribir

    http-server

Luego dirige tu navegador a `http://localhost:8080/`

Nota: si estás teniendo problema con que el navegador no refresca tus archivos JavaScript después de que haces cambios, puede que necesites instanciar el servidor con un valor especifico de cache. Para hacer esto, incluye la etiqueta cache timeout, con un valor de '-1'. Esto le indica al navegador que no tenga un cache de archivos (como sketch.js).

```bash
http-server -c-1
```

## Processing Simple HTTPServer (Tercera opción) 
Biblioteca Simple HTTPServer para Processing. Permite comunicación en ambas direcciones.
```
import http.*;

SimpleHTTPServer server;

void setup() {
  // Crea un servidor que escucha en el puerto 8000
  // sirviendo index.html, que está en el directorio "data"
  server = new SimpleHTTPServer(this); 
}
```

[Página de la biblioteca de Processing simple HTTP server](https://transfluxus.github.io/SimpleHTTPServer/)


## Apache Server (Cuarta opción) 

Python SimpleHTTPServer es bueno para empezar, pero en algún punto vas a querer configurar un servidor Apache.Un servidor Apache soporta una gran rango de funciones HTTP y escala bien para proyectos más grandes. Revisa más abajo la configuración específica según tu sistema operativo.
### Mac OS X

Mac OS X desde 10.5 Leopard tiene instalado un servidor web Apache, lo único que necesitas hacer es habilitarlo y ubicar los archivos en el lugar correcto.

#### Mac OS X 10.7 y arriba

1. Abre Terminal y escribe:
```
sudo apachectl start
```
2. Verifica que esté funcionando visitando `http://localhost` en tu navegador. Deberías ver "It works!" en el navegador.
3. Autoriza los permisos para los archivos en el servidor escribiendo los siguientes dos comandos en la Terminal:
```
sudo chown root:<tu nombreDeUsuario> -R /Library/WebServer/Documents

sudo chmod -R 755 /Library/WebServer/Documents
```
4. Ubica tu proyecto en algún lugar dentro de /Library/WebServer/Documents/.
5. Visítalo en http://localhost/(el directorio del proyecto dentro de /Library/WebServer/Documents).
```
http://localhost/mi-bosquejo-p5
```

#### Mac OS X 10.5 y 10.6

1. Enciende el servidor web. Anda a Preferencias de Sistema > Compartir, y marca la casilla “Web Shar­ing”.
2. Verifica que está funcionando, visitando `http://localhost/~<tu nombreDeUsuario>` en tu navegador. Deberías ver una página web por defecto con el título "Your Website".
3. Ubica tu proyecto dentro `<tu NombreDeUsuario>/Sites`.
4. Revísalo en http://localhost/~(tu nombreDeuUsuario)/(el directorio del proyecto dentro de `<tu nombreDeUsuario>/Sites`).
```
http://localhost/~macusername/mi-bosquejo-p5
```

### Windows

1. Descarga WampServer desde [http://www.wampserver.com/en/](http://www.wampserver.com/en/).
2. Instala WampServer y sigue las instrucciones.
3. El directorio “www” será creado automáticamente (usualmente c:\wamp\www).
4. Crea un subdirectorio dentro de “www” y ubica tus archivos HTML/JS dentro.
5. Abre tu navegador web y anda a la URL : http://localhost/tuarchivo.html.


### Linux

1. Instala apache2 con apt-get.
2. Ubica tu proyecto en algún lugar dentro de /var/www/.
3. Revísalo en http://localhost.

## Usando el servidor web incluido en PHP  (Quinta opción)

[PHP tiene (desde la versión 5.4.0) un servidor web incluido](https://secure.php.net/manual/en/features.commandline.webserver.php) para hacer pruebas, puede ser usado por p5.js.

Para revisar si tienes PHP instalado puedes abrir tu terminal y ejecutar el comando:

```
php -version
```

Si tienes instalado PHP CLI (Command Line Interpreter) puedes empezar un servidor local de desarrollo usando el comando:

```
php -S localhost:8000
```
Luego apunta tu navegador a `http://localhost:8000/`