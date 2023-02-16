
## Information

Important difference between how to handle threads while subscribing or working with the UI in RxSwift


## Check thread type

Use default `Thread.isMainThread` in the subscribe block in order to identify whether the thread is Main thread or background thread.

```swift
Observable<Int>.create { observer in
    observer.onNext(1)
 return Disposables.create()
}
.subscribe(onNext: { el in
    print(Thread.isMainThread)
})
```
Code snippet from the article linked below about `ObserveOn` vs `subscribeOn`

## Articles

ObserveOn vs subscribeOn
http://rx-marin.com/post/observeon-vs-subscribeon/

https://swiftsimplified.medium.com/thread-safety-with-subjects-in-rxswift-2543495aa35e


StackOverflow issue
https://stackoverflow.com/questions/58355951/rxswift-not-subscribing-on-main-thread

[RxSwift Multithreading](https://www.thedroidsonroids.com/blog/rxswift-examples-4-multithreading)

[RxSwift Deepcuts](https://academy.realm.io/posts/krzysztof-siejkowski-mobilization-2017-rxswift-deep-cuts/)

## Cross links

[[concurrency_rxSwift]]
[[Observe]]