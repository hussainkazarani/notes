## Main Commands
 1. `docker run -it --name <customName> <imageName>`
    - creates and starts a container from image with terminal open
    - `-it` &rarr; interactive terminal
    - `--name` &rarr; name to give to container
    - `<imageName>`, `<imageID>` &rarr; the name of image i want to use or ID of that image

2. `docker run -d <imageName>`
   - creates, starts, and runs in detached mode (outside terminal/in background)
   - `-d` &rarr; run in detached mode
   - `<imageName>`, `<imageID>` &rarr; the name of image i want to use or ID of that image

3. `docker create --name <customName> <imageName>`
   - creates but does not start container
   - `--name` &rarr; name to give to container
   - `<imageName>`, `<imageID>` &rarr; the name of image i want to use or ID of that image

4. `docker exec -it <containerID> bash`
   - opens the container in a shell
   - `-it` &rarr; interactive terminal
   - `bash` &rarr; opens in the bash shell
   - `<containerName>`, `containerID` &rarr; name/id of the container
  
5. `docker build -t <name> .`
   - builds a docker image from Dockerfile
   - `-t` &rarr; give tag (a name)
   - `.` &rarr; Dockerfile location (current directory)
   - `<name>` &rarr; image name i want to give

## Basics
> Docker is used to containerize applications such that they are always running in the same environment. It runs in an environment which always has the same versions for all the tools and frameworks used to build the application
>
> Write `Docker Compose YAML` &rarr; Write `Dockerfiles` &rarr; Build an `Image` using these `Dockerfiles` &rarr; Run `Containers` from that `Image` &rarr; Execute into `Container` (if running)


### Installation
Download `Docker Desktop` &rarr; it container both the Daemon and GUI <br>
`Daemon` &rarr; does all the work of containerization <br>
`GUI` &rarr; graphical interface for using docker

### Image vs Container
`Image` &rarr; act as OS which runs code. can create custom images with our required tools and versions. can be shared

`Container` &rarr; they are isolated instances. they are themselves empty. when steps are written in image they are executed as instructions on creation/bootup

### Commands
`docker` &rarr; shows all docker commands

`docker -v` &rarr; gives docker version

`docker ps`, `docker container ls` &rarr; shows running containers

`docker container ls -a` &rarr; shows all containers

`docker start <name>` &rarr; start a closed container with its name

`docker stop <name>` &rarr; stop a running container with its name

`docker images`, `docker images ls` &rarr; shows all your images

`docker image remove <name>` &rarr; remove an image

`docker log <containerName>`, `docker logs <containerID>` &rarr; check logs of a container

### Other
`.dockerignore` &rarr; to ignore files when building/creating container
`docker login` &rarr; login for dockerhub
`docker push <imageName` &rarr; to push to dockerhub (only after creating repository)

> Notes <br>
> \- docker also has the `DockerHub` where we can store our images on their server. it's similar to github <br>
> \- it gets images from `hub.docker.com` if image is not available locally <br>
> \- `layer caching` is present. this means that if a top part of the Dockerfile's build layer hasn't changed (say lines 1-5 of Dockerfile), then it caches them and only builds the layers that have changed (lines after 5). the simple way to look at it is \***Common at Top, changing at Bottom**\*

## Ports and envs
> \- We must run each of the services inside the Images (server, database) on a specific port inside docker. these ports must be secure and preferably be given via a `.env` file <br>
> \- the tag `-p` needs data as follows: `-p myMachinePort:containerMachinePort` <br>
> \- the tag `-e` needs data as follows: `-e key-value`

### Method 1 &rarr; Hardcode Port in Program
- Write the hardcoded port value when creating service `(server.listen(1000))`
- Write `EXPOSE 1000` in its corresponding `Dockerfile` for comprehension (so user knows he has to expose in the Image command)
- In the Image command when creating a container, add the tag `-p 1000:1000`. 

### Method 2 &rarr; Hardcode in `.env`
- In the `.env` file, add `PORT=1000`. use `process.env.PORT` when creating services with the `dotenv` package
- Write `EXPOSE 1000` in its corresponding `Dockerfile` for comprehension (so user knows he has to expose in the Image command)
- In the Image command when creating a container, add the tag `-p 1000:1000`
- Have a fallback variable with the `||` operator if necessary

### Method 3 &rarr; No fallback, no `.env`
- In the Image command when creating a container, add `-e PORT=1000 -p 1000:1000`
- Use `process.env.PORT` when creating services with the `dotenv` package

## Dockerfile
> to create any image we need to create a `Dockerfile` that dockerizes the entire application. first you will create a file named `Dockerfile`. you can differentiate between dockerfiles by giving it extra parameters like `Dockerfile.server`

```js
// node.js example
FROM ubuntu:22.04
RUN apt update
RUN apt install -y curl
RUN curl "https://nodejs.com/download/XX.XX"
RUN apt install -y nodejs
WORKDIR /app // its cd /app and creates the folder
// remember that the `.` means from the current directory i ran command from terminal in
COPY . . // COPY <source> <dest>
EXPOSE 4000 // documentation of port
CMD ["npm","start"]
```

```js
// other commands
ENV DEBIAN_FRONTEND=noninteractive
ENV TZ=Asia/Kolkata
COPY package*.json // regex
CMD ["npm","start"] // only double quotes
&& / // combine lines for a single command
```

## Docker Volume
> we can mount a folder to a docker container. this means changes in the local machine files are shown in container <br>

### Command
`docker run -it -v <folderLocationLocal>:<folderLocationContainer> <imageName> <shell>`
  - `-it` &rarr; interactive terminal
  - `-v` &rarr; create a volume
  - `<folderLocationLocal>` &rarr; `pwd` of local folder to show in container
  - `<folderLocationContainer>` &rarr; which folder in container to link it with
  - `imageName` &rarr; name of the image to use
  - `shell` &rarr; shell to run terminal in

```js
// example
docker run -it -v /Users/kazarani/project:/home/app node bash
```

## Docker Compose
> \- it helps spin up multiple docker container at the same time. <br>
> \- we can setup, create and delete multiple containers <br>
> \- created in a `YAML` file

### Commands
`docker compose up` &rarr; spin up container with intergrated terminal

`docker compose up -d` &rarr; spin up container detached

`docker compose down` &rarr; spin down containers

```js
// docker-compose.yml
services:
    custom-postgres:
        container_name: pathless-database
        env_file: ../.env
        build:
            // where to start the build from
            context: ..
            dockerfile: deploy/Dockerfile.db
        ports:
            - '${POSTGRES_PORT}:5432'
        restart: always
        volumes:
            - pathless-db:/var/lib/postgresql/data 

    custom-node:
        container_name: pathless-server
        env_file: ../.env
        build:
            context: ..
            dockerfile: deploy/Dockerfile.server
        ports:
            - '${PORT}:1000'
        restart: always
        depends_on:
            - custom-postgres

volumes:
  pathless-db:
```

```js
// postges environment
environment:
    POSTGRES_USER: postgres
    POSTGRES_DB: review
    POSTGRES_PASSWORD: password
    APP_NAME=App1
```
