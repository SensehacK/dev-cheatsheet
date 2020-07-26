# iOS Dark Mode




## Checking User Style


switch UIScreen.main.traitCollection.userInterfaceStyle {
case .light: //light mode
case .dark: //dark mode
case .unspecified: //the user interface style is not specified
}


## Override the App user style

You could use User Defaults to save the in app settings for different themes.



## Xcode assets

Utilize Color Set in Xcode with “Any” & “Dark” Mode. To better update the application with dynamic settings.
