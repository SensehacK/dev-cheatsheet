
## Package 

Different Targets accessible could result in certain classes or packages to be only importable when they have set the target to be build with internally.
I don't know how compiler or llvm compiler does linking internally but if its a dynamic library or framework you would have to specify its build dependency or specify which targets or scheme it should build against.

## Bundling 

When bundling you would have different call site depending on the Modules defined within the product. This below link defines how it works with SPM but I'm also quite new to it.
[spm](spm.md#Bundling)

## Access Control

Swift iOS Access Control options

- File private
- private
- public
- internal


## Importing NPM

Use NPM package in iOS Swift

https://medium.com/the-smyth-group/how-to-use-npm-packages-in-native-ios-apps-9af7e31d8345