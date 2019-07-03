# Port

## How to kill a process running on particular port

```sh
fuser -k 8080/tcp
```

## How to check if port is being used

```sh
lsof -i -P -n

# or

curl 0.0.0.0:3000
```
