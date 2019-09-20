# Async & Await

Basicallly Async & await is a better syntax sugar for promise's `then`

## Async function

```js
async function f() {
  return 1;
}
```

The above function `f` is `async` function which will return a promise even it does't use `resolve` and `reject`

### Async equvalent through promise

```js
function f() {
    return new Promise(resolve, reject){
        resolve(1)
    }
}
```

if the execute the above code

```js
f.then(function(data){
    console.log(data) //``
})
```

## Await keyword

What is await is that instead of writing the `then`  combination for to handle when a `promise` is resolving or getting rejected

```js
let result = await f;
```

## Await keyword in promise

```js
let result;
f.then(function(data){
    console.log(data) //``
    result = data;
})
```

We cannot `await` for a non-async function it will throw error.

```js
    function f(){return 1}; let result = await f //error
```

The error will be `SyntaxError: await is only valid in async function`

## sample async function example

```js
async function f() {
  return Promise.resolve(1);
}

f().then(alert); // 1
```

## sample async await example

```js
const fs = require('fs');
async function f() {
    let readFile = new Promise(function (resolve, reject) {
        setTimeout(() => {
            resolve('Hi I am awaited (callback) result');
        }, 1000);
    })
    const result = await readFile;
    console.log(result);
}
f(); //prints Hi I am awaited (callback) result after one second
```
