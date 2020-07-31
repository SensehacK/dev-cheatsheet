# Connection

## Connection

### Mongo GUI Compass

[Source](https://docs.mongodb.com/compass/current/#compass-index)

// Local Path for Homebrew service start of MongoDB /usr/local/var/mongodb

Custom Parameters with specific DB path and port mongod --dbpath /data/senseDB —port 666

Good explanation of why home-brew has different location path as Apple just has Read only access for Catalina OS. [Source](https://stackoverflow.com/questions/58283257/mongodb-cant-find-data-directory-after-upgrading-to-mac-os-10-15-catalina)

// Dev rough work Of commands history 2 brew services start mongodb-community@4.2 3 mongod 4 ps aux \| grep -v grep \| grep mongod 5 mongo 6 history 7 ps aux \| grep -v grep \| grep mongod 8 sudo chown -R `id -un` /data/db

### Connect and Use MongoDB

To begin using MongoDB, connect a mongo shell to the running instance. From a new terminal, issue the following:

> mongo

## CRUD

