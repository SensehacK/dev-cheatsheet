# Date and Time



## Conversion to UTC
Converting from one timezone to UTC timezone.

```/// Convert user timezone to UTC
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


    
```
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

## References


[Convert String to Date](https://izziswift.com/convert-string-to-date-in-swift/)

[](https://cocoacasts.com/swift-fundamentals-how-to-convert-a-string-to-a-date-in-swift)