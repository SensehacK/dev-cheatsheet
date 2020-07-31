# Deprecations

Listing which components or syntax doesn't work in ionic 4 but used to work in ionic 2/3 via following the ionic 2/3 tutorial from Udemy.

## Syntax Changes

### ion-toolbar vs ion-navbar

~~ion-navbar~~ is deprecated & using it leads to blank screen, have to replace it with ion-toolbar.

```markup
<ion-navbar>
<ion-toolbar>
```

### navPop navPush

Doesn't work with ion-button navPop & navPush in ionic 4.

```markup
<button ion-button NavPop>Go Back</button>
```

### ionic v4 Life cycle

New life cycle changes are updated on their migration guide on ionic website [here.](https://ionicframework.com/docs/building/migration#lifecycle-events)

> Older events like ionViewDidLoad, ionViewCanLeave, and ionViewCanEnter have been removed, and the proper Angular alternatives should be used.

### Authored by : [Kautilya Save](https://kautilya.design)

### [GitHub](https://github.com/SensehacK)

