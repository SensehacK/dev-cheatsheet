


## Indentation

- Go to Xcode Preferences.
- Choose Text Editing tab.
- Switch to the Editing page underneath.
- Check both `Automatically trim trailing whitespace` and `Including whitespace-only lines`.

This will not add extra whitespaces when choosing `Re-Indent` in the Editor for the specific selection of code or file.



## Key binding


**How to delete a keybinding on Xcode ?** (using version 9.3 of Xcode)

The first method is obviously the little **`-`** that sometimes appears when double-clicking a binding.

The second method is not so quick but (in my experience) just as efficient. (Here I am assuming you've got a personalised keybinding profile already. If you don't, create one. I'll call it `Personal`.)

1. In Xcode: select the shortcut you want to remove and attribute it a random binding (even one that causes conflicts, you'll delete it in two minutes, you don't really care).
2. Quit Xcode.
3. Go to `~/Library/Developer/Xcode/UserData/KeyBindings/`.
4. Open the file `personal.idekeybindings` (it's a simple XML file, any decent text editor should be able to handle it).
5. Find the shortcut you modified and want to delete by searching its name using `command + F`.

You should then find something looking like this (each `dict` corresponds to a modified shortcut):

```xml
<dict>
    <key>Action</key>
    <string>execute:</string>
    <key>Alternate</key>
    <string>NO</string>
    <key>CommandID</key>
    <string>Xcode.IDEPlaygroundEditor.CmdDefinition.Execute</string>
    <key>Group</key>
    <string>Editor Menu for Playground</string>
    <key>GroupID</key>
    <string>Xcode.IDEPegasusPlaygroundEditor.MenuDefinition.Editor</string>
    <key>GroupedAlternate</key>
    <string>NO</string>
    <key>Keyboard Shortcut</key>
    <string>^&lt;</string>
    <key>Navigation</key>
    <string>NO</string>
    <key>Title</key>
    <string>Execute Playground</string>
</dict>
```

Delete this part:

```xml
    <key>Keyboard Shortcut</key>
    <string>^&lt;</string>
```

Do that for each shortcut you want to remove and don't forget to save the file before closing it. Now open Xcode and check for the shortcut: the space for the keybinding should be empty.


[SO | Source](https://stackoverflow.com/a/49819308/5177704)
