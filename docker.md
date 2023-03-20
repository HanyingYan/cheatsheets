## 1. Background
**Containerization**: *operating system-level virtualization* or *application-level virtualization* over multiple network resources 
so that software applications can run in ***isolated*** user spaces called *containers* in any cloud or non-cloud environment, 
regardless of type or vendor.

**Docker**: a set of ***platform as a service (PaaS)*** products that use ***OS-level virtualization*** to deliver software in packages called ***containers***
  * The software that hosts the containers is called ***Docker Engine***
  * Containers are isolated from one another and bundle their own software, libraries and configuration files
  * Containers is **stateless**, so it does not retain persistent data; if you need to update the components inside, create another container instead.
  
**Image**: template to create a container. Its components are defined by a ```Dockerfile```.

**Volume**: storage area detached from the container for maintaining state.

**Foreground/interactive** vs **background/detached**: 
  * a detached container runs in the background 
  * an interactive container usually have a terminal for user to interact with.

## 2. Commands
1. List all local images.<br/>
  ```docker images```
1. Clean up images.<br/>
  ```docker image rm```
1. List all running containers.<br/>
   ```docker ps```
1. Run a Docker image inside a container.<br/>
  ```docker run -it --rm <image_name:tag_name>```
    * ```-it``` is a combination of ```-i``` (interactive mode) and ```-t``` (allocate a terminal).
    * ```--rm``` means that the container will be removed when exited.
    * Available Docker images can be found at at the [Docker Hub](https://hub.docker.com/). You can also create yours there.
    * This command use the entrypoint defined by the image. For example, it may open a terminal inside the container or start a python environment.
1. Run a Docker image inside a container and override the entrypoint.<br/>
  ```docker run -it --rm --entrypoint=bash <image_name:tag_name>```
    * This ```--entrypoint=``` will override the entrypoint of your image and open a bash terminal inside the container instead.
1. Run a Docker image inside a container and map a port in the container to a port in the host machine.<br/>
  ```docker run -it --rm -p 9696:9696 <image_name:tag_name>```
1. Create a basic ```Dockerfile``` to create a basic Docker image. <br/>
    ```
    # set base image
    FROM python:3.9

    # set the working directory in the container
    WORKDIR /app

    # copy dependencies to the working directory
    COPY requirements.txt .

    # Install dependencies
    RUN pip install -r requirements

    # Copy code to the working directory
    COPY . /app

    # command to run on container start
    CMD ["python", "./main.py"]
    ```
    More details can be found [here](https://github.com/HanyingYan/data-engineering-zoomcamp-hy/tree/main/week1#121---introduction-to-docker).

1. Build an image based on a Dockerfile.<br/>
  ```docker build -f Dockerfile -t <image_name> .```
    * The default Dockerfile that the command will look for is $PATH/Dockerfile. If your Dockerfile is in the same directory that you will run the command and you have not named it something else, -f Dockerfile can be removed from the command.
    * <image_name> will be the name of your image. You may optionally tag it using <image_name:tag_name> instead.
1. Exit Docker Container from an Interactive Shell Session
    * Exit and Stop Docker Container: press ```Ctrl+C``` to stop the process, then press ```Ctrl+D``` to exit and stop the container.
    * Exit Docker Container without Stopping It: press ```Ctrl+P``` and ```Ctrl+Q``` to detach the container and return to the system's shell.
    * To return to the container's interactive shell, use ```docker attach <container-name-or-id>```
1. Stop a running container.<br/>
  ```docker stop <container-name-or-id>```
  
## 3. Docker Compose  
```docker-compose``` allows us to launch multiple containers using a single configuration file, so that we don't have to run multiple complex ```docker run``` commands separately. 

With Compose, you use a single ```docker-compose.yml``` file to configure, create and start your application’s services.

More details can be found [here](https://github.com/HanyingYan/data-engineering-zoomcamp-hy/tree/main/week1#125---running-postgres-and-pgadmin-with-docker-compose).

1. basic ```docker-compose.yaml``` file
    ```
    services:
      pgdatabase:
        image: postgres:13
        environment:
          - POSTGRES_USER=root
          - POSTGRES_PASSWORD=root
          - POSTGRES_DB=ny_taxi
        volumes: 
          - "./ny_taxi_postgres_data:/var/lib/postgresql/data:rw"
        ports:
          - "5432:5432" 
      pgadmin:
        image: dpage/pgadmin4
        environment:
          - PGADMIN_DEFAULT_EMAIL=admin@admin.com
          - PGADMIN_DEFAULT_PASSWORD=root
        ports:
         - "8080:80"
    ```
    * The app has 2 components: ```pgdatabase``` and ```pgadmin```, and each component must have a Docker ```image```.
    * You may specify environment variables with ```environment```, port mappings with ```ports``` and storage places with ```volumes```.
    * The ```-``` means that the entry is a list.    
1. Run the app.<br/>
```docker-compose up```
1. Run the app in detached mode.<br/>
```docker-compose up -d```
1. Shut down the app.<br/>
```docker-compose down```
    
