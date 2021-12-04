# First test image
ARG MyARG=/home
FROM node:latest
MAINTAINER = Vladimir Sarychev
WORKDIR /opt
ADD 1.json .
RUN ls -la
WORKDIR /home
ADD *.json ./
RUN ls -la
ADD 1.tar.xz ./tarxz/
WORKDIR ./tarxz/
VOLUME ["/voldemar"]
CMD bash