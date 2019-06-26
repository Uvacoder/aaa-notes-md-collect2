# $parse, $compile, $interpolate
`$parse` is used by `$interpolate` to evaluate individual expressions (name, extension) against a scope. 

It can be used to both read and set values for a given expression. 

For example, to evaluate the name expression one would do: `$parse('name')($scope)`

to get the "image" value. To set the value one would do: `$parse('name').assign($scope, 'image2')`


# Interpolation

### What compiler internally uses 
    `$parse` service to evaluate strings aginst scope.d

```javascript=
    $interpolate(templateText)(object with properties);
```

Example
```javascript=
var app = angular.module("myApp", ["ngSanitize"]);

    app.controller("myCtrl", ["$scope", "$interpolate", function($scope, $interpolate) {

      var myname = {
        name: "<strong>Anil Singh</strong>"
      };

      var templateText = "Hello my name is {{name}} !";
      
      $scope.result = $interpolate(templateText)(myname);

}]);
```

Interpolate function takes the first argument and  finds the interpolate markups ({{}}) and resolves agains the properties of second argument.

### angularJS ng-href
```htmlmixed=
    <a ng-href="img/{{username}}.jpg">Hello {{username}}!</a>

```

During the compilation process the compiler uses the `$interpolate` service to see if text nodes and element attributes contain interpolation markup with embedded expressions.

if that is the case, the compiler adds an `interpolateDirective` to the node and registers watches on the computed interpolation function, which will update the corresponding text nodes or attribute values as part of the `normal digest cycle`.

### How interpolation markups get's replaced 
If the interpolation value is `String`

1. `undefined` and `null` are converted to ''
2. if the value is an `object` that is not a `Number`, `Date` or `Array`, `$interpolate` looks for a custom `toString()` function on the object, and uses that. 
3. if the above doesn't apply, `JSON.stringify` is used.

# Compiler Service

### What compiler internally uses 
    `interpolate` service to evaluate expressions agains scope
The `$compile` service is the service to use for compilation. Invoking `$compile` against markup will produce a function you can use to bind the markup against a particular scope


Let's say a directive says hello to different users and takes different 


```javascript=
app.directive("dynamicHello", function($compile){
    return{
        link: function(scope, element){
            var template = "<button ng-click='doSomething()'>{{label}}</button>";
            var linkFn = $compile(template);
            var content = linkFn(scope);
            element.append(content);
        }
    }
});



```


