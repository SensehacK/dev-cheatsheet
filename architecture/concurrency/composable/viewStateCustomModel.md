ViewState Model Structs

ViewSuccess

```swift
public struct CustomState: ViewSuccess {
	let canRequestNetwork: Bool
    let tokenExpire: Bool
    var isCustomComponentVisible: Bool { }
}
```


ViewError

```swift
enum CustomErrorState: ViewErrable, Error {
    case existingAccount(email: String, message: String)
    case error(DisplayableError)

    init(error: Error) {
        guard
            let existingAccountError = error as? SignUpViewModel.Error,
            let email = existingAccountError.requestData[Keys.email] as? String
        else {
            self = .error(error.displayableError)
            return
        }
        self = .existingAccount(email: email, message: existingAccountError.message)
    }
 }
```

Custom Loading State

```swift

```