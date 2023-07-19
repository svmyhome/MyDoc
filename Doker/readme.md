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
sudo docker run \
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

## Troubleshooting
При запуске могут быть проблемы через gitBush использовать ```winpty docker run -it ubuntu bash```
Либо через cmd ```docker run -it ubuntu bash```

## Container
docker container ls  - показывает работающие контейнеры
docker container ls –a – показывает все в том числе и остановленные
тоже самое
docker ps
docker ps -a
docker container inspect 2731223e570f  - показывает настройки контейнера
docker container inspect 2731223e570f | grep IPAddress – позволяет отфильтровать вывод
docker exec -it b8e45bef8a83 bash   -  запускает дополнительный процесс в запущенном контейнере
docker run -d --name my_nginx nginx -  запуск кнтейнера с именем
docker run -d -p 8080:80 nginx — публикация портов внешний:контайнер
docker run -d -v ${PWD}:/usr/share/nginx/html -p 8080:80 nginx - ${PWD} -показывает путь до текущей папки
docker run -d -v /home/vladimir/Downloads/Repository/PetProjects/MyDoc/Doker/nginx:/usr/share/nginx/html -p 8081:80 nginx   - абсолютный путь

запуск с разбиением
docker run \
--name my-nginx2 \
-v /home/vladimir/Downloads/Repository/PetProjects/MyDoc/Doker/nginx:/usr/share/nginx/html \
-p 8083:80 \
-d \
nginx

docker stop 2731223e570f   - останавливает работу контейнера
docker kill 2731223e570f 
docker container --rm имя или номер  eудаляет контейнер после остановки
docker container prun –f  - удаляет все остановленные контейнеры без переспрашивания
docker run –it –d  Ubuntu bash – позволяеь запустить в фоновом режиме
docker attach имя контейнера позволят зайти в конкретный контейнер
для выхода Ctrl + p после Ctrl + q
docker run -it -d --name test2 --rm ubuntu bash – задает имя контейнера, удаляет после остановки

### Exec
Выполнение действий или подключение в уже работающий контейнер
docker exec -w /tmp My_mongo pwd
docker exec -e Myenv=1 My_mongo printenv
docker exec -it My_mongo bash
docker exec My_mongo mongo -version > mongo.txt
docker exec -w /tmp My_mongo bash -c 'mongo -version > mongo1.txt'
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