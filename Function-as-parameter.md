Source: http://stackoverflow.com/questions/2824393/javascript-function-as-a-parameter-to-another-function

## Reasons to pass functions as parameters

### 1. "Wrapper" functions.

Lets say you have a bunch of different bits of code. Before and after every bit of code, you want to do something else (eg: log, or try/catch exceptions).

You can write a "Wrapper" function to handle this. EG:
```javascript
function putYourHeadInTheSand(otherFunc) {
    try{
         otherFunc();
    } catch(e) { } // ignore the error
}

....

putYourHeadInTheSand(function(){
    // do something here
});
putYourHeadInTheSand(function(){
    // do something else
});
```
### 2. Callbacks.

Lets say you load some data somehow. Rather than locking up the system waiting for it to load, you can load it in the background, and do something with the result when it arrives.

Now how would you know when it arrives? You could use something like a signal or a mutex, which is hard to write and ugly, or you could just make a callback function. You can pass this callback to the Loader function, which can call it when it's done.

Every time you do an XmlHttpRequest, this is pretty much what's happening. Here's an example.
```javascript
function loadStuff(callback) {
    // Go off and make an XHR or a web worker or somehow generate some data
    var data = ...;
    callback(data);
}

loadStuff(function(data){
    alert('Now we have the data');
});
```
### 3. Generators/Iterators

This is similar to callbacks, but instead of only calling the callback once, you might call it multiple times. Imagine your load data function doesn't just load one bit of data, maybe it loads 200.

This ends up being very similar to a for/foreach loop, except it's asynchronous. (You don't wait for the data, it calls you when it's ready).
```javascript
function forEachData(callback) {
    // generate some data in the background with an XHR or web worker
    callback(data1);
    // generate some more data in the background with an XHR or web worker
    callback(data2);
    //... etc
}

forEachData(function(data){
    alert('Now we have the data'); // this will happen 2 times with different data each time
});
```
### 4. Lazy loading

Lets say your function does something with some text. BUT it only needs the text maybe one time out of 5, and the text might be very expensive to load.

So the code looks like this
```javascript
var text = "dsakjlfdsafds"; // imagine we had to calculate lots of expensive things to get this.
var result = processingFunction(text);
```
The processing function only actually needs the text 20% of the time! We wasted all that effort loading it those extra times.

Instead of passing the text, you can pass a function which generates the text, like this:
```javascript
var textLoader = function(){ return "dsakjlfdsafds"; }// imagine we had to calculate lots of expensive things to get this.
var result = processingFunction(textLoader);
```
You'd have to change your processingFunction to expect another function rather than the text, but that's really minor. What happens now is that the processingFunction will only call the textLoader the 20% of the time that it needs it. The other 80% of the time, it won't call the function, and you won't waste all that effort.

### 4a. Caching

If you've got lazy loading happening, then the textLoader function can privately store the result text in a variable once it gets it. The second time someone calls the textLoader, it can just return that variable and avoid the expensive calculation work.

The code that calls textLoader doesn't know or care that the data is cached, it's transparently just faster.

There are plenty more advanced things you can do by passing around functions, this is just scratching the surface, but hopefully it points you in the right direction :-)

-----
## Example

Original article: http://tech.deepumohan.com/2013/07/javascript-pass-function-as-parameter.html

#### Quote from Mozilla developer website:

> In JavaScript, functions are first-class objects, i.e. they are objects and can be manipulated and passed around just like any other object.
Every Javascript function is a Function object. Hence we can pass them as arguments, like any other object.

Passing function as parameter is no different from passing any other object when it comes to syntax.

### The example problem
Bob wants to get sum of values [1, 2, 3, 4, 5, 6, 7, 8, 9]

So we give him the following solution
```javascript
// find sum of values
var total = function(values) {
    var sum = 0;
    values.forEach( function(value) {
        sum += value;
    });
    return sum;
};
```
Bob is happy with the function. But now he wants to get sum of all even numbers in the list of values.

So we copy-paste the above function, rename it and make slight changes.
```javascript
// find sum of values
var total = function(values) {
    var sum = 0;
    values.forEach( function(value) {
        sum += value;
    });
    return sum;
};

// find sum of even numbers in list of values
var totalEven = function(values) {
    var sum = 0;
    values.forEach( function(value) {
        if( value % 2 === 0 ) sum += value;
    });
    return sum;
};
```
Bob is happy again. But he wants more. Now he need sum of all odd numbers from the same list.

As usual, we copy-paste, rename and make slight changes.
```javascript
// find sum of values
var total = function(values) {
    var sum = 0;
    values.forEach( function(value) {
        sum += value;
    });
    return sum;
};

// find sum of even numbers in list of values
var totalEven = function(values) {
    var sum = 0;
    values.forEach( function(value) {
        if( value % 2 === 0 ) sum += value;
    });
    return sum;
};

// find sum of odd numbers in list of values
var totalOdd = function(values) {
    var sum = 0;
    values.forEach( function(value) {
        if( value % 2 !== 0 ) sum += value;
    });
    return sum;
};
```
The problem with that approach
- Lot of duplicate code.
- Cluttered and ugly source code.
- Source file becomes unnecessarily lengthy.
- Not applying re-usabilty principle.
- Have to create separate function for each additional request.

### Better code with passing function as argument
We can improve the above code a lot by passing the selection functionality as argument. In the above example, the basic operation is summation. Then, we need some kind of selection of values to sum. This selection can be anything, like even numbers, odd numbers etc. This is what we will pass an argument.
```javascript
var totalSelectValues = function(values, selector) {
    var sum = 0;
    values.forEach(function(value) {
        if(selector(value)) sum += value;
    });
    return sum;
};
```
The `selector`, is function passed as parameter. Here we are expecting it to return a boolean value.
```javascript
var values = [1,2,3,4,5,6,7,8,9];
// even numbers
totalSelectValues(values, function(value) { return value % 2 === 0});

// odd numbers
totalSelectValues(values, function(value) { return value % 2 !== 0});

// greater than 5
totalSelectValues(values, function(value) { return value > 5 });
```
- We just created functions on the fly and passed it as parameters, didn't even bother to name it! 
- Also we have reduced the code base by far. Just a single function and no ugly repetition.

### But that is not enough
We also need to make sure our little function works perfectly even if the second argument is not send.
```javascript
var totalSelectValues = function(values, selector) {
    // handle undefined selector
    if (typeof selector == 'undefined' ) {
        selector = function() {return true;};
    }

    var sum = 0;
    values.forEach(function(value) {
        if(selector(value)) sum += value;
    });
    return sum;
};
```
Now that should work.
