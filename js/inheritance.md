# Inheritance 

https://hackernoon.com/inheritance-in-javascript-21d2b82ffa6f


### Portion 1 (METHOD 1)
```js
//SuperType constructor function
function SuperType(){
	this.name = "Virat"
}

//SuperType prototype
SuperType.prototype.getSuperName = function(){
	return this.name
}

//SubType prototype function
function SubType(){
	this.age = 26
}

//Inherit the properties from SuperType
SubType.prototype = new SuperType();
```


### Portion 2 (METHOD 1)
```js
//Add new property to SubType prototype
SubType.prototype.getSubAge = function(){
	return this.age;
}

//Create a SubType object
var subTypeObj = new SubType();
console.log(subTypeObj.name); //Output: Virat
console.log(subTypeObj.age); //Output: 26
console.log(subTypeObj.getSuperName()); //Output: Virat
console.log(subTypeObj.getSubAge()); //Output: 26
```

### The problem in the Method 1
Before we going in to the problem lets reiterate the basics
```
function Person(){

}
console.log(Person.prototype)
```
Every function will contain `prototype` property
Every prototype property will contain a `constructor` property

The `constructor` will point to function Object where the prototype property live.

Also if we create a instance through the function Constructor for example
```
function Person(){
	this.dance = true;
}
var siva = new Person();
console.log(siva instanceOf Person) //true
```

#### Now lets take the method 1 and discuss the problem
In the method 1 code the subTypeObj will lose it's access to actual Constructor

```
console.log(subTypeObj instanceOf SubType) //false
console.log(subTypeObj instanceOf SuperType) //true
```

#### How to overcome the problem we face in method 1
Before go to the solution do a rewind of `Object.defineProperty`. More details available in note called `property Descriptor`.

```
SubType.prototype = new SuperType();
```

After assigning the new instance of SuperType function constructor, Again over-ride the right constructor object through `Object.defineProperty` function

```javascript=
SubType.prototype = new SuperType();
Object.defineProperty(SubType.prototype, 'constructor', {
	configurable : false,
	enumarable : false,
	writable: true,
	value : SubType
})
var subTypeObj = new SubType();
console.log(subTypeObj instanceof SubType) //true
```



### Portion 1 (Method 2)
```js
//SuperType constructor function
function SuperType(firstName, lastName){
	this.firstName = firstName,
	this.lastName = lastName,
	this.friends = ["Ashwin", "Jadeja"]
}

//SuperType prototype
SuperType.prototype.getSuperName = function(){
	return this.firstName + " " + this.lastName;
}

//SubType prototype function
function SubType(firstName, lastName, age){
	//Inherit instance properties
	SuperType.call(this, firstname, lastName);
	this.age = age;
}
```

### Portion 2 (Method 2)
```js
//Inherit methods and shared properties
SubType.prototype = new SuperType();

//Add new property to SubType prototype
SubType.prototype.getSubAge = function(){
	return this.age;
}

//Create SubType objects
var subTypeObj1= new SubType("Virat", "Kohli", 26);
var subTypeObj2 = new SubType("Sachin", "Tendulkar", 39);

//Modify the friends property using the subTypeObj1
subTypeObj1.friends.push("Amit");

console.log(subTypeObj1.friends);//["Ahswin", "Jadega", "Amit"]
console.log(subTypeObj2.friends);//["Ashwin", "Jadega"]

//subTypeObj1
console.log(subTypeObj1.firstName); //Output: Virat
console.log(subTypeObj1.age); //Output: 26
console.log(subTypeObj1.getSuperName()); //Output: Virat Kohli
console.log(subTypeObj1.getSubAge()); //Output: 26

//subTypeObj2
console.log(subTypeObj2.firstName); //Output: Sachin
console.log(subTypeObj2.age); //Output: 39
console.log(subTypeObj2.getSuperName()); //Output: Sachin Tendulkar
console.log(subTypeObj2.getSubAge()); //Output: 39
```

### Method 3
```javascript=
var ironman = {'intelligent': true};
var spiderman = {'jumphigh': true};
console.log('intelligent' in spiderman) // false
Object.setPrototypeOf(spiderman, ironman) 
console.log('intelligent' in spiderman) // true
```
`spiderman` before and after applying of
```
Object.setPrototypeOf(spiderman, ironman) 
```
BEFORE
![](https://i.imgur.com/6cWyhC4.png)

AFTER
![](https://i.imgur.com/6cWyhC4.png)

Let's add 'hulk'
```javascript=
var hulk = { 'strong' : true };
Object.setPrototypeOf(hulk, spiderman);
```
![](https://i.imgur.com/oO3b3Ku.png)

