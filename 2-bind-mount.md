# BIND MOUNT
En un bind mount mapeamos (montar) un directorio o archivo específico del sistema de archivos del host con una parte del sistema de ficheros del contenedor.

```
docker run -d --name <nombre contenedor> -v <ruta carpeta host>:<ruta carpeta contenedor> <imagen> 
```
ó
```
docker run -d --name <nombre contenedor> --mount type=bind,source=<ruta carpeta host>,target=<ruta carpeta contenedor> <imagen>
```
- destination, dst, target: La ruta donde se monta el archivo o directorio en el contenedor.
- source, src: El origen del montaje.
  
### En tu computador crear una carpeta llamada nginx y dentro de esta carpeta crea otra llamada html. Como se aprecia en la figura.
![Volúmenes](directorio.PNG)

### Crear un contenedor con la imagen nginx:alpine, mapear todos por puertos, para la ruta carpeta host colocar el directorio en donde se encuentra la carpeta html en tu computador y para la ruta carpeta contenedor: /usr/share/nginx/html (esta ruta se obtiene al revisar la documentación de la imagen)
![Volúmenes](volumen-host.PNG)
# COMPLETAR CON EL COMANDO
docker run -d --name srv-nginx-alpine -p 8080:80 -v C:\nginx\html:/usr/share/nginx/html nginx:alpine
### ¿Qué sucede al ingresar al servidor de nginx?
# COMPLETAR CON LA RESPUESTA A LA PREGUNTA
Aparece el siguiente mensaje: " 403 Forbidden nginx/1.31.6 ", esto debido a que el bind mount reemplaza la vista del directorio /usr/share/nginx/html del contenedor por el contenido de la carpeta del host. Siendo así que Nginx ya no encuentra su pagina predeterminada.
### ¿Qué pasa con el archivo index.html del contenedor?
# COMPLETAR CON LA RESPUESTA A LA PREGUNTA
El archivo index.html original del contenedor queda oculto debido a que el bind mount que está activo, ya que la carpeta del equipo anfitrión se monta sobre /usr/share/nginx/html. Siendo así que el archivo no se elimina, pero deja de ser visible.
### Ir a https://html5up.net/ y descargar un template gratuito, descomprirlo dentro de tu computador en la carpeta html
### ¿Qué sucede al ingresar al servidor de nginx?
# COMPLETAR CON LA RESPUESTA A LA PREGUNTA
Aparece cargado el template descargado, con el mensaje:" Hi, I'm Photon, another fine little freebie from HTML5 UP. ".
### Eliminar el contenedor
# COMPLETAR CON EL COMANDO
docker rm -f srv-nginx-alpine
### ¿Qué sucede al crear nuevamente un contenedor montado al directorio definidos anteriormente?
# COMPLETAR CON LA RESPUESTA A LA PREGUNTA
Al crear otra ves el contenedor, la página web del template descargado vuelve a mostrarse al ingresar al servidor Nginx. Esto es debido a que los archivos del template permanecen almacenados en la carpeta C:\nginx\html del host y no se pierden cuando se eliminó prerviamente el contenedor anterior.

