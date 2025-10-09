## In Class Exercises

1. Create a simple function that can reverse the contents of a sentence, word, phrase.
```
function reverseText( phrase ) {
  phrase = phrase.split("");
  phrase = phrase.reverse();
  phrase = phrase.join("");
  return phrase;
}

let vv = "hello there";
console.log( reverseText( vv ) );
```

OR:
```
function reverseText( phrase ) {
  return phrase.split("").reverse().join("");
}
let vv = "hello there";
console.log( reverseText( vv ) );
```

2. Create a function that can return the circumference and area of a circle, when provided with a diameter value.
```
function calculateArea(my_radius) {
  return { area: my_radius * my_radius * Math.PI, circum: my_radius * 2 * Math.PI };
}
console.log( calculateArea( 20 ) );

```

3. Write a program that checks if a given number is prime or not.
```
function checkPrime(num)
{
      let d = 2;
      while ( d < num ){
        if ( ( num % d ) == 0 ) {
          return false;
        }
        d++;
      }
      // no division found, number is a prime
      return true;
}
console.log( checkPrime( 2000 ) );
console.log( checkPrime( 11 ) );
```

4. Create a function that will accept a date or year and calculate if it falls on a Leap Year.
```
function leapYear(year)
{
  // year is either divisible by 400 OR (is divisible by 4 and NOT divisible by 100)
  return ( ( year % 4 == 0 ) && ( year % 100 != 0 ) ) || ( year % 400 == 0) ;
}

console.log( leapYear(2000) );
console.log( leapYear ( new Date().getFullYear() ) );
```

5. Create a function that checks a string or sentence and returns true if that parameter is a palindrome, (the string is the same forward as it is backward) . eg. kayak, racecar, madam, tenet, etc.
```
function palin( str ) {
    str = str.toLowerCase();
    let revsrt = str.split('').reverse().join('');
    return revsrt === str;
}
console.log( palin('kayak') );
console.log( palin('apple') );
```

6.	Use the object below and write a function(s) to determine the oldest person in this list.
```
const people = [
  {
    name: 'Carly',
    yearOfBirth: 2018,
  },
  {
    name: 'Ray',
    yearOfBirth: 1962,
    yearOfDeath: 2011
  },
  {
    name: 'Jane',
    yearOfBirth: 1912,
    yearOfDeath: 1941
  },
]
```

```
function findOldestPerson(people) {
  if (people.length === 0) {
    return null; // Handle empty array case
  }

  let oldest_person = people[0];

  for (let i = 1; i < people.length; i++) {
    const current_person = people[i];

    const current_age = ! current_person.yearOfDeath ? new Date().getFullYear() - current_person.yearOfBirth : current_person.yearOfDeath - current_person.yearOfBirth; 
    const oldest_age = ! oldest_person.yearOfDeath ? new Date().getFullYear() - oldest_person.yearOfBirth : oldest_person.yearOfDeath - oldest_person.yearOfBirth; 

    if (current_age > oldest_age) {
      oldest_person = current_person;
    }
  }

  return oldest_person;
}

console.log( findOldestPerson( people ) );
```
Alternative using array.reduce() iterator:
```
function getAge(birth, death) {
    if (!death) {
     death = new Date().getFullYear(); // return current year using Date()
    }
    return death - birth; // else just return age using death minus birth
}

function findOldestPerson( people ) { 
// Use reduce method to reduce the array by comparing current age with previous age
  return people.reduce((oldest, currentPerson) => {
    // oldestAge gets the age of the oldest person's year of death and birth
    const oldestAge = getAge(oldest.yearOfBirth, oldest.yearOfDeath);

    // currentAge gets the age of the current person's year of death and birth
    const currentAge = getAge(currentPerson.yearOfBirth, currentPerson.yearOfDeath);

    // return name if current age is older than the oldest age, else return current oldest age
    return oldestAge < currentAge ? currentPerson : oldest;
  });

}

console.log( findOldestPerson( people ) );
```

7. Build validation for a form and show a modal window with validation error messages when found. Then build another using inline validation. Basically check the value of an input and show the validation error in a dynamically created element on the page itself.

8. Use a form and DOM and form event listener to update the AI/Chatbot object created in class 4 assignment. Use basic validation to make sure a question is actually asked before submitting/processing.
