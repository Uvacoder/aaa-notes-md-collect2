# ES6 features

## Default valur for function parameter
```javascript
function greet(name, greetWith = 'Hello'){
	console.log(greetWith+' '+name);
}
greet('Sergio Ramos', 'Ola');
greet('Harry Kane');
````

## For loop
```js
var names = ['john' , 'ryan', 'jack']
for(var name of names){
	console.log(name)
}
```

## Template Strings
```js
var firstName = 'sivashanmugam';
var lastName = 'kannan'
var fullname = `${firstName} ${lastName}`;
console.log(fullname) //sivashanmugam kannan
```

## Lamdas
By default inside a class consturctor `this` variable inside eventListners does't mention the `object instance` created
```js
function Counter(el) {
    var container = document.getElementById('container');
    this.count = 0;
	el.addEventListener('click', function(event){
		this.count += 1 //here `this`mentions global variable not the object instance
		el.innerHTML = this.count; 
	})
}
new Counter(container);
```

To fix the `this` keyword issue inside event listner, We store the object instance inside the object instance with a variable `_this`
```javascript
function Counter(el) {
var _this = this;
    _this.count = 0;
	el.addEventListener('click', function(event){
		_this.count += 1 //here `this`mentions global variable not the object instance
		el.innerHTML = _this.count; 
	})
}
```

This conversion is now made as default in es6

But to make the conversion possible we have use ES6 arrow function instead of normal function callback syntax. Below is that

```javascript
function Counter(el) {
        this.count = 0;
        el.innerHTML = this.count;
        el.addEventListener('click', 
            (event) => el.innerHTML = (this.count += 1))
    }
```

By pasting the above script in babel es6 to es5 we can see the difference.


## Destructuring 

### Array
ES6 syntax
```javascript
var array = [32, "John", true];
var [totalStudents, teacherName, isMale] = array;
```
ES5 Conversion
```javascript
var array = [32, "John", true];
var totalStudents = array[0],
    teacherName = array[1],
    isMale = array[2];
```

### Object
es6
```javascript
const heroes = [
      { id: 11, name: 'dr strange' },
      { id: 12, name: 'spiderman' },
    ];
var marvel = {heroes};
marvel.heroes == heroes
Object.keys(marvel) //heroes
```

es5
```
const heroes = [
      { id: 11, name: 'dr strange' },
      { id: 12, name: 'spiderman' },
    ];
marvel.heroes = heroes;
```


es6
```javascript
function todoVarDecl(id){
	var todo = {
		"id": id,
		"name": "sivashanmugam",
		"location": "bengaluru"
	}
	return todo
}

var {id, name, location} = todo(21);
```
es5
```javascript
"use strict";

function todoVarDecl(id) {
	var todo = {
		"id": id,
		"name": "sivashanmugam",
		"location": "bengaluru"
	};
	return todo;
}

var _todo = todo(21),
    id = _todo.id,
    name = _todo.name,
    location = _todo.location;
```
Destructuring and optional parameter
es6
```javascript
function greet({name, greetWith:greetWith = 'Hello'}){
	console.log(`${greetWith} ${name}`);
}
greet('Sergio Ramos', 'Ola');
greet('Harry Kane');
```
es6
```javascript
'use strict';

function greet(_ref) {
	var name = _ref.name,
	    _ref$greetWith = _ref.greetWith,
	    greetWith = _ref$greetWith === undefined ? 'Hello' : _ref$greetWith;

	console.log(greetWith + ' ' + name);
}
greet('Sergio Ramos', 'Ola');
greet('Harry Kane');
```

## Spread Operator
When we don't how many parameters the function is going to have in that case we use spread operator
es6
```js
function calculate(action, ...values){
	if(action == 'add'){
		var i = 0, total;
		for(var i = 0;i < values.length;i++){
			total = total + values[i]
		}
	}
	return total;
}
calculate('add', 1,2,3,4,5);
```
es5
```js
'use strict';

function calculate(action) {
	if (action == 'add') {
		var i = 0,
		    total;
		for (var i = 0; i < (arguments.length <= 1 ? 0 : arguments.length - 1); i++) {
			total = total + (arguments.length <= i + 1 ? undefined : arguments[i + 1]);
		}
	}
	return total;
}
calculate('add', 1, 2, 3, 4, 5);
```

### Another example for spread
es6
```js
var source = [3, 4, 5];
var target = [ 1, 2, ...source, 6, 7 ];
```

es5
```javascript
var source = [3, 4, 5];
var target = [1, 2].concat(source, [6, 7]);
```
## Computed properties 
es6
```javascript
var fruit_var = 'fruit'
var eatables = {[fruit_var]: 'Apple', vegetable: 'Carrot'}
```
es5
```js
var eatables = {vegetable: 'Carrot'}
var fruit_var = 'fruit'
eatables[fruit_var] = 'Apple'
```
Another example for computed properties
```js
const osPrefix = 'os_';

var support = {
    [osPrefix + 'Windows']: isSupported('Windows'),
    [osPrefix + 'iOS']: isSupported('iOS'),
    [osPrefix + 'Android']: isSupported('Android'),
}

function isSupported(os) {
    return Math.random() >= 0.5;
}
```

## Let and const
Before we discuss about its usage, We will see it's behaviour inside Block Environment, Block environment is nothing but the scope between two curly brace. 
```js
// Global Environment
function Random(){
	//Function Environment
	if(){
		var name = 'siva';
		//Block Environment
	}
	console.log(name) //siva
}
```
If we define the a variable with `var` keyword that variable will be defined to the nearest Function environenment or Global Environment. The block level environment ignored for variables with defined using `var`;

But if define using `let` or `const` it will be defined to the nearest Block environment and it will be accessible in function environment.

```js
// Global Environment
function Random(){
	//Function Environment
	if(){
		//Block Environment
		var name = 'siva';
		let age = 18;
		const dob = '15-dec-1994'
	}
	console.log(name) //siva
	console.log(age) //undefined
	console.log(dob) //undefined
}
```

### Lets see How var and let workds works inside a forloop

```js
var arr = ['Red', 'Blue', 'Green']
for(var i =0; i < 3;i++){
	setTimeout(function(){
		console.log(`the Value of i is ${i} and array value is ${arr[i]})
	})
}
```
The above example will print the below line `4` times
```
the Value of i is 4 and array value is undefined 
```
For loop with `let`
```js
var arr = ['Red', 'Blue', 'Green']
for(let i = 0; i < 3;i++){
	setTimeout(function(){
		console.log(`the Value of i is ${i} and array value is ${arr[i]})
	})
}
```
Result
```
the Value of i is 0 and array value is Red
the Value of i is 1 and array value is Blue
the Value of i is 2 and array value is Yellow
```
The Reason being,  Upon each For loop execution a new block scope will be created and as `i` variable is defined as let, The `i` value will be created in Block Environment upon each for.

So setTimeout callback considers `i` from block scope not from function scope. 

#### let
variabled defined using let keyword can be modified even after it's declaration, It is same as `var` except it considers block environment during definition.


#### const
on the other hand variables defined const keyword cannot be changed for Non-Objects. If we try it will throw exception.
```js
	const name = 'sivashanmugam'
	name = 'karthi'; //THROWS EXCEPTION
```

But for objects the behaviour is different, Only the reference of the object cannot be changed, Which means the cannot have any other object reference or Non-object value
```js
const studentTopper = {}
studentTopper.name = 'Sivashanmugam'; //WORKS FINE 
studentTopper.name = 'Karthi'; //WORKS FINE
delete studentTopper.name; //WORKS FINE


var studentLoser = {};
const teacherHot = {};
studentTopper = studentLoser; //throws Exception 
studentTopper = teacherHot; //throws Exception
studentTopper = 'karthi' //throws Exception
```

## class keyword

Why class keyword was introduced

many developers, especially those from a classical object-oriented background, would prefer a simplification or abstraction of JavaScript’s inheritance system into one that they’re more familiar with

This inevitably leads toward the realm of classes, even though JavaScript doesn’t support classical inheritance natively. As a response to this need, several JavaScript libraries that simulate classical inheritance have popped up. Because each library implements classes in its own way, the ECMAScript committee has standardized the syntax for simulating class-based inheritance.

![reference](https://i.imgur.com/hL6myoh.png)

### Static keyword inside Class

```js
class Ninja {
    constructor(swordLength){
		this.swordLength = swordLength;
	}
	function swingSword(){
		return true;
	}
	static function compare(ninja1, ninja2){
		return ninja1.swordLength - ninja2.swordLength;
	}
}
var ninja1 = new Ninja(4);
var ninja2 = new Ninja(3);
console.log(ninja1.compare) //undefined
console.log(ninja2.compare) //undefined

console.log(Ninja.compare(ninja1, ninja2)); //1	
```

![](https://i.imgur.com/tUFl9tb.png)

## Inheritance in es6 
Before we see the inheritance of es6, Look at the note `inheritance` which compiles the different ways of inheritance in es5

![](https://i.imgur.com/673BCKg.png)
```js
class Person{
	constructor(name){
		this.name = name;
	}
	dance(){
		return true;
	}
}
```
![](https://i.imgur.com/zcE6gSd.png)

```js
class Ninja extends Person{
	constructor(name, weapon){
		super(name)
		this.weapon = weapon;
	}
	wieldWeapon(){
		return true;
	}
}
```
![](https://i.imgur.com/lMxRxku.png)

```
var ninja1 = new Ninja('shiva', 'sword');
```

![](https://i.imgur.com/93WIoBk.png)



## super keyword


## Proxy
```js
var emporer = {
	'name' : 'Siva'
}
var representative = new Proxy(emporer, {
	get:(target, key){
		console.log('Accessing through proxy');
		return key in target ? target[key] : 'Dont bother Emporer'
	}
	
	set: (target, key, value){
		console.log('Setting value of through proxy')
		target[key] = value;
	}
})
console.log(emporer.name) //'Siva'
console.log(representative.name) //Accessing through proxy //Siva
console.log(representative.nickName) // Dont bother Emporer
representative.nickName = 'Kannan'; // Setting value through proxy

```

In the above example we have only gone through two traps
`get` and `set` traps. But there are more traps like `apply` which will be applied when caling a function.
`enumarate` trap will be called during `for in` loop
`getPrototypeOf` and `setPrototypeOf` Will be invoked when setting or getting prototype object.

Some functions and conditions which cannot be trapped in proxy `instanceOf` and `typeOf`. 

## Map 
Before jumping in to the new Map keyword, lets go back and understand why it requires in the first place,

### Using regular objects as maps and its drawbacks

#### Examle - 1 dictionary

Imagine that somewhere on our site we need to access the translation for the word constructor, so we extend the dictionary example into the following code.

![](https://i.imgur.com/F4A7rZB.png)

Lets say there is a word `constructor` which we forgot to define in the dictionary.

So when we try to access `dictionary['ja']['constrctor']` it is expected to return `undefined`, 

But it returns `function Object() {[native Code]}`, Because every object will have a constructor property.

#### Examle - 2 DOM elements maping

In this example we set an object as a property for an object, When we do that instead of the object the string will stored.

```js
var siva = { name:'sivashanmugam'}
var mapObjCompanies = {};
mapObjCompanies[siva] = {workedCompanies : ['funtoot', 'higherone', 'indosakura']}
assert(Object.keys(mapObjCompanies) === ["[object Object]"]);

```
As we can see `mapObjCompanies` contains `[object Object]` as it's property, When 

### Solution through Map keyword

```js
var ninja1 = {name:'hatori'};
var ninja2 = {name:'goku'};
ninjaHomeLandMap.set(ninja1, {homeLand: "tokyo"});
ninjaHomeLandMap.set(ninja2, {homeLand: "herishima"});
assert(ninjaHomeLandMap.get(ninja1).homeLand == "tokyo", 'ninja1 is from tokyo')
```

![](https://i.imgur.com/VqYwGrs.png)
```js
assert(ninjaHomeLandMap.size == 2 ,'Size is two');
assert(ninjaHomeLandMap.has(ninja1) == true, 'Contains ninja1 in map')
ninjaHomeLandMap.delete(ninja2)
assert(ninjaHomeLandMap.has(ninja2) == false, 'ninja2 got deleted')


// Iterating Map Object
for(var item of ninjaHomeLandMap){
  assert(item[0] !== null, "Key:" + item[0]);
  assert(item[1] !== null, "Value:" + item[1]);
}
```

## Set and List

### Set

![](https://i.imgur.com/bNKsJzb.png)

```javascript
var samurai = ['jackson', 'hattori'];
var ninja = ['siva', 'hattori'];
var warriors = new Set([...samurai, ...ninja, 'bahubali']);
console.log(warriors) // Set(4) {"jackson", "hattori", "siva", "bahubali"}
```

## Symbols 

```js
var symbol_1 = Symbol('symbol one');
var obj = {}
console.log(symbol_1) //Symbole(symbol one);
obj[symbol_1] = 'ONE'
var symbol_one = Symbol('symbol one');
obj[symbol_one] = 'ஒன்று';
console.log(symbol_one) //Symbole(symbol one);
```

![](https://i.imgur.com/DtMgWcP.png)

### Behaviour

```js
var symbol_1 = Symbol('symbol one');
console.log(symbol_1) //Symbole(symbol one);
console.log(symbol_1 + ' haha') // throw error

typeof symbol_1;     // "symbol" 

const globalSym = Symbol.for('foo'); // global symbol
console.log(Symbol.keyFor(globalSym));
```

### Use case

<the use cases on yet to be fully explored >
The use case will be described here breifly, The use he has explained is keeping track of `isMoving` property on a DOM element before we apply a css transition.

https://hacks.mozilla.org/2015/06/es6-in-depth-symbols/