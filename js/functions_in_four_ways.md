# Functions in Four ways

1. Function Declarations
2. Function Expressions
3. Function Constructors
4. Function Generators

The Syntex definition as per ECMA ( https://www.ecma-international.org/ecma-262/5.1/ )

![](https://i.imgur.com/mSV8caB.png)

## differnce between function expression and declaration

![](https://i.imgur.com/G0rgY67.png)

```javascript=
function add(){} // function declaration
var add = function(){} // the right side of the assignment is function expression
function add(function(){ // the argument of add the return value of the argument both are function expression
	return function(){}
	```javascript=
}())
(function add(){})() //function expression
```

## Immedetly Invoked Function Expression  ( IIFE)

Example 1

```javascript=
(function(a){return a +2 })(3) // 5
(function(a){return a +2 }(3)) // 5
```

In the above example we use the argument outside paranthesis in 1st example inside paranthesis in second example, Both are same, There no difference between them.

The reason why we use a paranthesis around the function expression is the javascript parser need to differentiate between function expression and function declaration
If we put a function expression and without any paranthesis the javascript parser will consider it as a function declaration and throw error

![](https://i.imgur.com/5xgzJiM.png)

Example 2 (IIFE)

```javascript=
+function(){}();
-function(){}();
!function(){}();
~function(){}();
```

We can use the unary operators to mention functions expression to the javascript parser by placing them as prefix.
