Side Effects


## Good practise

Jersh comment on

```
Observable.just(nil),
```

no need to change now, but i've started keeping an eye out for uses of (Observable/Driver).just() and (Observable/Driver).empty() because those observable types emit complete events right away in order to enforce their namesakes, which in turn send complete events to any observers/subscribers which could cause unintended side effects or render parts of our view model functionality useless.


it's dependent on the scenario of course, but i think most of the time we'd rather use (Observable/Driver).of() and (Observable/Driver).never(), as these don't emit complete events that might cause issues downstream. while both are correct, we should try to reduce the cases/scenarios we need to account for by trying to be consistent with our choices around the backing observable types that we use!