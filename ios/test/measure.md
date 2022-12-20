# Measure


## Time elapsed

Many times you could benefit from measuring time elapsed when running a certain function in order to have better analytics and work around the efficiency of the so called custom function. To compare previous states around baseline tests and times with the updated Merge Requests or new features having a performance hit towards the implemented feature.

This is aa small snippet of what you could do to test the time differences in seconds.


```swift
let begin : NSDate = NSDate()
print("BEGIN extension")
// Call function
run_custom_function()
// function returns
let end : NSDate = NSDate()
let interval = end.timeIntervalSinceDate(begin)
print("DURATION extension: \(interval)")
```

## Test Coverage

Edit Scheme - Check `Gather Test Coverage` for the products.

https://www.hackingwithswift.com/articles/144/how-to-measure-code-coverage-in-xcode