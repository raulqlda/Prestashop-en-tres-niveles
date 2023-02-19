# Prestashop-en-tres-niveles
# Índice
# 1. Creacion del fichero Vagrantfile
# 2. Creacion de los scripts de aprovisionamiento
# 3. Configuración de la maquina Mysql
# 4. Configuración de la maquina NFS
# 5. Configuración de la maquinas Nginx
# 6. Configuración de la maquina Balanceador
# 7. Comprobacion




## 1. Creacion del fichero Vagrantfile
Creo 5 maquinas (un balanceador, dos nginx, un nfs y una mysql) mediante el fichero Vagrantfile

![](imagenes\vagrantfile.png)

## 2. Creacion de los scripts de aprovisionamiento
Creo los ficheros de aprovisionamiento para las diferentes maquinas

### 2.1 Fichero scriptbalanceador.sh

![](imagenes\scriptbalanceador.png)

### 2.2 Fichero scriptmysql.sh

![](imagenes\scriptmysql.png)

### 2.3 Fichero scriptnfs.sh

![](imagenes\scriptnfs.png)

### 2.4 Fichero scriptnginx.sh

![](imagenes\scriptnginx.png)

## 3. Configuración de la maquina Mysql

### 3.1 Configuracion del fichero 50-server.cnf
Lo primero que hago es modificar el fichero 50-server.cnf que se encuentra en la ruta /etc/mysql/mariadb.conf.d y cambiar el bind-address por la ip de la maquina mysql.

![](imagenes\50-server.cnf.png)

### 3.2 Ejecutar mysql_secure_installation
Lo siguiente es ejecutar el mysql_secure_installation para poder cambiar la contraseña del usuario root para poder entrar.

![](imagenes\mysql_secure_installation.png)

### 3.3 Creacion del usuario y de la base de datos
Despues de cambiar la contraseña de root se crea el usuario y la base de datos para prestashop

![](imagenes\database_prestashop.png)

A continuacion le damos todos los permisos en la base de datos creada al usuario creado 

![](imagenes\database_permisos.png)

## 4. Configuración de la maquina NFS

### 4.1 Descargar el wget y el prestashop.
Descargamos si no lo tenemos el wget y con eso descargamos el prestashop

![](imagenes\descaraga_prestashop.png)

### 4.2 Descomprimir el archivo de prestashop
Descargamos el unzip si no lo tenemos y descomprimimos el archivo descargado anteriormente

![](imagenes\unzip.png)
![](imagenes\ls_prestashop.png)

### 4.3 Creacion de la carpeta a compartir.
Creamos una carpeta en la ruta /var/www que sera la que compartamos con las maquinas de nginx

![](imagenes\carpetanfs.png)

### 4.4 Copiar el prestashop en la nueva carpeta creada
Copiamos el contenido de la carpeta prestashop a la carpeta nfs creada anteriormente

![](imagenes\copiaprestashop.png)

### 4.5 Configuracion del fichero exports.
Modificamos el fichero exports que se encuentra en etc colocandoles las ips de las dos maquinas de nginx

![](imagenes\exports.png)

### 4.5 Configuracion del fichero wp-config.php
Creamos una copia del fichero wp-config-sample.php y lo llamamos wp-config.php

![](imagenes\config.php1.png)

Luego modificamos el fichero creado colocando el usuario y la base de datos creada previamente y la ip de nuestra maquina mysql

![](imagenes\config.php2.png)

### 4.6 Configuracion del fichero www.conf
Configuramos el fichero www.conf que se encuentra en la ruta /etc/php/7.4/fpm/pool.d y modificamos la línea "listen" y le añadimos la direccion 0.0.0.0 y el puerto 9000

![](imagenes\fichero_www.conf.png)

## 5. Configuración de la maquinas Nginx

### 5.1 Creacion de la carpeta compartida y montaje de la misma.
Creamos la carpeta nfs en la ruta /var/www/

![](imagenes\carpetanginx.png)

Montamos la carpeta

![](imagenes\montarnginx.png)

### 5.2 Configuracion del fichero default que se encuentra en la ruta /etc/nginx/sites-enabled 
En este fichero pondremos la ruta de nuestra carpeta nfs de /var/www y bajaremos y agregaremos index.php al lado de index.html. Seguiremos bajando y habrá unas líneas que empiezan por location y estarán comentadas, las descomentaremos, pero en la que pone \.php dejaremos comentada la de unix ya que es un socket que no necesitamos. En la otra línea de fatscgi_pass pondremos la IP de nuestro servidor NFS y el puerto 9000.

![](imagenes\fichero_default.png)

## 6. Configuración de la maquina Balanceador

### 6.1 Creacion de claves certificadoras
Esta claves son necesaria para poder activar ssl en nginx para hacerlo hay que poner el siguiente comando:
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/servernginx.com.key -out /etc/ssl/certs/servernginx.com.pem

![](imagenes\balanceador.png)

### 6.2 Creacion del fichero de configuracion
Lo primero es ir a /etc/nginx/sites-available y crear un nuevo fichero

![](imagenes\confbalanceador1.png)

En el fichero escribir lo siguiente

![](imagenes\confbalanceador2.png)

Lo siguiente sera crear un enlace hacia sites-enabled y borraremos el default.

![](imagenes\confbalanceador3.png)

## 7. Comprobación

ip de la maquina balanceador

![](imagenes\comprobacion.png)

comprobación

![](imagenes\comprobacion2.png)
