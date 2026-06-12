# App Environment Variables


Setting environment variables on the project and reading from them via Xcode.

[environment_variables](os/linux/environment_variables.md)

## Xcode

Recent updates I believe from Xcode 12.5 gives an option for xcode-build-cli to be able to import the `Environment variables` of the host environment. 
Which leads to good opportunities towards getting xcode work in tandem with various CI/CD providers to have different `SWITCH` | `A/B Behavior` on dev environments locally or remote servers running the build commands.


## iOS Implementation

On iOS you can read the environment variable keys | values using this code snippet.

```swift
if let envV = ProcessInfo.processInfo.environment["IS_CI_SERVER"] {
	print("The environment variable \(envV)")													   
}
```
[xcode build Env variables](https://stackoverflow.com/questions/40722756/passing-arguments-to-ios-tests-with-xcodebuild)

[Sarunw | setup iOS Environments develop | staging | production](https://sarunw.com/posts/how-to-set-up-ios-environments/)

### Issues

While importing the environment variables, sometimes your host terminal environment variables aren't being imported properly. But if you edit the main scheme of the app and append the `Environment variables` to that scheme it would be able to properly import that value. 

But what if you want set it via `CLI` on your host and then xcode test or `xcode-build-test` CLI should appropriately get that file. You would have to specify the value as in Xcode Scheme GUI.

```bash
"IS_CI_SERVER" = ${IS_CI_SERVER}
"IS_CI_SERVER" = $(IS_CI_SERVER)
```


![](app_environment_variable.png)

### Xcode 13 Release notes

Maybe the syntax has been updated towards using `$(ENV_KEY)` but its such a mess to get `Xcode GUI` + `.env` direct source reference that at that point its better to just provide the xcode cli environment variables 

[More source comment for my run tests on xcode 16.3.0](https://blog.kulman.sk/reading-environment-variables-from-unit-tests/)

> - `xcodebuild` now supports passing certain environment variables to test runner processes. In the environment where `xcodebuild` is invoked, prefix any variable with `TEST_RUNNER_` to pass that variable (with the prefix stripped) to XCTest test runner processes. For example, running `env TEST_RUNNER_Foo=Bar xcodebuild test ...` causes the environment variable `Foo=Bar` to be set in the test runner’s environment. (74104870)

> Additionally, existing variables may be modified using the special token `__CURRENT_VALUE__` to represent their current value. For example, `TEST_RUNNER_Foo=__CURRENT_VALUE__:Bar` appends the string `:Bar` to any existing value of `Foo`. Note that only test runner processes receive these environment variables. To set them in apps targeted by UI tests, customize the `XCUIApplication.launchEnvironment` dictionary prior to launching the app.


## Export .env to Xcode CLI ProcessInfo

```sh
# Example script for the Run Script Phase (assuming .env is in project root)
    # This script will set environment variables that can be accessed by your app
    while IFS='=' read -r key value; do
        if [[ ! -z "$key" && ! "$key" =~ ^# ]]; then
            echo "Setting environment variable: $key=$value"
            export "$key=$value"
        fi
    done < "${SRCROOT}/.env"
```


## xcConfig source env


```yaml
- name: Add variables to xcconfig
  run: |
    echo "API_KEY = ${{ secrets.MY_API_KEY }}" >> MyProject.xcconfig
    echo "BUILD_NUMBER = ${{ github.run_number }}" >> MyProject.xcconfig
    echo "CUSTOM_SETTING = ${{ vars.MY_CUSTOM_VAR }}" >> MyProject.xcconfig
```



## Links

https://medium.com/tauk-blog/passing-arguments-and-environment-variables-to-xctests-ebb60e55cece

https://stackoverflow.com/questions/27500940/how-to-let-the-app-know-if-its-running-unit-tests-in-a-pure-swift-project

https://blog.kulman.sk/reading-environment-variables-from-unit-tests/

