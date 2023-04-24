

## Purpose

Frameworks have important purposes
- Encapsulation
- Reusability
- Modularization

## Creation

https://www.kodeco.com/17753301-creating-a-framework-for-ios


## Extracting frameworks


Sample project structure for videoKit
https://github.com/SensehacK/swift/blob/master/swiftUI/VideoContent/README.md


## Xcode Build Process

### Static vs Dynamic

Static - unit of codebase linked at compile time. Which doesnt change

Dynamic - binds symbols at runtime execution. Recommended approach to save storage. But has performance costs when the compiler does dynamic linking with `Mach-O` llvm and other process stuff.

### Framework 
It is a bundle of resources. Could include code, assets, bridging headers, documentation, UI code etc. 
In this also you can static or dynamic framework - same concept applies about generating / linking those assets internally. There is always a cost for storage or performance you have to pay with any approach. 

I got on a tangent about software updates in this post. Not fully technical but my thoughts.
[software_updates](software_updates.md)

So which is better ? 
**insert Senior Engineer Meme**:  **IT DEPENDS!**  
 

### Mach - O
`ABI` - `Application Binary Interface`


### Different extensions

`.tld` vs `.dylib` framework libraries embedding in Xcode . 
Linking binaries - embed or just dynamically link it to save space.

More sources around this topic

Apple WWDC 2018 talk

https://developer.apple.com/videos/play/wwdc2018/415/?time=2858

https://www.swift.org/blog/abi-stability-and-more/

https://stackoverflow.com/questions/15331056/library-static-dynamic-or-framework-project-inside-another-project?noredirect=1&lq=1

https://stackoverflow.com/questions/31450690/why-xcode-7-shows-tbd-instead-of-dylib



## Resources

Swift code reuse made simple: packages, modules, libraries - Julia Vashchenko - Swift Heroes 2019
https://www.youtube.com/watch?v=w3QGc8wWTIg