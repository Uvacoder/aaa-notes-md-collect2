# Use Strict

### What becomes strict
In the below case `print` & `tell` both executes in strct mode,
```js
"use strict"

function print(val){
    console.log(val);
}

function tell(val){
    alert(val);
}
```

"use strict"
In the below case only print function executes under strict mode
```js
function print(val){
	"use strict"
    console.log(val);
}

function tell(val){
    alert(val);
}
```
### Undeclared variable
```js
"use strict"
a = 12; //this throws exception in strict mode. In non-strict mode a new property for window object is created.
```
### Delete Operator
Delete operator is used to delete user defined object properties and array elements. If we try to delete anything other than user defined object properties or array elements we get an exception

```js
var a = 78;
delete a; //throws exception in strict mode. In non strict mode it returns false and program continues. 'a' is treated as a global variable not as an property of window object in both modes, so property operations are not allowed in variable a.
delete window.a; //throws exception in strict mode. In non strict mode it returns false and program continues.


window.b = 34;
delete window.b; //In both modes property b is deleted.


delete Math.PI; //In strict mode it returns Error as PI is pre defined. In strict mode exception is thrown.
delete Object.prototype; //deleting an undeletable
property in non-strict mode returns false. But in strict mode exception is thrown.

```


### Duplicate property names
When using the same name for your properties, the second property will overwrite the first.
```
var a = {x: 1, x: 2};
console.log(a); // {x: 2}
```
But under Strict mode this will be considered as a error 

```
function haveES2015DuplicatePropertySemantics() {
  'use strict';
  try {
    ({prop: 1, prop: 2});

    // No error thrown, duplicate property names allowed in strict mode
    return true;
  } catch(e) {
    // Error thrown, duplicates prohibited in strict mode
    return false;
  }}
```
### Modifing non-writable property in strict mode
While the world waits for ES6 to finally arrive with the desired const statement, non-writable properties are the most similar thing to a constant that we have in Javascript. Once its value is defined, it is not possible to change it using assignments
```
var ob = {a: 1};
 
Object.defineProperty( ob, 'B', {value: 2, writable:false} );
 
ob.B; // => 2
 
ob.B = 10;
 
ob.B; // => 2

n strict mode, trying to modifying a non-writable property would throw an TypeError exception:

function updateB(){
  'use strict';
  ob.B = 4; // This would throw an exception
}
 
updateB(); // Throws the exception. I told you.
```

### duplicate Parameter names
```js
function print(value, value) {} //throws exception.
```

### Octal numeric literals and escape character not allowed
```js
var testStrict = 010;  // throws exception
var testStrict = \010; // throws exception.
```


### eval and arguments
```js
var eval = 12; //In non-strict mode eval is overwritten. Exception thrown in strict mode.
var arguments = 12;//Same behavior as above.
```

### Reserved Keywords
```js
Reserved keywords are:

implements
interface
package
private
protected
public
static
yield
```

```js
"use strict"
 var private = 12; //in non-strict mode this is allowed. In strict mode this throws an exception.
```
### This inside global functions
```
"use strict"
function checkforthis(){
console.log(this); //will print undefined.
}
checkforthis();
```

### Creating variables using eval
```
"use strict"
eval("var q = 12");
console.log(q); //throws exception. q is not defined.
```

### Removes Alias behaviour between functions arguments and function parameter

Let's See first the normal javascript behaviour, In the below example name and anotherName are not a value reference as `name` variable hold string value. Only for objects references will be created.
```javascript=
var name = 'karthi'
var anotherName = name;
name = 'siva'
console.log(anotherName) //karthi

var cat = { name : 'blossom' }
var anotherCat = cat;
cat.name = 'spring';
console.log(anotherCat.name) //spring
```

( `Alias Behaviour` )In the below example eventhough name and arguments[0] hold string value they still refer the same value, Hence if we change anyone the other will get affected 
```javascript=
function printName(name){
	console.log(`name: ${name} and arguments[0] : ${arguments[0]}`) 
	name = 'new Karthi'
	console.log(`${arguments[0]}`) // new Karthi
}
printName('siva')
```

As we had seen the above example is a contradict behaviour of javascript, To prevent this behaviour we need to use `use strict`
```javascript=
use strict;
function printName(name){
	console.log(`name: ${name} and arguments[0] : ${arguments[0]}`) 
	name = 'new Karthi'
	console.log(`${arguments[0]}`) //siva
}
printName('siva')
```

