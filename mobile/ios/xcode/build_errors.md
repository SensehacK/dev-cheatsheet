# Build Errors

## Couldn’t find path for xcconfig pods

* Set the configuration file setting\* "None" for the Pods related target.
* Close the .xcworkspace.
* Run pod install again
* now open and build your .xcworkspace

[SO source](https://stackoverflow.com/questions/27109476/incorrect-path-for-pods-debug-xcconfig-in-xcode)

## Build input file cannot be found

Most probably you have changed the root “Info.plist” file and due to that Xcode haven’t updated its default move location in the Build Settings.

[SO Fix Link](https://stackoverflow.com/questions/52435202/build-input-file-cannot-be-found-swift-4-2-xcode-10-0)

## Build Xcode Target membership

Storyboard Target member should be for iOS screen and not watch storyboard.

[Link SO](https://stackoverflow.com/questions/44429415/illegal-configuration-compiling-ib-documents-for-earlier-than-ios-7-is-no-longe)

## Custom Class Can’t link

Whenever your custom class couldn’t be linked in Xcode and it still throws out the error of “Could not find any information for class named Custom Class”

This thing could happen if you have a habit of moving or segregating project files in different folders or changing locations internally. Usually Xcode should update the reference automatically while building or clean build but its a hit or miss. Closing Xcode, cleaning project or deleting derived data didn’t fix the issue for me.

So you should do the following for Xcode to rebuild its index or cache or linking classes / libraries.

```text
    In the project file explorer (left panel) find the class and right click -> Delete
    Remove reference (do not move to trash as you will lose the class for good)
    Right click on the folder that contained the class -> Add files to ...
    Find the class you just deleted in the file system
```

[SO Source Steps](https://stackoverflow.com/questions/17735182/could-not-find-any-information-for-class-named-viewcontroller)

## Invalid Element name

In storyboard and XIB files when there are merge conflicts or git stash conflicts Xcode couldn’t parse the XML data.

You just need to git diff from the files and open in your favorite text editor to accept the stash change or current change. Save it solving the file conflict.

[SO Link](https://stackoverflow.com/questions/21818821/couldnt-open-xib-file-after-git-pull-invalid-element-name)

## Error: Multiple commands produce

[https://medium.com/codespace69/xcode-10-xcode-11-2-x-error-multiple-commands-produce-4e5ab75558f2](https://medium.com/codespace69/xcode-10-xcode-11-2-x-error-multiple-commands-produce-4e5ab75558f2)

error: module name "" is not a valid identifier 

SWIFT\_ENABLE\_BATCH\_MODE [https://stackoverflow.com/questions/46690619/build-fails-with-command-failed-with-a-nonzero-exit-code](https://stackoverflow.com/questions/46690619/build-fails-with-command-failed-with-a-nonzero-exit-code)

## Failed to set plugin placeholders

[Stack Overflow](https://stackoverflow.com/questions/47344160/failed-to-set-plugin-placeholders-message)

