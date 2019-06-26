# Debugging ES6 to ES5
( Understanding Babel Conversion )
```javascript=
class Human {
    // ...
}

class Man extends Human {
    // ...
}

Man johnDoe = new Man();

```
Used babel to convert es6 to es5
```javascript=
"use strict";

function _possibleConstructorReturn(self, call) {
    if (!self) {
        throw new ReferenceError("this hasn't been initialised - super() hasn't been called");
    }
    return call && (typeof call === "object" || typeof call === "function") ? call : self;
}

function _inherits(subClass, superClass) {
    if (typeof superClass !== "function" && superClass !== null) {
        throw new TypeError("Super expression must either be null or a function, not " + typeof superClass);
    }
    subClass.prototype = Object.create(superClass && superClass.prototype, {
        constructor: {
            value: subClass,
            enumerable: false,
            writable: true,
            configurable: true
        }
    });
    if (superClass) Object.setPrototypeOf ? Object.setPrototypeOf(subClass, superClass) : subClass.__proto__ = superClass;
}

function _classCallCheck(instance, Constructor) {
    if (!(instance instanceof Constructor)) {
        throw new TypeError("Cannot call a class as a function");
    }
}

var Human = function Human() {
    _classCallCheck(this, Human);
};

var Man = function(_Human) {
    _inherits(Man, _Human);

    function Man() {
        _classCallCheck(this, Man);

        return _possibleConstructorReturn(this, (Man.__proto__).apply(this, arguments));
    }

    return Man;
}(Human);

var johnDoe = new Man();
```