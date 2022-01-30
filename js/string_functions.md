# string functions and props

### length

```js
let txt = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
let length = txt.length; //length of the string
```

### slice

it parses one elemnet before the end index

```js
let txt = "ABCDEF";
console.log(txt.slice(0,0))//''
console.log(txt.slice(0,1))//'A'
console.log(txt.slice(0,2))//'AB' 
console.log(txt.slice(0,5))//'ABCDE' 
```


### replace

two arguments
1 => the one you want to match
2 => the string you want to replace the match

```js
let text = "Bomboy is renamed";
let newText = text.replace("Bomboy", "Mumbai");
```

The replace first arguement also can be a regular expressions

### concat

1st arguement => while concating we can add an inbetween string
2nd arguement => the string which want to concat with

```js
let text1 = "Hello";
let text2 = "World";
let text3 = text1.concat(" ", text2);
```

### trim

removes empty spaces around the string and returns new string

```js
let text1 = "      Hello World!      ";
let text2 = text1.trim();//Hello world
```

### pad start and pad end

Pad enalbles add missing characters if we expect a string to have specifc length

```js
let str = 'TITLE';
let title = str.padStart(2, '*')) //TITLE//no use here as the str alredy filled the expected characters
title = str.padStart(10, '*')) //*****TITLE
title = str.padStart(7, '*')) //**TITLE
title = str.padEnd(2, '*')) //TITLE
title = str.padEnd(10, '*')) //TITLE*****
```

[use cases of pad start and end](https://javascript.plainenglish.io/3-practical-uses-of-padstart-and-padend-bc7f197d3e91)


### split function

```js
let text = "a,b,c,d,e,f";
let myArray = text.split(","); //['a', 'b', 'c', 'd', 'e', 'f']
myArray = text.split(""); ['a,b,c,d,e,f'];
```
