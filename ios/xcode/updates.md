

## Links

To see all the development tools from Apple's developer source.
https://developer.apple.com/download/all/

[xcodes app](https://github.com/XcodesOrg/XcodesApp/releases/) - multiple xcode app setup




## Xcode 15

### IDE improvements
#### Vision OS simulator added
![](vision_os.png)
![](xrOS_resources.png)
> Side Rant
Consumes too much memory. Need 64GB and M3Max / Ultra chips for smooth sailing since rendering 3D elements needs beefy cpu and lot of VRAM. Look at that SWAP memory usage of 22Gigs and Page Ins of 50MB/s. 



#### Auto completion - refined and faster inits


#### Modular Installs
ABI Application Binary Interface (Swift 5) but slightly related towards adding more independent modules to be installed or managed and not packaged all together. Bundled. (Saves lot of bandwidth) and storage space on resource limited devices. https://developer.apple.com/documentation/Xcode/installing-additional-simulator-runtimes
-

![](xcode14_size.png)
![](xcode15_size.png)

### Package Manager / Dependency improvements
Code Signing section added in inspector
Cant demo this since I don’t know if there’s any `.xcFramework` in our project dependency as an explicit marked via SPM. Maybe `Project_Name` app I can show it but first I would need the project to be locally build on my machine in order to reach to a conclusion.


https://developer.apple.com/documentation/Xcode/verifying-the-origin-of-your-xcframeworks

So SPM 2-way binding cache and comparing checksums also gets transferred over to XCFrameworks. (More secure and more explicit) warnings / dialogs would be presented in Xcode 15 if the code signature don’t match or change or removed

![](xcFramework_signatures.png)



### Xcode Logging/debug improvements
- Show demo of Logging library 

![](xcode_logging_improvements_UI.png)



### Preview improvements

UIKit preview now works like SwiftUI - no need for UIHostingController to wrap the UIKit into SwiftUI then to make it preview-able. 
