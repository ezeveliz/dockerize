## Comandos: 

* docker ps
  * Lista de contenedores corriendo

* docker image ls
  * Lista de imagenes instaladas
* docker image rm image:tag
  * Elimina la imagen image:tag

* docker stop <container-id-here>
  * detiene el contenedor asociado a la ID dada
* docker rm <container-id-here>
  * elimina el contenedor asociado a la ID dada, siempre y cuando no esté corriendo, para detenerlo usar el comando de arriba

* docker run --rm --name=<container-name> -e <env-var-name>=<env-var-value> -it -p 8080:80 -v $(pwd)/application:/var/www/html/public -w /di/rec/to/ry ubuntu:20.04 bash
  * docker run: instancia y ejecuta una imagen, la descarga si no estaba presente
  * --rm: cuando se termina el proceso a ejecutar elimina el contenedor
  * --name=<container-name>: le asigno un nombre al contenedor a ejecutar para poder referenciarlo por el mismo
  * -it(o -i -t): hace que la ejecución sea interactiva, se pueden meter comandos desde la consola, para que la ejecucion pase al fondo(background), usar -d
  * -p 8080:80: expone el puerto 8080 en el localhost(puedo acceder al contenedor desde localhost:8080), lo que se haga en este se va a enviar al puerto interno 80 del contenedor
  * -v $(pwd)/application:/var/www/html/public: comparte un volumen(un directorio) al directorio indicado dentro del contenedor
    * $(pwd)/application: esta primera parte genera la ruta al directorio en el que estoy ejecutando el comando + /application
    * /var/www/html/public: esta segunda parte indica a donde quiero colocar el volumen indicado por la primera parte dentro del contenedor
  * -w /di/rec/to/ry: setea el directorio en el que voy a ejecutar la orden que se va a pasar por parametro en este caso /di/rec/to/ry 
  * -e <env-var-name>=<env-var-value>: define una variable de entorno para pasarle al contenedor, se pueden agregar multiples agregando un -e por delante de cada una
  * ubuntu:20.04: imagen a usar y su tag correspondiente
  * bash: proceso a correr en el contenedor
* docker exec -it <container-id-here> bash
  * ejecuto un comando desde un contenedor en ejecucion, en este caso el comando bash

* docker commit -a "Eze Veliz" -m "Nginx installed" <container-id-here> mynginx:latest
  * Luego de hacerle cambios a un contenedor lo puedo commitear a mi instancia de docker, transformandolo en una nueva imagen que luego puedo utilizar

* docker build -t dockerize/app:latest -f docker/app/dockerfile docker/app
  * Buildeo un dockerfile, en este caso el ubicado en docker/app
  * -t dockerize/app:latest: cuando termina el buildeo(si y solo si termina sin errores) crea un nuevo tag y lo agrega a la lista de imagenes disponibles del sistema(como si lo hubiera commiteado)
  * -f docker/app/dockerfile: ubicacion del dockerfile
  * docker/app: contexto donde se va a encontrar lo que va a correr en el contenedor

* docker logs -f <container-id-here>
  * muestra por pantalla los logs generados por el contenedor asociado a la ID dada
  * -f: sigue los logs, a medida que se van generando los va agregando

### Network

* docker network ls
  * Muestra la redes creadas
* docker network create <network-name>
  * creo una red a la que se pueden asociar contenedores y ser visibles entre ellos
* docker network inspect <network-name>
  * inspecciona la red solicitada

## Extra

* images -> clase Image
* container -> instancia de clase Image