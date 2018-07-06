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
//This is just calling RTLTranslateDashboard method
-(NSInteger)fetchAlignment{
    return [[RTLTranslateDashboard sharedManager] fetchAlignment];
}
```

### Step 2

Invoke the class once to fetch the data from the server in the app life cycle.

#### Business Logic class

```objective-c.
//**AR
    [translationDashboard appAlignment];
//AR
```

### Step 3

Create a different class which handles all of your data parameters from restful services in middleware or back end services.
Use the API json data to persist the data throughout the application or maybe store it in constant variable.

#### RTLTranslate Dashboard Class

`code()`

    Markup :  `code()`

```objective-c.
    #pragma mark - AppLanguageInfo
@interface RTLTranslateInfo : NSObject

@property (nonatomic, retain) NSString *language;
@property (nonatomic, retain) NSString *country;
@property (nonatomic, retain) NSBundle *bundle;
@property (nonatomic, retain) NSString *locale;
@property (nonatomic) NSInteger finalAlignment;
@property (nonatomic, retain) NSString *appAlignmentText;


@end
```

### Step 4

Save the locale information currently used by the app or returned in response by service, use the same class used in Step 3.

#### RTLTranslate  Class

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

```objective-c.
-(RTLTranslateInfo *)fetchDefaultDeviceRTLTranslateInfo
{
    RTLTranslateInfo *translationInfo = [RTLTranslateInfo new];
    translationInfo.language = [RTLTranslateDashboard fetchCurrentLanguage];
    translationInfo.country = [RTLTranslateDashboard fetchCurrentCountry];
    translationInfo.locale = [RTLTranslateDashboard fetchCurrentLocale];
    translationInfo.appAlignmentText = [RTLTranslateDashboard fetchAppAlignment];
    //[self setAppLanguageWithDefaultRTLTranslateDashboardInfo];

    return translationInfo;
}
```

### Step 5

```objective-c.
//**AR
// changed function name from "fetchAlignment" >> "fetchFinalAlignment" so that swift/objC compiler or runtime executor will be able to differentiate it easily.
// Also less ambiguous overall. ARK
-(NSInteger)fetchFinalAlignment
{
    return _finalAlignment;
}
```

### Step 6

Main method called for fetchting the latest Text Alignment preference for the particular user.

```objective-c.
+(NSString *)fetchAppAlignment{
    NSString *finalAlignment;
    NSUserDefaults *userDefaults = [NSUserDefaults standardUserDefaults];
    finalAlignment = [userDefaults valueForKey:@"textAlignment"];
    return finalAlignment;
}
```

### Step 7

Method called for fetchting the Text Alignment preference from translation class method variables to check whether it is "RTL" or "LTR" abbreviation for the same is "Right To Left" & vice versa.

```objective-c.
//**AR
//Based on the alignment parameter from fetchRTLTranslate WS
//alignment for text fields and labels will be decided.
-(NSInteger)appAlignment{
    RTLTranslateInfo *translationInfo;
    NSInteger alignment = NSTextAlignmentLeft;
    translationInfo = [self fetchDefaultDeviceRTLTranslateInfo];
    if ([translationInfo.appAlignmentText isEqualToString:@"RTL"]) {
        alignment = NSTextAlignmentRight;
    }
    _finalAlignment = alignment;
    //Dev environment to simulate RTL ? 2 : 0
//    _finalAlignment = 2;
    return _finalAlignment;
}
```

NSTextAlignment can also accept variables in Integers :

* NSTextAlignmentLeft:0

* NSTextAlignmentCenter : 1

* NSTextAlignmentRight : 2

### Step 8

## Profit ???

## Implementation

This 1 line code determines the current user alignment based of from our web service call from server saved in singleton class so that we don’t need to import the function everywhere.
Just use single instance “sharedUtil” for class “Utility” which is imported by default to track user variables parameters used dynamically.

```objective-c.
//^ARK
    textView.textAlignment=[[Utility sharedUtil] fetchAlignment];
//^ARK
```

## Contribution

> Feel free to fork this project & raise a pull request to add more relevant information regarding development tools used in iOS ecosystem.

## Author : Kautilya Save

### [GitHub](https://github.com/SensehacK)