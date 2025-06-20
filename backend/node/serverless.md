Serverless


## Setup

Setting up the project with AWS nodejs template.

```sh
serverless create --template aws-nodejs --path project_name
```


## Deploy

Deploying your serverless to AWS if its properly configured with the credentials.

```sh
serverless deploy -v
```

## Offline

Start the AWS workstation project locally for testing offline before deploying.

```sh
serverless offline start
```


[Source](https://medium.com/hackernoon/a-crash-course-on-serverless-with-node-js-632b37d58b44)