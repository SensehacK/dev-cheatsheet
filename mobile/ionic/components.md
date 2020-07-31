# Components

Reusability is a major component for mobile and web app architecture. From lazy loading components, pages to pagination and optimization on thin client devices is crucial part of any design patterns by an architect.

## Generating component

Using this command we can generate components which can be imported throughout the app or modules required by us.

> ionic g component component/component\_name

Tip : Always create a new folder for components and then more folders depending on its usage. eg. Shared components, UI Components, Custom components

## Component Lifecycle

We don’t have access to Ionic lifecycle as other patterns have like class file. We don’t have “IonViewDidLoad” — “IonViewWillLoad” and many more.

We have access to “ngOnInit” and “ngAfterViewInit” provided that we implement that protocol like these examples

AfterViewInit Method

```typescript
import { Component, AfterViewInit } from '@angular/core';

 export class Custom_Component implements AfterViewInit {

     ngAfterViewInit() { }

  }
```

OnInit Method

```typescript
import { Component, OnInit } from '@angular/core';

 export class Custom_Component implements OnInit {

     ngOnInit() {     }

  }
```

## Referencing HTML Element

If we want to reference HTML elements in Angular and ionic 4, we could access it via using ‘\#id\_name’ in HTML page and referencing it in .TS file

```markup
 <div> 
     <canvas #myCanvas></canvas>
 </div>
```

```typescript
 @ViewChild('myCanvas', { static: false }) myCanvas: any;

     ngAfterViewInit() {
          // Accessing the html elements
             this.myCanvas.width = window.innerWidth;
            this.myCanvas.height = window.innerHeight;

             const myCanvasContext = this.myCanvas.nativeElement.getContext('2d');

             myCanvasContext.fillStyle = UI_color;
           myCanvasContext.fillRect(x,y,a,b);
     }
```

HTML elements could only be referenced after they are being rendered in DOM by angular / ionic or any other framework you’re using. So better check whether the instance or object is not null so that we can continue accessing the methods related to it.

## Component Import Export

If the component is created to be used by more than one module, then we would need to have higher module to import in both child modules ‘child\_a’ and ‘child\_b’.

So we would create Parent\_Module which would have Component.

And other modules who want to have shared component , would import the Parent\_Module in their

> @ngModule { imports:\[\] } statement. Will include the example later.

### Authored by : [Kautilya Save](https://sensehack.github.io/)

### [GitHub](https://github.com/SensehacK)

