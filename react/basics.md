# Basics

## How does React Work ?

- React creates a VIRTUAL DOM in memory.
- React only changes what needs to be changed!
- React finds out what changes have been made, and changes only what needs to be changed.

## ReactDOM  

The `ReactDOM.render()` function takes two arguments, HTML code and an HTML element.

## JSX

- JSX allows us to write HTML elements in JavaScript and place them in the DOM without any createElement()  and/or appendChild() methods.

- JSX converts HTML tags into react elements.

### Example  - 1 ( With JSX)

```js
const myelement = <h1>I Love JSX!</h1>;

ReactDOM.render(myelement, document.getElementById('root'));
```

### Example  - 1 ( With out JSX)

```js
const myelement = React.createElement('h1', {}, 'I do not use JSX!');

ReactDOM.render(myelement, document.getElementById('root'));
```

