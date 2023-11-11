# Listas de Control de Acceso (ACL)

## Introducción
Las Listas de Control de Acceso (ACL) son conjuntos de reglas que controlan el acceso a recursos en una red o sistema. Se utilizan para permitir o denegar el tráfico de red, el acceso a archivos u otras acciones basándose en condiciones específicas, como direcciones IP, protocolos o puertos. Existen ACL de entrada y de salida, que regulan el tráfico que ingresa o sale de una red. Son esenciales para gestionar la seguridad y el rendimiento de las redes al limitar el acceso no autorizado y permitir un flujo controlado de datos.

* * *
## Desarrollo

Para empezar vamos a simular una estructura de carpetas:

```bash
COMPARTIDO_DE_GRUPOS
    ├── ESO1
    ├── ESO2
    ├── STUDENTS
    └── TEACHERS
```
También crearemos unos usuarios y unos grupos.

|Nombre del usuario|Grupos a los que pertenece|
|-|-|
|student1|students, eso1|
|student2|students, eso2|
|student3|students|
|teacher1|teachers|
|teacher2|teachers|

En este caso queremos que en las carpetas ESO1 y ESO2, los profesores puedan leer y escribir y que los alumnos tengan permisos de solo lectura. En la carpeta de STUDENTS, todos tendrán permisos de lectura y escritura y por último en la carpeta de TEACHERS, solo teacher1 tendrá permisos de lectura y escritura y los demás profesores solo lectura. Los alumnos no podrán acceder a la carpeta TEACHERS. Así pues, estos serían los pasos a seguir:

- En las carpeta ESO1 y ESO2, otorgamos permisos de lectura y escritura a teachers y de lectura al grupo eso1.
    ```bash
    $ sudo setfacl -Rdm g:eso1:r,g:teachers:rw /COMPARTIDA_DE_GRUPO/ESO1 /COMPARTIDA_DE_GRUPO/ESO2
    ```
- En la carpeta STUDENTS, tanto teachers como students tendrán permiso de lectura y escritura
    ```bash
    $ sudo setfacl -Rdm g:students:rw,g:teachers:rw /COMPARTIDA_DE_GRUPO/STUDENTS
    ```
- En la carpeta TEACHERS, teacher1 tiene permisos de lectura y escritura y los demás profesores solo lectura, m
    ```bash
    $ sudo setfacl -Rdm u:teacher1:rw,g:teachers:r,g:students:- /COMPARTIDA_DE_GRUPO/TEACHERS
***
## Comprobación

Vamos a realizar unas pruebas como por ejemplo:

```bash 
$ su student1
$ cd /CONTENIDO_DE_GRUPO/ESO1/
$ touch prueba1.txt
touch: no se puede efectuar `touch' sobre 'prueba1.txt': Permiso denegado

$ su teacher2
$ cd /CONTENIDO_DE_GRUPO/TEACHERS/
$ touch prueba2.txt
touch: no se puede efectuar `touch' sobre 'prueba2.txt': Permiso denegado
```
