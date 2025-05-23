Always start with this code (if you have docker desktop you can skip this step):

```shell
run dockerd
```

___
## Alpine

- one of the most popular OS to run Containers

```shell
docker image pull apline
```

___
## 2 Way to Run Commands in the Container

```shell
docker container run alpine ...#runs whatever you put in ... in the alpine container
docker container run -it alpine #opens the terminal of the alpine container
docker container run --name *insert name* alpine #run container with custom name
```

___
## List Containers
```shell
docker container ls #shows list of all containers
docker container ls -a # lista all accessible containers in your history
```

___
## Purging Containers
```shell
docker container prune #remove all containers in history
docker container run --rm alpine *insert code to run* #will remove the container after running
docker container remove *insert container* #will remove container but still be in history
```

___
## Web Server Containers
Uses Apache WebServer
```
docker container run -d -p 8080:80 httpd
```

where:
-p: port mapping
-d: detach (run in the background)

```
curl localhost:8080
```

or if you want to open it in the browser: https://localhost:8080

___
## Running NodeJS files in the Containers
1. You need a folder with a JS file containing your JS code (call it app.js)
2. You need a docker file (named Dockerfile):

```dockerfile
FROM node #download node image
COPY ./app /app #copy the app file into your container
WORKDIR /app #be inside the app directory when you open the container (will create if none)
CMD node app.js #run app.js
```

Then run this code (*NOTE: Make sure you are in the project directory with the docker file*):

```shell
docker image build . # . refers to the current directory
docker image build -t *insert name*:*insert tag* # build image with a specific name and tag, if no tag is specified it will auto to "latest"
```

where
-t: tag

Once you create the image you can run the ID of the container to run the JS file

```shell
docker container run *insert container ID or name* 
```