

# Test LifeCycle 



## Diff between `class func` vs `func`

`class` gets called only once when the class is initialized.

`func` gets called every time  a test case is initialized.

```swift
override class func setUp() { }

override func setUp() { }
````





## Sample Code


```swift
import XCTest
@testable import TestCaseLifecycle

class TestCaseLifecycleTests: XCTestCase {

//    This code is based on Apples' documentation https://developer.apple.com/documentation/xctest/xctestcase/understanding_setup_and_teardown_for_test_methods
    
    override class func setUp() { // 1.
        super.setUp()
        // This is the setUp() class method.
        // It is called before the first test method begins.
        // Set up any overall initial state here.
        print("LOG: Class setup")
    }
    
    override func setUp() { // 2.
        super.setUp()
        // This is the setUp() instance method.
        // It is called before each test method begins.
        // Set up any per-test state here.
        print("LOG: instance method setup")
    }
    
    func testMethod1() { // 3.
        // This is the first test method.
        // Your testing code goes here.
        print("LOG: test method 1")
        addTeardownBlock { // 4.
            // Called when testMethod1() ends.
            print("LOG: teardown block test method 1")
        }
    }
    
    func testMethod2() { // 5.
        // This is the second test method.
        // Your testing code goes here.
        print("LOG: test method 2")
        
        addTeardownBlock { // 6.
            // Called when testMethod2() ends.
            print("LOG: first teardown block test method 2")
        }
        addTeardownBlock { // 7.
            // Called when testMethod2() ends.
            print("LOG: second teardown block test method 2")
        }
    }
    
    override func tearDown() { // 8.
        // This is the tearDown() instance method.
        // It is called after each test method completes.
        // Perform any per-test cleanup here.
        super.tearDown()
        print("LOG: instance method tearDown")
    }
    
    override class func tearDown() { // 9.
        // This is the tearDown() class method.
        // It is called after all test methods complete.
        // Perform any overall cleanup here.
        super.tearDown()
        print("LOG: Class tearDown")
    }
}
```

Code snippet source http://trikalabs.com/xctestcase-lifecycle/

## Resources


https://www.waldo.com/blog/xctest-setup

https://developer.apple.com/documentation/xctest/xctestcase/set_up_and_tear_down_state_in_your_tests

https://qualitycoding.org/xctestcase-teardown/