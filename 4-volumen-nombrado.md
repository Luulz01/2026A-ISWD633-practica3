## VOLUMEN NOMBRADO
Un volumen nombrado (named volume) es un tipo de volumen gestionado por Docker que se almacena en una ubicación específica del sistema de archivos del host y se identifica mediante un nombre único. Los volúmenes nombrados no requieren que especifiques una ruta del sistema de archivos del host, y en su lugar, Docker se encarga de la gestión y el almacenamiento del volumen.


### Crear volumen
```
docker volume create <nombre volumen>
```

### Crear el volumen nombrado: vol-postgres
# COMPLETAR CON EL COMANDO

docker volume create vol-postgres

<img width="527" height="57" alt="{F611302C-D5D7-4405-B325-C4718297325B}" src="https://github.com/user-attachments/assets/39702c51-85fe-4364-8b57-e758de3535b2" />


## MOUNTPOINT
Un mountpoint se refiere al lugar en el sistema de archivos donde un dispositivo de almacenamiento se une (o monta) al sistema de archivos. Es el punto donde los archivos y directorios almacenados en ese dispositivo de almacenamiento son accesibles para el sistema operativo y las aplicaciones.

Por ejemplo, en Windows las unidades de almacenamiento (como `C:`, `D:`, etc.) actúan como puntos de montaje principales para discos duros, unidades flash, unidades ópticas y otros dispositivos de almacenamiento.

Cuando creas un volumen nombrado, Docker asigna un punto de montaje específico en el sistema de archivos del host para ese volumen.

### Estructura del Punto de Montaje:
- /var/lib/docker/volumes/: Es la ubicación base donde Docker almacena todos los volúmenes en el sistema de archivos del host.
- nombreVolumen/: Es el nombre del volumen nombrado que has creado. Docker crea un directorio con este nombre dentro de /var/lib/docker/volumes/ para almacenar los datos del volumen.
- _data: Es el subdirectorio dentro de vol-postgres/ donde se almacenan los datos reales del volumen. El nombre _data es una convención utilizada por Docker para indicar el directorio donde se encuentran los datos del volumen.

### ¿Cómo acceder a ese Mountpoint?
En el contexto de WSL (Windows Subsystem for Linux), wsl$ se refiere al nombre de un recurso compartido de red especial que representa la raíz del sistema de archivos de Windows desde WSL. Cuando accedes a \\wsl$ desde el Explorador de archivos de Windows, puedes ver y acceder a los archivos del sistema de archivos de la distribución de Linux en WSL.
\\wsl.localhost\docker-desktop-data\data\docker\volumes

### Crear un contenedor vinculado a un volumen nombrado
```
docker run -d --name <nombre contenedor> -v <nombre volumen>:<ruta contenedor> <nombre imagen>
```
ó
```
docker run -d --name <nombre contenedor> --mount type=volume,src=<nombre >,dst=<mount-path>
```
- destination, dst, target: La ruta donde se monta el archivo o directorio en el contenedor.
- source, src: El origen del montaje. Para volúmenes con nombre, este es el nombre del volumen. Para volúmenes anónimos, este campo se omite.


### Crear la red net-drupal de tipo bridge
# COMPLETAR CON EL COMANDO
docker network create net-drupal

<img width="697" height="72" alt="{33F37F0E-8E54-48E3-B81B-436A750F551E}" src="https://github.com/user-attachments/assets/51d835f7-2638-43b8-bec5-af32d530a871" />


### Crear un servidor postgres vinculado a la red net-drupal, completar la ruta del contenedor
```
docker run -d --name server-postgres -e POSTGRES_DB=db_drupal -e POSTGRES_PASSWORD=12345 -e POSTGRES_USER=user_drupal --network net-drupal postgres
```
_No es necesario exponer el puerto, debido a que nos vamos a conectar desde la misma red de docker_


docker run -d --name server-postgres -e POSTGRES_DB=db_drupal -e POSTGRES_PASSWORD=12345 -e POSTGRES_USER=user_drupal -v vol-postgres:/var/lib/postgresql/data --network net-drupal postgres:14

<img width="991" height="491" alt="{0A5FC1B9-B1CA-4C3E-A3DE-BE2E259B1EDE}" src="https://github.com/user-attachments/assets/0d51eb19-c6ea-4e0c-90ee-bdb329bd7d32" />


### Crear un cliente postgres vinculado a la red drupal a partir de la imagen dpage/pgadmin4, completar el correo
```
docker run -d --name client-postgres --publish published=9500,target=80 -e PGADMIN_DEFAULT_PASSWORD=54321 -e PGADMIN_DEFAULT_EMAIL=<correo> --network net-drupal dpage/pgadmin4
```

docker run -d --name client-postgres --publish published=9500,target=80 -e PGADMIN_DEFAULT_PASSWORD=54321 -e PGADMIN_DEFAULT_EMAIL=hernandez.mayeli2004@gmail.com --network net-drupal dpage/pgadmin4

<img width="981" height="81" alt="{00A3B747-EF52-43B8-8772-087E8B3CA234}" src="https://github.com/user-attachments/assets/c5b99d96-c441-4d47-b605-591e35e10da2" />


### Usar el cliente postgres para conectarse al servidor postgres, para la conexión usar el nombre del servidor en lugar de la dirección IP.

<img width="1920" height="957" alt="{A9792A1A-DA8D-4221-B637-76B06948EDF2}" src="https://github.com/user-attachments/assets/a37fad2d-b0c4-4e66-b66e-de0a6d46d1b0" />

<img width="1920" height="946" alt="{82D129C8-0856-4F5E-9439-587C2DD1A6FD}" src="https://github.com/user-attachments/assets/cb8f0fa8-77ae-4d7d-8aff-5b9475f4beb0" />

<img width="1879" height="883" alt="{426426CA-4A1A-4979-B477-5C19AD23B09F}" src="https://github.com/user-attachments/assets/be5f299d-2096-4fe2-9654-ef043d1454ec" />


### Crear los volúmenes necesarios para drupal, esto se puede encontrar en la documentación
### COMPLETAR CON LOS COMANDOS

<img width="669" height="244" alt="{2372FF32-CA95-4CF4-ADDF-2AD63EADD7E4}" src="https://github.com/user-attachments/assets/cb2f217a-6515-4935-adc5-b00108cab098" />


### Crear el contenedor server-drupal vinculado a la red, usar la imagen drupal, y vincularlo a los volúmenes nombrados
```
docker run -d --name server-drupal --publish published=9700,target=80 -v <nombre volumen>:<ruta contenedor> -v <nombre volumen>:<ruta contenedor> -v <nombre volumen>:<ruta contenedor> -v <nombre volumen>:<ruta contenedor> --network net-drupal drupal
```

<img width="982" height="618" alt="{906870AF-CA28-4B9C-9F40-7355FBDD2233}" src="https://github.com/user-attachments/assets/367a4320-6191-46de-996a-ca2458f5abfc" />


### Ingrese al server-drupal y siga el paso a paso para la instalación.
# COMPLETAR CON UNA CAPTURA DE PANTALLA DEL PASO 4

<img width="1907" height="972" alt="{68A87320-373A-4A0C-BBC5-1E27D4039F89}" src="https://github.com/user-attachments/assets/f89bd95f-24a8-4564-b7a4-bb5c86d325ef" />


<img width="1656" height="858" alt="{BF29FD87-3CAA-4134-8531-D771827C7FE2}" src="https://github.com/user-attachments/assets/a302a1c0-6ab8-408a-b60f-a62cd95a84e9" />


_La instalación puede tomar varios minutos, mientras espera realice un diagrama de los contenedores que ha creado en este apartado._

# COMPLETAR CON EL DIAGRAMA SOLICITADO

### Eliminar un volumen específico
```
docker volume rm <nombre volumen>
```
**Considerar**
Datos Persistentes: Asegúrate de que el volumen no contiene datos críticos antes de eliminarlo, ya que esta operación no se puede deshacer.
Contenedores Activos: No puedes eliminar un volumen que está actualmente en uso por un contenedor activo. Debes detener y/o eliminar el contenedor primero.
