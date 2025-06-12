## Docker Volumes
- Generally docker containers are not persistent which means once container life cycle ends then the data inside this will be lost too.
- So to overcome this we place the data somewhere in our local machine 
- Docker has 3 options for volumes:
    - Bind Mount - here the data is stored in host machine
    - tempFs - it is temporary file system where it stores in RAM, in reality it won't use
    - Docker volumes - this will be maintained by docker it self, but bind mount and docker volumes are same including commands


## Bind Mount

```bash
# Bind Mount using --mount flag
mkdir target
docker container run -d --name bind-mount1 --mount type=bind,source="$(pwd)"/target,target=/app nginx

# Bind mount using -v flag this will create target2 if not exists
docker container run -d --name bind-volume -v "$(pwd)"/target2:/approot nginx

# Jenkins Example

docker run -d -p 8080:8080 -p 50000:50000 -u root -v /root/jenkinsbackup:/var/jenkins_home --name my-jenkins jenkins:2.60.3


# New Example
docker run -it -p 80:80 -v /root/vol-share:/var/www/html --name volsharing1 ubuntu /bin/bash
    apt update -y
    apt install vim -y
    apt install apache2 -y
    vim /var/www/html/index.html

# we are now creating a new container and mounting that with previously created mount path
docker run -it -p 81:80 -v /root/vol-share:/var/www/html --name volsharing2 ubuntu /bin/bash


```
## TMPFS
```bash
docker run -d --name tmpfstest --mount type=tmpfs,destination=/siva nginx
or
docker run -d --name tmpfstest --tmpfs /siva nginx 
# no source onlt destination is enough
```




## Docker Volumes

```bash
docker volume ls
docker volume create html-volume

# using --mount flag
docker container run -d -P --name nginx-volume-1 --mount type=volume,source=html-volume,target=/usr/share/nginx/html nginx

# using -v flag
docker container run -d -P --name nginx-volume-2 -v html-volume:/usr/share/nginx/html nginx

# Read only , you can't edit from contaier. But u can edit from volumes
docker container run -d -P --name nginx-volume-readonly --mount type=volume,source=html-volume,target=/usr/share/nginx/html,readonly nginx

```
