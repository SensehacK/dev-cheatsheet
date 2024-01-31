# Prerequisite

## [Best practices for apple ecosystem](ios/config/best_practices.md)

## Xcode Configs

- Don't commit unnecessary files to version control
- Avoid committing Team, config of Xcode signing, provisioning to protected branches.
- Use [.gitIgnore](ignore.md)  appropriate config files for apple/iOS projects.


## Things to look out for

- Always kind of make sure that if you can switch from class to structs - more optimized
- Use enums rather than other extra variables or configs in swift
- use `let` instead of `var` immutability vs mutability
- Always check whether the classes defined are finalized as it is more optimized
- Use string concatenation instead of [String interpolation](ios/swift/string#Performance)


