# Streams in nodejs

**streams are used to transfer data including requests to an HTTP server, opening a file, stdin, stdout, stderr etc.**

Streams can be readable, writable or both. We **can connect the readable stream to a writable stream using the pipe method**

**All streams are instances of event emitters** in node.js. We can get different events for data, for example  data event, error event, end event, readable event, writable event etc.

## Readable stream in node.js:

The Readable stream **is a source of data** which means that data comes out of Readable stream. It will not emit data until you indicate that you are ready to receive it.

Reading stream can be divided into **two modes of stream** based on their data flow mechanism:

**Flowing Mode**: In Flowing Mode the data is read from the system and provided to your program.

**Non-Flowing Mode**:  In non-flowing mode you have to call stream.read() explicitly to get chunk of data

### Examples
General use cases of Readable streams in nodejs:

http response
http request
Reading a file
Child process
Sockets tcp, etc.

### Some usefule read methods
1.read
`readable.read([size])`

This method is used to pull out data from source explicitly. If there is no data to transfer, it will return null. Size specifies how much data you want to read.

```javascript=
var readable=fs.createReadStream(‘abc.txt’);
 readable.read();
```
 2.setEncoding

 `Readable.setEncoding(encoding)`

 You can specify the encoding scheme of the data you want to receive.Call this function if you want to get stream in strings of specified encoding instead of buffer.
 
 ```javascript=
 var readable=fs.createReadStream(‘abc.txt’);
 readable.setEncoding('utf8')
 ```
 
 3. Resume and  Pause:

`readable.resume()` and `readable.pause()`

`readable.pause()` will pause the emitting of data event and correspondingly `readable.resume()` will resume emitting.

Both `(.pause() and .resume())`can be used only in flowing mode.
 
 
 
4.Pipe:

`Readable.pipe(destination,[option])`

`Pipe()` method is used to transfer data from Readable stream to Writable stream.

5.Unpipe:

`Readable.unpipe(destination,[option])`

This method will remove the hook set up on previous pipe call.

If destination is not specified, it will remove hook set up from all pipes.

Let take an example to see how pipe and unpipe works:

```javascript=
var fs= require(‘fs’)
 
var readable = fs.createReadStream(‘abc.txt’);
 
var writable=fs.createWriteStream(‘bcd.txt’);
 
readable.pipe(writable);
 
readable.on(‘end’,function(){
 
readable.unpipe(writable);
 
});
```