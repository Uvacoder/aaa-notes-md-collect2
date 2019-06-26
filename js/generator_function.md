# Generator Function

They’re especially good for working with multiple asynchronous steps

Before we see fully about generator function let's understand a scenario why and when we need a generator function

### Pseduo Scenario 
We need to get first ninja's mission details, The below pseduo code has a psedo syncGetJSON ( a non-existing syncronouse function to read a JSON file).
```
try {
   var ninjas = syncGetJSON("ninjas.json");
   var missions = syncGetJSON(ninjas[0].missionsUrl);
   var missionDetails = syncGetJSON(missions[0].detailsUrl);
   //Study the mission description
}
catch(e){
  //Oh no, we weren't able to get the mission details
}
```
Javascript cannot be blocked as it is single threaded.

### Let see actual Implementation of the Psedo-scenario in javascript

```javascript=
getJSON("ninjas.json", function(err, ninjas){
  if(err) {
    console.log("Error fetching list of ninjas", err);
    return;
  }
  getJSON(ninjas[0].missionsUrl, function(err, missions) {
    if(err) {
      console.log("Error locating ninja missions", err);
      return;
    }
  getJSON(missions[0].detailsUrl, function(err, missionDetails){
    if(err) {
      console.log("Error locating mission details", err);
      return;
    }
    //Study the intel plan
    });
  });
});
```

This code creates a callback hell and it's difficult to understand straight forward.

### Generator Function
It is defined by putting a asterick right after the function  keyword.

We can also use the yield keywords in generator function
```javascript=
async (function *(){
try{
	const ninjas = yield getJSON("ninjas.json");
	const missions = yield getJSON(ninjas[0].missionsUrl);
	const missionDescription = yield(missions[0].detailsUrl);
}
catch(e){
	//oh no, we were't able to get the mission details.
}
})
```

#### The theory definition
A generator is a function that generates a sequence of values, but not all at once, as a standard function would, but on a per request basis. 

We have to explicitly ask the generator for a new value, and the generator will either respond with a value or notify us that it has no more values to produce.

after a value is produced, a generator function doesn’t end its execution, as a normal function would. Instead, a generator is merely suspended.

#### the example

```javascript=
function WeaponGenerator(){
	yield "Katana";
	yield "Wakizashi";
	yield "Kasarigama";
	
}
```

#### Consuming WeaponGenerator Example 1 
```javascript=
for(let weapon of WeaponGenerator()) {
  assert(weapon, weapon);
}
```

#### Controlling generator function through iterator object

Making a call to a generator doesn’t mean that the body of the generator function will be executed. Instead, an iterator object is created, an object through which we can communicate with the generator

See the below self explainable image
![](https://i.imgur.com/J8uTEPu.png)

#### Generator function and while loop
![](https://i.imgur.com/8RgxZti.png)

#### Generator function delegation
By using the yield* operator on an iterator
![](https://i.imgur.com/ACgx3nN.png)

Output
```
"Sun Tzu"
"Hattori"
"Yoshi"
"Genghis Khan"
```

### Use case 1 ( Generating Unique Identifiers Using Generator Function)

#### requirement
When creating certain objects, often we need to assign a unique ID to each object.

#### The normal way
The easiest way to do this is through a global counter variable

#### The problem in the normal way
that’s kind of ugly because the variable can be accidently messed up from anywhere in our code. 

#### The generator way
```javascript=
function *idGenerator(){
	var i = 1;
	while(1){
		yield i++;
	}
}

var idIterator = idGenerator();
const ninja1 = { 'id' : idIterator.next().value } // {id:1}
const ninja1 = { 'id' : idIterator.next().value } // {id:2}
const ninja1 = { 'id' : idIterator.next().value } // {id:3}
```

#### The closure Way
```javascript=
function idGeneratorConstructor(){
	var id = 1;
	return function(){
		return id++;
	}
}
var idGenerator = idGeneratorConstructor();
const ninja1 = { 'id' : idGenerator() } // {id:1}
const ninja1 = { 'id' : idGenerator() } // {id:2}
const ninja1 = { 'id' : idGenerator() } // {id:3}
```

### Use case 2 - ( DOM Traversal )
The general way 
![](https://i.imgur.com/XWJspRQ.png)

Understand the DOM Traversal and make it better using Generator functions.
DONT SEE THE ANSWER
.
.
.
.
.
![](https://i.imgur.com/HsltF51.png)


## Communicating with generator Function
So far we have seen generator returning multiple values.

### Two Way communication
We can also send data to a genarator, there by acheiving two way communication.

A example to understand it
![](https://i.imgur.com/WtXXQfw.png)

#### Throwing exceptions into generator in two way communication
![](https://i.imgur.com/hkPE5r2.png)

Instead of calling next with iterator, just need to call iterator.throw()

### Exploring Generators under the Hood
Like promise generator also has multiple execution states

- Suspended start
Generator is created, But no code Executed
- Executing

- Executing
Code of the generator is getting executed either from start or from last suspended state.

- Suspended yield
When a generator reaches yield expression it creates a object carring the return value and suspends the execution. 

- Completed
If the generator returns or runs out of code to execute, it moves to completed state.

A diagram expalining the states of execution.

![](https://i.imgur.com/Wgg9QSj.png)


















