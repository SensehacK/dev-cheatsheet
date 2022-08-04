AutoComplete



Sometimes in Rx World we need to provide some return types for the compiler to make sense of the Rx closure chain or the observable chain.
Swift compiler is pretty nice to work with but few changes in the function implementation sometimes could lead to broken auto complete and errors auto compiling the code while we are typing.


Things to Note: 

To get the type information in the Rx observable chain we need to make sure that the succeeding rx chain should be commented out first in order for the compiler to take auto complete suggestions one step at a time.


Eg.

```swift
let (showSyncAlert, noSyncAlert) = accountRequestSubject
            .mapToVoid()
            .flatMap {  _ in
                return Observable<Bool>.of(true)
            }
```
The `showSyncAlert` & `noSyncAlert` won't be able to parse properly since it is not a tuple. So we need to assign back to just one variable `syncStatus`.
After that we could do a `split()` which 