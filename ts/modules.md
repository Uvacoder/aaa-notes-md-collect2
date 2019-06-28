# modules
https://www.typescriptlang.org/docs/handbook/modules.html#export


Modules are executed within their own scope, not in the global scope

this means that variables, functions, classes, etc. declared in a module are not visible outside the module unless they are explicitly exported using one of the `export forms`

Conversely, to consume a variable, function, class, interface, etc. exported from a different module, it has to be imported using one of the `import form`

## Export Forms

#### Direct Export
`ZipCodeValidator.ts`
```typescript
export const numberRegexp = /^[0-9]+$/;

export class ZipCodeValidator implements StringValidator {
    isAcceptable(s: string) {
        return s.length === 5 && numberRegexp.test(s);
    }
}
```

#### Renamed Export
```typescript
class ZipCodeValidator implements StringValidator {
    isAcceptable(s: string) {
        return s.length === 5 && numberRegexp.test(s);
    }
}
export { ZipCodeValidator };
export { ZipCodeValidator as mainValidator };
```

#### Re-export
`ParseIntBasedZipCodeValidator.ts`
```typescript
export class ParseIntBasedZipCodeValidator {
    isAcceptable(s: string) {
        return s.length === 5 && parseInt(s).toString() === s;
    }
}

// Export original validator but rename it
export {ZipCodeValidator as RegExpBasedZipCodeValidator} from "./ZipCodeValidator";
```

Optionally A Module can wrap one or more modules and combine them using 
`export * from "module`
```typescript
export * from "./StringValidator"; // exports interface 'StringValidator'
export * from "./LettersOnlyValidator"; // exports class 'LettersOnlyValidator'
export * from "./ZipCodeValidator";  // exports class 'ZipCodeValidator'
```


## Import Forms

Simple import
```typescript
import { ZipCodeValidator } from "./ZipCodeValidator";
let myValidator = new ZipCodeValidator();
```

#### Renamed Import
```typescript
import { ZipCodeValidator as ZCV } from "./ZipCodeValidator";
let myValidator = new ZCV();
```
#### Import complete module
```
import * as validator from "./ZipCodeValidator";
let myValidator = new validator.ZipCodeValidator();
```

#### Import for Side-effects
Though not recommended practice, some modules set up some global state that can be used by other modules. These modules may not have any exports, or the consumer is not interested in any of their exports. To import these modules, 

```typescript
import "./my-module.js";
```

#### Default Export and Import
- Each module can optionally export a default export
- Default exports are marked with the keyword default;
- there can only be one default export per module.
- default exports are imported using a different import form.
- Classes and function declarations and variables can be authored to default export

Default export 
`JQuery.d.ts`
```typescript
export default class JQuery { //adding default keyword

};
```

Default Import
```typescript
import Jquery from Jquery; // There won't be any curly braces like normal Import, See below for reference
//import { Jquery } from Jquery;
Jquery('#box').css('height':'50px')
```

Default Export of a function event without name will work
```typescript
export default function (s: string) {
    return s.length === 5 && numberRegexp.test(s);
}
```

Default Export can be also just values
```typescript
export default "123";
```

Import
```typescript
import num from "./OneTwoThree";
console.log(num); // "123"
```

#### Equal (=) Export form and require Import form
`ZipValidator.ts`
Export
```typescript
class ZipCodeValidator {
}
export = ZipCodeValidator;
```

Import
```typescript
var ZIP = require('ZipValidator')
var zipInstance = new ZIP();
```

### Code generation for modules
- Depending on the module target specified during compilation, the compiler will generate appropriate code for Node.js (CommonJS), require.js (AMD), UMD, SystemJS, or ECMAScript 2015 native modules (ES6) module-loading systems. 

- For more information on what the define, require and register calls in the generated code do, consult the documentation for each module loader.

Simple example 
`SimpleModule.ts`
```typescript
import m = require("mod");
export let t = m.something + 1;
```

How it got compiled in AMD ( require.js )
`AMD / RequireJS SimpleModule.js`
```typescript
define(["require", "exports", "./mod"], function (require, exports, mod_1) {
    exports.t = mod_1.something + 1;
});
```

How it got compiled in common js ( NodeJS )
```typescript
var mod_1 = require("./mod");
exports.t = mod_1.something + 1;
```
command to specifically compile typescript module into a target library

`tsc --module commonjs Test.ts` ( nodejs )
`tsc --module amd Test.ts` ( requirejs )

### declare keyword in typescript

`var` creates a new variable. 
`declare` is used to tell TypeScript that the variable has been created elsewhere. 
If you use `declare`, nothing is added to the JavaScript that is generated - it is simply a hint to the compiler.

For example, if you use an external script that defines `var externalModule`, you would use `declare var externalModule` to hint to the TypeScript compiler that externalModule has already been set up

We can also re-export a declared variable through a different name like below
`App.ts`
```typescript
declare let $: JQuery;
export default $;
```


## Optional module loading and advanced loading techniques
- In some cases, you may want to only load a module under some conditions. 

- In TypeScript, we can use the pattern shown below to implement this and other advanced loading scenarios to directly invoke the module loaders without losing type safety.

- The compiler detects whether each module is used in the emitted JavaScript. ( While compiling it will check whether module is not used anywhere other than as a type checker )

- This elision ( the omission of a sound or syllable ) of unused references is a good performance optimization, and also allows for optional loading of those modules. ( The omission of unused modules leads to good performence )

- The core idea of the pattern is that the import id = require("...") statement gives us access to the types exposed by the module.

- The module loader is invoked (through require) dynamically,

- This leverages the reference-elision optimization so that the module is only loaded when needed. 

- For this pattern to work, it’s important that the symbol defined via an import is only used in type positions (i.e. never in a position that would be emitted into the JavaScript).

 - To maintain type safety, we can use the typeof keyword. The typeof keyword, when used in a type position, produces the type of a value, in this case the type of the module.

Dynamic loading in nodejs
```typescript
declare function require(moduleName: string): any;

import { ZipCodeValidator as Zip } from "./ZipCodeValidator";

if (needZipValidation) {
    let ZipCodeValidator: typeof Zip = require("./ZipCodeValidator");
    let validator = new ZipCodeValidator();
    if (validator.isAcceptable("...")) { /* ... */ }
}
```

For more examples refer here
https://www.typescriptlang.org/docs/handbook/modules.html

## Working with other javascript libraries ( ambient )
- How to consume libraries which are not written in typescript inside typescript

- We call declarations that don’t define an implementation `ambient`. 

- Typically, these are defined in .d.ts files. If you’re familiar with C/C++, you can think of these as .h files. Let’s look at a few examples.

#### Ambient modules
< Did't understand fully, Hence moving forward >

#### Wildcard module declarations

Some module loaders such as SystemJS and AMD allow non-JavaScript content to be imported. 

```typescript
declare module "*!text" {
    const content: string;
    export default content;
}
```

Another 
```typescript
import fileContent from "./xyz.txt!text";
import data from "json!http://example.com/data.json";
console.log(data, fileContent);
```

#### UMD modules
Some libraries are designed to be used in many module loaders, or with no module loading (global variables). These are known as UMD modules. These libraries can be accessed through either an import or a global variable. For example:

`math-lib.d.ts`
```typescript
export function isPrime(x: number): boolean;
export as namespace mathLib;
```

```typescript
import { isPrime } from "math-lib";
isPrime(2);
mathLib.isPrime(2); // ERROR: can't use the global definition from inside a module
```

It can also be used as a global variable, but only inside of a script. (A script is a file with no imports or exports.)

```typescript
mathLib.isPrime(2);
```

