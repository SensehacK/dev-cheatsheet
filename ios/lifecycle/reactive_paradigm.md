

## Async AVPlayer

Q: do you all have anything to prevent the application from bad behavior like calling the player api before the ready event?


Ans: 
This is a subject we long had a placeholder to solve.We have a solution based on these principles:  

1. Should have one way to set things. So we don’t want a config param on build AND an API to set the same thing.
2. We don’t want to expose internal implementation via restrictions on when an API can be called.
3. We want a friendly API that’s not hard to use or requires a lot of documentation.

The solution is a combination of two phase init and a setter APIs and an rx BehaviorSubject pattern. Sequence is:  
App calls build  
App calls setters on returned player  
App calls player.load().The setters do a subject.next(val). The engine wrapper subscribes to the individual settings subjects when it is ready. And may apply the values on the engine before calling engine.play(). Being BehaviorSubjects, if the value is already set, they fire immediately on subscription.Using this pattern, we solved, for example, the problem of app does a mute and wants the volume to stay muted across player instances. Before doing this, there was a race condition when the app called setVolume(0) on a new stream start up where we ignored it because helio was still asynchronously initializing itself.