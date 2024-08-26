#### 1- Instalar Docker Community Edition 
  - Diferentes opciones para cada sistema operativo
  - https://docs.docker.com/
  - Ejecutar el siguiente comando para comprobar versiones de cliente y demonio.
```bash
docker version
```
![1](https://github.com/user-attachments/assets/35545229-e6e7-476e-a570-c65d438d4f04)


#### 2- Explorar DockerHub
   hecho
#### 3- Obtener la imagen BusyBox

  ```bash
  docker pull busybox
  ```
```bash
docker images
```

![2](https://github.com/user-attachments/assets/5668e26d-482a-447c-a84b-ab02091d49f3)


#### 4- Ejecutando contenedores

  - Especificamos algún comando a correr dentro del contenedor, ejecutar por ejemplo:
```bash
docker run busybox echo "Hola Mundo"
```
![3](https://github.com/user-attachments/assets/ae30e795-b6d3-492d-b5aa-5b89e6156932)
  - Ver los contenedores ejecutados utilizando el comando **ps**:
```bash
docker ps
```
  - Vemos que no existe nada en ejecución, correr entonces:
```bash
docker ps -a
```
  - Mostrar el resultado y explicar que se obtuvo como salida del comando anterior.

![4](https://github.com/user-attachments/assets/5f601031-007d-4c68-9e28-e8dea18733a1)

#### 5- Ejecutando en modo interactivo


  - Ejecutar el siguiente comando
```bash
docker run -it busybox sh
```
  - Para cada uno de los siguientes comandos dentro de contenedor, mostrar los resultados:
```bash
ps
uptime
free
ls -l /
```
  ![5](https://github.com/user-attachments/assets/47310278-243e-413e-8689-78f192e87fa6)


  - Salimos del contenedor con:
```bash
exit
```

#### 6- Borrando contenedores terminados

  - Obtener la lista de contenedores 
```bash
docker ps -a
```
![6](https://github.com/user-attachments/assets/43e9ca6b-ca93-4fd4-9192-000df4c53ef3)

  - Para borrar podemos utilizar el id o el nombre (autogenerado si no se especifica) de contenedor que se desee, por ejemplo:
```bash
docker rm elated_lalande
```
  - Para borrar todos los contenedores que no estén corriendo, ejecutar cualquiera de los siguientes comandos:
```bash
docker rm $(docker ps -a -q -f status=exited)
```
```bash
docker container prune
```

#### 7- Construir una imagen
- Conceptos de DockerFile
  - Leer https://docs.docker.com/engine/reference/builder/ 
  - Describir las instrucciones
     - FROM = Create a new build stage from a base image.
     - RUN = Execute build commands.
     - ADD = Add local or remote files and directories.
     - COPY = Copy files and directories.
     - EXPOSE = Describe which ports your application is listening on.
     - CMD = Specify default commands.
     - ENTRYPOINT =	Specify default executable.
- A partir del código https://github.com/ingsoft3ucc/SimpleWebAPI crearemos una imagen.
- Clonar repo
- Crear imagen etiquetándola con un nombre. El punto final le indica a Docker que use el dir actual
```
docker build -t mywebapi .
```
- Revisar Dockerfile y explicar cada línea
FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base //imagen base que se lee
WORKDIR /app  //directorio en el que se trabaja
EXPOSE 80 // selecciona los puertos que se van a usar
EXPOSE 443
EXPOSE 5254

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build  //imagen base que se lee
WORKDIR /src //directorio en el que se trabaja
COPY ["SimpleWebAPI/SimpleWebAPI.csproj", "SimpleWebAPI/"]  //copia la carpeta al contenedor docker
RUN dotnet restore "SimpleWebAPI/SimpleWebAPI.csproj" // restaura las dependencias para correr el proyecto
COPY . . //copia todo lo que esta en el directorio en el host
WORKDIR "/src/SimpleWebAPI" //directorio en el que se trabaja
RUN dotnet build "SimpleWebAPI.csproj" -c Release -o /app/build //compila la aplicacion

FROM build AS publish
RUN dotnet publish "SimpleWebAPI.csproj" -c Release -o /app/publish /p:UseAppHost=false //imagen base que se lee

FROM base AS final
WORKDIR /app //directorio en el que se trabaja
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SimpleWebAPI.dll"]
#CMD ["/bin/bash"]



  
- Ver imágenes disponibles
  ![image](https://github.com/user-attachments/assets/9e1c30d6-271d-493e-b0b2-043781f0bafd)

- Ejecutar un contenedor con nuestra imagen
  ![image](https://github.com/user-attachments/assets/3f56e621-5fb6-421b-bbfd-7cd65459004e)

- Subir imagen a nuestra cuenta de dockerhub
  - 7.1 Inicia sesión en Docker Hub
    - Primero, asegúrate de estar autenticado en Docker Hub desde tu terminal:
    ```bash
    docker login
    ```
    ![image](https://github.com/user-attachments/assets/4c8f2a6c-e981-4869-b9ac-275e55281142)

  - 7.2 Etiquetar la imagen a subir con tu nombre de usuario de Docker Hub y el nombre de la imagen. Por ejemplo:
    ```bash
    docker tag <nombre_imagen_local> <tu_usuario_dockerhub>/<nombre_imagen>:<tag>
    ```

  - 7.3 Subir la Imagen
    - Para subir la imagen etiquetada a Docker Hub, utiliza el comando docker push:
     ```bash
     docker push <tu_usuario_dockerhub>/<nombre_imagen>:<tag>
     ```
  - 7.4 Verificar la Subida
     ```bash
     docker pull <tu_usuario_dockerhub>/<nombre_imagen>:<tag>
     ```
![image](https://github.com/user-attachments/assets/159cc16a-5ce5-47ff-8fe8-d108660b281c)

#### 8- Publicando puertos

En el caso de aplicaciones web o base de datos donde se interactúa con estas aplicaciones a través de un puerto al cual hay que acceder, estos puertos están visibles solo dentro del contenedor. Si queremos acceder desde el exterior deberemos exponerlos.

  - Ejecutar la siguiente imagen, en este caso utilizamos la bandera -d (detach) para que nos devuelva el control de la consola:

```bash
docker run --name myapi -d mywebapi
```
  - Ejecutamos un comando ps:
  - Vemos que el contendor expone 3 puertos el 80, el 5254 y el 443, pero si intentamos en un navegador acceder a http://localhost/WeatherForecast no sucede nada.

  - Procedemos entonces a parar y remover este contenedor:
```bash
docker kill myapi
docker rm myapi
```
  - Vamos a volver a correrlo otra vez, pero publicando el puerto 80

```bash
docker run --name myapi -d -p 80:80 mywebapi
```
![image](https://github.com/user-attachments/assets/b7437249-2f36-4654-8a3b-0e6f68bc878d)

  - Accedamos nuevamente a http://localhost/WeatherForecast y vemos que nos devuelve datos.

![image](https://github.com/user-attachments/assets/29e771cf-d281-4a4a-a294-3a12d5f9e156)


#### 9- Modificar Dockerfile para soportar bash 

- Modificamos dockerfile para que entre en bash sin ejecutar automaticamente la app

 
```bash
#ENTRYPOINT ["dotnet", "SimpleWebAPI.dll"]
CMD ["/bin/bash"]
```
- Rehacemos la imagen
```
docker build -t mywebapi .
```
- Corremos contenedor en modo interactivo exponiendo puerto
```
docker run -it --rm -p 80:80 mywebapi
```
- Navegamos a http://localhost/weatherforecast
- Vemos que no se ejecuta automaticamente
- Ejecutamos app:
```
dotnet SimpleWebAPI.dll
```


-Volvemos a navegar a http://localhost/weatherforecast
- Salimos del contenedor

![image](https://github.com/user-attachments/assets/11a6cd9f-51a2-482d-84d7-b2360c8222ad)

  
#### 10- Montando volúmenes

Hasta este punto los contenedores ejecutados no tenían contacto con el exterior, ellos corrían en su propio entorno hasta que terminaran su ejecución. Ahora veremos cómo montar un volumen dentro del contenedor para visualizar por ejemplo archivos del sistema huésped:

  - Ejecutar el siguiente comando, cambiar myusuario por el usuario que corresponda. En Mac puede utilizarse /Users/miusuario/temp):
```bash
docker run -it --rm -p 80:80 -v /Users/miuser/temp:/var/temp  mywebapi
```
  - Dentro del contenedor correr
```bash
ls -l /var/temp
touch /var/temp/hola.txt
```
![image](https://github.com/user-attachments/assets/2c3406e4-64bd-4681-a5ca-c7a9f02e102a)

  - Verificar que el Archivo se ha creado en el directorio del guest y del host.
![image](https://github.com/user-attachments/assets/f3409d86-f5c4-44f6-8d52-fc49700b7967)

#### 11- Utilizando una base de datos
- Levantar una base de datos PostgreSQL

```bash
mkdir $HOME/.postgres

docker run --name my-postgres -e POSTGRES_PASSWORD=mysecretpassword -v $HOME/.postgres:/var/lib/postgresql/data -p 5432:5432 -d postgres:9.4
```

cambian los comandos al usar windows
![image](https://github.com/user-attachments/assets/52a324b8-ef12-483b-9f3d-99cd5ce493e7)


- Ejecutar sentencias utilizando esta instancia

```bash
docker exec -it my-postgres /bin/bash

psql -h localhost -U postgres

#Estos comandos se corren una vez conectados a la base

\l
create database test;
\connect test
create table tabla_a (mensaje varchar(50));
insert into tabla_a (mensaje) values('Hola mundo!');
select * from tabla_a;

\q

exit
```
![image](https://github.com/user-attachments/assets/cfcdd256-cb14-4815-94f6-3e9a4fe6d5c0)


#### 12- Hacer el punto 11 con Microsoft SQL Server
- Armar un contenedor con SQL Server
- Crear BD, Tablas y ejecutar SELECT
  
#### 13- Presentación del trabajo práctico.

Subir un archivo md (puede ser en una carpeta) trabajo-practico-02 con las salidas de los comandos utilizados. Si es necesario incluir también capturas de pantalla.
