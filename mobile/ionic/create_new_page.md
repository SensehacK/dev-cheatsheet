# Creating Page

When not using command, in ionic 4 you would have to define your new route so that IONIC could properly navigate within the app.

Eg. If we create folder with 3 files namely

```text
buyout.html
buyout.module.ts
buyout.ts
```

Then we would need to update our Angular Routing file in

```typescript
"app-routing.module.ts" in const routes: Routes = [
{ path: '', redirectTo: 'home', pathMatch: 'full' },
{ path: 'home', loadChildren: './home/home.module#HomePageModule' },
{ path: 'buy', loadChildren: './buyout/buyout.module#BuyoutPageModule' },
// BuyoutPageModule is the Class of "buyout.module.ts".
];
```

Also in buyout.module.ts, you would have to import the main "buyout.ts" file, change routes, @NGModule & have a class.

```typescript
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { FormsModule } from '@angular/forms';
import { Routes, RouterModule } from '@angular/router';

import { IonicModule } from '@ionic/angular';

import { BuyoutPage } from './buyout';

const routes: Routes = [
    {
        path: '',
        component: BuyoutPage
        // BuyoutPage is the Class of "buyout.module.ts".
    }
];

@NgModule({
    imports: [
        CommonModule,
        FormsModule,
        IonicModule,
        RouterModule.forChild(routes)
    ],
    declarations: [BuyoutPage]
    // BuyoutPage is the Class of "buyout.module.ts".
})
export class BuyoutPageModule { }
```

## Authored by : [Kautilya Save](https://kautilya.design)

## [GitHub](https://github.com/SensehacK)

