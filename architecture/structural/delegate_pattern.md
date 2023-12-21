# Delegate Pattern 

## Intro

1 : 1 type
[delegation-pattern-in-swift](https://medium.com/@nimjea/delegation-pattern-in-swift-4-2-f6aca61f4bf5)

## Pros

- No extra management of state. It is one to one.
- Less side effects.


## Cons

- Need to be one to one
- Not easy to understand at first glance - isn't intuitive if coming from other languages.
- Lots of bigger name delegate functions - more verbiage.
- need to isolate for cleaner readability in extensions with conformance to `delegate / datasource`


## Examples

iOS example
[delegation_pattern](delegation_pattern.md)