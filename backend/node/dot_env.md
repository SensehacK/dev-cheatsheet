Dot ENV

## Init

Good way to save all your keys and secrets for making sure that your specific keys won’t be committed to the public git repository.

> npm install dotenv --save


## Create file

Create .env file and save all your key values in that file.

```text
DATABASE_ENDPOINT=east-2.rds.amazonaws.com
DATABASE_USERNAME=admin
DATABASE_PASSWORD=ry436gdg
DATABASE_PORT=666
DATABASE_NAME=database_name
```


## Utilize

You can directly access the environment variables in your function or class in JS and TS.
It automatically gets invoked with the node process.

Access it via
```javascript
console.log(“Your environment key” , process.env.DATABASE_ENDPOINT)
 
```

### Manual Initialization

If you get process.env as undefined value, you should do the following

```javascript
const dotEnv = require("dotenv");
// Initialize
dotEnv.config();

console.log(process.env.DATABASE_USERNAME);
```


## References

Save in “.env” file
Set the production username, password and other parameters which you don’t want to commit to git.

[SO Link](https://stackoverflow.com/questions/22348705/best-way-to-store-db-config-in-node-js-express-app)

[SO](https://stackoverflow.com/questions/44915758/node-process-env-variable-name-returning-undefined)