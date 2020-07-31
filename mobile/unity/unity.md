# Config

## Environment

### Incomplete Installation

Disappearing downloading of Unity Hub downloads. 3rd time it worked by following this:

* Just install the standalone unity library. Add packages later when the unity is installed properly.

### Note

If the unity engine is installed manually without the “Unity Hub” then you can’t add modules directly from the Unity Hub.

* Android

  Which makes the android platform setup a bit cumbersome as their  Gradle or Android studio NLK platform has trouble signing + package generation as Mac OS Catalina doesn’t support third party libraries to be signed directly.

  Something of unsigned developer app and opening from system preferences with allowing exception would be needed to achieve the same functionality. To avoid this hoopla you can just utilize unity hub and add Unity older LTS version all via “Unity Hub”

## Scripts

### Script Component Can’t be added

Make sure you name the script the same with your filename. Also make sure console errors are solved, then it can add scripts automatically [SO Link](https://stackoverflow.com/questions/51713497/cant-add-script-component-because-the-script-class-cannot-be-found)

### Game component UIButton

First add the game component by creating an empty object. Then under element inspector, inherit Button class.

By having a global script manager like “ClassNameManager” game object with its child script components. Have their objects linked with other scenes or element object

So that they can appear under “onClick” function for the button class and pass the function name accordingly.

