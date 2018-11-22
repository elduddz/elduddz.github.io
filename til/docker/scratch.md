### Get thing

docker pull [image][:tag]

### build image

docker build -t simple-nuget-server .

(. loads the dockerfile nearby)

### list available images

docker images

### run container based on image

docker run -d -p 80:80 --name nuget free-nuget-server:latest --restart="always"

### list container

docker ps

### interative terminal on container

docker exec -it [SHA] cmd

### stop container

docker stop [SHA]

### remove container

docker rm [SHA]

**to remove container must be stopped**

## ARG and use there of

### in dockerfile setup and use

ARG configuration="default"

COPY ${configuration}

### passing parameters to docker build

docker build --build-arg configuration="value" -t tag .
docker rm [SHA]

docker save -o file.tar [image]

docker load -i file.tar

## Transfer to local repo

```powershell
# you will need to login

docker login localrepobaseurl

# moving images local
docker pull [image][:tag]
docker tag [image][:tag] localreponame/[image][:tag]
docker push localreponame/[image][:tag]

# where image and tag are the same throughout
```