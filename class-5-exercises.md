## Assignment 1
#### Update the style of the first paragraph tag in the HTML to use a different font family, color and/or size.
```
const  my_p_elements = document.getElementsByTagName("p");

// get the first p elements
const my_p1 = my_p_elements[0];
my_p1.style.background = "rgb(255,0,0)";

// get the second p elements
const my_p2 = myBodyElements[1];
my_p2.style.background = "rgb(255,255,0)";
```

## Assignment 2
#### Add a new paragraph tag at the bottom of the "section" node.
```
const new_para = document.createElement('p');
new_para.textContent = "This is the end.\nThanks for watching";
// or
new_para.innerHTML = 'This is really the <b>End</b>.';

// get the first section node and add inside it
const sect = document.getElementsByTagName('section')[0];
sect.appendChild(new_para);

```

## Assignment 3
#### Create a table and paint alternative colors to its rows. here's the html Markup:
```
<table>
  <tr>
    <td>Cell 1:1</td>
    <td>Cell 2:1</td>
    <td>Cell 3:1</td>
    <td>Cell 4:1</td>
    <td>Cell 5:1</td>
  </tr>
  <tr>
    <td>Cell 1:2</td>
    <td>Cell 2:2</td>
    <td>Cell 3:2</td>
    <td>Cell 4:2</td>
    <td>Cell 5:2</td>
  </tr>
  <tr>
    <td>Cell 1:3</td>
    <td>Cell 2:3</td>
    <td>Cell 3:3</td>
    <td>Cell 4:3</td>
    <td>Cell 5:3</td>
  </tr>
  <tr>
    <td>Cell 1:4</td>
    <td>Cell 2:4</td>
    <td>Cell 3:4</td>
    <td>Cell 4:4</td>
    <td>Cell 5:4</td>
  </tr>
  <tr>
    <td>Cell 1:5</td>
    <td>Cell 2:5</td>
    <td>Cell 3:5</td>
    <td>Cell 4:5</td>
    <td>Cell 5:5</td>
  </tr>
</table>
```

```
// option 1 using the rows convenience selector (very legacy)
// Note that if you are using an index to find the nth table in DOM, make sure it's selecting the correct one. eg. here I use 2 since in my html, this is the 3rd table.
let table = document.getElementsByTagName('table')[0];

// alt rows
for (let i = 0; i < table.rows.length; i++) {
  let row = table.rows[i];
  if ( i % 2 === 0 ) {
    row.style.backgroundColor = 'red';
  } else {
    row.style.backgroundColor = 'grey';
  }
}

// option 2 using query selectors
// first assign the table and ID (or class or whatever to identify it)
let rows = document.querySelectorAll('table tr');
for (let i = 0; i < rows.length; i++) {
  let row = rows[i];
  console.log(row);
  if ( i % 2 == 0 ) {
  	  row.style.backgroundColor = "green";
  }
}

// option 3 using more css systax in query selectors
const trs = document.querySelectorAll('table tr:nth-child(odd)');

//console.log(Array.from(trs));
for( let tr of Array.from(trs) ) {
  tr.style.backgroundColor = 'purple';
}
```

## Assignment 4
#### Create a listener to change the background of the body element
```
document.body.addEventListener('click', function() {
    let rnd_red = Math.floor( Math.random() * 255 )
    let rnd_blue = Math.floor( Math.random() * 255 )
    let rnd_green = Math.floor( Math.random() * 255 )
    document.body.style.backgroundColor = 'rgb( '  + rnd_red + ',' + rnd_blue + ',' + rnd_green + ')';
})
```

## Assignment 5
#### Write code that, on click of a button, can choose a random image from unsplash and add it inside the section tag: (you can use this url as the source: https://picsum.photos/600/400)
```
const an = document.getElementsByTagName('a')[0];

an.addEventListener("click", function(e){
  console.log('clicked on: a');
  e.preventDefault();

  const img = document.createElement('img');
  img.src = 'https://picsum.photos/600/400';

  // add image at the bottom of section
  let sect = document.getElementsByTagName('section')[0];
  sect.appendChild(img);
  e.preventDefault();
});
```

## Assignment 6
#### To an element, add a click handler that opens a popup box. Then add another handler that hides it when clicked outside the popup
```
// select the first link on the page
// also see what happens when you change it to different link on the page
const an = document.getElementsByTagName('a')[1];

// add a mouse hover event listener
an.addEventListener("mouseover", function(e){
  console.log('clicked on: a',e,e.pageX,e.pageY);

  // create a new element to hold the tip and add next to the mouse location
  const tip = document.createElement('div');
  tip.innerHTML = 'This is a tooltip';
  tip.classList.add('tip');
  document.body.appendChild(tip);

  tip.style.left = e.pageX + "px";
  tip.style.top = e.pageY + 10 + "px";
  e.preventDefault();
});

// add a mouse hover out listener
an.addEventListener("mouseout", function(e){
  const tip = document.getElementsByClassName('tip')[0];
  tip.remove();
});

// prevent default clicking
an.addEventListener("click", function(e){
  e.preventDefault();
});

```

