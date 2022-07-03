# Docker Java

## commands

- run locally

```shell
mvn install
mvn spring-boot:run
```

- run via Dockerfile

```shell
docker build -t docker-java .
docker run -dp 8080:8080 -t docker-java
```
