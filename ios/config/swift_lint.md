# SwiftLint


## Install

Home brew Approach
```sh
brew install swiftlint
```

Or Swift Xcode Code Plugin via SPM or different options.


### VSCode Extension

On M1 Macs you need to specify the updated path or manually copy the executable to the default path.

[swiftlint path](https://thisdevbrain.com/how-to-fix-the-swiftlint-not-installed-warning-on-m1-macs/)

Extension to use in VSCode
[Extension](https://marketplace.visualstudio.com/items?itemName=vknabel.vscode-swiftlint)



## Example Config

```yml
included:
  - Sources
  - Tests
excluded:
  - Tests/**/*Resources # files in this directory contains only JSON strings.
  - Tests/**/XCTestManifests.swift # auto-generated file
line_length:
  warning: 140 # needs discussion (default: 120)
  error: 350 # needs discussion (default: 200)
  ignores_comments: true
  ignores_urls: true
  ignores_function_declarations: true
  ignores_interpolated_strings: true

# Keeps the code nesting level at 2, to support swift name-spacing 
nesting:
    type_level: 2
type_name:
  allowed_symbols: "_"
identifier_name:
  allowed_symbols: "_"
  excluded:
    - ci
    - id
    - pr

disabled_rules:
  - trailing_comma
  - trailing_whitespace
  - vertical_whitespace
```

## Good Rules


```yaml
vertical_parameter_alignment_on_call

multiline_arguments

```



## Reasoning

### Identifier name rule 

> We can certainly enable identifier_name the Linter will have issues with something like let i: Int = 0. I can go either way on this, thoughts @ksave957_company

I don't like this rule because sometimes we need variables like `id` or `c` `x,y,z` or `foo` `bar`.  
If we start enabling this rule and enforce it to minimum 3 chars. It will add extra noise to the closure, for loop or any composition based programming.

for eg.

```swift
// This satisfies the rule
for item in items { 
  doSomething(with: item)
}
// but this doesn't 
for i in items {
  doSomething(with: i)
}
```

Too take this further, programmers will avoid programming in imperative way and adopt more functional side, which I don't oppose but by having a specific guard rail towards one rule shouldn't be focused.

```swift
items
    .forEach { doSomething($0) }
```

You can easily avoid that rule by substituting `$0` `$1...$n` for `x` `y` `z`. Sometimes 1 char variables are more readable compared to `Dollar, dollar bill y'all`

This is my reasoning towards having this rule as disabled.

## Disable specific code

Wrap your valid cases in comments

```swift
// swiftlint:disable force_cast
let foo = bar as! Bad
// swiftlint:enable force_cast
```


## Expiring TODOs

[reference](https://realm.github.io/SwiftLint/expiring_todo.html)

```yml
expiring_todo:
  approaching_expiry_severity: warning
  expired_severity: warning
  # bad_formatting_severity: warning
```

## References

[Kodeco article](https://www.kodeco.com/38422105-swiftlint-in-depth)
