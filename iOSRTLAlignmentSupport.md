# Reusable component for Text Alignment

## Prerequisites

* Xcode IDE
* Mac OS
* iTunes
* iOS Device

## Creation

### Step 1

Use the singleton class file where it is imported everywhere in the project. For my example, I have "Utility.m" in objective C.

#### Utility class

`code()`

    Markup :  `code()`

```objective-c.
//**AR
//Moving generic method here to use Singleton feature
//This is just calling TranslationDashboard method
-(NSInteger)getAlignment{
    return [[TranslationDashboard sharedManager] getAlignment];
}
```

### Step 2

Invoke the class once to get the data from the server in the app life cycle.

#### Business Logic class

```objective-c.
//**AR
    [translationDashboard appAlignment];
//AR
```

### Step 3

Create a different class which handles all of your data parameters from restful services in middleware or back end services.
Use the API json data to persist the data throughout the application or maybe store it in constant variable.

#### Translation Dashboard Class

`code()`

    Markup :  `code()`

```objective-c.
    #pragma mark - AppLanguageInfo
@interface TranslationInfo : NSObject

@property (nonatomic, retain) NSString *language;
@property (nonatomic, retain) NSString *country;
@property (nonatomic, retain) NSBundle *bundle;
@property (nonatomic, retain) NSString *locale;
@property (nonatomic) NSInteger finalAlignment;
@property (nonatomic, retain) NSString *appAlignmentText;


@end
```

### Step 4

Save the locale information currently used by the app or returned in response by service

#### Translation Dashboard Class

```objective-c.
-(void)saveLocaleDataToUserDefaults:(NSDictionary *)localeInfo {
    NSUserDefaults *userDefaults = [NSUserDefaults standardUserDefaults];
    [userDefaults setValue:[localeInfo valueForKey:@"locale"] forKey:@"locale"];
    [userDefaults setValue:[localeInfo valueForKey:@"country"] forKey:@"country"];
    [userDefaults setValue:[localeInfo valueForKey:@"language"] forKey:@"language"];
    [userDefaults setValue:[localeInfo valueForKey:@"textAlignment"] forKey:@"textAlignment"];
    [userDefaults synchronize];
}
```
