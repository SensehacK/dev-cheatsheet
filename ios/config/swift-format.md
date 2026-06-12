
## Build phase

Add a script phase `Swift format`

```sh
# Runs the swift formatter build in Xcode executable using swift runtime.
# To format it accordingly

echo "swift format rules applying across the project source files"
swift-format format -i -p --recursive "$SOURCE_ROOT"
```
Run script: 
Based on Dependency analysis
 - true  but because of xcode yelling me a warning

use discovered dependency file
- none

## Integration

Works great with [swift_lint](swift_lint.md) as the next step after first formatting your input files.

This eliminates `git pre commit hook` as well.
No need for CI runner to run things and start commenting on the PRs or even have co-pilot or anything else to run some static analysis on swift code around formatting and linting.

## Rules

`.swift-format` in your root project
```json
{
  "indentation" : {
    "spaces" : 4
  }
}

```



## Dependency Analysis

[medium | xcode build output files](https://medium.com/swiftblade/what-the-hell-is-this-output-files-in-xcode-build-phases-bfbec6391184)

## Reference

[github | swift format](https://github.com/swiftlang/swift-format)

[adding format to xcode build](https://justin.searls.co/posts/adding-swift-format-to-your-xcode-build/)

https://troz.net/post/2024/swift_format/