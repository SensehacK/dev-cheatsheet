

## Create

By utilizing property wrapper we can just decorate any variable with `@Pubished` to make it publish-eable

```swift
@Published var someVariable: String = ""
```

UserDefault custom property wrapper example [codable](codable.md)

Note:
Well suited for SwiftUI + Combine.
`willSet` internally it calls so that SwiftUI can make optimizations towards what should be refreshed on the UI when compared directly to `CurrentValueSubject` [subjects](subjects.md)

## Create custom Publisher
[apple doc | publisher](https://developer.apple.com/documentation/combine/publisher)

[building-custom-combine-publishers-in-swift](https://www.swiftbysundell.com/articles/building-custom-combine-publishers-in-swift/)

[lets-build-a-custom-publisher-in-combine](https://thoughtbot.com/blog/lets-build-a-custom-publisher-in-combine)


## Migrating to @Observable

View Model
```swift
import Combine

final class AppSettings: ObservableObject {
	@Published var confirmDeletion = true
}

// VS

import Observation
@Observable final class AppSettings {
	var confirmDeletion = true
}
```

View

```swift
struct SettingsView: View {
  @ObservedObject var appSettings: AppSettings
}

// VS

struct SettingsView: View {
  var appSettings: AppSettings
}
```

[migrating-to-observable](https://useyourloaf.com/blog/migrating-to-observable/)

## Type Erasure 

Just for reference if anyone is reading this one of the fundamental concepts of combine/reactive paradigm when everything is a stream / observable sequence. 

```swift
private let eventSubject = PassthroughSubject<EngineEvent, Never>()


```
When an observable is being initialized (it can be hot / cold) without going to overboard - here because its an `PassThroughSubject` which doesn't require initial value equivalent `PublishSubject` of RxSwift.

```swift
let eventPublisher: AnyPublisher<EngineEvent, Never>
init() {
    eventPublisher = eventSubject.eraseToAnyPublisher()
}
```

```swift
extension EngineEventBus: EventSendable {
    func sendEvent(_ type: EventType, metaData: EventMetaData?, url: URL) {
        eventSubject.send(EngineEvent(type: type, metaData: metaData, url: url))
    }
}
```

But author also has an extension with function to add explicit setters via a protocol `EventSendable` It does contradict sometimes with the purely functional reactive paradigm but this gives us more flexibility in the long run while doing more checks for `sending` values upstream.


[Apple doc reference](https://developer.apple.com/documentation/combine/anypublisher) doesn't make it crystal clear but if its any consolation - Reactive programming is harder to grasp at first level.



PS: Sorry for the long winded comment but I had a tough time wrapping my head around with Reactive programming when I was starting out. So adding this comment for others who are reviewing if that makes even 5% sense is helpful.

## Did Set

When you want to debug the Published properties, you can use `didSet` to get some more insights about the lifecycle of these combine properties.

```swift
@Published private var audioTracks: [AudioTrack] = [] {
	didSet {
		print("didSet \(audioTracks)")
	}
}
```

## Errors

### Cannot convert value of type 'Published<>.Publisher' to expected argument type 'Binding<>'


copied from slack overflow

Not sure why the proposed solutions here are so complex, when there is a very direct fix for this.

Found this answer on a [similar Reddit question](https://www.reddit.com/r/swift/comments/ixqp3m/comment/g68dkrs/?utm_source=share&utm_medium=web2x&context=3):

> The problem is that you are accessing the projected value of an @Published (which is a Publisher) when you should instead be accessing the projected value of an @ObservedObject (which is a Binding), that is: you have `globalSettings.$tutorialView` where you should have `$globalSettings.tutorialView`.


## Reference

Great article about how reactive paradigm works in a way. Touches how we can support pre iOS 13 deployment targets and make use of custom property wrappers to have a temporary migration solution for older devices. Or we can use community adopted RxSwift reactive framework to work with it. Either way this article sheds a light on approaching a problem with 3 different ways which I always prefer when making those architectural decisions.

[published-properties-in-swift](https://www.swiftbysundell.com/articles/published-properties-in-swift/)

[thoughts on number 3](ReadME_thoughts.md)

[Connecting and merging Combine publishers in Swift](https://www.swiftbysundell.com/articles/connecting-and-merging-combine-publishers-in-swift/)

[Core location example](https://brightdigit.com/tutorials/combine-corelocation-publishers-delegates/) 

[how-to-clean-up-resources-when-a-combine-publisher-is-cancelled](https://shareup.app/blog/how-to-clean-up-resources-when-a-combine-publisher-is-cancelled/)
