#Decorators

Before introducing decorators I would like to say few words about AOP (Aspect-oriented Programing). 

### AOP  ( Aspect Oriented Programming)

- AOP is a programming paradigm that aims to increase modularity by allowing the separation of cross-cutting concerns.

- The biggest advantage of using AOP is the separation of irrelevant code from the main functionality of the method to a different place.

### Example

##### Function without AOP ( Decorator )

```typescript
function add(x, y) {
    log(‘foo was called!’);
    If(!validate(arguments)) {
        throw (...)
    }
    If(!authorized()) {
        throw ()
    }
    return x + y;
}
```

##### Function with AOP
```typescript
@log
@validate
@authorize
function add(x, y) {
    return x + y;
}
```

### Typescript Decorators

Decorators can be attached to:
- Methods
- Classes
- Properties
- Parameters
- Accessor

#### Method Decorator

##### Simple example
```typescript
function log(target, key, descriptor) {
	console.log(`${key} was called!`);
}

class P {
	@log
	foo() {
		console.log(‘Do something’);
	}
}
const p = new P();
p.foo();

/* Output */
// foo was called!
// Do something
```

##### A Decorator function gets three parameters

`target` - Either the constructor function of the class for a static member ( `ClassName.PropertyName` )

or the prototype of the class for an instance member.
( `ClassName.prototype.PropertyName` )

`key` - The name of the member.
`descriptors` - The Property Descriptor for the member ( Enumarable, configurable, writable ( mutable ))

#####  Example - 2

The below is a classic example to get metrics of a function.

```typescript
function log(target, key, descriptor) {
    const originalMethod = descriptor.value;
    descriptor.value = function() {
        console.log(`${key} was called with:`, arguments);
        var result = originalMethod.apply(this, arguments);
        return result;
    };
    return descriptor;
}

class P2 {
    @log
    foo(a, b) {
        console.log(`Do something`);
    }
}
const p2 = new P2();
p2.foo('hello', 'world');
// printed to console :
// foo was called with: { '0': 'hello', '1': 'world' }
// Do something
```

### Decorator Composition ( multiple decorators and order )

 - Multiple decorators can be applied to a declaration, as in the following examples:
```typescript
@f
@g
function log(){
}	
```

- When multiple decorators apply to a single declaration, their evaluation is similar to function composition in mathematics. 

- In this model, when composing functions f and g, the resulting composite (f ∘ g)(x) is equivalent to f(g(x)).


- The expressions for each decorator are evaluated top-to-bottom.
- The results are then called as functions from bottom-to-top.

```typescript
function f() {
    console.log("f(): evaluated");
    return function (target, propertyKey: string, descriptor: PropertyDescriptor) {
        console.log("f(): called");
    }
}

function g() {
    console.log("g(): evaluated");
    return function (target, propertyKey: string, descriptor: PropertyDescriptor) {
        console.log("g(): called");
    }
}

class C {
    @f()
    @g()
    method() {}
}

/*output */
// f(): evaluated
// g(): evaluated
// g(): called
// f(): called
```

### Decorator Evaluation Order

There is a well defined order to how decorators applied to various declarations inside of a class are applied:

- Parameter Decorators, followed by Method, Accessor, or Property Decorators are applied for each instance member.
- Parameter Decorators, followed by Method, Accessor, or Property Decorators are applied for each static member.
- Parameter Decorators are applied for the constructor.
- Class Decorators are applied for the class.

### Class Decorators
 - Class Decorator is declared just before a class declaration. 
 
 - The class decorator is `applied to the constructor of the class` and can be used to observe, modify, or replace a class definition. 


 :exclamation: A class decorator cannot be used in a declaration file, or in any other ambient context (such as on a declare class).


:sparkle: For Class constructor of the decorated class as its only argument.

:sparkle: If the class decorator returns a value, it will replace the class declaration with the provided constructor function.

Example 
```typescript
@sealed
class Greeter {
    greeting: string;
    constructor(message: string) {
        this.greeting = message;
    }
    greet() {
        return "Hello, " + this.greeting;
    }
}
function sealed(constructor: Function) {
    Object.seal(constructor);
    Object.seal(constructor.prototype);
}
```

##### Overriding constrctor  ( need more clarity on this )
```javascript
function classDecorator<T extends {new(...args:any[]):{}}>(constructor:T) {
    return class extends constructor {
        newProperty = "new property";
        hello = "override";
    }
}

@classDecorator
class Greeter {
    property = "property";
    hello: string;
    constructor(m: string) {
        this.hello = m;
    }
}

console.log(new Greeter("world"));
```

### Access Descriptor
An Accessor Decorator is declared just before an accessor declaration. The accessor decorator is applied to the Property Descriptor for the accessor and can be used to observe, modify, or replace an accessor’s definitions.

Note 
TypeScript disallows decorating both the `get` and `set` accessor for a single member. Instead, all decorators for the member must be applied to the first accessor specified in document order. This is `because decorators apply to a Property Descriptor`, `which combines both the get and set accessor`, not each declaration separately.

Example
```javascript
class Point {
    private _x: number;
    private _y: number;
    constructor(x: number, y: number) {
        this._x = x;
        this._y = y;
    }

    @configurable(false)
    get x() { return this._x; }

    @configurable(false)
    get y() { return this._y; }
}
```

```javascript
function configurable(value: boolean) {
    return function (target: any, propertyKey: string, descriptor: PropertyDescriptor) {
        descriptor.configurable = value;
    };
}
```

### Property Descriptor
A Property Decorator is declared just before a property declaration.

The expression for the property decorator will be called as a function at runtime, with the following two arguments

1. Either the constructor function of the class for a static member, or the prototype of the class for an instance member.

2. The name of the member.

### Property Decorator <todo>

### Parameter Decorator <todo>

