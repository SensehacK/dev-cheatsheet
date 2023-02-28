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


## Error Parsing JSON

### Error Domain=NSCocoaErrorDomain Code=3840 "Badly formed object around

This could be due to your object or its value doesn't conform to proper primitive types like `INT, Bool, String, Date, ExpressibleByNilLiteral`.

Sometimes a JSON object described below
```json
{
	"key1": "Value"),
	"key2": "Value2"
}
```
Might have extra `)` or `}` or `"` value in that JSON file.

### Error Domain=NSCocoaErrorDomain Code=3840 "Something looked like a 'null' but wasn't around line

This could be due to your object or its value doesn't conform to proper primitive types like `ExpressibleByNilLiteral`.

Sometimes a JSON object described below
```json
{
	"key1": nil,
	"key2": null
}
```
Might need to swap the `nil` with `null` type for JSON parsing to work. Maybe because JSON doesn't have `nil` defined and it has equivalent `null` type.
