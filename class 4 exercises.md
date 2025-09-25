## EXERCISE 1

### The Dice Object

1. Create a Dice object
2. create a "side" property that can be changed on definition
3. create a method that rolls the dice and returns a number between 1 and the side.
4. create 2 instances of dice, one with 6 sides and one with 12 sides and run the methods on each.

```
// Option 1
const Dice = {
    sides: 6,
    roll: function() {
        return Math.floor(this.sides * Math.random()) + 1;
   }
   check_roll() {
        let val = Math.floor(this.sides * Math.random()) + 1;
        if ( val > 3 ) {
          return 'Good job - you rolled a large number!'
        } else {
          return 'TOo bad - try again!'
        }
   }
}

Dice.sides = 6;
Dice.roll();
Dice.check_roll();

Dice.sides = 12;
Dice.roll();
Dice.check_roll();
```

```
// Option 2
class Dice {
  constructor( side = 4 ) {
    this.sides = side;
  }
  rollDice() {
    return Math.floor(this.sides * Math.random()) + 1;
  }
   check_roll() {
        let val = Math.floor(this.sides * Math.random()) + 1;
        if ( val > 3 ) {
          return 'Good job - you rolled a large number: ' + val + '!'
        } else {
          return val + '...Too bad - try again!'
        }
   }
};

const dice = new Dice( 6 );
dice.rollDice();
dice.check_roll();

const dice2 = new Dice( 12 );
dice2.rollDice();
dice2.check_roll();
```

## EXERCISE 2

### The Maths Areas Calculator Object
1. Create a Shape object
2. create a "number of side" property that can be changed on definition or later.
3. create a method for areas calculation for the shape based on the number of sides provided.
4. Similarly create a method for perimeter calculation for the shape based on the number of sides provided

```
class Shape {
  constructor( side = 4, len = 1 ) {
    this.sides = side;
    this.length = len;
  }
  calcPer() {
    return (this.sides * this.length);
    return a;
  }
  calcArea() {
    // (sides x length^2) / (4 x tan(pi/sides))
    return (this.sides * this.length*this.length) / (4 * Math.tan(Math.PI/this.sides));
  }
};

const penta = new Shape( 5, 2 );
penta.calcArea();
penta.calcPer();

const octa = new Shape( 8, 2 );
octa.calcArea();
octa.calcPer();

```

 
