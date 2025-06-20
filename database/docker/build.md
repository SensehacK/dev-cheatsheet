# Docker Build


## Node JS

Beginners code flow with Node JS
### Dev Instance

[https://vast-reef-06229.herokuapp.com/](https://vast-reef-06229.herokuapp.com/)

### Setup

Manual setup for Node JS. Just npm install and nodemon app.js

```sh
localhost would be listening on port 3000
```

### Docker Run

### Pull Images

// MYSQL image

```sh
docker pull kautilyasave/sensehack-mysql
```


// Node js image

```sh
docker pull kautilyasave/sensehack-nodejs
```

### Build

After setting up the docker images run the container using these commands. First run MYSQL image as NodeJS image is dependent on it. Run command with port and environment variables

## MYSQL Container

```bash
docker run  -d \
--publish 3306:3306 \
--volume=/Users/SensehacK/Documents/GitHub/nodejs/mysql/data:/var/lib/mysql \
--name=sensehack-mysql-img kautilyasave/sensehack-mysql
```

Save the MYSQL Image container local ip address and port for linking it to NodeJS Image while running. GREP IP address of MYSQL docker image running container

```sh
docker inspect sensehack-mysql-img \| grep IPAddress
```

MYSQL\_HOST= 'Replace the IP address for giving the node js connection SQL Host address.

### Node JS Container

// Run command

```bash
docker run  -d \
--publish 3000:3000 \
-e MYSQL_USER='root' \
-e MYSQL_PASSWORD='kautilya' \
-e MYSQL_DATABASE='node_js' \
-e MYSQL_HOST='172.17.0.2' \
--link sensehack-mysql-img:db \
--name=sensehack-nodejs-img kautilyasave/sensehack-nodejs
```

### Docker Images Creation and Publish

### MYSQL Image

```sh
docker build -t kautilyasave/sensehack-mysql .
```

Push the image to docker Hub

```sh
docker push kautilyasave/sensehack-mysql
```

### Node JS Image

```sh
docker build -t kautilyasave/sensehack-nodejs .
```

Push the image to docker Hub

```sh
docker push kautilyasave/sensehack-nodejs
```

### Usage

### GET Method

/users To get all the users [https://vast-reef-06229.herokuapp.com/users](https://vast-reef-06229.herokuapp.com/users)

/users/:id To get specific ID of the user. [https://vast-reef-06229.herokuapp.com/users/2](https://vast-reef-06229.herokuapp.com/users/2)

Connected with MySql server for dynamic data

/user/country\_name ‘country\_name’ is the ID. Retrieve the data from the API while it executes the SQL query. eg. [http://localhost:3000/user/india](http://localhost:3000/user/india)

/user/country\_name/profession/work\_name ‘country\_name’ & ‘work\_name’ are both the IDs. Retrieve the data from the API while it executes the SQL query. eg. [http://localhost:3000/user/usa/profession/billionaire](http://localhost:3000/user/usa/profession/billionaire)

### POST Method

/user\_create To post users in MySql database

### UI Form

[http://localhost:3000/form.html](http://localhost:3000/form.html) GUI form to submit new users. [https://vast-reef-06229.herokuapp.com/form.html](https://vast-reef-06229.herokuapp.com/form.html)


## Docker build SQL

user-mysql-666

user-nodejs-777

```sh
docker build -t test-mysql .
```

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

```sh
docker stop container\_name docker rm /container\_name
```

\` Logs to check of the container

```sh
docker logs docker\_container\_name
```

To check images of docker

```sh
docker images
```

To check process of docker containers / images

```sh
docker ps
```

```sh
docker build -t user-mysql-666 .

docker run -d  --publish 3306:3306  --volume=/Users/SensehacK/Documents/GitHub/nodejs/mysql/data:/var/lib/mysql  --name=user-mysql-img-666 user-mysql-666

docker build -t user-nodejs-666 .

docker run -d  --publish 3000:3000  -e MYSQL\_USER='root'  -e MYSQL\_PASSWORD=‘your\_password’  -e MYSQL\_DATABASE='node\_js'  -e MYSQL\_HOST='172.17.0.2'  --link test-mysql-micro:db  --name=user-nodejs-img-666 user-nodejs-666
```

