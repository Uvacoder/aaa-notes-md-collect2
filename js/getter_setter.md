# Getter Setter

### get and set generated properties
Javascript provides option to access a `property` through a linked function defined using `get` Keyword.

Also allows a property to be stored through a function using `set` keyword

```js
let obj = {
  firstName: 'Siva',
  lastName: 'Shanmugam',
  get fullName() {
    return this.firstName + " " + this.lastName
  },
  set fullName(value) {
    var words = name.toString().split(' ');
    this.firstName = words[0] || '';
    this.lastName = words[1] || '';
  }
};

console.log(obj.fullName) //Siva Shanmugam
obj.fullName = 'Sivashanmugam Kannan'
console.log(obj.fullName) //Sivashanmugam Kannan
console.log(obj.firstName) //Sivashanmugam
console.log(obj.lastName) //Kannan
```

### set and get using Object.defineProperty 
```js
Object.defineProperty(person, 'fullName', {
    get: function() {
        return firstName + ' ' + lastName;
    },
    set: function(name) {
        var words = name.split(' ');
        this.firstName = words[0] || '';
        this.lastName = words[1] || '';
    }
});
```

Rather than setting the object properties through object literal Creating through `Object.defineProperty`  gives advantage of setting the `property descriptors` 
(Writable, Readable, Enumarable, value) 
along while creating.

If we set `value` property descriptor then `get` and `set` function not allowed  for the property and vice versha


#### Private variable implementation using getter and setter
![](https://i.imgur.com/YJlj6yV.png)

### Validating properties using getter and Setter
```javascript=
let obj = {
  get count() {
    return this.count;
  },
  set count(value) {
    if(Number.isInteger(value){
		this.count = value;
	}else{
		throw 'Error, Invalid variable type, Only Integers Allowed';
	}
  }
};
```


