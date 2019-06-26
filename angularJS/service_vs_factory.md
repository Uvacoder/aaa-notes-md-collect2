# Services vs Factory


```javascript=
app.service('MyService', function () {
  this.sayHello = function () {
    console.log('hello');
  };
});
```

## Service
**Definition**
`.service()` is a method on our module that takes a name and a function that defines the service. Pretty straight forward. Once defined, we can inject and use that particular service in other components, like controllers, directives and filters, like this:

```javascript=
app.controller('AppController', function (MyService) {
  MyService.sayHello(); // logs 'hello'
});
```


## Factory
```javascript=
app.factory('MyFactory', function () {
  return {
    sayHello: function () {
      console.log('hello');
    }
  }
});
```
**Definition**
Again, `.factory()` is a method on our module and it also takes a name and a function, that defines the factory. We can inject and use that thing exactly the same way we did with the service. Now what is the difference here?

**Difference**
In Factory instead of working with `this` in the factory, we’re returning an `object literal`.

> a service is a `constructor function` whereas a factory is not. Somewhere deep inside of this Angular world, there’s this code that calls `Object.create()` with the service constructor function,

## Angular source code of factory and service

### Factory source code
```javascript=
function factory(name, factoryFn, enforce) {
  return provider(name, {
    $get: enforce !== false ? enforceReturnValue(name, factoryFn) : factoryFn
  });
}
```

It takes the name and the factory function that is passed and basically `returns a provider` with the same name, that has a `$get` method which is our factory function

### Provider

 whenever you ask the injector for a specific dependency, it basically asks the corresponding provider for an instance of that service, by calling the `$get()` method.

```javascript=
MyServiceProvider.$get(); //
```

### Service Source code
```javascript=
function service(name, constructor) {
  return factory(name, ['$injector', function($injector) {
    return $injector.instantiate(constructor);
  }]);
}
```

So we can see when service is invoked it basically returns execution of a factory function, which means service is a superset of factory or service also a factory function internally.

But service not only passes the `service constructor` function. It passes a function that pass `$injector`which instantiates the constructor function as object. That's why service functions defined with `this` keyword.

## Finaly what's the difference

`Service` is just a constructor function
that will be called with 'new'

`factory` returns an object
you can run some code before, 
So for factory we can run predefined code 

So factory runs some code before it return our object literal. That basically allows us to do some configuration stuff or conditionally create an object or not

But we can also make a service function like a factory function

```javascript=
app.service('MyService', function () {

  // we could do additional work here too
  return {
    sayHello: function () {
      console.log('hello');
    };
  }
});
```

> So its clear that factory and services are't different, We can write a service as a factory, But not vice versa, 

## ES6 classes

We can write services using es6 classes
```javascript=
class MyService {
  sayHello() {
    console.log('hello');
  }
}

app.service('MyService', MyService);
```