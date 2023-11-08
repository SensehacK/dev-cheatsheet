# Docker Commands

## Deleting images

Source : [Link](https://techoverflow.net/2013/10/22/docker-remove-all-images-and-containers/) Problem:

You use Docker, but working with it created lots of images and containers. You want to remove all of them to save disk space.

Solution:

Warning: This will destroy all your images and containers. There is no way to restore them!

Run those commands in a shell:

```text
docker rm $(docker ps -a -q)
docker rmi $(docker images -q)
```

This solution has be proposed by GitHub user @crosbymichael in this issue

In case you want to delete even those images that are referenced in repositories, use

```text
docker rmi $(docker images -q) --force
```

Background information:

You can see the containers on your computer using

```text
docker container ls
```

When we tell docker to show us all images currently listed on the computer:

```text
docker image ls -a
```

Inspecting the containers info

```
docker inspect <container name/id>
```


Deleting docker containers

```
docker run -d nginx
```

https://www.educba.com/docker-delete-container/


## Cache control

https://forums.docker.com/t/how-to-delete-cache/5753

https://stackoverflow.com/questions/35134713/disable-cache-for-specific-run-commands

Particular cherry picked commit docker
https://stackoverflow.com/questions/70415746/how-to-checkout-at-particular-commit-in-dockerfile