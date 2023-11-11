# Gestión de política de contraseñas

## Introducción
Al usar contraseñas débiles la seguridad de nuestro sistema puede verse comprometida, haciendo uso de una buena política de contraseñas se pueden evitar muchos problemas.

El objetivo de la práctica es aprender a usar y configurar las políticas, usando el módulo pam, más concretamente pw_password.

* * *

## Desarrollo

1. Lo fundamental para empezar a trabajar es instalar lo siguiente.

```bash
    $ sudo apt install libpwquality-tools
```

2. Para empezar a asignar políticas debemos acceder al fichero **/etc/security/pwquality.conf**. En este encontraremos varias líneas comentadas, explicándonos las distintas configuraciones y como usarlas.
```bash
    $ sudo nano /etc/security/pwquality.conf
```

3. Para demostrar su correcto uso yo voy a usar la siguiente configuración, descomentando las líneas que me interesan y ajustandole a los parámetros que necesite.

 ```bash
    minlen = 12
    minclass = 3
    maxrepeat = 2
    difok = 3
```
Con esto habremos configurado que la contraseña sea de mínimo 12 caracteres, que requiere de al menos 3 clases de caracteres diferentes, un carácter solo se puede usar 2 veces de forma consecutiva y al cambiar la contraseña debe haber 3 caracteres diferentes a la anterior.

## Comprobación

Su comprobación es fácil, simplemente usando el comando pwscore podremos probar diferentes contraseñas

```bash
    $ pwscore
        h0lAh0lAh0lA
        Falló la comprobación de calidad de la contraseña:
        La contraseña no supera la verificación de diccionario - No contiene suficientes caracteres DIFERENTES
    $ pwscore
        h0lAqU3T4l
        Falló la comprobación de calidad de la contraseña:
        La contraseña tiene menos de 12 caracteres.
    $ pwscore
        h0lAqU3T4l!!
        34
    $ pwscore
        38jd73n10dj38df11SDF12
        100
```
