

## Array


```swift
// Even Odd example
let arr = [1, 2, 3, 4]
let evens = arr.filter { $0 % 2 == 0 }
print(evens)
```


```swift
print("\n Using Filter")
let filterDynamicRecordFields = arrFields.filter { $0.hasDynamicRecordId }
print(filterDynamicRecordFields)
```




## NS Predicate



```swift
let thisSection = 1
let thisPredicate = NSPredicate(format: "sectionNumber == \(thisSection)")
```

[NSPredicate | SO](https://stackoverflow.com/questions/31884863/swift-how-do-i-create-a-predicate-with-an-int-value)


```swift
let dataSource = [
    "Domain CheckService",
    "IMEI check",
    "Compliant about service provider",
    "Compliant about TRA",
    "Enquires",
    "Suggestion",
    "SMS Spam",
    "Poor Coverage",
    "Help Salim"
]
let searchString = "Enq"
let predicate = NSPredicate(format: "SELF contains %@", searchString)
let searchDataSource = dataSource
.filter { predicate.evaluate(with: $0) }
```

`predicate.evaluateWithObject`

You will get (playground)

comparing decimal-integer vs double? 

[ibn | definition decimal-integer](https://www.ibm.com/docs/en/i/7.3?topic=literals-decimal-integer)

> BANDWIDTH 
> The value is a decimal-integer of bits per second.  It represents the peak segment bit rate of the Variant Stream.

[hls rfc](https://datatracker.ietf.org/doc/html/rfc8216)


`SELF`
[Literals in Predicates](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/Predicates/Articles/pSyntax.html)

> The `%@` will be instantly recognizable to anyone who has used Objective-C before, and it means "place the contents of a variable here, whatever data type it is." In our case, the value of `filter` will go in there, and will do so safely regardless of its value.

[HWS | NSpredicate](https://www.hackingwithswift.com/read/38/7/examples-of-using-nspredicate-to-filter-nsfetchrequest)


Multiple arguments

```swift
var predicate = NSPredicate(format: "key1 = %@ AND key2 = %@", value1, value2)
```


Compound Predicate for multiple predicates


