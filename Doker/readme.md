# Docker

## Configure rights
1. Creating groups
```sudo groupadd docker```
2. Adding users to a group
```sudo usermod -aG docker $USER```

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
```docker run -d nginx``` -  running the container in detach mode 
```docker run -d --name my_nginx nginx``` -  running the container with the name
```docker run -d -p 8080:80 nginx``` — running the container with published ports HOST:CONTAINER  
```docker run -d -v ${PWD}:/usr/share/nginx/html -p 8080:80 nginx``` - mapping volumes to the container. ${PWD} - Show the path to local folder  
```docker run -d -v /home/vladimir/Downloads/Repository/PetProjects/MyDoc/Doker/nginx:/usr/share/nginx/html -p 8081:80 nginx``` - mapping using an absolute path  
```docker run –it –d  Ubuntu bash``` – позволяеь запустить в фоновом режиме
```docker run -it -d --name test2 --rm ubuntu bash``` – задает имя контейнера, удаляет после остановки  

запуск с разбиением
```
docker run \
--name my-nginx2 \
-v /home/vladimir/Downloads/Repository/PetProjects/MyDoc/Doker/nginx:/usr/share/nginx/html \
-p 8083:80 \
-d \
nginx
```


### Working
```docker exec -it b8e45bef8a83 bash```   -  запускает дополнительный процесс в запущенном контейнере выйти можно через exit. Контейнер не будет закрыт 
```docker stop 2731223e570f``` - останавливает работу контейнера  
```docker kill 2731223e570f``` - убивает зависший процесс  
```docker container --rm имя или номер```  eудаляет контейнер после остановки  
```docker container prun –f```  - удаляет все остановленные контейнеры без переспрашивания  
```docker attach имя контейнера``` позволят зайти в конкретный контейнер для выхода Ctrl + p после Ctrl + q  
Выполнение действий или подключение в уже работающий контейнер
docker exec -w /tmp My_mongo pwd
docker exec -e Myenv=1 My_mongo printenv
docker exec -it My_mongo bash
docker exec My_mongo mongo -version > mongo.txt
docker exec -w /tmp My_mongo bash -c 'mongo -version > mongo1.txt' 


### Monitoring
```docker container ls``` или ```docker ps``` - показывает работающие контейнеры  
```docker container ls –a``` или ```docker ps -a``` – показывает все в том числе и остановленные  
```docker container inspect 2731223e570f```  - показывает настройки контейнера  
```docker container inspect 2731223e570f | grep IPAddress```– позволяет отфильтровать вывод  




## Image
## Dive
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


что внутри слоя