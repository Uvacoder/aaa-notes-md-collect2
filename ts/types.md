# Types

## Why we need types

we need to be able to work with some of the simplest units of data: numbers, strings, structures, boolean values, and the like. In TypeScript

## Number

```ts
let decimal: number = 6;
let hex: number = 0xf00d;
let binary: number = 0b1010;
let octal: number = 0o744;
```

## String

```ts
let color: string = "blue";
color = 'red';
```

## Array

```ts
let list: number[] = [1, 2, 3];
```

## Tuple

```ts
let x: [string, number]; // Declare a tuple type
x = ["hello", 10]; // OK
x = [10, "hello"]; // Error
```

## Enum

### Auto Assign

```ts
enum Color {Red, Green, Blue}
let c: Color = Color.Green; // c = 2
```

### Auto increment

```ts
enum Color {Red = 10, Green, Blue}
let c: Color = Color.Green; // c = 11
```

### Manual

```ts
enum Color {Red = 1, Green = 2, Blue = 4}
let c: Color = Color.Green;
```

### Store as String

```ts
enum Color {Red = 1, Green, Blue}
let colorName: string = Color[2]; // colorName = Green
```

## Any

```ts
let notSure: any = 4;
notSure = "maybe a string instead";
notSure = false; // okay, definitely a boolean
```

## Void

```ts
function warnUser(): void {
    console.log("This is my warning message");
}
```

## null and undefined

```ts
// Not much else we can assign to these variables!
let u: undefined = undefined;
let n: null = null;
```

## Never

```ts
// Function returning never must have unreachable end point
function error(message: string): never {
    throw new Error(message);
}
```

```ts
// Function returning never must have unreachable end point
function infiniteLoop(): never {
    while (true) {
    }
}
```

## Object

`object` is a type that represents the non-primitive type

```ts
declare function create(o: object | null): void;
create({ prop: 0 }); // OK
create(null); // OK

create(42); // Error
create("string"); // Error
create(false); // Error
create(undefined); // Error
```

## Type assertions

Type assertions has two syntaxes

### Angle bracket syntax

```ts
let someValue: any = "this is a string";
let strLength: number = (<string>someValue).length;
```

### As syntax

```ts
let someValue: any = "this is a string";
let strLength: number = (someValue as string).length;
```
