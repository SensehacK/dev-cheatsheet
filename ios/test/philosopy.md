

## Why

excerpt from our mobile devs meetings

```text
You shouldn't be testing XFDesign. There's a distributed architecture. If it's a bug, it's everywhere. 

"What if I don't trust my Delivery System?! What if Velox doesn't work" <-- This isn't a valid mind-set! 

We shouldn't duplicate the (testing) responsibility of other squads. You're coupling your expectations and creating a development nightmare 

If you ever had a very complex string for a label, then just put that in a function and test that.
```


## View model

```
- Your viewModels should test against your **data-source** variations...
```

## Snapshot testing 

[screenshot_test](/ios/test/screenshot_test#Approach)