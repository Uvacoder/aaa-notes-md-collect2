# event Emitters

```javascript=
const EventEmitter = require('events');

class WithLog extends EventEmitter {
  execute(taskFunc) {
    console.log('Before executing');
    this.emit('begin');
    taskFunc();
    this.emit('end');
    console.log('After executing');
  }
}

const withLog = new WithLog();

withLog.on('begin', () => console.log('About to execute'));
withLog.on('end', () => console.log('Done with execute'));

withLog.execute(() => console.log('*** Executing task ***'));
```
**Output**
```
Before executing
About to execute
*** Executing task ***
Done with execute
After executing
```

**Changing execute function alone in above code**
```javascript=
withLog.execute(() => {
  setImmediate(() => {
    console.log('*** Executing task ***')
  });
});
```
**output**
```
Before executing
About to execute
Done with execute
After executing
*** Executing task ***
```

**more redable async await based event emitter for callbacks**
```javascript=
class WithTime extends EventEmitter {
  async execute(asyncFunc, ...args) {
    this.emit('begin');
    try {
      console.time('execute');
      const data = await asyncFunc(...args);
      this.emit('data', data);
      console.timeEnd('execute');
      this.emit('end');
    } catch(err) {
      this.emit('error', err);
    }
  }
}
```
