```html
<h2>Products</h2>
 
<div *ngFor="let product of products">
 
  <h3>
    <a [title]="product.name + ' details'">
      {{ product.name }}
    </a>
  </h3>
 
  <p *ngIf="product.description">
    Description: {{ product.description }}
  </p>
 
  <button (click)="share()">
    Share
  </button>
 
</div>
```

Based on the above code we have learned 5 things
*ngFor
*ngIf
Interpolation {{ }}
Property binding [ ]
Event binding ( )