# Docker

Beginners code flow with Node JS

## List

[[build]]
[[commands]]
[[docker_rough_build_commands]]
[[info]]

## Dev Instance

[https://vast-reef-06229.herokuapp.com/](https://vast-reef-06229.herokuapp.com/)

## Setup

Manual setup for Node JS. Just npm install and nodemon app.js

> localhost would be listening on port 3000

## Docker Run

### Pull Images

// MYSQL image

> docker pull kautilyasave/sensehack-mysql

// Node js image

> docker pull kautilyasave/sensehack-nodejs

### Build

After setting up the docker images run the container using these commands. First run MYSQL image as NodeJS image is dependent on it. Run command with port and environment variables

#### MYSQL Container

```bash
docker run  -d \
--publish 3306:3306 \
--volume=/Users/SensehacK/Documents/GitHub/nodejs/mysql/data:/var/lib/mysql \
--name=sensehack-mysql-img kautilyasave/sensehack-mysql
```

Save the MYSQL Image container local ip address and port for linking it to NodeJS Image while running. GREP IP address of MYSQL docker image running container

> docker inspect sensehack-mysql-img \| grep IPAddress

MYSQL\_HOST= 'Replace the IP address for giving the node js connection SQL Host address.

#### Node JS Container

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

## Docker Images Creation and Publish

### MYSQL Image

> docker build -t kautilyasave/sensehack-mysql .

Push the image to docker Hub

> docker push kautilyasave/sensehack-mysql

### Node JS Image

> docker build -t kautilyasave/sensehack-nodejs .

Push the image to docker Hub

> docker push kautilyasave/sensehack-nodejs

## Usage

### GET Method

/users To get all the users [https://vast-reef-06229.herokuapp.com/users](https://vast-reef-06229.herokuapp.com/users)

/users/:id To get specific ID of the user. [https://vast-reef-06229.herokuapp.com/users/2](https://vast-reef-06229.herokuapp.com/users/2)

Connected with MySql server for dynamic data

/user/country\_name ‘country\_name’ is the ID. Retrieve the data from the API while it executes the SQL query. eg. [http://localhost:3000/user/india](http://localhost:3000/user/india)

/user/country\_name/profession/work\_name ‘country\_name’ & ‘work\_name’ are both the IDs. Retrieve the data from the API while it executes the SQL query. eg. [http://localhost:3000/user/usa/profession/billionaire](http://localhost:3000/user/usa/profession/billionaire)

### POST Method

/user\_create To post users in MySql database

## UI Form

[http://localhost:3000/form.html](http://localhost:3000/form.html) GUI form to submit new users. [https://vast-reef-06229.herokuapp.com/form.html](https://vast-reef-06229.herokuapp.com/form.html)

## Tools

Hardware: MacBook Pro 13’ 2015 : Core i5 , 128GB SSD

OS: Mac OS Mojave 10.14.6

IDE: Xcode 11.2.1 VS Code latest patch

Browsers: Firefox Nightly /Dev /Main Safari /Technical Preview Microsoft Edge Dev \( Chromium \)

Writer: iA Writer

Version Management: Github

Task Manager: Things by Cultured Code

Terminal : iTerm

### Authored by : \[Kautilya Save\]

### [GitHub](https://github.com/SensehacK)

