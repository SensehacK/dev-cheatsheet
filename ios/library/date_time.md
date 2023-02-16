# Date and Time



## Conversion to UTC
Converting from one timezone to UTC timezone.

```swift
/// Convert user timezone to UTC
    public static func dateTimeToUTC(_ date: Date,
                                     timezone: TimeZone) -> Date {
        print("Current date passed \(date)")
        // First convert Device time zone into User saved timezone
        let userProfileRegion = Region(calendar: date.calendar, zone: timezone)
        // Generate date components from user profile date for year, month, day
        let components = DateInRegion(date, region: userProfileRegion).dateComponents
        // Confirm date contained valid components
        guard let year = components.year,
              let month = components.month,
              let day = components.day else { return date }
        print("Conversion USer PRofile TimeZone to UTC")
        print(components)
        
        let userProfileRegion2 = Region(calendar: date.calendar, zone: Calendar.current.timeZone)
        let defaultComponents = DateInRegion(Date(), region: userProfileRegion2).dateComponents
        // Confirm date contained valid components
        guard let hour = defaultComponents.hour,
              let minute = defaultComponents.minute else { return date }
        
        print(" printing components \(hour) \(minute)" )
        
        // Translate user profile date back into UTC date, keeping year, month, day
        let newRegion = Region(calendar: date.calendar, zone: Calendar.current.timeZone)
        
        let dateTestDummy = Date(year: year,
                                 month: month,
                                 day: day,
                                 hour: hour,
                                 minute: minute,
                                 region: newRegion)
        
        print("Printing TestDummy with region diff")
        print(dateTestDummy)
        let dateDummy2 = Calendar.current.dateComponents(in: TimeZone(secondsFromGMT: 0)!, from: dateTestDummy)
        print(" Printing direct conversion \(dateDummy2)"  )
        return dateTestDummy
    }
```


    
```swift
    public static func dateFromUTCToUserProfileTimezone(_ date: Date,
                                                      timezone: TimeZone) -> Date {
        
        let convertedString = DateUtils.string(date, timezone: timezone)
        print("Converting date string \(convertedString)")
        
        let secondsFromGMT = timezone.secondsFromGMT()
        print("seconds from GMT \(secondsFromGMT)")
        let userTZDateComponents = Calendar.current.dateComponents(in: TimeZone(secondsFromGMT: secondsFromGMT)!, from: date)
        print("Converted date components UTC to user timezone")
        print(userTZDateComponents)
        
        // Confirm date contained valid components
        guard let year = userTZDateComponents.year,
              let month = userTZDateComponents.month,
              let day = userTZDateComponents.day,
              let hour = userTZDateComponents.hour,
              let minute = userTZDateComponents.minute else { return date }
        print(day)
        print(hour)
        let dateTestDummy = Date(year: year,
                    month: month,
                    day: day,
                    hour: hour,
                    minute: minute)
        print("Converted Date components into Date Object")
        print(dateTestDummy)
        return dateTestDummy
    }
```


## Time

Mutating time object so that you can work around certain scenarios about it.


```swift

// Checking for custom refreshToken override

        var customExpirationDate: Date?

        if let storedExpiredToken = UserDefaults.standard.value(forKey: UserDefaults.Keys.customRefreshTokenValue) {

            print("Value was found")

            if let retrievedDate = storedExpiredToken as? Date {

                customExpirationDate = retrievedDate

            }

        } else {

            // Assuming the user has logged in - which is correct since `Mission Control`

            // setupRefreshTokenExpirationBindings checks if auth object is present and then .unwraps()

            // it which makes sure that auth object is present in order to override the expirationDate() in User Defaults.

            customExpirationDate = Date().addingTimeInterval(60)

            UserDefaults.standard.set(customExpirationDate, forKey: UserDefaults.Keys.customRefreshTokenValue)

        }
```

Date range ... operator to define a Range(startDate...endDate)
```swift

let easementDate = expirationDate.addingTimeInterval(Constant.easementTimeInternal)
let easementWindow = easementDate...expirationDate
print(easementWindow)
print("Easement window range \(easementWindow.contains(Date()))")
```

Check whether the date is way past current date.
```swift
let isCustomDateExpiredCheck = Date().isAfterDate(expirationDate, granularity: .minute)
print("My custom Expiration check: \(isCustomDateExpiredCheck)")
```


## Formatting 

Formatting time interval in swift using build in `DateComponentsFormatter()`
& `TimeInterval`.


https://cocoacasts.com/cocoa-fundamentals-formatting-a-time-interval-in-swift

[Formatting UTC Date](https://www.advancedswift.com/local-utc-date-format-swift/)

## Timezone Help


Also you can have Clock in your local timezone and UTC as mac os widgets or phone widgets.

Just adopt the ISO 8601 format for Date Time
https://www.iso.org/iso-8601-date-and-time-format.html

Converter to not kill yourself.

https://www.timeanddate.com/worldclock/converter.html

Different Timezone abbreviations 
https://www.timeanddate.com/time/zones/

Swift ISO date creation
https://onmyway133.com/posts/how-to-make-iso-8601-date-in-swift/


## References


[Convert String to Date](https://izziswift.com/convert-string-to-date-in-swift/)

[convert string to date cocoacasts](https://cocoacasts.com/swift-fundamentals-how-to-convert-a-string-to-a-date-in-swift)


https://iharishsuthar.github.io/posts/swift-date/