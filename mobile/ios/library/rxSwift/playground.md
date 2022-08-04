# Playground


## Build

- Open your terminal of choice and navigate to the repository. For our easy example we will start with `Subjects`. `cd` into that folder and `RxPlayground` as well.
- Run the shell script `bootstrap.sh` from the terminal
- Command to run `./bootstrap.sh`
- This script will download the library and appropriately bind the framework to the Playground for easy prototyping with less overhead compared to a normal xcode project.

## F.A.Q.s

- The RxSwift library not found error `No such module 'RxSwift'`. Could be fixed by selecting `Build Active Schemes` in the project inspector ( Right side menu ).

- RxRelay or Cocoa elements not building. This could be fixed by selecting the appropriate library / framework in the project build tools and first build it and then go back to the playground for clean building so this time it picks up the appropriate references.
