#Metadata reflection
http://blog.wolksoftware.com/decorators-metadata-reflection-in-typescript-from-novice-to-expert-part-4

In this post we will learn about:

1. Why we need reflection in JavaScript?
2. The metadata reflection API
3. Basic type serialization
4. Complex type serialization


## 1. Why we need reflection in JavaScript?
The name `reflection` is used to describe code which is able to inspect other code in the same system

##### Use cases ( no cluse what are each now ) 
Reflection is useful for a number of use cases (Composition/Dependency Injection, Run-time Type Assertions, Testing).

Our JavaScript applications are getting bigger and bigger and we are starting to need some tools

### What reflection is allows to examine
A powerful reflection API should allow us to examine an unknown object at run-time and find out everything about it.

1.The name of the entity.
2.The type of the entity.
3.Which interfaces are implemented by the entity.
4.The name and types of the constructor arguments of the entity.
5.The name and types of the constructor arguments of the entity.

##### Some basic javascript reflection

In JavaScript we can use functions like `Object.getOwnPropertyDescriptor()` or `Object.keys()` to find some information about an entity but we need reflection to implement more powerful development tools

## 2.The metadata reflection API
We must use it with TypeScript 1.5 and the `compiler flag emitDecoratorMetadata`

We also need to including a reference to `reflect-metadata.d.ts` and load the `Reflect.js` file


How to get metadata info
##### 1.Type metadata uses the metadata key `design:type`

```javascript
 function logType(target : any, key : string) {
      var t = Reflect.getMetadata("design:type", target, key);
      console.log(`${key} type: ${t.name}`);
}
	
class Demo{ 
      @logType // apply property decorator
      public attr1 : string;
    }

// output : attr1 type: String

```

##### 2.parameter type metadata uses the metadata key `design:paramtypes`.
```javascript=
 function logParamTypes(target : any, key : string) {
 	var types = Reflect.getMetadata("design:paramtypes", target, key);
 	var s = types.map(a => a.name).join();
 	console.log(`${key} param types: ${s}`);
 }  
	
 class Foo {}
 interface IFoo {}

class Demo{ 
	@logParameters // apply parameter decorator
	doSomething(
	param1 : string,
	param2 : number,
	param3 : Foo,
	param4 : { test : string },
	param5 : IFoo,
	param6 : Function,
	param7 : (a : number) => void,
	) : number { 
	return 1
	}
}

// output :   doSomething param types: String, Number, Foo, Object, Object, Function, Function
```

##### 5.Return type metadata uses the metadata key `design:returntype`.

```javascript
Reflect.getMetadata("design:returntype", target, key);
```

### 3.Basic Type serialization
- In the above parameter type metadata example we can able to see `IFoo` and Object literal `{ test : string}` are serialized as object. 

- because TypeScript only supports basic type serialization 

Basic serialization rules
number serialized as Number
boolean serialized as Boolean
any serialized as Object
void serializes as undefined
Array serialized as Array
If a Tuple, serialized as Array











