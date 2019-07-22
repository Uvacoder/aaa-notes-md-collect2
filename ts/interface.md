# Interfaces

## Typescript Core princeple

One of TypeScript’s core principles is that type checking focuses on the shape that values have. This is sometimes called `duck typing` or “structural subtyping”

```ts
function printLabel(labeledObj: { label: string }) {
    console.log(labeledObj.label);
}
let myObj = {size: 10, label: "Size 10 Object"};
printLabel(myObj);
```

## Optional parameter

```ts
interface SquareConfig {
    color?: string;
    width?: number;
}
```

## Readonly properties

```ts
interface Point {
    readonly x: number;
    readonly y: number;
}
let p1: Point = { x: 10, y: 20 };
p1.x = 5; // error!
```

### readonly vs const

`readonly` is used inside object properties not to change  

`const` is used instead of `var` or `let`

## Funtion types

```ts
interface SearchFunc {
    (source: string, subString: string): boolean;
}
```

function declaration and definition

```ts
let mySearch: SearchFunc;
mySearch = function(sre: string, subStr: string) {
    let result = source.search(subString);
    return result > -1;
}
```

## Indexble types

```ts
interface StringArray {
    [index: number]: string;
}
let myArray: StringArray;
myArray = ["Bob", "Fred"];
```

## Class Types

One of the most common uses of interfaces in languages like C# and Java, that of explicitly enforcing that a class meets a particular contract, is also possible in TypeScript.

```ts
interface ClockInterface {
    currentTime: Date;  // instance property
    setTime(d: Date): void; // instance method
}

class Clock implements ClockInterface {
    currentTime: Date = new Date();
    setTime(d: Date) {
        this.currentTime = d;
    }
    constructor(h: number, m: number) { }
}
```

### Restrictions

- Only `public` side of the classes can be defined in interfaces

- interface `checks only the instance of the classes`. It will not check any static methods of the class.

### checking construcotr of a class

[Refer here for clear details ](https://www.typescriptlang.org/docs/handbook/interfaces.html#difference-between-the-static-and-instance-sides-of-classes)

```ts
interface ClockConstructor {
    new (hour: number, minute: number): ClockInterface;
}
interface ClockInterface {
    tick(): void;
}

function createClock(ctor: ClockConstructor, hour: number, minute: number): ClockInterface {
    return new ctor(hour, minute);
}

class DigitalClock implements ClockInterface {
    constructor(h: number, m: number) { }
    tick() {
        console.log("beep beep");
    }
}
class AnalogClock implements ClockInterface {
    constructor(h: number, m: number) { }
    tick() {
        console.log("tick tock");
    }
}

let digital = createClock(DigitalClock, 12, 17);
let analog = createClock(AnalogClock, 7, 32);
```

## Extending interface

```ts
interface Shape {
    color: string;
}

interface Square extends Shape {
    sideLength: number;
}
let square = {} as Square;
square.color = "blue";
square.sideLength = 10;
```

Can also extend multiple interfaces

```ts
interface Shape {
    color: string;
}

interface PenStroke {
    penWidth: number;
}

interface Square extends Shape, PenStroke {
    sideLength: number;
}
```

## Interface extending classes

```ts
class Control {
    private state: any;
}

interface SelectableControl extends Control {
    select():void;
}

// valid
class Button extends Control implements SelectableControl {
    select() {

     }
}

// invalid
// Error :Class 'TextBox' incorrectly implements interfac
class TextBox implements SelectableControl {
   select() {

    }
}
// Only descendents of the Control class can use Control interface

```


