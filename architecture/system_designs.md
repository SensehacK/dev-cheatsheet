# System Designs

## Intro

System design is very much a way to express your architectural designing skills in order to give high level picture of the system and express the foundation of the app or product you're building. It defines the initial contract Input / Output for any components in the system design architecture of how orchestration is taking place between different agnostic systems.

Below is my list of factors which I consider when designing a system.

## Scope 

Defining scope is very important to begin with.

### Deployment

Is the app just on Mobile or would be it multi platform like watchOS, iOS, iPadOS, macOS, Carplay.
Is orientation important.
What is minimum target OS version and hardware we are targetting.

Do we want to promote reusability of UI components? 

Do we also want shared business logic with multiplatform for Swift based apps or would it be also supported for Android or other OS.

Is the product based on shared login credentials. Like a Google workspace or Microsoft Office suite login options.

### Time

Is there a project deadline ?

Are we targetting a release data or market to beat ? 

How many resources are available in parallel.



## Roadmap

If the app is planned to be supported for ESR ( Extended Support Release ) for enterprise products or it is constantly evolving. 
Is force upgrade or API contract obsolete. Poison pill ? Force upgrade apps. 
Bad UX ? or drive for users to consume more of the app.
### Usage

### Target Audience

Is it aimed at certain demographic ? 

Is there an MVP (Minimum Viable Product)

## Security

Is the app open for anyone to consume ? Free trials sign ups

Login Credentials would be just passed and token would be stored on Keychain.

Banking app ? Man in the middle attacks prevention. SSL pinning.


## Network 

What is the network API threshold ? 

Are we supporting Offline architecture

Do we limit API networking -> caching policies ?

CDN - > load balancer to keep the response time faster.

Is the app media heavy ? No SQL or media driven data backed store options. Also defining the caching policy, image specific resolutions. 

Is the backend owned by us ? Or hosted on third party services. Pricing could be a factor.

Pagination supported ? Is it static based data or very dynamic ? -> We can utilize for dynamic keypaths for pagination.

Network Reachability -> Spotty network -> UX defining low internet zones with cache data, app shouldn't automatically switch to different screen or refresh the app. No data / user flow should be lost. Small UI `new data is available`

Prefetching - collections view - images or lists. Cancel old tasks if the User scrolled past that screen.

Background downloads - syncing - 

Network JSON / API contract definition.

## Product led growth

Are we experimenting with the app for different flows>? 
A/B Testing.

[Server driven UI | OTA](over_the_air.md)

Event driven App updates for specific time of the year.

Analytics loosely coupled managers -> So they can be swapped depending on our preferences.



## Implementation

###  UI Communication Design pattern

MVC ? -> Just Proof of concept ( POC ) or smaller project

MVVM -> Big team -> testable code ? 
VIPER ??? RIBs  - company specific ideas to be transferable ? 


### Storage

Caching in memory >? Or slow storage options
Should we prioritize device memory ? Proportional to the available disk space.

Cache invalidation policy. How often should we clean the app.
Only cache things which are core feature of the app ? Or most used app or most data driven UI or most performance intensive app.


## Single Source of Truth

Session Coordinator or Global App Session Coordinator

Different source of truth
- Network API 
- Cache / Database Online
- Offline

### Data Overriding strategies? 
Merge timestamp and override data ? 

## [Design Tools](/tools/apps.md#Design)
## Implementation

[iOS Swift equivalent WIP docs](/ios/library/API_design.md)

## Good articles to read

[Right Data Structure](https://www.swiftbysundell.com/articles/picking-the-right-data-structure-in-swift/)

[themobileinterview | cracking-the-mobile-system-design-interview](https://themobileinterview.com/cracking-the-mobile-system-design-interview/)

[medium | system-design-interview-for-mobile-engineers](https://medium.com/geekculture/system-design-interview-for-mobile-engineers-ce712d6ac2c1)
## Resources

[hello interview | system design - core concepts](https://www.hellointerview.com/learn/system-design/in-a-hurry/core-concepts)

[techinterview handbook | system-design](https://www.techinterviewhandbook.org/system-design/)