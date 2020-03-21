# Docker

## Stop all containers

```sh
docker container stop $(docker container ls -aq)
```

## Remove all containers

```sh
docker container rm $(docker container ls -aq)
```

## Clear volumes and images

```sh
docker image prune -f
docker volume prune -f
```
