

## UI Thread


```kotlin
runOnUiThread { }
```


> Before getting into example, we should know what is runOnUiThread() in android. Sometimes Main thread performs some heavy operations. if user wants to add some extra operations on UI, it will get load and provides ANR. Using runOnUiThread going to do back ground operations on worker thread and update the result on main thread.

## Reference


[tutorial points | ui thread](https://www.tutorialspoint.com/how-do-we-use-runonuithread-in-android)