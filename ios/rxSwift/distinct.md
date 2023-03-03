
```swift
sessionState
	.rx
	.user
	.distinctUntilChanged(at: \.?.uniqueId)
	.unwrap()
```
vs 
```swift
sessionState
	.rx
	.user
	.unwrap()
	.distinctUntilChanged(at: \.?.uniqueId)
```

Before 													After

non nil object = unique_id							 	

Initial app launch

1.
User 1: nil 

2. 
User 1 logs in: old(nil) vs (unique_id)

3.
User Deactivated: old(unique_id) vs new(nil) - session Coordinator purgeEntries

4.
User activated & app isn't closed
old(nil) vs new(unique_id)			