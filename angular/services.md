# Services

Services are an integral part of Angular applications. In Angular, a service is an instance of a class that can be made available to any part of your application using Angular's dependency injection system.

Services are the place where you share data between parts of your application.

Example Cart service

```ts
import { Injectable } from '@angular/core';

@Injectable({
  providedIn:'root'
})
export class CartService {
  items = []
  constructor() { }
  addToCart(product){
    this.items.push(product)
  }
  getItems(){
    return this.items;
  }
  clearCart(){
    this.items = [];
    return this.items;
  }
}
```

Need to add the service as part of providers
Injecting or adding the service as part of a specified module

```ts
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { RouterModule } from '@angular/router';

import { AppComponent } from './app.component';
import { CartService } from './cart.service';
import { CartComponent } from './cart/cart.component';

@NgModule({
  imports: [
    BrowserModule,
    RouterModule.forRoot([
      { path: '', component: CartComponent },
    ])
  ],
  declarations: [
    AppComponent,
    CartComponent,
  ],
  bootstrap: [ AppComponent ],
  providers: [ CartService ]
})

export class AppModule { }
```

Using cart service inside a cart component
```typescript
import { Component, OnInit } from '@angular/core';
import { CartService } from '../cart.service';

@Component({
  selector: 'app-cart',
  templateUrl: './cart.component.html',
  styleUrls: ['./cart.component.css']
})
export class CartComponent implements OnInit {
  items;
  constructor(
    private cartService : CartService
  ) {}

  ngOnInit() {
    this.items = this.cartService.getItems();
  }
}
```



