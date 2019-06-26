# Prototype

https://hackernoon.com/prototypes-in-javascript-5bba2990e04b


### Prototype property, Prototype Object, Constructor property

- When a function is created in JavaScript, JavaScript engine adds a `prototype` property to the function. 

- This `prototype` property is an object (called as `prototype object`) 

- IT has a `constructor` property by default. 

- `constructor` property points back to the `function` on which `prototype object` is a `property`. 

- We can access the function’s prototype property using the syntax `functionName.prototype`.

![](https://cdn-images-1.medium.com/max/800/1*15Qo3ab3NPkLfXpj5AncaQ.png)


The above example shows Function Called `Human`,
`Human` Function has a `prototype` property
`prototype` property points to `prototype` Object
`prototype` Object has a `constructor` property
`constructor` property points back to `Human` Function


```js
function Human(firstName, lastName) {
	this.firstName = firstName,
	this.lastName = lastName,
	this.fullName = function() {
		return this.firstName + " " + this.lastName;
	}
}
```

What Human Function has inside `prototype` property
```js
console.log(Human.prototype)
```
![](https://cdn-images-1.medium.com/max/1000/1*kh4nYJdSFj76DM576F_brg.png)


So from the above image we can able understand prototype property of a function is a Object with two property

1. `constructor` property (which points back to Human Function)
2. `__proto__` property (which is called as hich is called as `dunder proto`)


### Instance of a Constructor Function 

```js
var person1 = new Human("Virat", "Kohli");
```

Let’s create Human instances person1 and person2 using the Human constructor function

As we can see in the below Image `person1` has a `__proto__` property which points back to `prototype Object` of the `constructor` function (Human);

![](https://cdn-images-1.medium.com/max/800/1*425LxRkFEldC5CJWyhZRBg.png)

If we print the person 1 It will print
![](https://cdn-images-1.medium.com/max/800/1*j4eUj1Ck_M93pijoX8S3Bw.png)


In the above  `person.__proto__` and `Human.prototype both are equal`

```js
person1.__proto__ === Human.prototype //true
person1.__proto__.constructor === Human //true
person`.__proto__.constructor === Human.prototype.constructor //true
```

### dunder proto is constructor function's prototype property in all instances

Let's Create one more Human instance
```
var person2 = new Human("Sachin", "Tendulkar");
```

![](https://cdn-images-1.medium.com/max/800/1*5qHhF8HTzZD2xdx3p-RLIQ.png)


Now from the above image we can able to see 
`person1` and `person1` both share same `dunder proto perperty`

> `Prototype object` of the `constructor function` is shared among all the objects created using the constructor function.


In the above `person1` and `person2` will have it's own property and method, Having own properties makes senses, But having own methods(`fullname`) does't make sense because having copy of a method for every object instance consumes more memory,


We have understood that the `prototype Object` of the constructor function is shared among it's instances, So lets declare the constructor function methods inside the prototype property. 

### Property Delegation Using prototype

//Create an empty constructor function
```js
function Person(){

}
Person.prototype.name = "Ashwin" ;

var person1 = new Person();
console.log(person1.name)//  Ashwin
```
If we print `person1`

![](https://cdn-images-1.medium.com/max/800/1*TrdhtLL9toNPQcmSgbFE7A.png)


- It doest have any property named `name`

- So What basically javascript engine does is it tried to find the `name` property in the `person1` Object,
- Once it is not available, It tried to find `name` in the `dunder proto` of the `person1` and prints the value.

- For properties other than `name` it will go on all the `dunder proto` of the `dunder proto` until `dunder proto` becomes undefined.

### Behaviour between primitive and non-primitive when it comes to property(prototype) delegation

Let's create `person1` and `person2` from the below `Person` constructor
```js
function Person(){

}
Person.prototype.name = 'Ashwin'
Person.friends = ['Jadeja', 'Vijay'];

var person1= new Person();
var person2 = new Person();
```

currently both the persons will have same `name` and same `friends`, Lets change the name of `person1` and add new friend to him.

```js
person1.name = 'Ganguly';
person1.friends.push('Karthik');
```


Now If we print `person2` name and person1 `friends`

```js
console.log(person1.name) //Ganguly
console.log(person2.name) //Ashwin
console.log(person1.friends) //['Jadeja', 'Vijay', 'Karthik']
console.log(person2.friends) //['Jadeja', 'Vijay', 'Karthik']
```


We can able to see `primitive` types does't change value of `dunder proto`, It just added new property `name` insdie `person1`;

But for `non-primitive` types the value is updated inside the `dunder proto`


In the above case if we need `friends` property not to be shared among `Instances` we simple have to move `friends` property from `prototype` of the `constructor Function` to inside the `constructor` itself

```
function Person(){
	this.friends = ['Jadeja', 'Vijay'];
}
Person.prototype.name = 'Ashwin'

```

### getPrototypeOf
```js
var Hai = function(){
	this.name = 'hai'
}
var blaHai = new Hai()
Object.getPrototypeOf(blaHai) === Hai.prototype //true
```


### Prototype Over-riding
```javascript=
function Ninja(){
	this.swing = true;
}

var ninja1 = new Ninja();

Ninja.prototype.swingSword = function(){
	return this.swing;
}

console.log(ninja1.swingSword()) // true, Accessible

Ninja.prototype = {
	jumpingHigh : function(){
		return true;
	}
}

console.log(ninja1.swingSword()) // true, Still accessible because `ninja1.__proto__` has the reference of old `Ninja.prototype` Object
```





