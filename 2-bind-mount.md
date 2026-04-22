# BIND MOUNT
En un bind mount mapeamos (montar) un directorio o archivo específico del sistema de archivos del host con una parte del sistema de ficheros del contenedor.

```
docker run -d --name <nombre contenedor> -v <ruta carpeta host>:<ruta carpeta contenedor> <imagen> 
```
ó
```
docker run -d --name <nombre contenedor> --mount type=bind,source=<ruta carpeta host>,target=<ruta carpeta contenedor> <imagen>
```
- destination, dst, target: La ruta donde se monta el archivo o directorio en el contenedor.
- source, src: El origen del montaje.
  
### En tu computador crear una carpeta llamada nginx y dentro de esta carpeta crea otra llamada html. Como se aprecia en la figura.
![Volúmenes](directorio.PNG)

<img width="469" height="126" alt="{8F9D45DD-D325-4714-B858-C332AE773407}" src="https://github.com/user-attachments/assets/ed0b1c23-0d7a-4a66-b2d6-147492954c8e" />

### Crear un contenedor con la imagen nginx:alpine, mapear todos por puertos, para la ruta carpeta host colocar el directorio en donde se encuentra la carpeta html en tu computador y para la ruta carpeta contenedor: /usr/share/nginx/html (esta ruta se obtiene al revisar la documentación de la imagen)
![Volúmenes](volumen-host.PNG)
# COMPLETAR CON EL COMANDO

<img width="1038" height="81" alt="{AE4E60B3-18F5-4B80-B028-B2C79CCDADB5}" src="https://github.com/user-attachments/assets/d8484cb0-639e-45c8-b31b-f479d99bbec1" />


### ¿Qué sucede al ingresar al servidor de nginx?
# COMPLETAR CON LA RESPUESTA A LA PREGUNTA

<img width="1912" height="935" alt="{ECD01E30-0DE9-4CC9-9F44-539711B6053D}" src="https://github.com/user-attachments/assets/72e327b5-d293-4b75-b67b-601e9e1108d3" />

No se visualiza ningun archivo debido a que no se ha creado un archivo html por lo que no hay información que leer.

### ¿Qué pasa con el archivo index.html del contenedor?
No existe, sin embargo, al crearlo se visualiza la información dentro del archivo

<img width="1920" height="978" alt="{076DBE35-BB57-45FF-A034-194ECC0C252A}" src="https://github.com/user-attachments/assets/8ab03ed3-e036-4e66-83c1-95a11c5cf389" />

# COMPLETAR CON LA RESPUESTA A LA PREGUNTA

### Ir a https://html5up.net/ y descargar un template gratuito, descomprirlo dentro de tu computador en la carpeta html

Descarga template

<img width="1910" height="930" alt="{FAFF83A8-0FE0-4F30-A4E4-7C9CCDCF41A1}" src="https://github.com/user-attachments/assets/cbaa73c7-7a6b-4ea6-a099-3cb1ac073c0e" />

### ¿Qué sucede al ingresar al servidor de nginx?

<img width="1914" height="985" alt="{71000382-1CA2-4363-B80B-6ABB3BE2AAEC}" src="https://github.com/user-attachments/assets/df205761-40a2-45c0-b399-b6b068fc944b" />

Al descomprimir el archivo se visualiza el template que se descargó, y al entrar al servidor se lo visualiza.

# COMPLETAR CON LA RESPUESTA A LA PREGUNTA

### Eliminar el contenedor
# COMPLETAR CON EL COMANDO

Se eliminó

<img width="500" height="61" alt="{6D561BC9-D7D8-47B0-AA26-7D0C7FE74E94}" src="https://github.com/user-attachments/assets/9e264600-f193-48f8-8bdd-a84496cef671" />

Se entró al servidor

<img width="1920" height="967" alt="{1E901203-CCD9-4BEA-B189-A5F6FECB72B8}" src="https://github.com/user-attachments/assets/b7c59154-cf55-4720-ac1e-e3f144feccf3" />

Se volvió a crear

<img width="1086" height="63" alt="{776389C5-672B-43C2-88E3-42E4BC699329}" src="https://github.com/user-attachments/assets/b23b79c6-1cce-4292-b6ed-3a076d5a9887" />

Se visualiza la información que se descomprimió en la carpeta

<img width="1883" height="970" alt="{E4C81367-6283-4368-AD48-ABD5F9C13142}" src="https://github.com/user-attachments/assets/965785c6-9700-4eaf-bdc0-e570f346f2eb" />


### ¿Qué sucede al crear nuevamente un contenedor montado al directorio definidos anteriormente?

Se conserva la información que estaba en ese directorio.

# COMPLETAR CON LA RESPUESTA A LA PREGUNTA


