# docker\_build\_\_t\_user\_mysql\_666

docker build -t user-mysql-666 .

docker run -d  --publish 3306:3306  --volume=/Users/SensehacK/Documents/GitHub/nodejs/mysql/data:/var/lib/mysql  --name=user-mysql-img-666 user-mysql-666

docker build -t user-nodejs-666 .

docker run -d  --publish 3000:3000  -e MYSQL\_USER='root'  -e MYSQL\_PASSWORD=‘your\_password’  -e MYSQL\_DATABASE='node\_js'  -e MYSQL\_HOST='172.17.0.2'  --link user-mysql-img-666:db  --name=user-nodejs-img-666 user-nodejs-666

docker run -d  --publish 3000:3000  -e MYSQL\_USER='root'  -e MYSQL\_PASSWORD='your\_password'  -e MYSQL\_DATABASE='node\_js'  -e MYSQL\_HOST='172.17.0.2'  --link user-mysql-img-666:db  --name=user-nodejs-img-888 user-nodejs-777

