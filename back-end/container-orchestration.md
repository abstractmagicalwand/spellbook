# Container orchestration

## Docker Compose

Compose is a tool for defining and running multi-container Docker applications. Compose has
traditionally been focused on **development** and **testing** workflows.

- [Docker Compose](https://docs.docker.com/compose/)
- [Application Containerization and Microservice Orchestration](https://training.play-with-docker.com/microservice-orchestration/)
- [This repository illustrates step by step approach to learn Docker](https://github.com/ibnesayeed/linkextractor)
- [Use a Docker container as a development environment with Visual Studio Code](https://docs.microsoft.com/en-us/learn/modules/use-docker-container-dev-env-vs-code/)

`docker-compose.yml`:

```yml
version: '3'

services:
  api:
    image: linkextractor-api:step6-ruby
    build: ./api
    ports:
      - "4567:4567"
    environment:
      - REDIS_URL=redis://redis:6379
    volumes:
      - ./logs:/app/logs
  web:
    image: linkextractor-web:step6-php
    build: ./www
    ports:
      - "80:80"
    environment:
      - API_ENDPOINT=http://api:4567/api/
  redis:
    image: redis
```

### Commands

- `docker-compose up -d --build` ups and builds docker containers
- `docker-compose up -d` ups docker containers
- `docker-compose down` downs docker containers
- `docker-compose restart` restarts all containers
- `docker-compose restart rabbitmq` restarts container
- `docker-compose exec redis redis-cli monitor` executes sh comand in container

## Kubernetes (K8s)

It is an open-source system for automating deployment, scaling, and management of containerized applications.

- `kubectl exec -it -n app-staging frontend sh` enters into shell
- `kubectl scale -n app-staging deployment imager-deploy --replicas=0` scales
- `kubectl delete pod -n app-staging frontend` restarts pod
- `kubectl get -n app-staging pods` shows pods
- `kubectl logs -n app-staging frontend` shows logs

## Show environment variables

```sh
kubectl describe configmaps -n app-staging frontend-config

# or

kubectl exec -it -n app-staging frontend sh
env
```

## Check new pod

```sh
kubectl describe pod -n app-staging frontend

# or

kubectl get pods -n app-staging
```

## Docker Swarm

- [Swarm stack introduction](https://training.play-with-docker.com/swarm-stack-intro/)
- [Get Started, Part 4: Swarms](https://docs.docker.com/get-started/part4/)
