Relays


RxRelay provides three kinds of Relays: PublishRelay, BehaviorRelay and ReplayRelay. They behave exactly like their parallel Subjects, with two changes:

    - Relays never complete.
    - Relays never emit errors.

In essence, Relays only emit .next events, and never terminate.