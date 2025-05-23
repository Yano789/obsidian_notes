Always start with this code:

```shell
run dockerd
newgrp docker
```

## Alpine

- one of the most popular OS to run Containers

```shell
docker image pull apline
```

## 2 Way to Run Commands in the Container

```shell
docker container run alpine ...#runs whatever you put in ... in the alpine container
docker container run -it alpine #opens the terminal of the alpine container
docker container run --name *insert name* alpine #run container with custom name
```

```shell
docker container ls -a # lista all containers in the history
```

## Purging Containers
```shell
docker container pruce #remove all containers in history
docker container run --rm alpine *insert code to run* #will remove the container after running
```