# It Depends

I can't count the number of times I have to say `It Depends` when asked in a meeting with non technical people to implement certain feature or functionality or approach a new project with all the requirements.
But rather than poking fun at anything since everyone is good at what they do and we can't expect anyone to know something which they aren't familiar with. 

This is my list of things I always consider when I go through my mental gymnastics of when I say `It Depends and in order to get you a concrete answer I would need to block some time on my calendar to really explore all options and come up few different approaches` 

I do love architecture in general and understanding how when making a certain technical decision what things were being considered and tradeoffs being made in those choices we make and  assumptions we pass on.

So below is in non sorted order is my brain dump of why I believe it would depend.





## Right Data Structure

Know the right data structure to choose from when you're assuming how the app architecture is leaning towards modularization, concurrency heavy or just thin clients.
The right data structure also comes into picture when you're deciding whether to allocate chunks of memory and just link it using linked list or doubly linked list. Arrays and list always are directly accessible by the nth element.
Dictionary has a O(1) access time but there is a cost towards that constant time. Everytime there is a new value added to the dictionary, the internal mechanism goes through creating a unique enough key to uniquely identify the address in the table it needs to jump in and then access the value which points to the memory address or storage address where it stored the data blob. 
Would add more info in [swift data structure post](data_structure)


## Hardware acceleration

Of course computers of current era have multiple hardware level decoders, accelerators and engines which only does one thing and have been optimized to do that task very efficiently so we won't noticed all those performance issues. But remember when h264 or h265 video decoding support wasn't hardware accelerated 5 - 8 years back on mobile phones, laptops and CPU used to take care of it. It used to throttle a lot of lowered powered devices. If there is enough applications need for anything the CPU manufacturers or chipset designers will just add the hardware accelerated modules in the chipset since they are already surpassed the moore's law as well as now they are on 5nm or 3 nm chipset die process. So it leaves us with lot of space to add more accelerated modules.

#### Covid / Market drives innovation

Before pandemic laptops never had hardware accelerated chipsets which supported `blur video backgrounds`, `noise isolation` and all these good features on iPads, iPhones, Macbooks or PC AMD/Intel x86 - amd64 based processing chips. But in pandemic Covid19 everyone started to notice while having video chat applications, sharing screens they were taking 30 - 45% performance hit while doing their actual jobs / tasks. So quickly manufacturers started adding these video decoding, audio signal processing accelerated modules in their next generation of processors. Of course they will also show statistics that they are 20 - 40 % better than their predecessor but if you look carefully they are only a leap improvements in only certain things which they have added hardware accelerated modules to their CPU die/dye chipset.
Apple's transition from Intel x86 based CPUs to ARM architecture M1 & emulation of x86 using Rosetta v2 was a monumental shift in processing power. Like the time when 8086 chipset was revealed from 4 bit to 8bit, 16bit and 32 bits. Then amd64 invented the 64 bit processor back in 2003 or 2006. Next time there was a cpu innovation was integrated GPUs in CPUs and apple made the switch from 32bit to 64bit architecture on their iPhone/iPad chipsets named `A9, A10`.. etc. Also Apple switched from Power PC (IBM) to Intel back in 2008 I believe because Intel's power per watt performance was way ahead of IBM's powerPC. It greatly benefitted the macbooks. AMD Threadripper and Ryzen chipsets are also great improvement recently for normal PC x86 based architecture. Enterprise computers also have on disk encryption modules and chipsets with hardware level decryption/encryption support in order to have secure data on their devices.


## Communication Pattern

It would also affect how the application communitcation pattern is being deployed internally.
It is observer pattern, closure based, delegates or fully reactive.


## Scalability

You need to consider the trade offs between storage needs, latency and throughput as well.

Loadbalancer balancing out the user requests and routing it to appropriate servers and keeping track of it internally.


## Hashing 

Hashing solves lot of problems and it takes smaller performance hit at the time when it is initialized or changed everytime but the cost is negligible for its applications where your architecture has constant need to reads from I/O to get status updates or polling of data for changes or displaying / reading data every `n` of times.

Great hashing algorithms solve the problems of collision and makes it easier for the consumer to have a trully unique ID to reference in a given context.
This guarantees faster checks of huge data by just running checksums and quickly identifying what changed and what not. Great performance boost in most cases.


## Reusability

Apple has perfected the reusability aspect of User interface when scrolling on an iOS device. It was always smooth and there were no jitteryness or hiccups while scrolling. Part of the reason is iOS relies on OSX which internally relies on NS ( NeXT ) OS company. The foundation was great to begin with, and the way apple handles dequeing and reusing the same cell when the cell or UI component goes out of screen boundaries on low powered, cpu bound devices back in 2007 - 09 was genius.


## Concurrency

Making imperative code in reactive code is nice until the application becomes big and we slowly start seeing side effects. Which we can't properly debug and then again resort to waiting for async calls to complete and thus make tasks async but the execution serial or signal bounded. These problems are really hard to debug and having core foundation about how internally OS does scheduling of tasks, processes, threads and exclusive access would further help write better sustainable and easy to debug codebase. 
Easier said than done.
Usually optimization of serial execution to concurrent execution or async should come after we have identified the mutual relations or exclusive containerization of dependency graph of our modules. Very important to not just chase concurrency in the name of doing it for the right thing. It does involve quite a bit of planning and clarity from consumer and publisher side of things. Or else unintended effects could be seen in most of the applications we are writing to make our lives easier.

OS IDE tools now offer lot of checks like `Thread Sanitizer`, `Main Thread Checker`, `Race conditions`, `Mutability state checking` and lot of other tools which can just gather lot of telemetry data related to the debug application. 



## Encryption

Usually the OS offers us lot of core solutions to tackle this problem. I have very few things to add on this topic.

But consulting with a security engineer is a must for any application which deals with financial or Personally Identifiable Information or classified information. 

SSL pinning, cryptography, code signing, certificates, public - private key infrastructure. Lot of things to consider. 


## Design Pattern

Design patterns in mobile app development usually comes is MVC, MVVM, MVP, VIPer etc. The architecture of the mobile app constitues of networking, caching, data management, application states, caching, analytics, third party libraries etc. Design pattern just establishes how a certain module which could be UI related is communicating with its own view state, viewmodel and data model. Invoking those state and interacting with other aspects of the app is totally different.



## Technology Stack


## Tech Debt

When I was starting with my career as a software engineer, I always used to consider tech debt as a no brainer. Since if there is a debt in the SDLC we should address it in subsequent releases. Well it was easier said than done. Tackling tech debt requires a monumental shift in release planning and management should also be ready to invest in those decisions. Since it is a collective effort of prioritizing new features or perfecting existing functionality or addressing bugs. It is a common problem and it fits perfectly with the `333` Trifecta prioritization problem. 
