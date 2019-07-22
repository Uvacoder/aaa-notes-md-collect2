# Generics

C# and Java, one of the main tools in the toolbox for creating reusable components is generics, that is, being able to create a component that can work over a variety of types rather than a single one. This allows users to consume these components and use their own types.

The below function would lost it's keeping the ability of argument.

```ts
function identity(arg: any): any {
    return arg;
}
```

To keep the type of the argument we use generic

```ts
function identity<T>(arg: T): T {
    return arg;
}
let output = identity<string>("myString");  // type of output will be 'string'
let output = identity(12); // type of the output will be 'number'  
```

## Constrains for using generics

in general there are two criteria we should meet when deciding whether to use generics:

- When your function, interface or class will work with a variety of data types

- When your function, interface or class uses that data type in several places

## Generic type arguments array

### wrong

```ts
function loggingIdentity<T>(arg: T): T {
    console.log(arg.length);  // Error: T doesn't have .length
    return arg;
}
```

### right

Method - 1

```ts
function loggingIdentity<T>(arg: T[]): T[] {
    console.log(arg.length);  // Array has a .length, so no more error
    return arg;
}
```

Method - 2

```ts
interface Length {
    length: number;
}

function identity<T extends Length>(arg: T): T {
   // length property can now be called
   console.log(arg.length);
   return arg;
}
```

### to mention return value

```ts
function loggingIdentity<T>(arg: Array<T>): Array<T> {
//(or)
function loggingIdentity<T>(arg: T[]): T[] {
    console.log(arg.length);  // Array has a .length, so no more error
    return arg;
}
```

## Generic Function Types

So far we have seen how to handle diffent argument types in generic. Now we are going to see the types of diffent generic functions.

- The type of generic functions is just like those of non-generic functions, type parameters listed first

```ts
function identity<T>(arg: T): T {
    return arg;
}

let myIdentity: <T>(arg: T) => T = identity;
```

### Writing generic type as object literal signature

```ts
function identity<T>(arg: T): T {
    return arg;
}

let myIdentity: {<T>(arg: T): T} = identity;
```

### Generic Interface

The above Object literal lead us to write interface for generic functions

```ts
interface GenericIdentityFn {
    <T>(arg: T): T;
}

function identity<T>(arg: T): T {
    return arg;
}

let myIdentity: GenericIdentityFn = identity;
```

### Generic Classes

code-sample

```ts
class GenericNumber<T> {
    zeroValue: T;
    add: (x: T, y: T) => T;
}

let myGenericNumber = new GenericNumber<number>();
myGenericNumber.zeroValue = 0;
myGenericNumber.add = function(x, y) { return x + y; };

let stringNumeric = new GenericNumber<string>();
stringNumeric.zeroValue = "";
stringNumeric.add = function(x, y) { return x + y; };

```

The above class is named as `GenericNumber`, But still can be used for `String` and `Number` while creating instances and use it;

### Extending with Generic classes

```ts
class Animal {
    numLegs: number;
}

class Lion extends Animal {
    keeper: string;
}

function createInstance<A extends Animal>(c: new () => A): A {
    return new c();
}

createInstance(Lion).keeper.nametag;  // typechecks!

```

## Use case examples

### API Services

The APIService is a class which will be a parent class for many other services. And each services might handle different data type or class types

```ts
class APIService extends API {
   public getRecord<T, U> (endpoint: string, params: T[]): U {}
   public getRecords<T, U> (endpoint: string, params: T[]): U[] {}
}
```

### Manipulating arrays

The below example will be base class many departments and the departments might have differnt data types it's employees

```ts
class Department<T> {
   //different types of employees
   private employees:Array<T> = new Array<T>();
   public add(employee: T): void {
      this.employees.push(employee);
   }
   ...
}
```

### Type constrain in generic function parameter

```ts
function getProperty<T, K extends keyof T>(obj: T, key: K) {
    return obj[key];
}

let x = { a: 1, b: 2, c: 3, d: 4 };

getProperty(x, "a"); // okay
getProperty(x, "m"); // error: Argument of type 'm' isn't assignable to 'a' | 'b' | 'c' | 'd'.
```
