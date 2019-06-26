# Buffer

https://medium.freecodecamp.org/do-you-want-a-better-understanding-of-buffer-in-node-js-check-this-out-2e29de2968e8


## Buffer Class
mechanism for `reading or manipulating streams of binary data`. The Buffer class was introduced as part of the Node.js API to make it possible `to interact with octet streams` in the context of things like `TCP streams and file system operations`

## Binary Data
Binary data and the story of `L`

```javascript=
    "L".charCodeAt(0) //76
```

76 is Number representation or `Character Code` or `Character Point`

76 will be represented 00001100 in binary


## Character Sets
Character Sets are `already defined rules of what exact number represents each character`. We have different definitions of these rules.The very popular ones include `Unicode` and `ASCII`

## Character Encoding
 how that `number should be represented in binaries`. Specifically, `how many bits to use to represent the number`. This is called Character Encoding.

## Stream
 sequence of data being moved from one point to the other over time
## Buffer

That `waiting area` is the buffer! It is a `small physical location in your computer, usually in the RAM`, where data are temporally gathered, wait, and are eventually sent out for processing during streaming

## Interacting with a Buffer



we can manipulate or interact with the binary data being streamed. What kind of interaction could we possibly have with this raw binary data? The Buffer implementation in Node.js provides us

```javascript=
// Create an empty buffer of size 10. 
// A buffer that only can accommodate 10 bytes.
const buf1 = Buffer.alloc(10);
// Create a buffer with content
const buf2 = Buffer.from("hello buffer");
// Examine the structure of a buffer
buf1.toJSON()
// { type: 'Buffer', data: [ 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 ] }
// an empty buffer
buf2.toJSON()
// { type: 'Buffer',
     data: [ 
       104, 101, 108, 108, 111, 32, 98, 117, 102, 102, 101, 114 
     ] 
   }
// the toJSON() method presents the data as the Unicode Code Points of the characters
// Examine the size of a buffer
buf1.length // 10
buf2.length // 12. Auto-assigned based on the initial content when created.
// Write to a buffer
buf1.write("Buffer really rocks!") 

// Decode a buffer
buf1.toString() // 'Buffer rea'
//oops, because buf1 is created to contain only 10 bytes, it couldn't accommodate the rest of the characters
// Compare two buffers
```

Mentioned to read about `zlib.js` library
https://github.com/nodejs/node/blob/master/lib/zlib.js