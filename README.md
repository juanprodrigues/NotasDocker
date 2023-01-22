# NotasDocker
## Comandos Importantes de Docker
Docker es una herramienta poderosa para crear, desplegar y ejecutar aplicaciones en contenedores. A continuación se presentan algunos comandos útiles para trabajar con Docker.

### Construir una imagen
Para construir una imagen de Docker a partir de un archivo "Dockerfile", utilice el comando "docker build". Este comando toma como argumento la ruta al directorio que contiene el archivo "Dockerfile" y opcionalmente una etiqueta para la imagen resultante.

```
docker build -t my-image .
```
Por ejemplo en el siquiente repositorio se uso
```
C:\Users\Juan\Downloads\2_curso-kubernetes[postgres]\curso-kubernetes\msvc-usuarios>docker build -t microusuarios . 
[+] Building 5.0s (8/8) FINISHED
 => [internal] load build definition from Dockerfile                                                                                         0.0s 
 => => transferring dockerfile: 32B                                                                                                          0.0s 
 => [internal] load .dockerignore                                                                                                            0.0s 
 => => transferring context: 2B                                                                                                              0.0s 
 => [internal] load metadata for docker.io/library/openjdk:8                                                                                 1.8s 
 => [internal] load build context                                                                                                            1.9s 
 => => transferring context: 48.02MB                                                                                                         1.9s 
 => [1/3] FROM docker.io/library/openjdk:8@sha256:86e863cc57215cfb181bd319736d0baf625fe8f150577f9eb58bd937f5452cb8                           0.0s 
 => CACHED [2/3] WORKDIR /app1                                                                                                               0.0s 
 => [3/3] COPY ./target/msvc-usuarios-0.0.1-SNAPSHOT.jar .                                                                                   0.5s 
 => exporting to image                                                                                                                       0.6s 
 => => exporting layers                                                                                                                      0.6s 
 => => writing image sha256:37f2ce16684a242d0a7adcf75ed42574b3e3daf9678e3c6c81bc06714d4c109c                                                 0.0s 
 => => naming to docker.io/library/microusuarios 
```
el parametro -t nos permite ingresar el nombre del repositorio que se mostrara al ingresar docker images.

### Listar imágenes
Para ver una lista de las imágenes de Docker instaladas en su sistema, utilice el comando "docker images". Este comando mostrará información como el repositorio, la etiqueta y el tamaño de cada imagen.

```
docker images
```
### Ejecutar un contenedor
Para ejecutar un contenedor a partir de una imagen de Docker, utilice el comando "docker run". Este comando toma como argumento el nombre o ID de la imagen y opcionalmente algunas opciones para personalizar la forma en que se ejecuta el contenedor.

```
docker run -p 8080:8080 -v data-volume:/data my-image
```
El flag "-p 8080:8080" se utiliza para exponer el puerto 8080 del contenedor al host, de esta manera se podrá acceder al contenedor a través de ese puerto. El flag "-v data-volume:/data" se utiliza para montar un volumen externo llamado "data-volume" en el directorio "/data" dentro del contenedor. El volumen externo puede ser utilizado para almacenar datos persistentes o para compartir archivos entre diferentes contenedores.

Para el repo se usa 
```
docker run -p 8001:8001 af97ac283325
```
El flag "-p 8080:8080" en el comando "docker run" se utiliza para exponer un puerto específico del contenedor al host. La sintaxis es "-p hostPort:containerPort", donde "hostPort" es el puerto en el host y "containerPort" es el puerto en el contenedor. En este caso, se está exponiendo el puerto 8080 del contenedor al puerto 8080 del host.

De esta manera, se permite que las aplicaciones en el host puedan acceder a las aplicaciones que se ejecutan en el contenedor a través de ese puerto. Por ejemplo, si una aplicación en el contenedor está escuchando en el puerto 8080, se podrá acceder a ella desde el host utilizando http://localhost:8080.

Además, si se desea exponer varios puertos, se puede hacer de forma separada con varios flags -p o se puede utilizar una sola vez indicando varios puertos separados por comas.

```
docker run -p 8080:8080,8081:8081 -v data-volume:/data my-image
```
Es importante tener en cuenta que solo se puede exponer un puerto específico a un puerto específico y debe estar libre en el host, caso contrario se tendra un error.

### Detener un contenedor
Para detener un contenedor de Docker que se está ejecutando, utilice el comando "docker stop" seguido del nombre o ID del contenedor.

```
docker stop my-container
```
### Cambiar el nombre de una imagen
Para cambiar el nombre de una imagen de Docker, utilice el comando "docker tag" seguido del nombre o ID actual de la imagen y el nuevo nombre que desea asignar.

```
docker tag old-name new-name
```
### Eliminar una imagen
Para eliminar una imagen de Docker, utilice el comando "docker rmi" seguido del nombre o ID de la imagen que desea eliminar.

```
docker rmi my-image
```
Posible error
```
Error response from daemon: conflict: unable to delete [image ID] (must be forced) - image is being used by stopped container [container ID]
```

Indica que hay un contenedor detenido que está utilizando la imagen que intentas eliminar.

Para solucionar este problema, sigue los siguientes pasos:

1. Utiliza el comando "docker ps -a" para ver una lista de todos los contenedores, tanto en ejecución como detenidos.

2. Identifica el contenedor que está utilizando la imagen que deseas eliminar.

3. Elimina ese contenedor utilizando el comando "docker rm [container ID]"

4. Una vez que el contenedor ha sido eliminado, puedes utilizar el comando "docker rmi [image ID]" para eliminar la imagen.

En caso de que el contenedor no se pueda eliminar, puede utilizar el flag --force o -f

```
docker rm -f [container ID]
```
Ten en cuenta que al eliminar un contenedor, también se eliminan los datos almacenados en el contenedor.

### Inspect a container
Para obtener información detallada sobre un contenedor específico, utilice el comando "docker inspect" seguido del nombre o ID del contenedor.

```
docker inspect my-container
```
### Ver los contenedores en ejecución
Para ver una lista de los contenedores de Docker que se están ejecutando actualmente en su sistema, utilice el comando "docker ps".

```
docker ps
```
### Ver todos los contenedores
Para ver una lista de todos los contenedores de Docker, tanto en ejecución como detenidos, utilice el comando "docker ps -a".

```
docker ps -a
```
### Detener y eliminar un contenedor
Para detener y eliminar un contenedor de Docker, utilice los comandos "docker stop" y "docker rm" seguido del nombre o ID del contenedor.

```
docker stop my-container
docker rm my-container
```
Espero que estos comandos te ayuden a trabajar con Docker de manera eficiente. Recuerda que estos son solo algunos de los comandos básicos, hay muchas otras opciones y características disponibles. Siempre puedes consultar la documentación oficial de Docker para obtener más información.
