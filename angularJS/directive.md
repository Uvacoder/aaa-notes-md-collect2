# angularJS directive

### Custom directive


### $scope true, false or undefined {} inside angular custom directive

### 2CP( Controller, Compile, Prelink, Postlink)

![](https://i.imgur.com/EmFY9id.png)

### Example Code 2CP
```htmlmixed=
<div ng-controller="msg">
     <div message text="first">
     </div>
</div>
```
in the above code message is a custom angular js directive
```javascript=
app.directive('message', function(){
     return;
})
```

msg controller and message directive
```javascript=
var app = angular.module('app', [])   ;

app.controller('msg', ['$scope', function($scope){

});

app.directive('message', function($interpolate){
     return {
          //compile phase
          compile: function(tElement, tAttributes){ //tElement is template element
               console.log(tAttributes.text + '_in compile');
               return {
                    //pre linking and post linking phase will returned as part of compilation phase, but the execution will happen only happen after the controller phase 
                    //iElement= i instance
                    pre: function(scope, iElement, iAttributes){
                         console.log(iAttributes.text + "_in pre ");
                    },
                    post: function(scope, iElement, iAttributes){
                         console.log(iAttributes.text + "_in post ");
                    },
                   
               }
          }

          //controller phase
     controller: function($scope, $element, $attrs){
          console.log($attrs.text +'_in controller');
     }
     }
})
```

### Naming of Controller parameters
```javascript=
    controller: function($scope, $element, $attrs){
```

     The `$element` and `$attrs` name should same, If it changes the injector will fail for controller

### Order of execution 2CP
![](https://i.imgur.com/TLhjDkW.png)


### Example order of 2CP

```htmlmixed=
<html>
   <head>
      //angular bootstrap code
   </head>
   <body ng-app="app">
      <div ng-controller="msg">
      l
      <div message text="first">
         <div message text="....second">
             <div message text="........third">
             </div>
          </div>
      </div>
      </div>
   </body>
</html>
```

```
first_in compile
....second_in compile
........third_in compile
first_in controller
first_in pre link
....second_in controller
....second_in pre link
........third_in controller
........third_in pre link
........third_in post link
....second_in post link
first_in post link
```


### Real Example 2CP
```htmlmixed=
<html>
     <head>
          //angular bootstrap code
     </head>
     <body ng-app="app">
          <div ng-controller="msg">
              <div message text="{{i}}" ng-repeat="i in [1,2,3,4,5]>
                    {{i}}
               </div>
          </div>
     </body>
</html>
```

**Result**

```
1
2
3
4
5
```


**Console log output**
```javascript=
{{i}}_in compile //Compilation only once, no scope, hence {{i}}
{{i}}_in controller 
1_in pre //scope avail
1_in post //scope avail
{{i}}_in controller
2_in pre
2_in post
{{i}}_in controller
3_in pre
3_in post
{{i}}_in controller
4_in pre
4_in post
{{i}}_in controller
5_in pre
5_in post
```

### Real Example notes
* compilation no scope 
* why controller prints `{{i}}_in controller`
* interpolate function 
```javascript=
     controller: function($scope. $element, $attrs){
          var v = $interpolate($attrs.text)($scope);
          //console.log($attrs.text +'_in controller');
          console.log(v +'_in controller');
     }
```
* After chaning controller function output
```javascript=
{{i}}_in compile
1_in controller
1_in pre
1_in post
2_in controller
2_in pre
.
.
.
etc
```

### interpolate

### Applying border color in compilation
```javascript=
compile: function(tElement, tAttributes){ //tElement is template element
    tElement.css("border", 1px solid red");
    console.log(tAttributes.text + '_in compile');
}
```
![](https://i.imgur.com/8CvHL9r.png)

### Which places is Changing DOM correct
Post linkign is best place 
```javascript=
post: function($scope, iElement, iAttributes) {
   if (iAttributes.text === "3") {
	   iElement.css("border", "1px solid red")
   }
   console.log(iAttributes.text + "_in post ");
},
```
![](https://i.imgur.com/o3WpdU7.png)

### When compile phase not needed

```javascript=
app.directive('message', function($interpolate){
    return {   
        link: {
                    pre: function(scope, iElement, iAttributes){
                    },
                    post: function(scope, iElement, iAttributes, controller){
                    },                   
     },
        controller: function($scope. $element, $attrs){
         
        }
    }
})

```


### No need Pre linking phase
```javascript=
/only written the body of the return function of app diretive 
compile: function(tElement, tAttributes) {
  //post-link funciton
  return function(scope, iElement, iAttributes, controller) {
    
  }
}
```

### No need compile, pre
```javascript=
app.directive('message' function($interpolate){
     //post-link function
     return function(scope, iElement, iAttributes, controller){
     }        
}
```

### Priority and Terminal
The priority is only relevant when you have multiple directives on one element. The priority determines in what order those directives will be applied/started. 

https://stackoverflow.com/questions/15266840/how-to-understand-the-terminal-of-directive