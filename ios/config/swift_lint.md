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

```yaml
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


## References


[Kodeco article](https://www.kodeco.com/38422105-swiftlint-in-depth)
