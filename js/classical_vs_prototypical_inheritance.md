# Classical vs Prototypical inheritance 

https://medium.com/javascript-scene/master-the-javascript-interview-what-s-the-difference-between-class-prototypal-inheritance-e4cd0a7562e9

https://stackoverflow.com/questions/19633762/classical-inheritance-vs-prototypal-inheritance-in-javascript

http://ngninja.com/posts/prototypal-vs-classical-inheritance

# Classical Inheritance vs Prototypical

**Classical inheritance**  Creating using `new` Operator

**Prototypical inheritance** Creating using Object.create(1)

Example ES6
```javascript=
class Human {
    // ...
}

class Man extends Human {
    // ...
}

Man johnDoe = new Man();

```

### Level of Abstraction
```
----------------------+----------------+---------------------------------------+
| Level of Abstraction | Name of Entity |                Comments               |
+----------------------+----------------+---------------------------------------+
| 0                    | John Doe       | Real World Entity.                    |
| 1                    | johnDoe        | Variable holding object.              |
| 2                    | Man            | Class of object johnDoe.              |
| 3                    | Human          | Superclass of class Man.              |
+----------------------+----------------+---------------------------------------+
```


### prototypical inheritance
```javascript=
var human = {};
var man = Object.create(human);
var johnDoe = Object.create(man);
```

### Level of Abstraction
```
+----------------------+----------------+---------------------------------------+
| Level of Abstraction | Name of Entity |                Comments               |
+----------------------+----------------+---------------------------------------+
| 0                    | John Doe       | Real World Entity.                    |
| 1                    | johnDoe        | Variable holding object.              |
| 2                    | man            | Prototype of object johnDoe.          |
| 3                    | human          | Prototype of object man.              |
+----------------------+----------------+---------------------------------------+
```

