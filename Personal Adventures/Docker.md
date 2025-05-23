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
```

```shell
docker container ls -a # lista all containers in the history
```