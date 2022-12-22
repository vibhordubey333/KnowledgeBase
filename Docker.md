### Docker Frequently Used CMD's

* To save an Image locally as tar : docker save hello-world > hello-world.tar 
* To extract above tar : tar -xfv hello-world.tar'
* docker images
* docker rmi -f image_name
* docker container ls -a
* docker container stop container_name
* docker container prune
* docker-compose up
* docker-compose up [Detached Mode]
* docker build -f build/Dockerfile -t tag_name
* docker-compose ps [To List All The Containers]
* docker-compose -f build/docker-compose.yml up -d 
* docker run -d -p 127.0.0.1:7777 filemgmt:latest
* docker-compose rm
* Push images to private docker registry.
  - docker tag ubuntu altimauthserver.com:6010/ubuntu
  - docker push altimauthserver.com:6010/ubuntu
* docker info
* docker tag image_name new_image_tag_name
* Debug mongodb inside container 
  - docker exec -it mongoservice mongo
* Prune old images, containers, volumes
  - `docker container prune && docker image prune && docker network prune && docker volume prune`
* Debug Docker Failing Image While Building
  - `docker commit paste-hash temp-image-name`
  - `docker run -it temp-image-name`
* Debug Container
  - `docker exec -it container_name /bin/bash or sh`

### To spin postgres docker container on local
 - Windows `docker run --name postgresql -e POSTGRES_USER=myusername -e POSTGRES_PASSWORD=mypassword -p 5432:5432 -v D:/data:/var/lib/postgresql/data -d postgres`
 - Linux `docker run --name postgresql -e POSTGRES_USER=myusername -e POSTGRES_PASSWORD=mypassword -p 5432:5432 -v /data:/var/lib/postgresql/data -d postgres`
