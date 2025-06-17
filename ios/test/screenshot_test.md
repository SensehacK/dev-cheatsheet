
## Desc

When we want to compare screenshots of previous develop / master / main branch as baseline with newly updated PR. Just to make sure you're not introducing changes in UI which are not designated for specific devices or viewpoints.


## Library

We can utilize this library [swift-snapshot-testing](https://github.com/pointfreeco/swift-snapshot-testing)



## Approach

```
- Snapshots should not be against variation of your viewModels. But more on the **layout** variations (or just use a different screen)
```