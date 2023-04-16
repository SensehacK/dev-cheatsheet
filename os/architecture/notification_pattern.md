## Notification Pattern

1 - > N 

Pros:
- Broadcasting everything at once.
- Big state change and you need to reflect that everywhere.

Cons:
- Subscribing and disposing of subsribers
- Multiple firing of events.
- Hot / Cold observers