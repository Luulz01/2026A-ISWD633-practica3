# MI APRENDIZAJE
En esta tercera práctica se siguió viendo acerca de Docker mediante la implementación de volúmenes nombrados, persistencia de datos y la integración de múltiples servicios más complejos como PostgreSQL, pgAdmin y Drupal. Comprendí cómo Docker gestiona internamente el almacenamiento sin necesidad de rutas explícitas del sistema host, y la importancia de los volúmenes para mantener la información incluso después de eliminar contenedores.

Además, reforcé la comunicación entre contenedores dentro de una red y entendí mejor cómo funcionan los servicios cliente-servidor dentro de Docker. También identifiqué que una mala configuración en rutas, volúmenes o variables puede afectar directamente la instalación y funcionamiento de aplicaciones.

Comprendí que los volúmenes nombrados son fundamentales para garantizar la persistencia de la información, ya que permiten almacenar datos fuera del ciclo de vida del contenedor. Esto significa que, aunque un contenedor sea eliminado o recreado, la información no se pierde. Este concepto es clave en entornos productivos donde la integridad de los datos es crítica. Además, aprendí el concepto de mountpoint, entendiendo que Docker gestiona internamente una ubicación específica en el sistema donde almacena los datos de los volúmenes. Esto me permitió comprender mejor cómo Docker abstrae el manejo del almacenamiento, facilitando el trabajo sin necesidad de depender directamente de rutas del sistema operativo.

### Conocimientos previos
- Creación y ejecución de contenedores con Docker.
- Uso de imágenes y comandos básicos como docker run, docker ps y docker rm.
- Uso de redes para comunicación entre contenedores.
- Configuración de variables de entorno en contenedores.

### Conocimientos adquiridos después de la práctica
- Uso de volúmenes nombrados (named volumes) para persistencia de datos sin depender de rutas del sistema.
- Comprensión del concepto de mountpoint.
- Implementación de bases de datos con PostgreSQL dentro de contenedores.
- Integración de múltiples servicios (PostgreSQL + Drupal).
- Configuración de contenedores con múltiples volúmenes simultáneamente.
- Comprensión de que los datos no se almacenan en el contenedor sino en los volúmenes.

### Comandos

- **docker volume create `<nombre_volumen>`:**  
  Permite crear un volumen nombrado gestionado por Docker.

- **docker volume ls:**  
  Lista todos los volúmenes disponibles en el sistema.

- **docker volume rm `<nombre_volumen>`:**  
  Elimina un volumen específico, debe no estar en uso.

- **docker network create `<nombre_red>`:**  
  Crea una red para permitir la comunicación entre contenedores.

- **docker run -d --name `<nombre>` -v `<volumen>:<ruta_contenedor>` `<imagen>`:**  
  Crea un contenedor en segundo plano vinculando un volumen nombrado a una ruta del contenedor.

- **docker run -d --name `<nombre>` --mount type=volume,src=`<volumen>`,dst=`<ruta>` `<imagen>`:**  
  Crea un contenedor utilizando la sintaxis avanzada de montaje de volúmenes.

### Cosas que realicé y aprendí
- Creé volúmenes nombrados para almacenar datos de PostgreSQL.
- Comprendí cómo Docker guarda los datos en rutas internas como: /var/lib/docker/volumes/<nombre>/_data
- Logré conectar pgAdmin con PostgreSQL usando el nombre del contenedor como host.
- Implementé Drupal con múltiples volúmenes para persistir configuraciones, módulos y archivos.
- Observé que al eliminar contenedores, la información permanece gracias a los volúmenes.

### ¿Qué ventaja tienen los volúmenes nombrados frente a los bind mounts?
Los volúmenes nombrados son gestionados directamente por Docker, lo que permite mayor portabilidad, seguridad y facilidad de uso, ya que no dependen de rutas específicas del sistema operativo. Además, reducen errores de configuración y son ideales para entornos productivos.

### Conclusión
En esta práctica aprendí a gestionar datos persistentes mediante volúmenes nombrados, a comprender cómo Docker maneja internamente el almacenamiento y a integrar servicios más complejos como PostgreSQL, pgAdmin y Drupal. 
