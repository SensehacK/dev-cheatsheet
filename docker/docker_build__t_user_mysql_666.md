docker build -t user-mysql-666 .

docker run  -d \
--publish 3306:3306 \
--volume=/Users/SensehacK/Documents/GitHub/nodejs/mysql/data:/var/lib/mysql \
--name=user-mysql-img-666 user-mysql-666


docker build -t user-nodejs-666 .

docker run  -d \
--publish 3000:3000 \
-e MYSQL_USER='root' \
-e MYSQL_PASSWORD=‘your_password’ \
-e MYSQL_DATABASE='node_js' \
-e MYSQL_HOST='172.17.0.2' \
--link user-mysql-img-666:db \
--name=user-nodejs-img-666 user-nodejs-666







docker run  -d \
--publish 3000:3000 \
-e MYSQL_USER='root' \
-e MYSQL_PASSWORD='your_password' \
-e MYSQL_DATABASE='node_js' \
-e MYSQL_HOST='172.17.0.2' \
--link user-mysql-img-666:db \
--name=user-nodejs-img-888 user-nodejs-777