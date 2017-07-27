
# Docker Cheatsheet  

List all images   
`docker images`

Remove an image
`docker rmi <imageID>`

List all containers  
`docker ps -a`

Remove a container  
`docker rm -f <containerID>`

Build image  
`docker build -t <tag> <path to Dockerfile>`


Run image, launch container    
`docker run <image name(local or remote on DockerHub)>`

Run docker with exposed ports (check Dockerfile if ports are exposed)  

`docker run -p 4000:80 friendlyhello`

* Jupyter default 8888
* JupyterHub default 8000

Change the name and tag of an image  
`docker tag image username/repository:tag`

Upload docker image to DockerHub (Note that image has to have the name username/imagename:tag)  
`docker login`  
`docker push username/repository:tag`  

Building images

`docker build --no-cache -t <name> <folder with DockerFile>`

Cleanup

remove all images Linux
`docker rmi $(docker images -f dangling=true -q)`

remove all containers Linux
docker rm $(docker ps -a -q)

remove none images Windows
``FOR /f "tokens=*" %i IN ('docker images -q -f "dangling=true"') DO docker rmi %i``

Newer versions of Docker only: remove unused data  
`docker system prune`
`docker container prune`
`docker image prune`
`docker network prune`
`docker volume prune`