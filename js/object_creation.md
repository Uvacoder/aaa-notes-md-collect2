# Object Creation

Ways to Create
- Object.create()
- new Object,
- var a = {};
- constructor function
### Object.create()

```js
Object.create(prototype_object, propertiesObject)
```

`Object.create` methods accepts two arguments.

`prototypeObject`: Newly created objects prototype object. It has to be an object or null.

`propertiesObject`: Properties of the new object. This argument is optional


[![Object.create](https://cdn-images-1.medium.com/max/800/1*rSHmnlUotrjc5lXV1xDtGA.png "Object.create")](Object.create "Object.create")

### Creating Object With Prototype

```js
prototypeObject = {
	fullName: function(){
		return this.firstName + " " + this.lastName		
	}
}

var person = Object.create(prototypeObject)

console.log(person) // Object with prototype object as prototypeObject and no properties

// Adding properties to the person object
person.firstName = "Virat";
person.lastName = "Kohli";

person.fullName() // Virat Kohli
```

[![Create object with prototype](https://cdn-images-1.medium.com/max/800/1*oRQuacFiOY4oY8CveoIWRQ.png "Create object with prototype")](Create object with prototype "Create object with prototype")
### propertiesObject

In the above example
we have added `firstName` and `lastName` properties after the object creation. It would have been great if we could add these properties while creating the object. To do that, we will use the `2nd argument of Object.create` method.

`propertiesObject` is used to create properties on new object. It acts as a `descriptor` for the new properties to be defined. Descriptors can be `data descriptor` or `access descriptors`.

Data descriptors are
1. configurable
2. enumerable
3. value
4. writable

Access descriptors are
1. get
2. set


```js
prototypeObject = {
	fullName: function(){
		return this.firstName + " " + this.lastName		
	}
}

var person = Object.create(prototypeObject, {
      'firstName': {
	value: "Virat", 
	writable: true, 
	enumerable: true
      },
      'lastName': {
	value: "Kohli",
	writable: true,
	enumerable: true
      }
})
    
console.log(person) // Object with prototype object as prototypeObject and properties as firstName and lastName
```

### Creation Object by Literal {}
```js
var human = {}
console.log(human);// {}
```

### Creating Object by new
```
var human = new Object()
console.log(human);// {}
```
### Constructor 

Some Testing and understanding
```js
function Pai(){

}
var hai = Object.create({})
var bai = {};
var dai = new Object();
var pai = new Pai()

hai instanceof Object //true
bai instanceof Object //true
dai instanceof Object //true

pai instanceof Object //true
pai instanceof Object //true
```
#### hai
![](https://i.snag.gy/ydZ8V7.jpg)

#### bai
![](https://i.snag.gy/g5cITN.jpg)

#### dai
![](https://i.snag.gy/5URvKA.jpg)

#### pai
![](https://i.snag.gy/WEgUdm.jpg)





