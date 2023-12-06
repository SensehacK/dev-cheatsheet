# Software Updates

## Intro

This piece is quite opinionated from point of view. No way this is scientific or academic. So take it with a grain of salt or a glass of Whiskey talk speaking.
But none theless enjoy my thought process around Software updates in general.

## Process

Part of the reason Apple updates are huge, since they repackage it again for each release. Microsoft updates and other linux distros have a great pipeline saving the world thousands of network storage and throughput for every time there is an update. 

Google even though they are fragmented with their android ecosystem , their app architecture for providing new updates is phenomenal with delivery smaller chunks of data being changed and quickly linking them appropriately. It is slower but cost effective for countries with lower bandwidth or lower storage options. Sometimes Android after updating the OS, triggers these kinds of processing of linking dynamic dependency chains in the background. `Preparing android system` message in your notifications. 

Xbox on the other hand provides both options for game developers to push updates. Microsoft always was great back from the Windows 2000 ME, and XP editions with service packs v1, 2 and 3 for major OS updates as well keeping up security updates in a manageable fashion. Back when OTA (Over the Air) updates weren't the norm. Remember you had to use 3 - 5 Floppy disks to install an OS. Now even though you have installed the OS, there are still day one patches for new OS. Thus leading to SaaS (Software as a service) model. 

They can defer prioritization and just ship things when its important to beat the market.

One could argue that this leads to poor software quality but others mention that software needs to be soft easily adaptable and following latest patterns or security mechanisms. So having SaaS is a boon for lot of less maintenance. 
As a fellow engineer, the code I wrote yesterday is already obsolete and the code I'm writing is also in the same phase. So updates are good if done in a timely fashion and not too much force updates. Auto updates are also cool.


## Other

ABI - consideration
ABI Stability is very crucial when delivering different executables or packaging libraries or modules of code to be reusable and frozen.
I'll share some reference links to read about it.
[Difference between API and ABI](https://stackoverflow.com/questions/3784389/difference-between-api-and-abi/59270667#59270667)

[Swift ABI v5.0](https://stackoverflow.com/questions/58654714/module-compiled-with-swift-5-1-cannot-be-imported-by-the-swift-5-1-2-compiler/63305234#63305234)

[Official swift ABI](https://www.swift.org/blog/abi-stability-and-more/)



## Dark UX Pattern

Mac OS upgrades & don't get me started on how Windows 10 handles force upgrades ever since Windows 8.
[upgrade](ios/config/upgrade.md)


## OS

[windows updates](disable_updates.md)

[macOS updates](ios/macOS/updates.md)

[Xcode updates](ios/xcode/updates.md)

[release](process/release.md)

## References




ABI Stability Manifesto Swift
https://github.com/apple/swift/blob/main/docs/ABIStabilityManifesto.md

What is ABI Stability
https://medium.com/@deekshithbellare/what-is-abi-stability-and-why-does-it-matter-48c918554be1

Stack Overflow
https://stackoverflow.com/questions/2171177/what-is-an-application-binary-interface-abi

Android docs
https://source.android.com/docs/core/architecture/vndk/abi-stability

https://www.dpdk.org/blog/2019/10/10/why-is-abi-stability-important/


https://faultlore.com/blah/swift-abi/

https://libcxx.llvm.org/DesignDocs/ABIVersioning.html

LLVM official video
https://www.youtube.com/watch?v=MgPBetJWkmc


https://www.donnywals.com/what-is-module-stability-in-swift-and-why-should-you-care/