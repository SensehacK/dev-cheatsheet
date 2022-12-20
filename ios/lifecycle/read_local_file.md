# Read Local Files


## JSON
Reading the file using Bundle Main URL.
[SO](https://stackoverflow.com/questions/24410881/reading-in-a-json-file-using-swift)
```swift

struct Person : Codable {
    let name: String
    let lastName: String
    let age: Int
}

func loadJson(fileName: String) -> Person? {
   let decoder = JSONDecoder()
   guard
        let url = Bundle.main.url(forResource: fileName, withExtension: "json"),
        let data = try? Data(contentsOf: url),
        let person = try? decoder.decode(Person.self, from: data)
   else {
        return nil
   }

   return person
}

```


[Parse Local JSON](https://praveenkommuri.medium.com/how-to-read-parse-local-json-file-in-swift-28f6cec747cf)


[Apple Working with JSON](https://developer.apple.com/swift/blog/?id=37)

https://stackoverflow.com/questions/24410881/reading-in-a-json-file-using-swift