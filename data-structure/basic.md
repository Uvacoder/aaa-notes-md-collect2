https://www.youtube.com/watch?v=D6xkbGLQesk

# Big O Notation 
The notation used to descrive How much time a function takes the execute When the number of input grows

### Simple example
Get the sum the of the given array

*code*
```javascript
given_array = [1,2,3,4,5....10];
find_sum(given_array){
    total = 0;
    given_array.foreach(i = >{
         total =+ i
    }) 
    return total;
}
```
To analyse the performance of the code lets ask the below question  
`How much time does this function take to run this function ?`

But unfortunately the above question depends on 
- computer RAM,
- Processor,
- Programming language etc.

So let's change the question   
`How does the runtime of the function grow ? `  
To answer the above questions we use `Big O Notation and Time Complexity`

Let's create a graph between the number of inputs and the amount of time the function takes to execute

n - number of input
t - time it takes takes to execute function


X Axis - n
Y Axis - t ( in ms )

`Linear Time Complexity O(n)`
![](https://i.imgur.com/SeynNr7.png)

From the graph what we can understand is the time complexity grows linerly as the number of input grows.  
The time complexity of it called `Linear Time`

### Time Complexity
A way of showing how the runtime of a function increases as the size of the input (n) increases
 
 
`Constant Time Complexity O(1)`  
The runtime of the function remains constant as the number of input grows

 Example
 ```javascript
get_length(input_array){
     return input_array.length
}
 ```
 Time complexity and input length graph  
 ![](https://i.imgur.com/OZgJ2Uz.png)

 T = c*1 
 = O(1) 

### Big O Notation
Instead of the mentioning the Time Complexity as words like Linear time complexity or Constant time complexity we are using a mathamatical notation called ( Big O notation )

`Linear Time` => O(n)  
`Constant Time` => O(1)  

Generating Big O notation from the function Above examples

![](https://i.imgur.com/AoUJ5vH.png)

### Finding Big O Notation for function
![](https://i.imgur.com/KxN4rU7.png)

`Quadradic Time Complexity `  O(n<sup>2</sup>)


```javascript
var 2d_array = [ 
    [1,2],
    [3,4]
]
var another_2d_array = [
    [1,2,3],
    [4,5,6],
    [7,8,9]
]

// input increases 2x2 or 3x3 or 4x4 ... nxn => n2

function find_sum_2d_array(array){
    var total = 0;
    2d_array.forEach(arr => {
        arr.forEach(elem => {
            total =+ elem;
        })
    })
    return total;
}
```
Finding Big O Notation for the above example 
![](https://i.imgur.com/P2FzCbA.png)

`Logarithmic time Complexity` O(log n)
Before we going into loarithmic time complexity let's understand Logarithms first

Just like subtraction is inversion of addition `Logarithms are inversion of Exponential ( power or )`

Opposite of 2<sup>10</sup> => log<sub>2</sub>10  
Oppsite of n<sup>m</sup> => log<sub>m</sub>n

x<sup>z</sup> = y  
Then  
log<sub>x</sub>y = z

*Code sample*
```javascript
var array = [1,2,3,4,......64];
for(var i = array.length; i <= 1; i = i/2 ){
    console.log(i)   
}
```

In the above example the i value reduces by half upon each iterations
For The above code the time complexity is O(log n)

For binary search the upon each iterations the size of the input reduces by half, Hence For binary search the Big O Notation is O(log n)
