# Object

### Computed Property
```js
let fruit = 'apple';

let bag = {
  [fruit]: 5, // the name of the property is taken from the variable fruit
};
```

### Reserved Words are allowed as Object Properties
A variable cannot have a name equal to one of language-reserved words like “for”, “let”, “return” etc.

But for an object property, there’s no such restriction. Any name is fine:
```js
 let obj = {
  for: 1,
  let: 2,
  return: 3
}

alert( obj.for + obj.let + obj.return );
```
### Object Property proto
Basically, any name is allowed, but there’s a special one: `__proto__`
```js
let obj = {};
obj.__proto__ = 5;
alert(obj.__proto__); // [object Object], didn't work as intended
```

### Property value shorthand
In real code we often use existing variables as values for property names.

For instance
```js
function makeUser(name, age) {
  return {
    name: name,
    age: age
    // ...other properties
  };
}

let user = makeUser("John", 30);
alert(user.name); // John
```
In the example above, properties have the same names as variables. The use-case of making a property from a variable is so common, that there’s a special property value shorthand to make it shorter.

Instead of name:name we can just write name, like this:
```js
function makeUser(name, age) {
  return {
    name, // same as name: name
    age   // same as age: age
    // ...
  };
}
```

We can use both normal properties and shorthands in the same object:
```js
let user = {
  name,  // same as name:name
  age: 30
};
```

### Property Existence check
let user = {};

```js
alert( user.noSuchProperty === undefined ); // true means "no such property"
```
or
```js
let user = { name: "John", age: 30 };

alert( "age" in user ); // true, user.age exists
alert( "blabla" in user ); // false, user.blabla doesn't exist
```

### The for…in loop
```js
for(key in object) {
  // executes the body for each key among object properties
}
```
Note that all “for” constructs allow us to declare the looping variable inside the loop, like let key here.
```js

for(let key in user) {
  // keys
  alert( key );  // name, age, isAdmin
  // values for the keys
  alert( user[key] ); // John, 30, true
}
```

### Ordered like an object
```js
let codes = {
  "49": "Germany",
  "41": "Switzerland",
  "44": "Great Britain",
  // ..,
  "1": "USA"
};

for(let code in codes) {
  alert(code); // 1, 41, 44, 49
}
```
But if we run the code, we see a totally different picture:

USA (1) goes first
then Switzerland (41) and so on.
### Integer property
So, “49” is an Integer property name, because when it’s transformed to an integer number and back, it’s still the same. But “+49” and “1.2” are not:
```js
 // Math.trunc is a built-in function that removes the decimal part
alert( String(Math.trunc(Number("49"))) ); // "49", same, integer property
alert( String(Math.trunc(Number("+49"))) ); // "49", not same "+49" ⇒ not integer property
alert( String(Math.trunc(Number("1.2"))) ); // "1", not same "1.2" ⇒ not integer property
````
### Two objects are equal only if they are the same object.

```js
let a = {};
let b = a; // copy the reference

alert( a == b ); // true, both variables reference the same object
alert( a === b ); // true
```

```js
let a = {};
let b = {}; // two independent objects

alert( a == b ); // false
```

### Object.assign
How to get clone of the object rather than getting reference of the object
```js
let user = {
  name: "John",
  age: 30
};

let clone = {}; // the new empty object

// let's copy all user properties into it
for (let key in user) {
  clone[key] = user[key];
}

// now clone is a fully independant clone
clone.name = "Pete"; // changed the data in it

alert( user.name ); // still John in the original object
```

Rather than writing for loop for we can use `Object.assign` function 

The syntax is 
`Object.assign(dest[, src1, src2, src3...])
`

And Example for Cloning using Object.assign
```
let user = {
  name: "John",
  age: 30
};

let clone = Object.assign({}, user);
```
More Examples about Object.assign

```js
let user = { name: "John" };

let permissions1 = { canView: true };
let permissions2 = { canEdit: true };

// copies all properties from permissions1 and permissions2 into user
Object.assign(user, permissions1, permissions2);

// now user = { name: "John", canView: true, canEdit: true }
```

If the destination Object has a property of any one of the source Object property then Destination Obj Property  value will be overridden by the source Object Property value

```js
let user = { name: "John" };

// overwrite name, add isAdmin
Object.assign(user, { name: "Pete", isAdmin: true });

// now user = { name: "Pete", isAdmin: true }
```

### Deep Cloning

the simple Object.assign will create a clone only when all the Object properties Data types are Primatives

If Source Object has a property and if that is Object, Then Object.assign will not help

```js
let user = {
  name: "John",
  sizes: {
    height: 182,
    width: 50
  }
};

let clone = Object.assign({}, user);

alert( user.sizes === clone.sizes ); // true, same object

// user and clone share sizes
user.sizes.width++;       // change a property from one place
alert(clone.sizes.width); // 51, see the result from the other one
```

To fix that we should use a cloning loop which check any of the cloning property is also a Object, If yes then it replicates that structure as well which is called `deep cloning`

### Object.seal
:sparkle: method seals an object, preventing new properties from being added to it 

:sparkle: marking all existing properties as non-configurable.

```javascript=
const object1 = {
  property1: 42
};

Object.seal(object1);
object1.property1 = 33;
console.log(object1.property1);
// expected output: 33

delete object1.property1; // silently cannot delete when sealed
object1.anotherPropery = 2; // silently cannot be added
```

We can also check whether it's sealed through

```javascript=
Object.isSealed(obj); // === true
```

### Object.values

Returns object property values in a array

```js
var person = {
  'name':{
    'firstname' : 'siva',
    'lastname' : 'shanmugam'
  },
  'age' : {
    'value':12
  }
}
Object.values(person)
/*
[
  {firstname: "siva", lastname: "shanmugam"},
  {value: 12}
]
 */
```

