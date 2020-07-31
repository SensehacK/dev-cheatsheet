# Data Service

## Create CLI command for generating the service

> ionic g service services/service\_name

Let's start with creating a new file named 'data.service.ts'

```typescript
import { Injectable } from '@angular/core';

@Injectable({
    providedIn: 'root'
})

export class DataService {
    private message: string;

    constructor() {
        this.message = 'Hello Sensehack';

    }

    getMessage() {
        return this.message;
    }
}
```

Copy this boilerplate code, so that you can at least get around retrieving one value anywhere you need.

## Utilizing the Data Service

So for our example, we would retrieve the data service object in class 'ShopPage' 'shop.page.ts'

```typescript
import { DataService } from '../data.service';
@Component({
  selector: 'app-shop',
  templateUrl: './shop.page.html'
})
export class ShopPage {
testData: string;
constructor(private data2: DataService) {
    this.testData = data2.getMessage();
    // returns "Hello Sensehack"
```

Our shop page html where we display all of the html content. @'shop.page.html'

```markup
<ion-header>
  <ion-toolbar>
    <ion-title>Shop</ion-title>
  </ion-toolbar>
</ion-header>

<ion-content padding>
    <p> Hello Shop Page</p>
    <p> {{ testData }} </p>
</ion-content>
```

### Authored by : [Kautilya Save](https://kautilya.design)

### [GitHub](https://github.com/SensehacK)

