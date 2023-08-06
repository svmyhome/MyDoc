# Docker

## Configure rights
1. Creating groups
```sudo groupadd docker```  
2. Adding users to a group
```sudo usermod -aG docker ${USER}```  

## Location
```sudo ls /var/lib/docker/``` - catalog  
```sudo du -sh /var/lib/docker/overlay2``` – layers size  
```sudo ls /var/lib/docker/overlay2/0267c5ce17995e650659ca27b7344af4edff6a9a705d1a9a7f3547b84012f6f9```  - what's inside, in the layer

## General information
```docker version``` – docker version  
```docker info``` – docker information

## Operational information
```docker stats``` – operational data about working containers  
```docker stats -a``` — operational data about all containers
```docker stats --format "table {{.Name}} \t {{.ID}} \t {{.CPUPerc}} \t {{.MemUsage}}"``` – output only a few fields

## Monitoring
VERSION=v0.47.2 # use the latest release version from https://github.com/google/cadvisor/releases
```sudo docker run \
  --volume=/:/rootfs:ro \
  --volume=/var/run:/var/run:ro \
  --volume=/sys:/sys:ro \
  --volume=/var/lib/docker/:/var/lib/docker:ro \
  --volume=/dev/disk/:/dev/disk:ro \
  --publish=8080:8080 \
  --detach=true \
  --name=cadvisor \
  --privileged \
  --device=/dev/kmsg \
  gcr.io/cadvisor/cadvisor:$VERSION
  ```

## Troubleshooting
When you use gitBash on Windows. You should use ```winpty docker run -it ubuntu bash```
or cmd ```docker run -it ubuntu bash```

## Container

### Starting
```docker run -it -d nginx``` -  running the container in interactive and detach mode 
```docker run -d --name my_nginx nginx``` -  running the container with the name
```docker run -d -p 8080:80 nginx``` — running the container with published ports HOST:CONTAINER  
```docker run -d -v ${PWD}:/usr/share/nginx/html -v ${PWD}/22:/mathefaka:ro -p 8080:80 nginx``` - mapping volumes to the container. ${PWD} - Show the path to work folder. :ro - read only 
```docker run -d -v /home/vladimir/Downloads/Repository/PetProjects/MyDoc/Doker/nginx:/usr/share/nginx/html -p 8081:80 nginx``` - mapping using an absolute path  
```docker run -it -d --name test2 --rm ubuntu bash``` - set name when container is creating and delete container after stop  
older
running container with line split
```
docker run \
--name my-nginx2 \
-v /home/vladimir/Downloads/Repository/PetProjects/MyDoc/Doker/nginx:/usr/share/nginx/html \
-p 8083:80 \
-d \
nginx
```


### Working
### login into the same terminal session
```docker attach NAME``` - login into the same terminal session. Exit ```Ctrl + p after Ctrl + q```  
### Creation of a new terminal session
```docker exec -it b8e45bef8a83 bash``` - running additional process in a running container. You must use ```exit``` to exit the session. Container won't close  
```docker exec -w /tmp container pwd``` - changing the working directory
```docker exec d1f465dc6157 node --version > 1.txt``` - output data
```docker exec -w /tmp d1f465dc6157 sh -c 'node --version > 1.txt'``` - changing the work directory and running the command in this directory  
```docker exec -e Myenv=1 My_mongo printenv``` - adding a new environment to the container
```docker stop 2731223e570f``` - stops the container  
```docker kill 2731223e570f``` - kills a hung process
### Delete containers
```docker container --rm NAME or HASH``` - delete the container after stop  
```docker container prun –f``` - delete all containers after stop without confirmation   

### Monitoring
```docker container ls``` or ```docker ps``` - show only work containers  
```docker container ls –a``` or ```docker ps -a``` – show all created containers  
```docker container inspect 2731223e570f```  or ```dockerclear inspect 2731223e570f```- show container settings  
```docker container inspect 2731223e570f | grep IPAddress```– filtering   

## Image
```docker history mongo``` – the history of image creation  
```docker inspect mongo``` – information about image  

```docker save имя_образа > transfer.tar``` - сохраняет образ в виде файла
```docker load -i transfer.tar``` - загружает образ в систему
или
```docker save –output nginx.tar nginx``` – сохраняет образ в виде файла
```docker import nginx.tar svmyhome\nginx1```  - загружает образ в систему


```docker image pull ubuntu``` – скачать образ
```docker image push svmyhome/catnip``` – запушить в репозиторий
```docker image push my_repo/my_image:my_tag``` – с тегом

```docker images``` – список образов
```docker image ls``` - – список образов
```docker images --format "{{.Repository}} {{.Tag}}"``` – список нужных полей
```docker images --format "table {{.Repository}} \t {{.Tag}}"``` – в виде таблицы лучшее читается


```docker rmi hello-world``` – удаление образа

```docker image rm python:3-onbuild``` – тоже 
```docker image rm -f $(docker images -a -q)``` – удаление всех образов
```docker image prune``` or ```docker rmi -f$(docker images -f "dangling=true" -q)```– удаляет образы none
```docker image prune – a```  удаляет все образы для которых нет запущенных контейнеров
```docker tag svmyhomenginx1:latest 11111``` – создает тег
```docker images -f "dangling=true"``` show not nessasery images  
## Dive
dive id -утилита для анализа образа и его слоев
## Dockerfile
### build
### Multistaging build
## Network
### Commands
## MOUNT FILES AND DISKS
### Volumes
### volume in Dockerfile
### BIND папки
## TRPFS
## Копирование файлов и папок
## DOCKER COMPOSE
### Команды
