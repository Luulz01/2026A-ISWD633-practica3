## Esquema para el ejercicio
![Imagen](esquema-ejercicio3.PNG)

### Crear red net-wp
# COMPLETAR CON EL COMANDO COMANDO
docker network create net-wp

<img width="672" height="67" alt="{98BC983E-1FBF-4A43-AD24-A4FF3EF1810E}" src="https://github.com/user-attachments/assets/41606049-3706-4b2c-a39c-b968e4a06fbf" />


### Para que persista la información es necesario conocer en dónde mysql almacena la información.
# COMPLETAR LA SIGUIENTE ORACIÓN. REVISAR LA DOCUMENTACIÓN DE LA IMAGEN EN https://hub.docker.com/
En el esquema del ejercicio carpeta del contenedor (a) es /var/lib/mysql

Ruta carpeta host: .../ejercicio3/db

### ¿Qué contiene la carpeta db del host?

Inicialmente no contiene nada, está vacía.

# COMPLETAR CON LA RESPUESTA A LA PREGUNTA

### Crear un contenedor con la imagen mysql:8  en la red net-wp, configurar las variables de entorno: MYSQL_ROOT_PASSWORD, MYSQL_DATABASE, MYSQL_USER y MYSQL_PASSWORD
# COMPLETAR CON EL COMANDO

docker run -d --name cont-mysql-wp --network net-wp -v C:\ejercicio3\db:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=1234 -e MYSQL_DATABASE=wordpress -e MYSQL_USER=lizeth -e MYSQL_PASSWORD=1234 mysql:8

<img width="956" height="76" alt="{143202BA-8A55-4826-8695-D2877040E297}" src="https://github.com/user-attachments/assets/8d4af89b-56db-4f32-b683-dcfa4de30cb2" />


### ¿Qué observa en la carpeta db que se encontraba inicialmente vacía?

Se crearon archivos y carpetas automáticamente, archivos de datos de MySQL.

# COMPLETAR CON LA RESPUESTA A LA PREGUNTA

<img width="1427" height="994" alt="{C33029C0-C72F-4BBC-8C50-5995878230FA}" src="https://github.com/user-attachments/assets/39714c80-7df3-4741-bb52-22d3b8650ac3" />


### Para que persista la información es necesario conocer en dónde wordpress almacena la información.
# COMPLETAR LA SIGUIENTE ORACIÓN. REVISAR LA DOCUMENTACIÓN DE LA IMAGEN EN https://hub.docker.com/
En el esquema del ejercicio la carpeta del contenedor (b) es /var/www/html

Ruta carpeta host: .../ejercicio3/www

### Crear un contenedor con la imagen wordpress en la red net-wp, configurar las variables de entorno WORDPRESS_DB_HOST, WORDPRESS_DB_USER, WORDPRESS_DB_PASSWORD y WORDPRESS_DB_NAME (los valores de estas variables corresponden a los del contenedor creado previamente)
# COMPLETAR CON EL COMANDO
docker run -d --name wordpress-wp --network net-wp -p 9500:80 -v C:\ejercicio3\www:/var/www/html -e WORDPRESS_DB_HOST=cont-mysql-wp:3306 -e WORDPRESS_DB_USER=lizeth -e WORDPRESS_DB_PASSWORD=1234 -e WORDPRESS_DB_NAME=wordpress wordpress

<img width="964" height="106" alt="{F8E2B895-D71A-44DC-A5E7-3A57743C9161}" src="https://github.com/user-attachments/assets/c4f0f4c6-14dd-47d7-ac91-e7264348cbe5" />


### Personalizar la apariencia de wordpress y agregar una entrada

<img width="1920" height="948" alt="{14EE5B25-5874-4E3D-85CD-6045761E9EF7}" src="https://github.com/user-attachments/assets/34c7dbf1-5bdb-4260-9108-d914856f4159" />

<img width="1920" height="939" alt="{9F067B2F-D639-4A72-B0F3-CDE94CA86712}" src="https://github.com/user-attachments/assets/03e89988-9f8f-44de-97e8-a57dd07095fe" />


### Eliminar el contenedor y crearlo nuevamente, ¿qué ha sucedido?

<img width="414" height="68" alt="{EE1E96A2-81AF-48AC-AB36-29991B7EB07B}" src="https://github.com/user-attachments/assets/8113caec-6045-4755-a742-6b91b593d5ac" />

<img width="966" height="113" alt="{13725F79-5CCF-42E4-8C12-C638CAA72116}" src="https://github.com/user-attachments/assets/7cf23b5c-4710-4d5f-b082-8435abe1ddd7" />

<img width="1895" height="999" alt="{269A6812-A47E-49E0-9845-DC46DA0DD47C}" src="https://github.com/user-attachments/assets/86e23d32-fa7c-4981-ba74-0af580e3451b" />


La carpeta db contiene archivos de base de datos y la carpeta www contiene archivos del sitio WordPress. Por lo que, al eliminar el contenedor no se pierde información porque está en el host

# COMPLETAR CON LA RESPUESTA A LA PREGUNTA 

