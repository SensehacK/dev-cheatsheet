

# String Segregation

## Code Ergonomics

Multi level Nested namespaces -> Direct one level namespace.

Question asked: 

appending the nested enum namespace as a suffix to some variables is good to move forward right?

for Eg.

```swift
enum CreateApp { 
        public static let title
}
```

Usage `String.CreateApp.title`

New Code

```swift
public static let createAppTitle
```

Usage `String.createAppTitle`

Mentor comments answer

only if it's necessary, but in most cases it shouldn't be. the property name really just needs to be the string value with whitespace and diacritics removed. if you follow that algorithm, then you're more likely to prevent duplicate properties and values.

again, the point of this effort is to reduce duplication and promote reusability and discoverability of available user facing strings. so including "where" the value will be used in its property declaration goes against reusability. consider the following example

```swift
public extension String {
  public static let errorCreatingApp = "Error Creating App"
  enum Error {
    public static let createAppTitle = "Error Creating App"
    public enum CreateApp {
      public static let title = "Error Creating App".localized
    }
  }
}
```

they all have the same value, but we should always consider the APIs we're creating/exposing and how developer friendly they are; we call that code ergonomics

```swift
UIAlertController(title: String.Error.CreateApp.title, message: nil, preferredStyle: .alert)
UIAlertController(title: nil, message: String.Error.createAppTitle, preferredStyle: .alert)
UIAlertController(title: nil, message: .errorCreatingApp, preferredStyle: .alert)
```

i'd argue the last option is the most developer friendly

-   since it'd declared directly on `String` as a static property, we can omit the `String` portion of the fully qualified name
-   since the property name is exactly what its value is, the call site reads more naturally and we can easily surmise what text will actually be rendered without needing to go look at the actual property definition
-   since it doesn't mention anything about "where" it's intended to be used and only "what" the actual string is, we're more inclined to reuse it in places other than those deemed to be a "title" or a "description" or whatever and it not feel like we're misusing a simple string value