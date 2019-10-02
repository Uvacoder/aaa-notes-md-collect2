# forEach, map, reduce, Filter, Every, Some, Find

## forEach

Foreach takes a callback function and run that callback function on each element of array one by one.

```js
var sample = [1, 2, 3];
// es5
sample.forEach(function (elem, index){
   console.log(elem + ' comes at ' + index);
})
```

## filter

filter is that forEach just loop over the array and executes the callback but filter executes the callback and check its return value

```js
var sample = [1, 2, 3] // yeah same array
// es5
var result = sample.filter(function(elem){
    return elem !== 2;
})

console.log(result) //[1,3]
```

## map

 makes it unique is it generate a new array based on your existing array.

```js
var sample = [1, 2, 3] // i am never gonna change Boo! Yeah
// es5
var mapped = sample.map(function(elem) {
    return elem * 10;
})

console.log(mapped) // [10, 20, 30]
```

## reduce ( aggregating )

```js
var array = [1,2,3,4]
var sum = array.reduce(function(aggregate, number){
    return aggregate + number
},0)
assert(sum === 10, 'aggregate is 10');
```

```js
var array = [1,2,3,4]
var sum = array.reduce(function(aggregate, number){
    return aggregate + number
},100)
assert(sum === 110, 'aggregate is 110');
```

```js
var array = [1,2,3,4]
var sum = array.reduce(function(aggregate, number){
    return aggregate + '--' +number
},'siva')
assert(sum === 'siva--1--2--3--4', 'aggregate return string');
```

## every and some ( returns Boolean )

```js
var ninjas = [
{ name : 'katana', weapon : 'katana' }
{ name : 'shinchan' },
{ name : 'naruto', weapon: 'needle' }
];

var allNinjasAreNamed = ninjas.every(function(ninja){
    return 'name' in ninja;
})

var allNinjasAreArmed = ninjas.every(function(ninja){
    return 'weapon' in ninja;
})
assert(allNinjasAreNamed, 'All the ninjas are named');
assert(!allNinjasAreArmed, 'Not all the ninjas armed');

var someNinjasAreArmed = ninjas.some(function(ninja){
    return 'weapon' in ninja
})
assert(someNinjasAreArmed, 'Some ninjas are armed');
```

## find

```js
var ninjas = [
{ name : 'goku', weapon : 'katana' }
{ name : 'shinchan' },
{ name : 'naruto', weapon: 'needle' }
];

var result = ninjas.find(function(ninja){
    return ninja.weapon == 'needle';
})
assert(ninja.name === 'goku', 'goku is weapon katana');
```

## findIndex

```js
var ninjas = [
{ name : 'goku', weapon : 'katana' }
{ name : 'shinchan' },
{ name : 'naruto', weapon: 'needle' }
];

var result = ninjas.findIndex(function(ninja){
    return ninja.name == 'shinchan';
})
assert(result === 1, 'Shinchan is sitting at 1st index')
```

## sort

```js
var array = [5,3,1,2,4];
array.sort(function(a,b){
    return a-b;
})
console.log(array) // [1,2,3,4,5]
```

- If a callback returns a value less than 0, then item a should come before item b.
- If a callback returns a value equal to 0, then items a and b are on equal footing (as far as the sorting algorithm is concerned, they’re equal).
- If a callback returns a value greater than 0, then item a should come after item b.




