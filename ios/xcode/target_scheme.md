# Target Scheme
## Information

Plain language meaning post from Stack Overflow

## Workspace 

Contains one or more projects. These projects usually relate to one another

## Project 

Contains code and resources, etc. (You'll be used to these!)

## Target

Each project has one or more targets.
- Each target defines a list of build settings for that project
- Each target also defines a list of classes, resources, custom scripts etc to include/ use when building.
- Targets are usually used for different distributions of the same project.
        
    - For example, my project has two targets, a "normal" build and an "office" build that has extra testing features and may contain several background music tracks and a button to change the track (as it currently does).
    
    - You'll be used to adding classes and resources to your default target as you add them.
    - You can pick and choose which classes / resources are added to which target.
                In my example, I have a "DebugHandler" class that is added to my office build
    - If you add tests, this also adds a new target.


## Scheme

A scheme defines what happens when you press "Build", "Test", "Profile", etc.
 - Usually, each target has at least one scheme
 - You can autocreate schemes for your targets by going to Scheme > Manage Schemes and pressing "Autocreate Schemes Now"


[target-and-scheme-in-plain-language](https://stackoverflow.com/questions/20637435/xcode-what-is-a-target-and-scheme-in-plain-language?rq=1)


## Multiplatform Target 

Creating few visionOS and iPad targets to make it easier for testing and development is very important for initial stages.
Definitely needs to have some caveats added for migration and checks in place for different platforms.

Having the wildcards is important sometimes to differentiate those things overall.


## Scheme No Devices

So sometimes Xcode has trouble finding the right target destination to build against for the selected scheme. Give it some time and if its SPM integrated xcode project you can refer this section [refs/remotes/origin](/ios/xcode/spm_errors#origin%20not%20found).
Make sure 

``