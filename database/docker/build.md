# Docker Build

## Docker build SQL

user-mysql-666

user-nodejs-777

> docker build -t test-mysql .

Output :

Successfully built 9097bf803efd Successfully tagged test-mysql:latest

2nd run : Successfully built 1b6928e93485 Successfully tagged test-mysql:latest

```text
docker run  -d \
--publish 6603:3306 \
--volume=/Users/SensehacK/Documents/GitHub/nodes/mysql:/var/lib/mysql \
--name=test-mysql-micro test-mysql
```

Output : b0144d3054130f1ea63fe58d0399709a32301902b1424c913b9491c126e37636

2nd : 688eba7ddf87236e00e139c0bddf02d8f2e64ad9623ce436e425376b5ab70fac

> docker stop container\_name docker rm /container\_name

\` Logs to check of the container

> docker logs docker\_container\_name

To check images of docker

> docker images

To check process of docker containers / images

> docker ps

docker build -t user-mysql-666 .

docker run -d  --publish 3306:3306  --volume=/Users/SensehacK/Documents/GitHub/nodejs/mysql/data:/var/lib/mysql  --name=user-mysql-img-666 user-mysql-666

docker build -t user-nodejs-666 .

docker run -d  --publish 3000:3000  -e MYSQL\_USER='root'  -e MYSQL\_PASSWORD=‘your\_password’  -e MYSQL\_DATABASE='node\_js'  -e MYSQL\_HOST='172.17.0.2'  --link test-mysql-micro:db  --name=user-nodejs-img-666 user-nodejs-666

