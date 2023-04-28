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


## JSON Codable helper

Small Extension helper with Codable

### Code

```swift
```swift
enum JSONParseError: Error {
    case fileNotFound
    case dataInitialisation(error: Error)
    case decoding(error: Error)
}
**
extension Decodable {
    static func from(localJSON filename: String,
                     bundle: Bundle = .main) -> Result<Self, JSONParseError> {
        guard let url = bundle.url(forResource: filename, withExtension: "json") else {
            return .failure(.fileNotFound)
        }
        let data: Data
        do {
            data = try Data(contentsOf: url)
        } catch let error {
            return .failure(.dataInitialisation(error: error))
        }

        do {
            return .success(try JSONDecoder().decode(self, from: data))
        } catch let error {
            return .failure(.decoding(error: error))
        }
    }
}
```
Source
https://stackoverflow.com/questions/24410881/reading-in-a-json-file-using-swift

### Usage 

For SwiftUI easier local json testing.
```swift
struct UserCellView: View { }

static var previews: some View {
	switch User.from(localJSON: "user") {
	case .success(let value):
		UserCellView(user: value)
	case .failure(_):
		Text("No Data loaded")
	}
}
```


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
