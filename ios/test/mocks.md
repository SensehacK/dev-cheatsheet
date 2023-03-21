Mocks



## Less JSON files

In order to effectively test better without adding more fluff, dependencies and assets you would need to carefully choose your objects or make them mutable or utilize `@testable` into the class/struct code.


MR feedback around unit tests from Jersh - Mentor
```text
i don't think we need to have multiple and nearly identical JSON structures. for the most part, dependencies can usually be built in the code without needing JSON. plus, relying on it and using this strategy won't scale very well because we'll potentially end up with hundreds or thousands of JSON files each with just a small variation in them. and at that point, we'll be spending as much time maintaining JSON files as we will writing actual code
```

## Manual Mocking

http://iosunittesting.com/manual-mocking-swift/

## Resources

http://iosunittesting.com/