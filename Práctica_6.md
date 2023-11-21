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

Habilitamos el módulo ssl y activamos el sitio. Después reiniciamos.

  ```bash
      $ sudo a2enmod ssl
      $ sudo a2ensite default-ssl.conf
      $ sudo service apache2 restart
  ```
5. Habilitar la Seguridad de Transporte HTTP Estricta (HSTS) en Apache

   Habilitamos el módulo headers y reiniciamos el servicio
   
   ```bash
       $ sudo a2enmod headers
       $ sudo systemctl restart apache2
   ```
   Modificamos el archivo /etc/apache2/sites-available/mydomain.conf y añadimos lo siguiente
   ```bash
       <VirtualHost *:443>
        # .....
        # ....
        Header always set Strict-Transport-Security "max-age=31536000; includeSubDomains"
       </VirtualHost>
   ```

6. Habilitar HTTP/2 en Apache

   Habilitamos el módulo http2
   ```bash
        $ sudo a2enmod http2
   ```
   Abrimos el fichero  /etc/apache2/sites-enabled/your-domain-name-le-ssl.conf y añadimos la línea
   ```bash
       Protocols h2 http/1.1
   ```
   Por último reiniciamos.

7. Deshabilitar la directiva ServerSignature en Apache

   En el archivo de configuración de apache debemos buscar la opción ServerSignature y ponerla en Off
   ```bash
       ServerSignature Off
   ```

   Reiniciamos.

8. Asignar la directiva ServerTokens a Prod

   Igual que en el paso anterior, pero con la opción ServerTokens
   ```bash
       ServerTokens Off
   ```
9. Deshabilitar módulos innecesarios

   Podemos ver los módulos que tenemos habilitados con
   ```bash
       $ sudo apache2ctl -M
   ```
   
   Si queremos buscar un módulo especifico podemos usar
   ```bash
       $ apache2ctl -M | grep nombredelmodulo
   ```
   
   Deshabilitamos el módulo deseado
   ```bash
       $ sudo a2dismod rewrite
   ```
   
10. Limitar el tamaño de los archivos que se suben a Apache

    Debemos añadir las siguientes líneas en nuestro archivo de configuración. 4194304 es el equivalente a 4MB
    ```bash
        <Directory "nombre_directorio">
	          LimitRequestBody  4194304
        </Directory>
    ```

    Hay que reiniciar.

11. Arrancar Apache con un usuario y grupo separado

    Creamos el grupo y añadimos el usuario
    ```bash
        $ sudo groupadd apachegroup
        $ sudo useradd -g apachegroup apacheuser
    ```
    
    En el archivo de configuración de Apache añadimos las siguientes líneas
    ```bash
        User apacheuser
        Group apachegroup
    ```

    Cambiamos la propiedad de los directorios
    ```bash
        $ sudo chown -R apacheuser:apachegroup /var/www/html
    ```se utiliza para establecer un límite en el tamaño de los campos de encabezado de las solicitudes HTTP. Estos campos de encabezado incluyen información como cookies, información de autenticación, encabezados personalizados, etc.

    Reiniciamos Apache.

12. Protección ante ataque DDoS y Hardening

    Hay ciertas directivas en el archivo de configuración que nos ayudaran a hacerlo más seguro, como pueden ser:

    - **TimeOut.** Esta directiva controla el tiempo de espera tanto para la recepción de datos como para el envío de datos.
    - **MaxClients.** Este valor establece el límite en la cantidad de procesos hijos o subprocesos que Apache puede crear para atender las solicitudes de los clientes.
    - **KeepAliveTimeout.** Keep-Alive es un mecanismo que permite a la conexión entre el cliente y el servidor permanecer abierta después de que se haya completado una solicitud, permitiendo que varias solicitudes se realicen a través de la misma conexión.
    - **LimitRequestFields.** Esta directiva establece un límite en la cantidad de campos de encabezado de solicitud HTTP aceptados por los clientes.
    - **LimitRequestFieldSize.** Se utiliza para establecer un límite en el tamaño de los campos de encabezado de las solicitudes HTTP. Estos campos de encabezado incluyen información como cookies, información de autenticación, encabezados personalizados, etc.
    

   
  
