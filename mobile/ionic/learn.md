# Learning Timeline

## ionic 4 vs ionic 3

Big difference overall in terms of handling syntax.

## Navigation ionic 4

You have to use Angular Routing tool for navigating the web pages in ionic.

## Issues

### Navigate Button Not appearing

Navigation stack doesn't have the button being displayed. Use this code in `<ion-toolbar>`

```markup
<ion-buttons slot="start">
<ion-back-button defaultHref="home"></ion-back-button>
</ion-buttons>
```

### ionic 3 - 4 folder structure

Most of the folders have moved to "app" parent directory.

```text
     V3                 V4
/src/pages ->      /src/app/pages
/src/models ->     /src/app/models
/src/providers ->  /src/app/providers
```

### typescript object initialization

We would check two methods described while initializing objects in Typescript.

#### 1st Method

Variable object which hasn't been initialize at start or constructor would have error if you try to directly replace data.

```typescript
class expC {
     productData2: { name: string, quantity: number };

onInit() {
     this.productData2 = { name: "Kautilya", quantity: 577 };
}

}
```

#### 2nd Method

So you would have to define null in the objects where it is defined. So it won't have the error.

```text
error : Uncaught (in promise):
        // TypeError: Cannot set property 'name' of undefined
```

```typescript
class expC {
     productData2: { name: string, quantity: number } = { name: null, quantity: null };

onInit() {
     // Two ways to access values of object
     this.productData2.name = "Sensehack";
        this.productData2['quantity'] = 7584;
}

}
```

### Authored by : [Kautilya Save](https://kautilya.design)

### [GitHub](https://github.com/SensehacK)

