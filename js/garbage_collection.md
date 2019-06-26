# Garbage Collection

https://javascript.info/garbage-collection

In javaScript Garbage collection is based on `rechability`.

Checking whether and Object are Primitive Object Values are rechablie from the Root (Global)

### Simple Example
```js
// user has a reference to the object
let user = {
  name: "John"
}
```
[![Simple Example](https://javascript.info/article/garbage-collection/memory-user-john.png "Simple Example")]("Simple Example "Simple Example")

Currently The Variable `user` reference the Object with property `name` which stored the value Jhon. So the Object is rechable from the global scope through `user` variable.

But Once the user Variable Overridden, The The Object becomes unrechanble.

```js
user = null;
```

[![Object Null](https://javascript.info/article/garbage-collection/memory-user-john-lost.png  "Object Null")](Object Null "Object Null")

So The Object memory does't have any reference we can delete this

### Two references
```js
// user has a reference to the object
let user = {
  name: "John"
};

let admin = user;
```
[![two ref](https://javascript.info/article/garbage-collection/memory-user-john-admin.png "two ref")](two ref "two ref")

Now if we do the same:
```js
user = null;
```
Then the object is still reachable via admin global variable, so it’s in memory. If we overwrite admin too, then it can be removed.

### Interlinked objects
```js
function marry(man, woman) {
  woman.husband = man;
  man.wife = woman;

  return {
    father: man,
    mother: woman
  }
}

let family = marry({
  name: "John"
}, {
  name: "Ann"
});
```
[![2 family](https://javascript.info/article/garbage-collection/family.png "2 family")](2 family "2 family")

As of now, all objects are reachable.

Now let’s remove two references:
```js
delete family.father;
delete family.mother.husband;
```
[![delete member](https://javascript.info/article/garbage-collection/family-delete-refs.png "delete member")](delete member "delete member")


It’s not enough to delete only one of these two references, because all objects would still be reachable.

But if we delete both, then we can see that John has no incoming reference any more:
![](https://javascript.info/article/garbage-collection/family-no-father.png)


Outgoing references do not matter. Only incoming ones can make an object reachable. So, John is now unreachable and will be removed from the memory with all its data that also became unaccessible.

After garbage collection:
![](https://javascript.info/article/garbage-collection/family-no-father-2.png)

### Unreachable island

It is possible that the whole island of interlinked objects becomes unreachable and is removed from the memory.

The source object is the same as above. Then:
```js
family = null;
```

The in-memory picture becomes:
![](https://javascript.info/article/garbage-collection/family-no-family.png)

### Garbage Collection Algorithms
Some of the Internal Algorithms of Garbage Collection
- mark and sweep
- Generational collection 
- Incremental collection
- Idle-time collection

