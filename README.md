# Spring Docker
<small>Projeto base como criar imagem docker de uma aplicação Spring Boot</small>

## Gerar a primeira image docker

1. Primeiro tem gerar a buid da imagem
```shell
.\mvnw clean package
```
Testar o jar
```shell
java -jar .\target\springdocker-0.0.1-SNAPSHOT.jar 
```

2. Criar arquivo `Dockerfile`
```dockerfile
FROM openjdk:11
WORKDIR /app
COPY ./target/*.jar ./application.jar
EXPOSE 8080

ENTRYPOINT java -jar application.jar
```

3. Build
```shell
docker build -t jnsousa/springdocker .
```
Verificar se image foi criada
```shell
docker images
REPOSITORY                   TAG         IMAGE ID       CREATED         SIZE
jnsousa/springdocker         latest      25569890447b   2 minutes ago   680MB
```

4. Agora pode criar containers com essa imagem
```shell
docker run --name springdockercontainer -p 8081:8080 jnsousa/springdocker
```
Criar outro container
```shell
docker run --name springdockercontainer2 -p 8082:8080 jnsousa/springdocker
```
Listar os containes
```shell
docker ps
CONTAINER ID   IMAGE                  COMMAND                  CREATED              STATUS          PORTS                    NAMES
da6ae2c54e25   jnsousa/springdocker   "/bin/sh -c 'java -j…"   57 seconds ago       Up 59 seconds   0.0.0.0:8082->8080/tcp   springdockercontainer2
7f2fb65be58a   jnsousa/springdocker   "/bin/sh -c 'java -j…"   About a minute ago   Up 2 minutes    0.0.0.0:8081->8080/tcp   springdockercontainer
```






