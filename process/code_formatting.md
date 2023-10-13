# Code Formatting

## Intro

Usually in 21st century we don't need to format our code most of the times as IDEs and code editors which takes north of 1GB RAM space has lot of plugins running in the background which takes care of these trivial formatting issues. But there comes a time when you're editing a `YAML` file or source files where spacing is the deciding factor on some programming / scripting languages that you have to be very mindful of your spaces. 


## Visual Studio Code

I believe opening the config files in Visual Studio Code is usually the best option since it is kind of a light IDE - code editor and has few things in its sleeves to make sure your config file is validated appropriately.

I do recommend installing extensions for different `.fileTypes` since it gives the language processor engine of the file to properly deduce lint errors and source file errors.

Turning on `whitespaces` and `tabspaces` also visually helps where is the extra space in the given file you're editing.

## Validator

Before pushing your config file changes, it is always beneficial to validate it locally and then commit those changes to CI server. Since it saves us lot of resources which includes Network bandwidth, time, space and headaches. Personally it saves me getting anxious till the CI build pushes out a slack `SUCCESS` notification.

I believe Jenkins, GitLab runner and [FastLane](https://docs.fastlane.tools/getting-started/ios/fastlane-swift/) should most probably have some internal function which we can pass the local config file and it will generate the warnings / errors on the terminal for us to address.

## Spell Checker

You can even turn on spell checker on your favorite IDEs. 

### Xcode 

```
Xcode -> Edit -> Format -> Spelling and Grammar -> Check Spelling While Typing
```

### Visual Studio Code

Install a handy extension named [Code Spell Checker](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker)


## End 
Hope this was helpful to some extent

P.S - Are you a tabs guy or a space guy ? Silicon Valley debacle

![Tabs versus Spaces](../assets/59a0ac94867a60973e5e50c75c2b4c6d_MD5.gif)