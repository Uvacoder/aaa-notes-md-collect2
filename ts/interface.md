# Interfaces

## Typescript Core princeple

One of TypeScript’s core principles is that type checking focuses on the shape that values have. This is sometimes called `duck typing` or “structural subtyping”

```javascript
function printLabel(labeledObj: { label: string }) {
    console.log(labeledObj.label);
}
let myObj = {size: 10, label: "Size 10 Object"};
printLabel(myObj);
```


