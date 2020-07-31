# Listeners

## Button listeners

### Add Listener

Adding a listener is straight forward

```text
textButtonObj.onClick.AddListener(delegate { checkCheckmarkButton(Timing12To3PMCheckmark); });
```

### Remove listener

Removing Listener goes something like this.

Quirks: If your script is getting invoked twice then maybe you would have to remove its old listener or else it would invoke twice which is undesirable for toggling states or updating UI as you don’t want overhead in your code.

```text
textButtonObj.onClick.RemoveListener(delegate { checkCheckmarkButton(Timing12To3PMCheckmark); });
```

[Link](ttps://docs.unity3d.com/ScriptReference/Events.UnityEvent.RemoveListener.html)

