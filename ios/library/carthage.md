
## Working

Carthage leaves the linking part to end user and just generate the frameworks or libraries. It makes sure that it gets cloned and build. After that the developer can have scripts which can do copy commands to get all the dependencies to the appropriate folder in `Xcode_project_name_folder/Frameworks`

## Note

I do believe that the community has moved away from Carthage in general to either Cocoapods or Swift Package manager.

## Error

```bash
A shell task (/usr/bin/env git fetch --prune --quiet [https://github.com/ephread/Instructions.git](https://github.com/ephread/Instructions.git) refs/tags/_:refs/tags/_ +refs/heads/_:refs/heads/_ (launched in /Users/GALSIV/Library/Caches/org.carthage.CarthageKit/dependencies/Instructions)) failed with exit code 1
```

Just clear the carthage cache 

```bash
rm -rf ~/Library/Caches/org.carthage.CarthageKit
```

https://github.com/Carthage/Carthage/issues/443