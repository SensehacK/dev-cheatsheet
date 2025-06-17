# Notification Center









## didSet 

```swift
class MockAVPlayItem: AVPlayerItem {
    nonisolated(unsafe) private var _status: AVPlayerItem.Status = .unknown
    override dynamic var status: AVPlayerItem.Status {
        set(newStatus) {
            willChangeValue(for: \.status)
            _status = newStatus
            didChangeValue(for: \.status)
        }
        get {
            return _status
        }
    }
}
```
status property is overridden which can be modified & new changes reflects in KVO


```swift
 self.playerItem = MockAVPlayerItem(url: testUrl)
        self.player = MockAVPlayer()
        self.bus = EngineEventBus()
        player.replaceCurrentItem(with: playerItem)
        self.observer = AVPlayerObserver(url: testUrl,
                                         player: player,
                                         playerItem: playerItem,
                                         telemetry: bus)


 func testPlayerItemReadyEvent() {
        let expectation = self.expectation(description: "Receive Player Item Ready To Play Event")
        subscription = bus.events
            .filter { $0.type == .playerItemStatusChanged }
            .sink { event in
                // filtering out for desired event type here
                guard event.data?.playerItemStatus == .readyToPlay else { return }
                expectation.fulfill()
            }
        playerItem.status = .readyToPlay // deliberately update player item status
        wait(for: [expectation], timeout: 3.0)
    }
```


## Notification Center
```swift
func testPlayerItemReadyEvent() {
        let expectation = self.expectation(description: "Receive Player Item Ready To Play Event")
        subscription = bus.events
            .filter { $0.type == .playerItemTimeJumped }
            .sink { event in
                // filtering out for desired event type here
                XCTAssertEqual(event.url, self.testUrl)

                expectation.fulfill()
            }

        NotificationCenter.default.post(name: AVPlayerItem.timeJumpedNotification, object: player.currentItem)

        wait(for: [expectation], timeout: 5.0)
    }
```