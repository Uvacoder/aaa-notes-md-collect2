# new Operator

### How it is used
```js
function User(name) {
  this.name = name;
  this.isAdmin = false;
}

let user = new User("Jack");

alert(user.name); // Jack
alert(user.isAdmin); // false
```

### Behind the scenes
```js
function User(name) {
  // this = {};  (implicitly)

  // add properties to this
  this.name = name;
  this.isAdmin = false;

  // return this;  (implicitly)
}
```
### Return from constructors

Usually, constructors do not have a `return` statement. Their task is to write all necessary stuff into `this`, and it automatically becomes the result.

But if there is a return statement, then the rule is simple:

- If return is called with object, then it is returned instead of this.
- If return is called with a primitive, it’s ignored.
In other words, return with an object returns that object, in all other cases this is returned

### Explicit return of constructor function

##### Behaviour when  Non Object return value inside constructor function

```javascript=
function fnClass(){
	this.print = function(){}
	return '1'
}
var fnInstance = new fnClass()
typeof fnInstance === 'object' //true
typeof fnInstance.print === 'function' //true
```
As we can see the explicit return value is ignored, the `this` returned

##### Behaviour when  Object return value inside constructor function

```javascript=
var mirrorObj = {
	amIMirror : true
}
function fnClass(){
	amIMirror : false
	return mirrorObj
}
var fnInstance = new fnClass()
typeof fnInstance === 'object' //true
typeof fnInstance.amIMirror === true //true
```
As we can see the explict return value got accepted when it is a Object





