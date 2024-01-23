# Objective C syntax
## Intro

Objective-C was a language introduced by apple for developing software on OS X and iOS, apple platforms.

## Syntax

Add `;` to every line like the old days of C, C++ days.

### Print statement

```objc
printf("Hello World");
```

In Objective C:

```objc
NSLog(@"Hello, World!");
```

In Objective C with variables:

```objc
NSString * myString = @"Hello World";
NSLog(@"%@", myString);
```

String Array

```objc
NSString *allEvents = [[event.sourceStates valueForKey:@"name"] componentsJoinedByString:@", "]] 
```

Array 
```objc
@property (nonatomic, copy, readwrite) NSArray *sourceStates;
```


Set ?
```objc
@property (nonatomic, strong) NSMutableSet *mutableStates;
```

Computed Property? 
```objc
- (NSSet *)states
{
    return [NSSet setWithSet:self.mutableStates];
}
```

Function

```objc
- (void)setCurrentState:(CustomState *)currentState
{
}
```

Boolean

```objc
return NO 
return YES
```


Pointers
```objc
- (BOOL)fireEvent:(id)eventName uInfo:(NSDictionary *)uInfo error:(NSError *__autoreleasing *)error
{
	if (error) *error = [NSError errorWithDomain:TKErrorDomain code:TKInvalidTransitionError userInfo:userInfo];

	return NO;
}
```

Dictionary

```objc
NSString *failureReason = [NSString stringWithFormat:@"An attempt was made to '%@' while in the '%@'", event.name, self.currentState.name;

NSDictionary *userInfo = @{ NSLocalizedDescriptionKey: @"The event cannot be fired from the current state.", NSLocalizedFailureReasonErrorKey: failureReason };
```