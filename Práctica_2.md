# Gestión de Política de Contraseñas

## Introducción
Al usar contraseñas débiles la seguridad de nuestro sistema puede verse comprometida, haciendo uso de una buena política de contraseñas se pueden evitar muchos problemas.

El objetivo de la práctica es aprender a usar y configurar las políticas, usando el módulo pam, más concretamente pw_password.

* * *

## Desarrollo

1. Lo fundamental para empezar a trabajar es instalar lo siguiente.

```bash
    $ sudo apt install libpwquality-tools
```

2. Para empezar a asignar políticas debemos acceder al fichero **/etc/security/pwquality.conf**.

```bash
    $ sudo nano /etc/security/pwquality.conf
```

3. Para demostrar su correcto uso yo voy a usar la siguiente configuración, descomentando las líneas que me interesan y ajustandole a los parámetros que necesite.

```bash

