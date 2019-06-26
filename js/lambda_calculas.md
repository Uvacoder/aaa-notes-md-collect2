# Lamda Calculas

https://www.youtube.com/watch?v=3VQ382QG-y4
### Identification
```js
I = a => a
```

### Mocking Bird
```js
M = f => f(f)
```

### Kestral
```js
K = a => b=> a
```

### Kite
```js
KI = a => b => b
```

### Cardinal
```js
C = f => a => b => f(b)(a)
```

### True and False
```
T = K
T.inspect = function() { return 'T / K' } 
F = KI 
F.inspect = function() { return 'F / KI' }
```

### Not Operator
```js
not = p => p(F)(T)
```

### And Operator
```js
and = p => q => p(q)(p)
```

### Boolean equality
checks whether True boleans same or not
```js
beq = p => q => p(q)(not(q))
```

