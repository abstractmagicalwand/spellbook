# Docker

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

# --interactive says you want an interactive session.
# --tty allocates a pseudo-tty.
# --rm tells Docker to go ahead and remove the container when it’s done executing.
```

You can run a container and verify all the steps you need to deploy your app, and capture them in a Dockerfile.

### In the background

```sh
docker container run \
--detach \
--name mydb \
-e MYSQL_ROOT_PASSWORD=my-secret-pw \
mysql:latest                           #

# --detach will run the container in the background
# --name mydb will name it mydb.
# -e will use an environment variable to specify the root password (NOTE: This should never be done
# in production).
```

## List containers

```sh
docker container ls --all # List all containers
docker container ls       # List the running containers
```

## List images

```sh
docker image ls
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
docker container rm --force linux_tweet_app
# or
docker container stop linux_tweet_app
docker container rm linux_tweet_app
```

## How to automatically start containers after rebooting system

[Start containers automatically](https://docs.docker.com/config/containers/start-containers-automatically/)

We can run container with flags:

```sh
docker run -dit -p 27017:27017 --restart always mongo
```

## How to package your own images

### 1. `cd ~/linux_tweet_app`

### 2. Add `Dockerfile`

```dockerfile
FROM nginx:latest

COPY index.html /usr/share/nginx/html
COPY linux.png /usr/share/nginx/html

EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]
```

- `FROM` specifies the base image to use as the starting point for this new image you’re creating.
- `COPY` copies files from the Docker host into the image, at a known location.
- `EXPOSE` documents which ports the application uses.
- `CMD` specifies what command to run when a container is started from the image.

### 3. `docker image build --tag linux_tweet_app:1.0 .`

- `--tag` allows us to give the image a custom name.
- `.` tells Docker to use the current directory as the build context.

### 4. Start a new container from the image

```sh
docker container run \
--detach \
--publish 80:80 \
--name linux_tweet_app \
  linux_tweet_app:1.0
```

- `--publish` will allow traffic coming in to the Docker host on port 80 to be directed to port 80
in the container.

## Modify a running container

### Start our web app with a bind mount

```sh
docker container run \
--detach \
--publish 80:80 \
--name linux_tweet_app \
--mount type=bind,source="$(pwd)",target=/usr/share/nginx/html \
linux_tweet_app:1.0
```

## Push your images to Docker Hub

You must have docker id.

`export DOCKERID=<your docker id>`

And build images with the Docker ID attached to the name. It allow us to store it on Docker Hub:

`docker image build --tag $DOCKERID/linux_tweet_app:1.0 .`

### Login and push

```sh
docker login
docker image push $DOCKERID/linux_tweet_app:1.0
```

You can browse to `https://hub.docker.com/r/<your docker id>/` and see your newly-pushed Docker images.
