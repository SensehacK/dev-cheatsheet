# Dynamic Environment

We can achieve different environment variables and behaviors by checking our environment status in run time and append or alter our app behavior depending on what was been passed at launch. We can utilize property list or add a subgroup API layer which will orchestrate the app’s behavior to a certain extent. There is no limit to how much dynamic behavior we can have.

## Presumption
We are presuming that .dotEnv file would be already been setup by the developer for  storing our environment status.


```text
APP_ENVIRONMENT=develop
```
That could range to different cases depending on your project requirements.
1. develop
2. production
3. qa
4. a/b testing



## Utilization

```javascript

// Function for dynamically setting different perspective.
function setupEnvironment() {
	// Setup environment accordingly.
	if (process.env.APP_ENVIRONMENT == "develop") {
		console.log("develop build");
		return pool;
	} else if (process.env.APP_ENVIRONMENT == "production") {
		console.log("PROD build");
		return pool_aws;
	}
}


```