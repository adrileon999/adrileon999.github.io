# Introducción

* * *
## Desarrollo

1. Instalar Easy-RSA
   
Primero actualizamos los repositorios e instalamos easy-rsa
  ```bash
      $ sudo apt update
      $ sudo apt install easy-rsa
  ```

2. Preparar un directorio para la infraestructura de la clave pública

   Creamos el siguiente directorio
   ```bash
       $ sudo mkdir ~/easy-rsa
   ```
   En este directorio crearemos los enlaces simbólicos hacia los archivos del paquete previamente instalado
   ```bash
       $ sudo ln -s /usr/share/easy-rsa/* ~/easy-rsa
   ```
   Modificaremos los permisos para que solo el propietario pueda acceder a esta carpeta en la que se alberga la PKI
   ```bash
       $ chmod 700 /home/adrian/easy-rsa
   ```
   Ahora iniciamos la PKI en el directorio
   ```bash
       $ cd ~/easy-rsa
       $ ./easyrsa init-pki
   ```
3. Crear una entidad de certificación

  Para crear la clave privada y el certificado debemos crear el siguiente archivo con algunos valores predeterminados en la carpeta anteriormente creada
  ```bash
      $ cd ~/easy-rsa
      $ nano vars
  ```
  Debemos añadir las siguientes lineas al fichero
  ```bash
  set_var EASYRSA_REQ_COUNTRY    "SPAIN"
  set_var EASYRSA_REQ_PROVINCE   "Cuenca"
  set_var EASYRSA_REQ_CITY       "Motilla del Palancar"
  set_var EASYRSA_REQ_ORG        "AdrianCA"
  set_var EASYRSA_REQ_EMAIL      "adleobla@alu.edu.gva.es"
  set_var EASYRSA_REQ_OU         "Community"
  set_var EASYRSA_ALGO           "ec"
  set_var EASYRSA_DIGEST         "sha512"
  ```
  Para crear el certificado root público y las claves privadas para la entidad certificadora hay que ejecutar lo siguiente
  ```bash
      $ ./easyrsa build-ca
  ```
  Acto seguido, rellenamos la información que nos pide y ya tendríamos los dos archivos importantes, ~/easy-rsa/pki/ca.crt y ~/easy-rsa/pki/private/ca.key, que conforman los componentes públicos y privados de una entidad de certificación.
4. Distribuir el certificado público de su entidad de certificación

  Sin ser root ejecutaremos el siguiente comando
  ```bash
      $ cat ~/easy-rsa/pki/ca.crt
  ```
   Esto nos va dar nuestro certificado, debemos exportarlo a la máquina cliente incluyendo las líneas de BEGIN CERTIFICATE y END CERTIFICATE

   En el cliente creamos el siguiente archivo y pegamos el contenido que acabamos de exportar.
   ```bash
      $ nano /tmp/ca.crt
   ```
   Ahora tenemos que importar el certificado y actualizar.
   ```bash
      $ sudo cp /tmp/ca.crt /usr/local
      $ sudo update-ca-certificates
   ```
   En el apartado de Firefox añadimos el certificado y ya habremos acabado con esta parte.
   ![tux](certificado.png)
   

      
