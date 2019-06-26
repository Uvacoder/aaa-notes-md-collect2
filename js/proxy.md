# proxy
It is introduced in es6

```javascript=
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

#### Usecase of proxy 
##### 1 ( Making loggin easier for functions )
![](https://i.imgur.com/eYyCRfr.png)

##### 2 ( Evaluating Performence of a function )
![](https://i.imgur.com/MLPOmUu.png)

##### 3 ( Negative Index of a function )
Accessing values through Negative index is a regular thing in Python, Ruby, Pearl. But in javascript with the help of Proxy we can implement it.

![](https://i.imgur.com/4aQs2hS.png)

##### 4 ( Auto Populating Properties )
```javascript=
const rootFolder = new Folder();
rootFolder.ninjasDir = new Folder();
rootFolder.ninjasDir.firstNinjaDir = new Folder();
rootFolder.ninjasDir.firstNinjaDir.ninjaFile = "yoshi.txt";
```
![](https://i.imgur.com/UAIc66J.png)

#### Performence measurement of proxies
In the below code we can see the time difference ratio of accessing array through direct object and proxy object
```javascript=
function measure(items){
	var startTime = new Date();
	for(var i = 0;i < 500000;i++){
		items[0] === 'siva';
		items[1] === 'shanmugam';
		items[2] === 'karthi';
	}
	return new Date() - startTime;
}

const name = ['siva', 'shanmugam', 'karthi']
var nameProxy = new Proxy(name, {
	get: function(target, index){
		return target[index]
	},
	set : function(target, index, value){
		return target[index] = value;
	}
})
Math.round(measure(nameProxy) / measure(name)) // 20 ( Will return different values in different browsers and differnt time )
```


