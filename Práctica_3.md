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

|Usuarios|Grupos|
|-|-|
|Student1|students, eso1|
|Student2|students, eso2|
|Student3|students|
|Teacher1|teachers|
|Teacher2|teachers, eso2|

