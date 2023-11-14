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
    ServerSignature Off
  
