# property Descriptor

To remember shortly 
WrEnCo ()

## What is property descriptor in Object
In JavaScript, every object property is described with a property descriptor through which we can configure the following keys:

### property Descriptors

`configurable`
- If set to true, the property’s descriptor can be changed and the property can be deleted. 
- If set to false, we cannot do either of these things.

`enumerable`
- If set to true, the property shows up during a for-in loop over the object’s properties (we’ll get to the for-in loop soon).

`value`
- Specifies the value of the property. Defaults to undefined.


`writable`
- If set to true, the property value can be changed by using an assignment.

`get`
- Defines the getter function, which will be called when we access the property. Can’t be defined in conjunction with value and writable.

`set`
- Defines the setter function, which will be called whenever an assignment is made to the property. Also can’t be defined in conjunction with value and writable.


## Example 
```
ninja = {};
ninja.name = "Yoshi";
```

The property name will configurable, enumarable, writable, value will assigned to "Yoshi" and get and set would be undefined.

## Object.defineProperty
![](https://i.imgur.com/dzI7V9G.png)

In the above example `name` and `weapon` will be listed down in a `for in loop`.

But the `sneaky` will not be as its property descriptor `enumarable` set to false.




