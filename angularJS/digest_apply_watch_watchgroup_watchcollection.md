# $digest, $apply, $watch, $watchCollection, $watchGroup

### digest Cycle
Angular's digest cycle can be called on any scope object (be it rootScope or a child scope in a controller). 

When `$scope.digest()` gets called, Angular goes through all of the watchers that have been registered in the current scope and any child scopes. For each watcher, if the watched value has changed since the previous digest cycle, the watcher's listener function gets called. If the watched value has not changed, Angular simply moves on to the next watcher in the list. You may see this process referred to as dirty checking.

After Angular reaches the last watcher that has been registered in the scope, the digest cycle is not quite done. Angular runs through all of the watchers again to see if any changed values in the first journey through the list of watchers has caused any other watched expressions to change. Angular will continue running through the list of watchers up to 10 times. If it finds that no values have changed, the digest cycle is complete, and the DOM will be updated accordingly. If at the end of 10 trips through there are still changed values, Angular will throw an error.

### how does $scope.digest() get called
Sometimes you need to manually trigger the digest cycle by calling `$scope.$apply()` (the best practice) or `$scope.digest()`
```javascript=
scope.$apply(function() {
    //fire the onClick function
    scope.$eval(attrs.myClick);
});
```

### $apply equvalent and why it's nearly equivalent
```javascript=
$scope.$apply(doSomething)
//is nearly equivalent to

doSomething();
$scope.digest();
```
### $watch a function 
```javascript=
$scope.$watch(function() { return someVal; }, function() {
    //someCallback
});
```

This listener function here (someCallback) would be called any time `function() { return someVal; } `returns a value that is different than the previous one.

### $watch collection
`$watchCollection` will shallow watch the properties on a single object and notify you if one of them changes.
```javascript=
var person = {
	'name':'jhon',
	'age':13,
	'parents':{
		'mother':'jasmine',
		'father':'ryan'
	}
};
$scope.$watchCollection('person', function(updatedPerson) {
    //the array has been updated
    console.log('updated array: ', updatedArray);
});
if any of the properties of `person` changes the watch will be triggered
```

### $watchGroup 
however watches a group of individual watch expressions.
```
var person = 'sivashanmugam';
var personLoc = 'Bengaluru';
var personAge = 15;
$scope.$watchGroup(['person', 'personLoc', 'personAge'] function(updatedPersonVariable) {
    
});
```
If any changes in the any of scope variables happens then the watch listener will be triggered

### $watch 
```javascript=
var values = ['firstName', 'lastName', 'email'];
$scope.$watchGroup(values, function(values) {
    //the details for the user have been updated
});
```