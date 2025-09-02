## Exercise 1
### Hello World!
```
console.log('Hello Fall 2025');
```
### Using vars with Hello World!
```
let greeting_container;
// assign greeting to variable
greeting_container = 'Hello Fall 2025';
console.log(greeting_container);
```

### Generate an Alert
```
alert('Greetings ' + greeting_container);
```
### Update the Document
```
document.write('<p>' + greeting_container + '</p>');
```

## Exercise 2
### Event Listener
```
/* event listener to change body background */
const btn = document.getElementById('button');

const rainbow = ['red','orange','yellow','green','blue','rebeccapurple','violet'];
function change() {
  const num = Math.floor( 7*Math.random() );
  document.body.style.background = rainbow[Math.floor(7*Math.random())];
}
btn.addEventListener('click', change);
```
### Automatic
```
setInterval( change, 500 );
```

## Exercise 3
### DOM Manipulation
```
/* Simple DOM Manipulation example */
const now = new Date();
const hours = now.getHours();

document.write(`It's now: ${hours}. <br><br>`);
let bgColor = "black";

if (hours > 17 && hours < 20){
  bgColor = "orange";
}
else if (hours > 19 && hours < 22){
  bgColor = "orangered";
}
else if (hours > 21 || hours < 5){
  bgColor = "#C0C0C0";
}
else if (hours > 8 && hours < 18){
  bgColor = "lightblue";
}
else if (hours > 6 && hours < 9){
  bgColor = "skyblue";
}
else if (hours > 4 && hours < 7){
  bgColor = "steelblue";
}
else {
  bgColor = "white";
}

document.body.style.backgroundColor = bgColor;
```

## Exercise 4
### AJAX and APIs

Use the boilerplate files provided.








