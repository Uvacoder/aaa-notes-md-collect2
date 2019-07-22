# Type Inference

It is a intelligent way of assigning type to variables when the type is explicitely not mentioned

There are several places where type inference is used to provide type information when there is no explicit type annotation.

```ts
let x = 3;
```

The type of the x variable is inferred to be number.

## Best common type

When a type inference is made from several expressions, the types of those expressions are used to calculate a “best common type”.

For the below the best common type is infered as number

```ts
let x = [0, 1, null]; // x : Number[]
```

For the below example if the common parent class is `Animal` then the type of `zoo` infered as `Animal`

```ts
let zoo = [new Rhino(), new Elephant(), new Snake()];
```

```ts
let zoo :Animal[] = [new Rhino(), new Elephant(), new Snake()];
```

## Contexual typing

Typescript is intelligent enough to identify type based on the context. The below example is DOM event handler. It knows the `MouseEvent` does't have `kangaroo` property.

```ts
window.onmousedown = function(mouseEvent) {
    console.log(mouseEvent.button);   //<- OK
    console.log(mouseEvent.kangaroo); //<- Error!
};
```

Typescript knows the `UIEvent` does't have `button` property

```ts
window.onscroll = function(uiEvent) {
    console.log(uiEvent.button); //<- Error!
}
```
