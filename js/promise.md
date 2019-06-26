# Promise

My own promise impelementation
https://github.com/shivashanmugam/js-lab/blob/master/promiese-implementation/promise.js

```
A Promise is an object representing the eventual completion or failure of an asynchronous operation.
```

## Promise Example
```javascript=
var timeOutIn = 1000; //1 second
var sPromise = new Promise(function(resolve, reject){
	setTimeout(function(){
		if(Math.floor(Math.random() * 100) % 2 == 0){
			resolve('SUCCESS')
		}else{
			reject('ERR')
		}
	}, timeOutIn)
})
```

## States
Promise has three states basically
- pending
- fulfilled
- rejected

`pending` is when the asyncronous event is not yet finished (neither rejected nor resolved),  If the above code example if we increase `timeOutIn` value to `15` seconds and if we check the `sPromise` Object before 15 seconds exceed, the status of the `sPromise` will be `pending`.
![](https://imgur.com/b0b6155d-c458-4959-aa87-ff6166c6860f)


after executing the promise and if it is resolved the value of `sPromise`
![](https://i.imgur.com/S4E9mzA.png)

after executing the promise if the promise is rejected it will throw an error if there is no catch

![](https://i.imgur.com/U8yTJlO.png)

Now Lets attach a event for then Property for a resolved promise 
### then property of promise 
```javascript=
var successCallBack = function(resolvedData){
	console.log('The resolved Value is ' + resolvedData)
}
sPromise.then(successCallBack);  //The resolved Value is SUCCESS
```

### catch property of promise 
Now lets attach a catch function for a failed callback
```javascript=
sPromise.catch(function(rejectedData){
	console.log(`rejected Data is ${rejectedData}`);
})
rejected Data is ERR
```

### finally property of promise
Finally is a property which is used to do some processing regardless of the outcome,

```javascript=
sPromise.finally(function(){
	console.log(`finally the promise is over, Let's do something irrespective whether it failed of success`);
	console.log('Eat pizza');
})
```

## Chained Promises
 As the `Promise.prototype.then()` and `Promise.prototype.catch()` methods return promises, they can be chained.

![](https://mdn.mozillademos.org/files/15911/promises.png)

Let's take an example to understand promise chain
```
var firstPromise = new Promise(function(resolve, reject){
	setTimeout(function(){
		resolve('SUCCESS')
	}, 10000)
})

var anotherPromise = sPromise.then(function(data){
	return 'this string will go as a resolved value of a promise'
})
```

Hence it's clear that inside then function the return value is a promise;
```
var firstPromise = new Promise(function(resolve, reject){
	setTimeout(function(){
		resolve('SUCCESS')
	}, 10000)
})
firstPromise.then(function(data){
	return 'this string will go as a resolved value of a promise'
}).then(function(data){
	console.log('from finside chained promise');
	console.log(data)
})
```
So we can write code like below 

If the print the `anotherPromise` 
![](https://i.imgur.com/9c1gxT0.png)

## Promise.all
Returns a promise that either fulfills when all of the promises in the iterable argument have fulfilled or rejects as soon as one of the promises in the iterable argument rejects.

## Promise.race 
Returns a promise that fulfills or rejects as soon as one of the promises in the iterable fulfills or rejects

## Promise syncronous event
```
var value = new Promise(function(resolve, reject){
	resolve(42);
})
```
If we print value it will show
`Promise {<resolved>: 42}`


## Promise.all
In the below code p2 is not a return of promise resolve, But 

Syntax
```
Promise.all(iterable);
```

An iterable object such as an Array or String.

>An already resolved Promise if the iterable passed is empty.

```javascript=
var p1 = Promise.resolve(3);
var p2 = 1337;
var p3 = new Promise((resolve, reject) => {
  setTimeout(resolve, 100, 'foo');
}); 

Promise.all([p1, p2, p3]).then(values => { 
  console.log(values); // [3, 1337, "foo"] 
});
```
> If the iterable contains non-promise values, they will be ignored, but still counted in the returned promise array value 

That's why when values got printed `1337` also got printed.

## Promise.race

The Promise.race(iterable) method returns a promise that resolves or rejects as soon as one of the promises in the iterable resolves or rejects,

```
var promise1 = new Promise(function(resolve, reject) {
    setTimeout(resolve, 500, 'one');
});

var promise2 = new Promise(function(resolve, reject) {
    setTimeout(resolve, 100, 'two');
});

Promise.race([promise1, promise2]).then(function(value) {
  console.log(value);
  // Both resolve, but promise2 is faster
});
```

