hello world

build docker:
`docker build -t friendlyhello testDocker`

`RutgerMacbook:Aqueduct30Docker rutgerhofste$ docker run -d -v /Users/rutgerhofste/GitHub/Aqueduct30Docker/notebooks/:/mnt/notebooks/ -p 8888:8888 eboraas/jupyter`


run docker:

`docker run -p 4000:80 friendlyhello`


share repo on hub.docker
`docker login`
`docker tag image username/repository:tag`
e.g.: `docker tag friendlyhello rutgerhofste/get-started:part1`
`docker push username/repository:tag`


Building images

docker build --no-cache -t <name> <folder with DockerFile>


cleanup

check containers
`docker ps -a`

remove all containers Linux
docker rm $(docker ps -a -q)

remove none conatiners Windows
``FOR /f "tokens=*" %i IN ('docker images -q -f "dangling=true"') DO docker rmi %i``

`docker stop <containerID>`

`docker rm <containerID>`

check images
`docker images`

`docker rmi <imageID>`
`docker rmi $(docker images -f dangling=true -q)`

docker system prune
docker container prune
docker image prune
docker network prune
docker volume prune