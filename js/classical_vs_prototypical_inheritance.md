# Classical vs Prototypical inheritance 

[link 1](https://medium.com/javascript-scene/master-the-javascript-interview-what-s-the-difference-between-class-prototypal-inheritance-e4cd0a7562e9)

[link 2](https://stackoverflow.com/questions/19633762/classical-inheritance-vs-prototypal-inheritance-in-javascript)

[link 3](http://ngninja.com/posts/prototypal-vs-classical-inheritance)

## Classical inheritance Example ES6

```js
class Human {
    // ...
}

class Man extends Human {
    // ...
}

var johnDoe = new Man();

```

## prototypical inheritance

```js
var Human = function(){
}

var man = function(){
    this = new Human();
}

var jhon = new function
var human = {};
var man = Object.create(human);
var johnDoe = Object.create(man);
```
