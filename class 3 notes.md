
#### SESSION #3
# SYNTAX & STRUCTURE: FUNCTIONS


## FUNCTIONS
Function: a block of code that performs a specific task and makes it reusable by having a name.  
Reduces repetition and allows for cleaner code.
- Initialization
- Scopes 
- First Class Object
- Functions as Values
- Closures

##  NEW FUNCTIONS

```
// a new basic function - pretty useless
function createRandomNumber() {
	console.log('I am returning', Math.random());
}
```
```
// a little more useful
function createRandomNumber(max) {
	console.log('I am returning', Math.floor(Math.random() * max));
}
```

## CALLING FUNCTIONS
```
// this returns the actual reference, not the function evaluation
randomNumber; 

// this executes the function
randomNumber();
```


## PURE/IMPURE FUNCTIONS
```
// a new basic function - impure
function convertToCelsius() {
	let deg_fah = 100;
	let converted_deg = ( deg_fah-32 ) * 5/9;
	console.log( 'The converted temperature is', converted_deg );
}
```
```
// a new basic function - pure…kind of
function convertToCelsius() {
 	let deg_fah = 100;
	let converted_deg = ( deg_fah-32 ) * 5/9;
return( converted_deg );
}
console.log( convertToCelsius() );
```
```
// a new basic function - pure
function convertToCelsius( deg_fah ) {
	let converted_deg = ( deg_fah-32 ) * 5/9;
return( converted_deg );
}
console.log( convertToCelsius(100) );
```


## FUNCTION PARAMETERS / ARGUMENTS

Default params can be set by checking if undefined:
Method 1:
```
function convertToCelsius( deg_fah ) {
	if ( deg_fah === undefined ) {
     deg_fah = 32;
   }
 	let converted_deg = ( deg_fah-32 ) * 5/9;
return( converted_deg );
}
console.log( convertToCelsius() );
console.log( convertToCelsius(100) );
```

Method 2:
```
function convertToCelsius(deg_fah) {
	deg_fah = deg_fah || 32;
 	let converted_deg = (deg_fah-32) * 5/9;
return(converted_deg);
}

console.log( convertToCelsius() );
console.log( convertToCelsius(100) );
```
Above breaks with param of 0


Default params can be set by checking if undefined:

Method 3 (ES6):
```
function convertToCelsius(deg_fah = 32) {
 	let converted_deg = (deg_fah-32) * 5/9;
return(converted_deg);
}
console.log( convertToCelsius(32) );
console.log( convertToCelsius(77) );
console.log( convertToCelsius() );
```

## MULTIPLE PARAMETERS / ARGUMENTS

Multiple parameters can be defined/set.
Order Matters!
```
function convertToCelsius(deg_fah,dec_fixed) { // no default for optional param
	let converted_deg = (deg_fah-32) * 5/9;
	converted_deg = converted_deg.toFixed(dec_fixed)
		console.log(converted_deg);

	return(converted_deg);
}

console.log( convertToCelsius(100,2) );


console.log( convertToCelsius(32) );
console.log( convertToCelsius(77) );
console.log( convertToCelsius() );
```

## FUNCTION PARAMETERS / ARGUMENTS

Some new  ES6 patterns: arbitrary params (rest operator)
```
function logAllArguments(...args) {  
    for (const arg of args) {
        console.log(arg);
    }
}
```
With first as required:
```
function logAllArguments(param1,...args) {     
	console.log(param1);
   for (const arg of args) {
        console.log(arg);
   }
}
```



## SCOPE

Scope is how a variable is available to the entire program:
**Global scope:**
- Any variables or functions declared outside of a function will be available to all JavaScript code on the page, whether that code is inside a function or otherwise 

**Functional/Local scope:**
- Variables and functions declared inside a function are visible only inside that function—no code outside the function can access them. 
- Local variables also have a lifetime - they die when the function  finishes executing.



## FUNCTION: A 1st CLASS OBJECT

One of the more powerful and flexible features of Javascript.
functions can be treated just like any other variable
```
// assign function to variable 
const new_function =  convertToCelsius;
console.log(new_function(100));

// pass function as a parameter
function convert(converter, temperature) { 
console.log(converter(temperature));
}
convert(convertToCelsius, 23);
```


## FUNCTION: ALTERNATE DEFINITIONS

Function Expression:
```
// assign anonymous function to variable 
const convertToCelsius = function(deg_fah) {
	let converted_deg = (deg_fah-32) * 5/9;
	return converted_deg;
};

// assign named function to variable 
const newFunction =  function convertToCelsius(deg_fah) {
	let converted_deg = (deg_fah-32) * 5/9;
	return converted_deg;
};
```

## FUNCTION HOISTING

Expressions are defined where they are inserted in code. function declarations are moved to top of code automatically during run:
```
console.log(convertToCelsius(12));
const convertToCelsius = function templateFunction(deg_fah) {
	let converted_deg = (deg_fah-32) * 5/9;
	return converted_deg;
};
console.log(convertToCelsius(2));
```
```
// hoisted:
console.log(convertToCelsius(12));
function convertToCelsius(deg_fah) {
	let converted_deg = (deg_fah-32) * 5/9;
	return converted_deg;
};
console.log(convertToCelsius(2));
```

## FUNCTION CALLBACKS

Function that are sent as arguments to another function:
```
// pass function as a parameter
const convertToCelsius =  function(deg_fah) {
	let converted_deg = (deg_fah-32) * 5/9;
	return converted_deg;
};
// pass function as a parameter
function convert(converter, temperature) { 
console.log(converter(temperature));
}
convert(convertToCelsius, 23);
```
```
// pass action function as a parameter
const convertToCelsius =  function(deg_fah, callback) {
	let converted_deg = (deg_fah-32) * 5/9;
	callback(converted_deg);
};
// pass function as a parameter
function displayOnLog(temperature) { 
console.log(temperature);
}
convertToCelsius(23, displayOnLog);
```

## FUNCTION: ALTERNATE DEFINITIONS

Arrow Notation (ES6): 
- Very compact
- Works great for one line functions
- Better handling of this (will see later)
```
// assign anonymous function to variable 
const convertToCelsius = deg_fah => (deg_fah-32) * 5/9;

const convertToCelsius = (deg_fah,dec) => (deg_fah-32) * 5/9;

const convertToCelsius = deg_fah => {
  return (deg_fah-32) * 5/9;
}
```




## BUILT-IN FUNCTIONS

```
// typical built-in functions
my_string.charAt(1); //returns a string
parseInt(12.34); //returns integer
Math.random(); //returns a floating number
[1,2,3,4].map(); //returns array
isNaN(varname); //returns true or false
```

## ARRAY ITERATORS 
```
const my_array =  ["blue", "red", "green"];
my_array.map(function (val) {
  return (val).toUpperCase();
});
```
Similar to:
```
var toUppercase = function (value) {
  return (value).toUpperCase();
}
my_array.map( toUppercase );
```
Another example:
```
const array_sum = [1,2,3,4,5].reduce( function(prev,current){
  return prev + current;
});
console.log(array_sum);
```


## CLOSURE
Function that contain functions get access to the outer functions variables and parameters, even after the call is made to the outer function.
Used for data privacy as the enclosed variables are only in scope within the containing (outer) function.
```
const module = function() {
    let localVar = 1913;
    const localFunc = function() {
       return localVar;
    }
    return localFunc;
}

let newmod = module();
console.log( newmod() ); // 1913
```

- Function that contain functions get access to the outer functions variables and parameters, even after the call is made to the outer function.
- Used for data privacy as the enclosed variables are only in scope within the containing (outer) function.

```
//get and set
const module = function() {
    let localVar = 1913;
    const localFunc = function( new_val ) {
      if ( new_val )  {
        localVar = new_val;
      }
      return localVar;
    };
    return localFunc;
}

let newmod = module();
console.log( newmod() ); // 1913

newmod(1776);
console.log(newmod()); //1776
```



