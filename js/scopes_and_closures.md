# Scopes & Closures

### Scope 
If a variable or function is accissible it is in the scope of execution context
There are three scopes
	- Local Scope
	- Clousure Scope
	- Global Scope
	
### Closure Scope

Simple closure
```javascript
function pam() {
    var name = "Pam Beesly";
    function setName(newName) {
        name = newName; //Here name variable is accessible through global scope
    }
	function displayName(){
		console.log(name)
	}
    setName("Pam Halpert");
}
pam();
```

Closure scope from a returned function
```
function makeWorker() {
  let name = "Pete";

  return function() {
    alert(name); //when this getting executed the variable `name` will be available in closure scope
  };
}

let name = "John";

// create a function
let work = makeWorker();

// call it
work();
```

### closure usecases

Closures used to create factory functions
And closures are core of functional programming
#### Function factories
There are many ways to create a object, 
Object.create, {} (Object literal), new Object, and factory function
```javascript
function Employee(designation){
	var dbAccess;
	if(designation == 'prject manager'){
		dbAccess = true;
	}else{
		dbAccess = false;
	}
	return function(name){
		console.log(`${name} the ${designation} and dbAccess ${dbAccess}`);
	}
}
var projectManager = Employee('project manager');
var ram = projectManager('Ram'); //Ram the manager and dbAccess true
var juniorDeveloper = Employee('Junior Developer');
var siva = juniorDeveloper('Siva') //Siva the Junior Developer and dbAccess false
```

### Callbacks 
Whenever IO request or Settimeout callback is executing the callback uses Closure scope to access the variables outside it's local scope.

```javascript
let name = "Siva"
settimeout(function(){
	console.log(name) //name is accessed through closure scope here
}, 2000)
```

### Find out the answer ( Test )

```js
let deck = {
    suits: ["hearts", "spades", "clubs", "diamonds"],
    cards: Array(52),
    createCardPicker: function() {
        return function() {
            let pickedCard = Math.floor(Math.random() * 52);
            let pickedSuit = Math.floor(pickedCard / 13);

            return {suit: this.suits[pickedSuit], card: pickedCard % 13};
        }
    }
}

let cardPicker = deck.createCardPicker();
let pickedCard = cardPicker();
```

[Answer and explnation](https://www.typescriptlang.org/docs/handbook/functions.html#this-and-arrow-functions)
