# Docker

- An application container.
- Packages dependencies.
- Isolates applications.
- Processes run on the host OS.
- Lighter than VM.
- Developers can get going quickly by starting with one of the 13,000+ apps available on Docker Hub.
- Open-source.

## Hostname and container ID

The container ID is the `hostname` that the container displayed.

## Run some Docker containers

There are different ways to use containers. These include:

1. **To run a single task:** This could be a shell script or a custom app.
2. **Interactively:** This connects you to the container similar to the way you SSH into a remote server.
3. **In the background:** For long-running services like websites and databases.

### Run a single task

```sh
docker container run alpine hostname
```

You could build a Docker image that executes a script to configure something. Anyone can execute
that task just by running the container - they don’t need the actual scripts or configuration information.

### Interactively

```sh
docker container run --interactive --tty --rm ubuntu bash
```

- `-it`, `--interactive --tty`
- `--interactive` says you want an interactive session.
- `--tty` allocates a pseudo-tty.
- `--rm` tells Docker to go ahead and remove the container when it’s done executing.

You can run a container and verify all the steps you need to deploy your app, and capture them in a Dockerfile.

### In the background

```sh
docker container run \
--detach \
--name mydb \
--publish 80:80 \
-e MYSQL_ROOT_PASSWORD=my-secret-pw \
mysql:latest
```

- `-e` will use an environment variable to specify the root password (NOTE: This should never be done
in production)
- `-d`, `--detach` will run the container in the background.
- `--name` mydb will name it mydb.
- `-p`, `--publish` will allow traffic coming in to the Docker host on port 80 to be directed to port
80 in the container.

## List containers

```sh
docker container ls --all # List all containers
docker container ls       # List the running containers
docker ps                 # List the running containers
```

## List images

```sh
docker image ls
docker image ls -f reference="app" # Matching
```

## Run a command inside a container

```sh
docker exec -it mydb \
mysql --user=root --password=$MYSQL_ROOT_PASSWORD --version
```

## Connect to a shell inside a running container

```sh
docker exec -it mydb sh
```

## Check what’s happening in container

```sh
docker container logs container_name
docker container top container_name
```

## Shut a container down and remove it

```sh
docker container rm --force linux_tweet_app # -f is shortcut to --force
# or
docker container stop linux_tweet_app
docker container rm linux_tweet_app

docker rm $(docker ps -a -q) # remove all containers
```

## How to automatically start containers after rebooting system

[Start containers automatically](https://docs.docker.com/config/containers/start-containers-automatically/)

We can run container with flags:

```sh
docker run -dit -p 27017:27017 --restart always mongo
```

## How to package your own images

### Dockerfile

[Dockerfile reference](https://docs.docker.com/engine/reference/builder/)

Docker can build images automatically by reading the instructions from a `Dockerfile`.

A `Dockerfile` is a text document that contains all the commands a user could call on the command
line to assemble an image.

```dockerfile
FROM     node:12.4.0-alpine
LABEL    maintainer="Sawood Alam <@ibnesayeed>"

ENV      LANG C.UTF-8
ENV      REDIS_URL="redis://localhost:6379"

WORKDIR  /app
COPY     . .

EXPOSE   3000

RUN      yarn
RUN      yarn build
CMD      ["yarn", "start"]
```

- `ENV` sets environment variable
- `FROM` specifies the base image to use as the starting point for this new image you’re creating.
- `LABEL` adds metadata to an image.
- `COPY` copies files from the Docker host into the image, at a known location.
- `EXPOSE` documents which ports the application uses.
- `RUN` instruction will execute any commands in a new layer on top of the current image and commit
the results.
- `CMD` specifies what command to run when a container is started from the image.

### Build

`docker image build --tag linux_tweet_app:1.0 .`

- `-t`, `--tag` allows us to give the image a custom name.
- `.` tells Docker to use the current directory as the build context.

## Use bind mounts

```sh
docker container run \
--detach \
--publish 80:80 \
--name linux_tweet_app \
--mount type=bind,source="$(pwd)",target=/usr/share/nginx/html \
linux_tweet_app:1.0
```

## Build and push image to registry

```sh
docker build -t registry.gitlab.com/<your_registry>:tag .
docker login registry.gitlab.com
docker push registry.gitlab.com/<your_registry>:tag
```

### Docker Hub

You must have docker id.

`export DOCKERID=<your docker id>`

And build images with the Docker ID attached to the name. It allow us to store it on Docker Hub:

`docker image build --tag $DOCKERID/linux_tweet_app:1.0 .`

```sh
docker login
docker image push $DOCKERID/linux_tweet_app:1.0
```

You can browse to `https://hub.docker.com/r/<your docker id>/` and see your newly-pushed Docker images.
Anyone with access can pull that image and run a container from it. The behavior of the app in the
container will be the same for everyone, because the image contains the fully-configured app - the
only requirements to run it are Linux and Docker.

## Details

- [Docker Cheat Sheet](https://github.com/wsargent/docker-cheat-sheet)
- [Play with Docker Classroom](https://training.play-with-docker.com/)
- [What’s the Diff: VMs vs Containers](https://www.backblaze.com/blog/vm-vs-containers/)
