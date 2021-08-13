## create new network

```console
docker network create my_network
```

## then start a container in new network:

```console
docker container run -d --name new_nginx --network my_network nginx
```