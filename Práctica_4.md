# Introducción
RAID (Redundant Array of Independent Disks) es una técnica que utiliza múltiples discos para mejorar la confiabilidad y/o el rendimiento del almacenamiento. Hay varios niveles de RAID, algunos ofrecen redundancia, mientras que otros se centran en el rendimiento. Se utiliza comúnmente para proteger datos y mantener la operatividad ante fallos de disco.

* * *
## Desarrollo
Para este caso usaremos una RAID 10, también conocido como RAID 1+0, la cual es una configuración que combina las características de RAID 1 y RAID 0. En RAID 10, los datos se espejean (duplican) en pares de discos (como en RAID 1), y luego estos pares se organizan en un conjunto RAID 0 para mejorar el rendimiento. Esto proporciona tanto redundancia como beneficios de rendimiento, asegurando la integridad de los datos incluso si uno de los discos falla. Sin embargo, debido a la duplicación de datos, la capacidad de almacenamiento efectiva es la mitad de la capacidad total de los discos involucrados. RAID 10 es ampliamente utilizado en entornos empresariales donde se busca un equilibrio entre rendimiento y seguridad de datos.

