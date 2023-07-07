
# Swift Types



## Copy on Write (CoW)

Various memory addresses in the debugger to check Copy on Write feature of Swift internal mechanisms.
### Array
```swift
let array1 = [1,2,3]
let array2 = array1
array1.withUnsafeBufferPointer { (point) in
    print("Array1 Address \(point)")
}
array2.withUnsafeBufferPointer { (point) in
    print("Array2 Address \(point)")
}
```
Mutate the array and then it will print a new address for array type. But till there is no mutation there is no extra copy is made internally with swift.
let vs var for compiler optimization by swift language parser.

### Structs

```swift
struct CustomType { let name = "Hello" }
var firstObj: CustomType = CustomType()
var secondObj: CustomType = firstObject
withUnsafePointer(to: firstObj) { print("First \($0)") }
withUnsafePointer(to: secondObj) { print("Second \($0)") }
```
While referencing another structA with StructB there is a copy made only if the value type inner values are changed or only after few seconds the new copy is made. So if we assign the structA object to another object and quickly print out the memory address. It will return same address for the time being but swift will copy the elements of struct in the background and after some delay if you again ask for memory address of structB then it will have new memory address.

You can mutate struct  and check the address after a delay using `DispatchQueue.main.asyncAfter(deadline: .now()+5) { }`



### Examples
Copy on write example.
[Medium](https://medium.com/ne-digital/copy-on-write-in-swift-96357bd6c830)

[Medium Example](https://betterprogramming.pub/understand-copy-on-write-in-swift-5-52a4716165a3)

Good [article](https://medium.com/@lucianoalmeida1/understanding-swift-copy-on-write-mechanisms-52ac31d68f2f) 




## Class and Struct

Classes (reference types) are allocated in the heap, value types (like Struct, String, Int, Bool, etc) live in the stack. See this topic for more detailed answers: Why Choose Struct Over Class?


## Value and Reference types

[Apple docs](https://developer.apple.com/swift/blog/?id=10)
