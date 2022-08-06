---
description: Readme file of my mongo db experiences
---

# Mongo

## List

[[connection]]

## Setup

### Mac

Commands install MongoDB using Home-brew, less overhead of configuring and pointing the right directories in the development workstation environment.

[Source](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-os-x/)

Tap command maybe just adds mongoDB script or repo to the home-brew. I’m clueless what this command does. But official docs mention to use this command first.

> brew tap mongodb/brew

Install MongoDB

> brew install mongodb-community@4.2

Run services start

> brew services start mongodb-community@4.2

Use this to check if mongo service is running

> ps aux \| grep -v grep \| grep mongod



