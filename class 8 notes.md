#### SESSION #8
# OBJECT ORIENTED PROGRAMMING / ERROR MANAGEMENT


## 1. OBJECTS REVISITED
- Object Types
- Constructors vs Literals
- Prototypes
- Inheritance and Extending

## 2. CREATING OBJECTS

DATE `const the_date = new Date(949278000000);`

ARRAY `const array_one = new Array("one", "two", 3); `

STRING `const string_one = new String("Hello");`

PROPERTIES `string_one.length`

METHODS `string_one.indexOf("l");`


## 3. CUSTOM OBJECTS
```
// literal
const john_object = {};
john_object.firstName = "John"; 
john_object.lastName = "Doe";

john_object.greet = function() {
  alert("My name is " + this.firstName + " " + this.lastName);
};

john_object.greet();
```
OR
```
// constructor syntax
const john_object = new Object();
```
```
// constructor function
function createPerson(first_name, last_name) {
  const obj = {
    first_name: first_name,
    last_name: last_name, 
    getFullName: function() {
      return this.first_name + " " + this.last_name 
    },
    greet: function(person) {
      alert("Hello, " + person.getFullName() + ". I'm " + this.getFullName());
  	} 
  };
  return obj;
}

const john_doe = createPerson("John", "Doe"); 
const jane_doe = createPerson("Jane", "Doe");
john_doe.greet(jane_doe);
```


## 4. OOP DEFINITIONS

Objects are used to model real world things that need to be represented inside programs, and provide an easy way to access their properties and methods

- Encapsulation
- Polymorphism
- Inheritance

## 5. OBJECT CONSTRUCTOR

The constructor function (equivalent of a class in most classical languages) builds the object and defines its methods and properties.

The familiar way (Factory/Literal approach):
```
const john_doe = { 
  first_name : "John", 
  last_name : "Doe",

 	greet : function() { 
    alert("My name is " + this.first_name + " " + this.last_name;
  } 
};
```

The Constructor Approach:
```
function Person(first_name, last_name) { 
  this.first_name = first_name; 
  this.last_name = last_name;
  this.getFullName = function() {
    return this.first_name + " " + this.last_name ;
  }
  this.greet = function(person) {
    console.log("Hello, " + this.getFullName() + ". I'm " + this.getFullName());
 	}
}

const john_doe = new Person("John", "Doe"); 
const jane_doe = new Person("Hannah", "Doe"); 
jane_doe.greet();
john_doe.getFullName();
john_doe.greet();

jane_doe.constructor;
john_doe.constructor;
```

Using the Object constructor approach:
```
const john_doe = new Person();
john_doe.first_name = "John";
```

OR 

Using the Object.create approach with a literal:
```
const john_doe = {
			first_name: "John",
			last_name: "Doe",
			getFullName: function() {
        return this.first_name + " " + this.last_name ;
      }
};

john_doe.getFullName();
const jane_doe = Object.create(john_doe);
```

## 6. OBJECT PROTOTYPES

- Prototype object acts as a template object that inherits methods and properties from its creator.
- A property of an object containing all its properties and functions. 
- Used to add any new properties and methods after the constructor function has been defined.

```
function Person(first_name, last_name) { 
  this.first_name = first_name; 
  this.last_name = last_name;
}

Person.prototype.getFullName = function() {
  return this.first_name + " " + this.last_name ;
};

Person.prototype.greet = function(person) {
  alert("Hello, " + this.getFullName() + ". I'm " + this.getFullName());
 };

const john_doe = new Person("John", "Doe"); 
const jane_doe = new Person("Jane", "Doe");
john_doe.greet();
jane_doe.greet();
```

Get an object's prototype:
```
Object.getPrototypeOf(jane_doe);
jane_doe.constructor.prototype
Person.prototype.isPrototypeOf(jane_doe)
```


## 7. LIVE PROPERTY

The prototype object is live, so if a new property or method is added to the prototype, any instances of it will inherit the new properties and methods automatically, even if that instance has already been created.
```
Person.prototype.sayHi = function(person) {
  alert("Hello, " + this.getFullName());
};

jane_doe.sayHi();
john_doe.sayHi();
```

## 7. PROPERTIES AND METHODS

Common pattern is to define all properties inside the constructor and methods on its prototype:
```
function Test(a, b, c, d) {
  // property definitions
}

// First method definition
Test.prototype.x = function() { ... };

// Second method definition
Test.prototype.y = function() { ... };

// etc.
```

## 8. INHERITANCE/EXTENDING

Prototype properties and methods are inherited from the chain - the prototype tree. But not all properties and methods are inherited.

Those defined in the prototype property are inherited. eg. Object.prototype.sayHi. But the ones that are not defined on it are available only to the object scope.
```
// add directly to constructor
Person.sayBye = function(person) {
  alert("Bye, " + this.getFullName());
};

jane_doe.sayBye(); //errors
john_doe.sayBye(); //errors
```


Constructor method:
```
function Person(first_name, last_name) {
  this.first_name = first_name;
  this.last_name = last_name;
  this.sayHi = function() {
    return console.log("Hi, " + this.getFullName());
  };
}

Person.prototype.getFullName = function() {
return this.first_name + " " + this.last_name ;
};
Person.prototype.greet = function(person) {
console.log("Hello, " + this.getFullName() + ". I'm " + this.getFullName());
};

function Student(status, first_name, last_name) {
    Person.call(this, first_name, last_name)
    this.status = status;
}

Student.prototype = Object.create(Person.prototype);
Student.prototype.constructor = Student;

Student.prototype.getState = function() {
     console.log("Student " + this.first_name + "'s status is " + this.status);
};

Person.prototype.sayBye = function() {
  console.log("See you later, " + this.getFullName());
};

const student1 = new Student( "Genius", "Stephen", "Hawkins" );
student1.getState();
student1.getFullName();
student1.sayBye();
```
PHEW - that's a lot!!

## 9. CLASS-BASED CONSTRUCT/ES6

The constructor function (equivalent of a class in most classical languages) builds the object and defines its methods and properties.
```
class Person {
    constructor(first_name, last_name) {
        this.first_name = first_name;
        this.last_name = last_name;

    }
    greet() {
        console.log( "Hi, my name is " + this.getName() );
    }
    getFullName() {
     	console.log( `${this.first_name} ${this.last_name}` );
    }
}

const writer = new Person('bill', 'bryson');
me.getFullName();

const athlete = new Person('jackie', 'smith');
athlete.getFullName();

```


Extending - inheritance:
```
class Student extends Person {
    constructor(status, first_name, last_name ) {
      super(first_name, last_name);            
      this.status = status;
    }
    getState() {
      console.log("Student " + this.first_name + "'s status is " + this.status);
    }
}

const student1 = new Student("Genius", "Stephen", "Hawkins");
student1.getState();
student1.getFullName();
```



## 10. MODIFYING EXISTING OBJECTS

Add more methods to the prototype of JavaScript’s built-in objects—such as Number, String, and Array—to add more functionality (monkey-patching):
```
Number.prototype.isEven = function() {
  return this%2 === 0;
}
Number.prototype.isOdd = function() {
  return this%2 === 1;
}

Array.prototype.first = function() {
   return this[0];
}
Array.prototype.last = function() {
  return this[this.length -1];
}
```

## 11. ERROR MANAGEMENT
Approaches
Logging
Try...Catch

## 12. COMMON ERRORS

- Variable Definition (var, let)
- Case sensitivity
- Strict mode:  
- "use strict";
- Semicolons and braces/parentheses
- Using = vs == or ===
- Non-existent methods or properties
- consistent indentation
...

## 13. DEBUGGING

- Using console.log()
- Use browser breakpoints and stack traces: debugger
- Step through code line by line
- Watch expressions


## 14. ERROR HANDLING

Using the try...catch statement:
```
try {
  alert("This is code inside the try clause"); 
  alert("No Errors so catch code will not execute");
} catch (exception) {
  alert("The error is " + exception.message);
}
```

## 15. OOP EXAMPLE

### Converting the Ajax code to use OOP (Constructor)
```
const button = document.getElementById('GetUsers');
button.addEventListener("click", getUserData);

// main process
function getUserData() {
    let url = "https://randomuser.me/api/?results=10";
    fetch(url)
        .then(function(response) {
            return response.json();
        })
        .then(function(resp) {
            document.getElementById("Output").innerHTML = JSON.stringify(resp.results);
            buildUserData( resp.results );
        })
        .catch(function(error) {
            document.getElementById("Output").innerHTML = "There was an error "+error;
        });
}

// handlers
function buildUserData(data) {
  for( item of data ) {
    const person = new Person(item);
    const p_el = document.createElement('p');
    p_el.innerHTML = person.render();
    document.body.appendChild(p_el);
  }
}

// Person model
Person = function(item) {
  this.first_name = item.name.first;
  this.last_name = item.name.last;
  this.image = item.picture.thumbnail;
  this.getName = function() {
    return this.first_name + " " + this.last_name;
  }
  this.getPicture = function() {
    return this.image;
  }
  this.render = function() {
    return `<a href=""><img src="${this.getPicture()}" /><br>${this.getName()}</a><br>`;
  }
}
```

### EXAMPLE: Converting the Ajax code to use OOP (Class)
```
const button1 = document.getElementById('GetSwiss');

button1.addEventListener("click", getGetCHData);

function getGetCHData() {
    let url = "https://randomuser.me/api/?results=10&nat=CH";
    fetch(url)
        .then(function(response) {
            return response.json();
        })
        .then(function(resp) {
            document.getElementById("Output").innerHTML = JSON.stringify(resp.results);
            buildSwissData( resp.results );
        })
        .catch(function(error) {
            document.getElementById("Output").innerHTML = "There was an error "+error;
        });
}


function buildSwissData(data) {
  for( item of data ) {
    const person = new CountryPerson(item);
    const p_el = document.createElement('p');
    p_el.innerHTML = person.render();
    document.body.appendChild(p_el);
  }
}

class Person {
    constructor(item) {
      this.first_name = item.name.first;
      this.last_name = item.name.last;
      this.image = item.picture.thumbnail;
    }

    getName() {
      return this.first_name + " " + this.last_name;
    }
    getPicture() {
      return this.image;
    }
    render() {
      return `<a href=""><img src="${this.getPicture()}" /><br>${this.getName()}</a><br>`;
    }
}


class CountryPerson extends Person {
    constructor(item) {
      super(item);
      this.nationality = item.nat;
      this.city = item.location.city;
    }
    getLocation() {
      return this.city + ', ' + this.nationality;
    }
    render() {
    return `<a href=""><img src="${this.getPicture()}" /><br>${this.getName()}<br>${this.getLocation()}</a><br>`;
    }
}
```
