# Introducción

* * *
## Desarrollo

1. Como ocultar la versión e información de Apache

  Introducimos el siguiente comando
   ```bash
       $sudo vim /etc/apache2/apache2.conf
   ```
  Y añadimos las siguientes líneas al fichero
  > ServerTokens Prod

  > ServerSignature Off

  Guardamos el fichero y reiniciamos Apache
  ```bash
      $ sudo systemctl restart apache2
  ```
2. Deshabilitar el listado de directorios en Apache

  Para hacer la prueba creamos el directorio /var/www/html/test y creamos varios archivos
  ```bash
    $ sudo mkdir /var/www/html/test
    $ cd /var/www/html/test
    $ sudo touch app.py main.py
  ```
  Ahora si accedemos a http://localhost/apache nos aparecerá un listado del directorio test. Para desactivar esto vamos al archivo de configuración de Apache y añadimos las siguientes líneas
  
    <Directory /var/www/html/test>
      Options -Indexes
    </Directory>

3. Actualización regular de Apache

   Simplemente hacemos un apt update y apt upgrade

   ```bash
       $ sudo apt update
       $ sudo apt upgrade
   ```
4. Usar la encriptación HTTPS en Apache

5. Habilitar la Seguridad de Transporte HTTP Estricta (HSTS) en Apache

   Habilitamos el módulo headers y reiniciamos el servicio
   ```bash
       $ sudo a2enmod headers
       $ sudo systemctl restart apache2
  
