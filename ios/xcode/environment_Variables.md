## Environment Variables


Setting environment variables on the project and reading from them via Xcode.

### Setting variables
```export TEST_RUNNER_QAENV=EnvironmentQA1```

[xcode build Env variables](https://stackoverflow.com/questions/40722756/passing-arguments-to-ios-tests-with-xcodebuild)

### Removing Environment variable

`unset variablename` 

https://www.cloudbooklet.com/how-to-set-list-and-remove-environment-variables-in-linux/

Recent updates I believe from Xcode 12.5 gives an option for xcode-build-cli to be able to import the `Environment variables` of the host environment. 
Which leads to good opportunities towards getting xcode work in tandem with various CI/CD providers to have different `SWITCH` | `A/B Behavior` on dev environments locally or remote servers running the build commands.


You would need to either set the environment variable using 
```bash
export IS_CI_SERVER="false"

// Confirm your environment variable works
echo $IS_CI_SERVER
```

You could also define an `.env` file to source these kind of variables and your project or any kind of host runner needs to include this step as a script before executing the `xcode-build`

```bash
source .env
```


On iOS you can read the environment variable keys | values using this code snippet.

```swift
if let envV = ProcessInfo.processInfo.environment["IS_CI_SERVER"] {
	print("The environment variable \(envV)")													   
}
```



### Issues

While importing the environment variables, sometimes your host terminal environment variables aren't being imported properly. But if you edit the main scheme of the app and append the `Environment variables` to that scheme it would be able to properly import that value. 

But what if you want set it via `CLI` on your host and then xcode test or `xcode-build-test` CLI should appropriately get that file. You would have to specify the value as in Xcode Scheme GUI.
```bash
"IS_CI_SERVER" = ${IS_CI_SERVER}
```

![](app_environment_variable.png)


## Links

https://medium.com/tauk-blog/passing-arguments-and-environment-variables-to-xctests-ebb60e55cece

https://stackoverflow.com/questions/27500940/how-to-let-the-app-know-if-its-running-unit-tests-in-a-pure-swift-project

https://blog.kulman.sk/reading-environment-variables-from-unit-tests/

