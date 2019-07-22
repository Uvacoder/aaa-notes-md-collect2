# Template syntax

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
<input [(user.name)] /> //two way data binded variable
```

Based on the above code we have learned 5 things

- *ngFor
- *ngIf
- Interpolation {{ }}
- Property binding [ ]
- Event binding ( )
- Two way binding [()]

## Three ways of data binding in angular

- From the source-to-view
- From view-to-source
- Two-way sequence: view-to-source-to-view

![table-of-binding-associations](images/2019-07-16-17-15-10.png)

The target of a binding is the property or event inside the binding punctuation: [], () or [()].

## HTML Attribute binding

```html
<!-- Bind button disabled state to `isUnchanged` property -->
<button [disabled]="isUnchanged">Save</button>
```

## HTML Attribute vs DOM property

- Attributes are defined by HTML. Properties are accessed from DOM, or the Document Object Model, nodes.

- attributes initialize DOM properties and then they are done. Property values can change; attribute values can't.

- So it is not necessary that a DOM change result in HTML change

### Binding Targets Table

#### Property

![Property](images/2019-07-17-06-11-37.png)

Sample when we don't bind the property, value of parentItem is lamp

![Property](images/2019-07-17-06-42-07.png)

#### Event

![Event](images/2019-07-17-06-12-08.png)

#### Two way data binding

![Two-way](images/2019-07-17-06-12-54.png)

#### Attribute

![Attribute](images/2019-07-17-06-13-14.png)

#### class and style

![Class & Style](images/2019-07-17-06-13-43.png)

## Property Binding vs interpolation

You often have a choice between interpolation and property binding. The following binding pairs do the same thing

```html
<p><img src="{{itemImageUrl}}"> is the <i>interpolated</i> image.</p>
<p><img [src]="itemImageUrl"> is the <i>property bound</i> image.</p>

<p><span>"{{interpolationTitle}}" is the <i>interpolated</i> title.</span></p>
<p>"<span [innerHTML]="propertyTitle"></span>" is the <i>property bound</i> title.</p>
```

## content-Security

### Interpolation

```ts
evilTitle = 'Template <script>alert("evil never sleeps")</script> Syntax';
```

```html
<p><span>"{{evilTitle}}" is the <i>interpolated</i> evil title.</span></p>
```

Output

```output
"Template <script>alert("evil never sleeps")</script> Syntax" is the interpolated evil title.
```

During Interpolation angular makes sure no scripts tag get's exeucted, The script tas displayed as text

### Property Binding

```html
<!--

 WARNING: sanitizing HTML stripped some content (see http://  g.co/ng/security#xss).
-->
<p>"<span [innerHTML]="evilTitle"></span>" is the <i>property bound</i> evil title.</p>
```

```output
"Template alert("evil never sleeps")Syntax" is the property bound evil title.
```

## Attribute Binding

*wrong* will throw error

```html
<tr><td colspan="{{1 + 1}}">Three-Four</td></tr>
```

*right* validates correctly

```html
<tr><td [colSpan]="1 + 1">Three-Four</td></tr>
```

## Class binding

```html
<h3>Overwrite all existing classes with a new class:</h3>
<div class="item clearance special" [attr.class]="resetClasses">Reset all classes at once</div>
```

Adding a new class without overwriting the existing class attirbute and values

```html
<h3>Add a class:</h3>
<div class="item clearance special" [class.item-clearance]="itemClearance">Add another class</div>
```

Class toggle

```html
<div [class.special]="isSpecial">The class binding is special.</div>
```

Use `NgClass` when handling multiple classes

## Event binding

```html
<button (click)="onSave($event)">Save</button>
```

Without `ngModel` event binding with input

```html
<input [value]="currentItem.name"
       (input)="currentItem.name=$event.target.value" >
```

### CustomEvents

Defining custom events

```ts
@Output() deleteRequest = new EventEmitter<Item>();

delete() {
  this.deleteRequest.emit(this.item);
  this.displayNone = this.displayNone ? '' : 'none';
  this.lineThrough = this.lineThrough ? '' : 'line-through';
}
```

```html
<app-item-detail (deleteRequest)="deleteItem($event)" [item]="currentItem"></app-item-detail>
```

## Two way data binding ( parent child component )

[](https://angular.io/guide/template-syntax#basics-of-two-way-binding)

## Built in directives

### NgClass

*simple example* -

```html
<div [ngClass]="isSpecial ? 'special' : ''">This div is special</div>
```

*Multiple classes* -

```html
<div [ngClass]="currentClasses">This div is initially saveable, unchanged, and special.</div>
```

```ts
  this.currentClasses =  {
    'saveable': true,
    'modified': this.dirty,
    'special':  true
  };
```

### NgStyle

#### simple example NgStyle

```html
<div [style.font-size]="isSpecial ? 'x-large' : 'smaller'">
  This div is x-large or smaller.
</div>
```

#### Multiple classes NgStyle

```html
<div [ngStyle]="currentStyles">
  This div is initially italic, normal weight, and extra large (24px).
</div>
```

```ts
this.currentStyles = {
    'font-style':  this.canSave      ? 'italic' : 'normal',
    'font-weight': !this.isUnchanged ? 'bold'   : 'normal',
    'font-size':   this.isSpecial    ? '24px'   : '12px'
  };
```

### NgModel

it is part of `FormsModule`, need to be imported in NgModule before using NgModel

```html
<label for="example-ngModel">[(ngModel)]:</label>
<input [(ngModel)]="currentItem.name" id="example-ngModel">
```

## input

### Example 1

```html
<input [(name)] />
<button (click)="add()"></button>
```

Inside component

```ts
private name : string;
add():{
  this.nameService.add(name);
}
```

### Example 2

```html
    <input #heroName />
    <button (click)="add(heroName.value); heroName.value=''">
```

inside component

```ts
add(name:string):{
  this.nameService.add(name);
}
```
