## Esquema para el ejercicio
![Imagen](esquema-ejercicio3.PNG)

### Crear red net-wp
docker network create net-wp

### Para que persista la información es necesario conocer en dónde mysql almacena la información.
En el esquema del ejercicio carpeta del contenedor (a) es (/var/lib/mysql)
Ruta carpeta host: .../ejercicio3/db

### ¿Qué contiene la carpeta db del host?
De momento no contiene un elemento, revisando la documentación la carpeta db del host va a llegar a almacenar los archivos de datos de MySQL, que contienen la información persistente de las bases de datos y sus tablas, esto se concluye ya que son generados y administrados por MySQL dentro de la ruta /var/lib/mysql del contenedor.

### Crear un contenedor con la imagen mysql:8  en la red net-wp, configurar las variables de entorno: MYSQL_ROOT_PASSWORD, MYSQL_DATABASE, MYSQL_USER y MYSQL_PASSWORD
docker run -d --name srv-mysql --network net-wp -v C:\Desktop\ejercicio3\db:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123 -e MYSQL_DATABASE=wordpress -e MYSQL_USER=wuser -e MYSQL_PASSWORD=wp456 mysql:8

### ¿Qué observa en la carpeta db que se encontraba inicialmente vacía?
La carpeta db, que anteriormente estaba vacía, ahora contiene archivos y directorios generados por MySQL durante su inicialización y funcionamiento, donde se puede evidenciar  carpetas como mysql, performance_schema y wordpress, además de archivos como ibdata1, mysql.ibd y los archivos binlog.

### Para que persista la información es necesario conocer en dónde wordpress almacena la información.
# COMPLETAR LA SIGUIENTE ORACIÓN. REVISAR LA DOCUMENTACIÓN DE LA IMAGEN EN https://hub.docker.com/
En el esquema del ejercicio la carpeta del contenedor (b) es (/var/www/html)
Ruta carpeta host: .../ejercicio3/www

### Crear un contenedor con la imagen wordpress en la red net-wp, configurar las variables de entorno WORDPRESS_DB_HOST, WORDPRESS_DB_USER, WORDPRESS_DB_PASSWORD y WORDPRESS_DB_NAME (los valores de estas variables corresponden a los del contenedor creado previamente)
docker run -d --name srv-wordpress --network net-wp -p 9500:80 -v C:\Desktop\ejercicio3\www:/var/www/html -e WORDPRESS_DB_HOST=srv-mysql -e WORDPRESS_DB_USER=wuser -e WORDPRESS_DB_PASSWORD=wp456 -e WORDPRESS_DB_NAME=wordpress wordpress

### Personalizar la apariencia de wordpress y agregar una entrada


### Eliminar el contenedor y crearlo nuevamente, ¿qué ha sucedido?
Al eliminar el contenedor WordPress y crearlo nuevamente con el mismo bind mount, los archivos del sitio que se encuentran en la carpeta www del host se conservan. Además la entrada publicada se conserva porque su contenido se almacena en la base de datos MySQL.
