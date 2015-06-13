# Conectarse con privilegios de super usuario #

Abrir una terminal de comandos, escribir ``` su ``` y escribir la contraseña con privilegios de super usuario.


# Configurar los repositorios de Debian Wheezy #

```
#!python

nano /etc/apt/sources.list
```

Poner en comentarios los que estén en el archivo y agregar los siguientes.

```
#!python

# Repositorios Basicos y oficiales estable 
deb http://ftp.fr.debian.org/debian/ wheezy main contrib non-free
deb-src http://ftp.fr.debian.org/debian/ wheezy main contrib non-free

# Repositorio  actualizaciones de seguridad estable
deb http://security.debian.org/ wheezy/updates main contrib non-free  
deb-src http://security.debian.org/ wheezy/updates main contrib non-free
```

###### Guardar (Ctrl + O), Aceptar (Enter) y Salir (Ctrl + X).

# Actualizar la base de datos de paquetes e instalar las actualizaciones más recientes (si los hay) #

```
#!python

aptitude update && aptitude upgrade
```

# Instalar Apache Server #

```
#!python

aptitude install apache2 apache2-mpm-prefork
```

Para probar que Apache Server está funcionando, en el navegador web poner la dirección IP de la computadora y apacerera una página en blanco con el texto It works!.

# Instalar PHP #

```
#!python

aptitude install php5 php5-mysql php5-gd libapache2-mod-php5
```

Para probar que PHP está funcionando, crear un script para obtener información de la instalación de PHP.

```
#!python

nano /var/www/info_php.php
```

Escribir lo siguiente.

```
#!python

<?php
	phpinfo();
?>
```

###### Guardar (Ctrl + O), Aceptar (Enter) y Salir (Ctrl + X).

En el navegador web poner la dirección IP de la computadora, agregar /info_php.php y apacerera una página con la información de la instalación de PHP.

# Instalar MySQL #

```
#!python

aptitude install mysql-server mysql-client
```

El instalador de MySql pedirá una contraseña para el usuario root de MySQL.

# Instalar phpMyAdmin #

```
#!python

aptitude install phpmyadmin
```

En la instalación de phpMyAdmin seleccionar Apache como servidor, en la siguiente opción seleccionar si, para configurar phpMyAdmin y el instalador pedirá la contraseña para el usuario administrativo de phpMyAdmin. 

Abrir el archivo de configuración de apache.

```
#!python

nano /etc/apache2/apache2.conf
```

Agregar al final del archivo la siguiente línea.

```
#!python

Include /etc/phpmyadmin/apache.conf
```

###### Guardar (Ctrl + O), Aceptar (Enter) y Salir (Ctrl + X).

Reiniciar los servicios de Apache.

```
#!python

/etc/init.d/apache2 restart
```

Para probar que phpMyAdmin está funcionando, en el navegador web poner la dirección IP de la computadora, agregar /phpmyadmin y apacerera la página de inicio de phpMyAdmin.
