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

## Container
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