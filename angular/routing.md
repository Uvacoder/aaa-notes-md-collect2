# Routing

The Angular router **enables you to show different components and data to the user based on where the user is in the application**.

## Some of the example tasks

- Enter a URL in the address bar, and the browser navigates to a corresponding page.
- Click links on the page, and the browser navigates to a new page.
- Click the browser's back and forward buttons, and the browser navigates backward and forward through the history of pages you've seen.

A route associates one or more URL paths with a component.

## Route properties

A typical Angular Route has two properties:

`path`: a string that matches the URL in the browser address bar.
`component`: the component that the router should create when navigating to this route.

```javascript
@NgModule({
  imports: [
    BrowserModule,
    ReactiveFormsModule,
    RouterModule.forRoot([
      { path: '', component: ProductListComponent },
      { path: 'products/:productId', component: ProductDetailsComponent },
    ])
  ],
```

*A route associates one or more URL paths with a component.*

## RouterModule.forRoot

You first must initialize the router and start it listening for browser location changes.

Add `RouterModule` to the `@NgModule.imports array` and configure it with the routes in one step by calling `RouterModule.forRoot()` within the imports array, like this:

```typescript
imports: [ RouterModule.forRoot(routes) ],
```

### Exampe

`app-module.ts` importing Routermodule

```javascript
@NgModule({
  imports: [
    BrowserModule,
    RouterModule.forRoot([
      { path: '', component: ProductListComponent },
      { path: 'products/:productId', component: ProductDetailsComponent },
    ])
  ],
  declarations: [
    AppComponent,
    ProductListComponent,
  ],
  bootstrap: [ AppComponent ],
  providers: [ ]
})
```

### Note : forRoot
The method is called `forRoot()` because you configure the router at the application's root level. The `forRoot()` method supplies the service providers and directives needed for routing, and performs the initial navigation based on the current browser URL.

## Router Outlet

`<router-outlet></router-outlet>`
We have to add this above directory in `root component` (generlly the app component will be the root component )in order to expose the routes to the  

Other wise the path will not work

```html
<h1>App component {{title}}</html>
<header>{{Header text}}</header>
<router-outlet></router-outlet>
<footer></footer>
```

### Router Link ( Navigation link )

Define a link using the `RouterLink directive`. The routerLink defines how the user navigates to the route (or URL) declaratively in the component template.

```html
<a [title]="product.name + ' details'" [routerLink]="['/products', product.id]">{{product.name}}</a>
```

or

```html
<a [title]="product.name + ' details'" routerLink="/products/{{product.id}}">{{product.name}}</a>
```

### Activated Route ( Using route information )

We can parse and use the route information

```typescript
import { ActivatedRoute } from '@angular/router';

export class ProductDetailsComponent implements OnInit {
  product;

  constructor(
    private route: ActivatedRoute,
  ) { }

    ngOnInit() {
        this.route.paramMap.subscribe(params => {
            this.product = products[+params.get('productId')];
            // Route must be predefined 
            // { path: 'products/:productId', component: ProductDetailsComponent },
            // if the URL is www.host/products/1 params.get('productId') will return 1
        });
    }
}
```

## App Routing module

Instead declaring all the paths directly in the `app-module.ts` we could declare the routes in a seperate route module `app-routing-module.ts` and import it in to `app-module.ts`

The below code is a example app routing module and how we can import app routing module into
app module

`app-routing-module.ts`
```typescript
import { NgModule } from '@angular/core';
import { Routes, RouterModule } from '@angular/router';
import { HeroDetailComponent } from './hero-detail/hero-detail.component';
const routes: Routes = [
  {'path' : 'heroes/:heroId','component' : HeroDetailComponent }
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```

`app-module.ts`
```typescript
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';

import { AppRoutingModule } from './app-routing.module';
import { FormsModule } from '@angular/forms';
import { AppComponent } from './app.component';
import { HeroesComponent } from './heroes/heroes.component';

@NgModule({
  declarations: [
    AppComponent,
    HeroesComponent,
    HeroDetailComponent,
    MessagesComponent
  ],
  imports: [
    FormsModule,
    BrowserModule,
    AppRoutingModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

