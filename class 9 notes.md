#### SESSION #10
# FUNCTIONAL PROGRAMMING

## WHAT IS FUNCTIONAL PROGRAMMING
- In Javascript, functions are objects, and they behave like other variables/values with their own properties and methods and can be passed as arguments and returned by functions. 
- This makes functions very flexible and they can be used to create modules and libraries for cleaner code and speedier execution.
- Functional programming  uses functions and their features to build out the operations to perform single discrete tasks through encapsulation. Then it can combine them all to build out more complex structures.
- Each function performs a task and returns a value that can be worked on by another (doesn't change or use the outside world).
- The emphasis is on simplicity where data and functions are concerned, and building complex tasks through a series of simple tasks.


## THE BASICS

### A Pure Function
- No side-effects - non-destructive data transformation
- No external dependencies
- Return Transparency


### Basic Structure:
- At least one argument
- A return value

## FUNCTIONAL CONCEPTS
```
const xs = [1,2,3,4,5];

// pure
xs.slice(0,3); // [1,2,3]
console.log(xs); //the same as before

// impure - as it mutates original data and can have side effects
xs.splice(0,3); // [1,2,3]
```

Simple example of pure:
```
function random(a, b) {
  if (b === undefined) {
    b = a, a = 1; // if no 2nd argument, lower limit is 1
  }
  return Math.floor((b - a + 1) * Math.random()) + a;
}
random(6);
random(6, 20);
```

An impure example:
```
let def = 6;
function random(a, b) {
  if (b === undefined) {
    b = a, a = def; // if no 2nd argument, lower limit is def
  }
  return Math.floor((b-a+1) * Math.random()) + a;
}
```

An Example of daisy chaining functions using the dot notation:
```
function reverse(string) {
  let array = string.split("");
  array.reverse();
  return array.join("");
}

const message = "Hello";
const newmess = reverse(message);
console.log(newmess);
console.log(message);

This can also be written as: 
function reverse(string) {
return string.split("").reverse().join(""); 
}
```

This makes it easier to string/chain - method chaining
```
const newmess = reverse(message).toLowerCase().substr(0,3);
```

OR without that function
```
const newmess = message.split("").reverse().join("").toLowerCase().substr(0,3);
```


Another Example:
```
const string = " The Answer is Forty-Two ";

const slugify = string =>
 string
   .toLowerCase()
   .trim()
   .split(" ")
   .join("-");

slugify(string); // slugged up version
```
OR without a wrapper function:
```
string.toLowerCase().trim().split(" ").join("-");
```

## HIGHER ORDER FUNCTIONS

An approach used to write more compact and simple functions that can be re-combined to create more complex functions:
```
function square(x){
  return x*x;
}

function hypotenuse(a,b) {
  let total = square(a) + square(b);
  return Math.sqrt(total);
}
```

## CALLBACKS

Functions that are sent as arguments to another function. Allows for more generalized function definitions with delegating complex tasks to externally defined functions
```
// pass function as a parameter
const convertToCelsius =  function(deg_fah) {
     let converted_deg = (deg_fah-32) * 5/9;
     return converted_deg;
};
const convertToFahrenheit =  function(deg_cent) {
     let converted_deg = (deg_cent * 9/5) + 32;
     return converted_deg;
};
// pass function as a parameter
function convert(converter, temperature) {
     console.log(converter(temperature));
}
convert(convertToCelsius, 23);
convert(convertToFahrenheit, 23);
```


## RECURSIVE FUNCTIONS

Calls itself until a certain condition is met - useful for iterative processes:
```
function factorial(n) {
  if (n === 0) {
    return 1
  } else {
    return n * factorial(n - 1);
  }
}

factorial(10);
```


## RETURNING FUNCTIONS

Returns a function based on specific params:
```
function power(x) {
  return function(power) {
    return Math.pow(x,power);
  }
}
let twoExp = power(2);
twoExp(5);

// can also be used in the following format:
power(2)(5);
```

## CLOSURES

Function that contain functions that get access to the outer function's variables and params, and stay alive after the initial call:

```
function counter(start){
  i = start;
  return function() {
return i++; 
  }
}
let count = counter(1); // start a counter at 1
count();
```
```
function multiplier(factor) {
  let ret = function(number) {
    return number * factor;
  };
  return ret;
}
const square = multiplier(2);
const cubed = multiplier(3);

square(3);
cubed(3);
multiplier(2)(3); // same as above square(3)
```

## PROMISES

Created to better manage the results of asynchronous operations. Cleans up Callback Hell:

```
const promise = new Promise( (resolve, reject) => {
    // initialization code goes here
    if (success) {
        resolve(value);
    } else {
        reject(error);
    }
});

const dice = {
  sides: 6,
  roll: function() {
    		return Math.floor(this.sides * Math.random()) + 1;
  }
}

const promise = new Promise( (resolve,reject) => {
const n = dice.roll();
setTimeout(() => {
        (n > 3) ? resolve(n) : reject(n);
     }, 2000);
});

// the call format: promise.then(resolve_function, reject_function);

promise.then(	result => console.log(`Yes! I rolled a ${result}`), 
              result => console.log(`Drat! ... I rolled a ${result}`) 
);

promise.catch( result => console.log(`Damn! ... I made a mistake - ${result}`));

```


### A more compact version - skip the reject since catch works as the reject function:
```
const dice = {
  sides: 6,
  roll: function() {
    		return Math.floor(this.sides * Math.random()) + 1;
  }
}

const promise = new Promise( (resolve,reject) => {
        const n = dice.roll();
        setTimeout(() => {
          (n > 3) ? resolve(n) : reject(n);
        }, 2000);
   	})
    .then( result => console.log( `Yes! I rolled a ${result}`) )  //resolver function
    .catch( result => console.log(`Dammit! ... I rolled a ${result}`));  //rejector function

```
### PROMISE WITH XHR
```
const button = document.getElementById('find');
button.addEventListener("click", getUserData);

function getUserData() {
  let url = "https://reqres.in/api/users";
  console.log(url);
  
  // define promise structure
  const get = new Promise((resolve, reject) => {
    let xhr = new XMLHttpRequest();
    xhr.open("GET", url);
  	xhr.setRequestHeader( 'x-api-key', 'reqres-free-v1');
    xhr.onload = function() {
      if (xhr.status >= 200 && xhr.status < 300) {
          resolve(xhr.response);
      } else {
          reject(xhr.statusText);
      }
    };
    xhr.onerror = () => reject(xhr.statusText);
    xhr.send();
  });

  // run when promise resolves
  get.then( function(data) {
    document.getElementById("Output").innerHTML = data;
  });

  // run when promise is rejected or errors out
  get.catch( function(data) {
    document.getElementById("Output").innerHTML = "OOPS";
  });
}
```

### fetch is a special promise structure designed for ajax requests:
```
const button = document.getElementById('find');
button.addEventListener("click", getUserData);

function getUserData() {
  let url = "https://reqres.in/api/users";
  fetch(url, {
    			headers: {
          'x-api-key': 'reqres-free-v1'
        }
  })
	.then(function(response) {
	  return response.json();
	})
	.then(function(resp) {
	  document.getElementById("Output").innerHTML = JSON.stringify(resp.data);
	})
	.catch(function(resp) {
	document.getElementById("Output").innerHTML = "There was an error";
	});
}
```

## IIFEs
An Immediately Invoked Function Expression is a function that gets invoked as soon as it’s defined.
- Keeps scope of variables local and doesn't clutter global.
- Also called Anonymous Closures
- One of the most useful Javascript features!

```
( function() {
  const temp = "world";
  console.log("Hello " + temp);
}() );


console.log('What is temp outside the IIFE', temp); // will error out
```

## IIFEs - block scopes

Most languages let a variable have scope inside a code block, but not JavaScript (pre ES6) - its variables can live outside a block. But IIFE can mimic the block scope:
```
const list = [1,2,3];
for (var i = 0, max = list.length ; i < max ; i++ ){
  console.log(list[i]);
}
console.log(i); //i is still outside


const list = [1,2,3];
(function(){
for (var i = 0, max = list.length ; i < max ; i++ ){
  		console.log(list[i]);
}
}());
console.log(i); // i is not available outside the for block
```


## IIFEs - global import, local scope

IIFEs can access the global scope just like any function. But it's better practice to pass a global variable to it to keep the block self-contained:
```
let list = [1,2,3];
(function(my_list){
for (let i = 0, max = my_list.length ; i < max ; i++ ){
  		console.log(my_list[i]);
}
}(list));
console.log(i); // i is not available outside the for block
```

This is how we use jQuery!
```
(function($){
  // we have access to globals jQuery (as $)
  // bind click event to all internal page anchors
  $(".menu-link").bind("click touchstart", function (e) {
      // prevent default action and bubbling
      e.preventDefault();
      e.stopPropagation();
      $("#off-canvas-nav").toggleClass("active");
      $("#wrapper").toggleClass("active");
  });
})(jQuery);
```

## IIEFs - with ES6

Using ES6 variable initializers let, const, you don't need IIFEs since both these declariations are block scoped:
```
{
  const list = [1,2,3];
  for (let i = 0, max = list.length ; i < max ; i++ ){
  		console.log(list[i]);
  }
};
console.log(i); // i is not available outside the for block
console.log(list); // list is not available outside the for block
```

WHAT HAPPENS WITH THIS CODE?
```
{
  var list = [1,2,3];
  for (let i = 0, max = list.length ; i < max ; i++ ){
  		console.log(list[i]);
  }
};
console.log(i);
console.log(list);
```
