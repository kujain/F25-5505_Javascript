#### SESSION #2

# SYNTAX, DATA TYPES, OPERATORS, CONDITIONS, LOOPS


## 1 JAVASCRIPT SYNTAX
The Structure of a Javascript Program
- Comments
- Expressions
- Statements 
- Blocks

## COMMENTS
As time goes on, programs become more and more complex and we need comments inside the code to describe what the code does and why.
Comments can be put into any place of a script. They don’t affect its execution because the engine simply ignores them.
```
// This is my first code
let scheme_map = 42;
```
```
/* 
 * Here I am building a new plugin that uses the following arguments:
 * color_code: array()
 * event_name: JSON object
 * returns JSON object
 */
let scheme_map = 42; //used for storage
```

## EXPRESSIONS & STATEMENTS
Expressions are similar to phrases:
```
// This is my first expression
42
alert("Hello")
"Good" + " " + "Morning"
```
```
Statements are similar to sentences:
// This is my first statement
let answer = 42;
alert("Hello" + answer);
let greeting = "Good" + " " + "Morning";
```



## STRUCTURE

Similar to C-style/Java-style:
```
let scheme_map = 42
console.log(scheme_map)
```
Optional but recommended use of semi-colons:
```
let scheme_map = 42;
console.log(scheme_map);
```
Same as:
```
let scheme_map = 42;console.log(scheme_map);
```
OR
```
let scheme_map = 42
console.log(scheme_map)
```

## BLOCKS
A series of statements that are collected together inside curly braces:
```
// This is my first code
{
  let answer = 42;
  alert("Hello" + answer);
  let greeting = "Good" + " " + "Morning";
}
```


## DATA TYPES
**Primitives:**
- String
- Number
- undefined/null
- Booleans
- Symbol 

Objects:
- Arrays
- Functions
- Objects
- Maps
- Sets

## TYPEOF
An operator (action) to find out the type of data.Takes a single operand (the value) only:


12 				->	"number"
Hello			->	"string"
true			->	"boolean"
{key: 2}		->	"object"
function(){}	->	"function"
Undefined		->	"undefined"
Null			->	"object

eg.
```
typeof(45);
typeof("What am I?");
```





## NUMBERS

These are all numbers: 

```
42
3.1415
3e8
4*(12+6)/3
NaN
0xFF00AE
0b10110
Infinity / -Infinity
```


## STRINGS

These are all string expressions: 
```
"Do not Panic"
"Do \"not\" Panic"
"Don't Panic"
'Don\'t Panic'
"We are the Knights Who Say…\n" + "\"Ni\"!"

//ES6 only:
`We are the Knights 
Who Say… 
"Ni"!`
```



## UNDEFINED/NULL

```
// is this defined?
typeof(varName);
```
```
// what is this value?
let null_variable = null; // null
console.log( null_variable ); // "object"
```





## BOOLEANS

Every value/expression  in JS has a Boolean value: true or false.
```
10 			// true
0 			// false
40 > 39 	// true
"A" > "B"	// false
"a" > "A" // true (lowercase has a higher value)
```
Most values always are TRUE except a few:.
False values:"" '' 0 NaN false null undefined

To check for the Boolean value use: `Boolean(expression)`
eg. 
```
Boolean(0); // false
Boolean(42); // true
```



## OPERATORS
- Arithmetic
- Assignment
- Comparison
- Logical 
- Conditional


### ARITHMETIC
```
2 + 23; 
23 * 5.6;
2 ** 5; //ES2017 onwards
46 % 2; //remainder
```








### ASSIGNMENT

```
let a = "5";
let b = 4; 
b++;
++b;
b += a; // same as b = b + a
b *= a; // same as b = b * a
b %= a; // same as b = b % a
```

### COMPARISON
Returns Boolean value:
```
5 == 6 			// false
5 != 6 			// true
5 < 6 			// true
7 <= 6 			// false

"1" == 1 		// true
"1" === 1 		// false
1 == true 		// true
1 === true 		// false
NaN === NaN;	// false (huh...whaat?)
```


### LOGICAL

Logical operators convert the values into their boolean version (truthy/falsey) and then return a value:
```
!30
!null
!!null //shortcut to find its boolean
20 && 26 
20 && -1
3 && 0
true || false || false
NaN || undefined
45 || undefined
```


## VARIABLES
A data type value that's stored in memory during the running of a program and given a name
helps dealing with long strings or expressions as it saves the effort of typing them over and over.
- Declaration/Assignment
- Typecasting
- Patterns



## VARIABLES

**storing a string**
```
let my_string = "This is the end."; 
let my_string = new String("This is the end."); // not used much
```
**storing a number**
```
let my_num = 12; 
let my_num = new Number(12); // not used much
```

ways to assign
```
let my_num = 12; // preferred ES6 approach
const my_num = 12; // cannot change it
var my_num = 12; //traditional and loose
```

## VARIABLES PATTERNS
**Naming patterns (case-sensitive):**
```
let $element, first_name, _counter;
const CONSTANT;
const functionName();
const ObjectName;
```
The name can contain only letters, digits, or the symbols $ and _.
The first character cannot be a digit.
Case-sensitive.
English characters are recommended.

**Hoisting - always declare and assign before using:**
```
console.log(my_string); // returns error
----
console.log(my_string); // returns undefined
var my_string = "Hello";
console.log(my_string); // returns Hello
----
console.log(my_string); // returns error
let my_string = "Hello";
console.log(my_string); // returns Hello
----
let my_string = "Hello";
let my_string = "Goodbye"; // returns Error

```





## TYPECASTING/COERCION

Javascript auto-converts the value from one type to another (such as string to number, object to boolean, and so on) as needed to complete an operatioon:
```
14 + "" 
42 + "0" 
"42" - 7 
"42" * 7 
null || "34" 
2 == true
4 === true
```
```
let answer = "5" * 1; 
typeof answer; // number

let answer = "5" + 1; 
typeof answer; // string

let answer = true + false; 
typeof answer; // number
```



## PROPERTIES  & METHODS
Properties are information about the object or value. 
Methods perform an action on the object or value ― either to change it or to provide some information about it.
- Strings
- Numbers
- Boolean 



### STRING PROPERTIES & METHODS

Property:
```
let my_string = "the answer is 42."
console.log(my_string.length)
```

Methods:
```
my_string.slice(0,3);
my_string.charAt(1);
my_string.indexOf("w");
my_string.includes("42");
my_string.toUpperCase();
my_string.concat(" ","To be precise","!"); 
// OR 
my_string + " " + "To be precise!"
my_string.startsWith('T');
my_string.endsWith('2');
etc...
```


### NUMBER PROPERTIES & METHODS

Methods:
```
let my_number = 3.1415;
Number.isInteger(my_number);
Number.parseInt(my_number);
my_number.toExponential();
my_number.toFixed(1);
etc...
```



## CONDITIONS
- if...else if...else
- ternary
- switch 

### IF … ELSE IF … ELSE ...
```
let age = 23;if (age === 18) {
  console.log("Sorry, you shouldn't be here.");
}
if (age < 18) {
  alert("Sorry, you shouldn't be here.");
  alert(' do this as well');
} else {
  console.log("Please proceed.");
}
if (age < 18) // works without {} symbols but not recommended
  alert(' do this as well');
else
  console.log("Please proceed.");
```




### TERNARY

A shorthand way of writing an if ... else:
```
(a > b) ? 100 : 200;

let age = 23;
(age < 18) ? console.log("Sorry, you shouldn't be here.") : console.log("Please proceed.");

(age < 18) ? alert("Sorry, you shouldn't be here.") : console.log("Please proceed.");

console.log((age < 18) ? 'Sorry, you shouldn't be here.' : 'Please proceed.'));
```
Use this mostly when assigning the result:
```
let c = (a > b) ? 100 : 200;
```




### SWITCH

```
let num = Math.floor(Math.random() * 10);
console.log(num);
switch (num) {
  case (4):
    console.log("You rolled a four");
    break;
  case (5):
    console.log("You rolled a five");
    break;
  case (6):
    console.log("You rolled a six");
    break;
  default:
    console.log("You rolled a number less than four");
}
```






## ARRAYS
A list of values placed in a particular order

- Defining - literal,  constructor
- Common Operations
- Statements 
- Blocks




### DEFINING AN ARRAY

Arrays are special types of objects.
```
// literal approach
const my_array = [];
```
```
// constructor approach - not used much
const my_array = new Array(); // returns object
```










### DEFINING AN ARRAY WITH VALUES
```
// prepopulating
const my_array =  ["blue", "red", "green"];

// adding
my_array[0] = "pink";
my_array[3] = "purple";
my_array[5] = null;
my_array[6] = 4;
```
=> ['pink', 'red', 'green', 'purple', empty, null, 4]











### PROPERTIES & METHODS


```
// property
console.log(my_array.length)
```
```
// modifiers
my_array.pop(); // updates array
my_array.push(item); // updates array
my_array.concat(second_array); // new array
my_array.join(joiner); // new string
my_array.slice(2,4); // new array starting at index 2 and ending at index 3
my_array.splice(2,1,"brown");
my_array.indexOf("brown");// position or -1
my_array.includes("brown"); //ES6
my_array.reverse();
```
```
// JOIN 2 ARRAYS
const array1 =  ["blue", "red", "green"];
const array2 =  ["brown", "red", "green"];

const array3 = array1.concat(array2);
```

```
// using the spread operator
const array3 = [ ...array1, ...array2 ];
// returns: ["blue", "red", "green", "brown", "red", "green"];
```

```
// DESTRUCTURING AN ARRAY
const [ a,b,c ] = array1;
console.log( a,b,c );
```


## LOOPS

- while
- do...while
- for
- for...of 





### WHILE LOOPS

Repeat a block of code until a condition remains true:
```
let max_time = 7;
while (max_time < 10){
  console.log("Keep working. It's still only " + max_time);
  max_time++; 
}
```
```
let max_time = 10;
while (max_time--){
  console.log("Keep working. It's still only " + max_time);
}
```



### DO...WHILE LOOPS

Run a block of code at least once and then until a condition remains true:
```
let max_time = 7;
do {
  console.log("Keep working. It's still only " + max_time);
  max_time++; 
} while (max_time < 10)
```

### FOR LOOPS

Keeps all loop-related vars in one place: 
```
for (initialization ; condition ; after)  {  
    do something;  
}

```

```
for (var max_time = 7; max_time < 10; max_time++) {
  console.log("Keep working. It's still only "+max_time);
}

var my_array =  ["blue", "red", "green"];
for (var i = 0; i < my_array.length; i++) {
  console.log("The selected color: "+my_array[i]);
}
```

ADDED in ES6: Use let in block to keep scope local to the loop. eg. 
```
for (let i = 0; i < my_array.length; i++) {
  ...
}
console.log(i); //throws error
```


### FOR...OF LOOPS

ADDED in ES6 for looping over arrays:
```
let my_array =  ["blue", "red", "green"];
for (const value of my_array) {
  console.log("The selected color: "+value);
}
```

### ARRAY ITERATORS

```
let my_array =  ["blue", "red", "green"];

my_array.forEach(function (val) {
  console.log("Keep working. It's still only " + val);
});

my_array.map(function (val) {
return (val).toUpperCase();
});

let new_array = my_array.reduce(function (prev, current) {
  return (prev + " " + current);
});
```

