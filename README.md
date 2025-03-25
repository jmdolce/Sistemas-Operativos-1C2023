# tp-2023-1c-PeladOS

## Vista General

### Descripción 📌

El objetivo del TP es la simulación de un sistema distribuido compuesto por diferentes módulos que interactúan entre sí, permitiendo la ejecución de procesos con planificación, administración de memoria y manejo de archivos.

### Arquitectura del sistema 🏗️

El sistema está compuesto por cinco módulos principales:

- Consola: Envia los procesos al sistema con sus instrucciones.
- Kernel: Administra la ejecución de procesos y la comunicación entre módulos.
- CPU: Ejecuta instrucciones de los procesos simulados.
- Memoria: Administra la memoria de los procesos con segmentación.
- File System: Simula un sistema de archivos basado en un esquema indexado.

### Tecnologías utilizadas ⚙️ 

Lenguaje de programación: C
Sistema operativo: Linux
Librerías: Sockets, pthreads, commons

### Principales funcionalidades implementadas 📊

- Planificación de procesos (FIFO y HRRN).
- Administración de memoria (segmentación con algoritmos de asignación First Fit, Best Fit y Worst Fit).
- Manejo de archivos (operaciones de apertura, lectura, escritura y truncado).
- Sincronización de procesos (manejo de recursos y bloqueos con WAIT/SIGNAL).
- Compactación de memoria para optimizar el uso del espacio.
- Logs detallados de cada operación realizada.


## Guia de deployment

### Distribución de máquinas

Se usarán 4 computadoras y los módulos se distribuirán de la siguiente forma:

- Computadora 1: Consola y CPU
- Computadora 2: Kernel
- Computadora 3: Memoria
- Computadora 4: File System

### Primeros pasos

1. En cada computadora vamos a conectar un PuTTY (en el caso de la Computadora 1 debemos duplicar la terminal del PuTTY después de clonar el repo). Recordar que para poder conectar un PuTTY desde Windows a la MV, tenemos que hacerlo a través del protocolo SSH y debemos conocer la IP de la computadora (hacer `ifconfig`).
2. Chequear que no tengamos ningun directorio y/o archivos en el sistema. En caso de tenerlos, borrarlos con los comandos `rm -r nombre_directorio` o `rm nombre_archivo`
3. Como un paso extra, podemos limpiar los puertos 8000 a 8004 con el comando `sudo fuser numero_puerto/TCP`
4. Hacemos git clone del repo en cada una de ellas
5. Ejecutamos el script `deploy.sh` que se encarga de instalar las commons y compilar el TP 

Importante tener a mano el token de GitHub en cada una de las computadoras, así como el link del repo. Estas dos cosas las tendremos en un notepad que enviaremos al mail de uno de los integrantes.

Podemos usar una página como Udrop (https://www.udrop.com/) para, una vez logueado en una de las máquinas, descargarnos el notepad y mandarlo por link a las otras computadoras, y asi evitamos tener que loguearnos en todas las computadoras para acceder al mail.


### Cambio de IPs

1. Se deben averiguar las IPs de cada computadora con el comando `ifconfig`
2. Debemos anotarnos en un notepad las IPs correspondientes a cada módulo
3. Ejecutamos el script para cambiar las IPs: `./set_ips.sh IP_CPU IP_MEMORIA IP_FILESYSTEM IP_KERNEL` (las IPs se pasan por parámetros en el orden indicado y separadas por un espacio)
4. Repetir el paso 3 por cada computadora donde hayamos clonado el repo

Hecho esto, tendremos todas las IPs cambiadas correctamente en todos los .config de todas las pruebas.

 ### Levantamiento de los módulos 

 Para levantar los módulos por cada prueba, se debe ejecutar el comando `./nombre_modulo "../tests/NOMBRE_PRUEBA/nombre_modulo.config"`

 En el caso particular de Consola, no es necesario ejecutar el comando, ya que tenemos scripts que ejecutan las instrucciones provistas por la cátedra. Entonces sólo debemos hacer `cd scripts` y luego ejecutar el script deseado con `./NOMBRE_PRUEBA.sh`

 **NOTA:** Recordar hacer `make` antes, ya que el comando mencionado no compila cada módulo automáticamente.

 **Correr con Valgrind:** Las pruebas no se corren con Valgrind en el laboratorio, pero si deseáramos chequear los leaks en cada prueba debemos ejecutar el comando `valgrind --tool=memcheck --leak-check=yes --show-possibly-lost=no --show-reachable=no --num-callers=20 ./nombre_modulo "../tests/NOMBRE_PRUEBA/nombre_modulo.config"`

 

 

  
