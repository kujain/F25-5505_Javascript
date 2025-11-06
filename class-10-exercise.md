
### Data to graph
```
const data = [
  {name: "Name 1", count: 1045, color: "green"},
  {name: "Name 2", count: 563, color: "purple"},
  {name: "Name 3", count: 231, color: "silver"},
  {name: "Name 4", count: 423, color: "brown"}
];
```

### Set up Canvas
```
const canvas1 = document.getElementById('canvasDrawing1');
const context1 = canvas1.getContext('2d');
```

### The simple approach
```
let y = 0;
// loop through data and draw rectangle for each
for (let item of data) {
  console.log(item);
  let x = 20;
  y = y + 50;
  let w = item.count/2;
  let h = 25;
  context1.fillStyle = item.color;
  context1.fillRect(x, y, w, h);

  context1.fillStyle = "#000000"; // fill color
  context1.font = "bold 15px sans-serif";
  context1.fillText( item.name, w + x, y+18);
}
```

### Better approach: this can scale as per the data limits dynamically
```
// get the max count from the list
const max = data.reduce(function(val, sel) {
      if (val > sel.count) {
        return val;
      } else {
        return sel.count;
      }
    }, 0);
console.log('max', max);

// calculate the scaling factor for all bars
const scaleX = ( ( canvas1.width - 100 ) / max );
console.log('scaleX', scaleX);

// move down for some padding
context1.moveTo(10,300);

// start the loop and bar generation
let n = 0;
for( const item of data ) {
  n++;
  console.log(item);
  let len = item.count;
  context1.fillStyle = item.color;
  context1.fillRect(10, 10 + (n * 70) , len * scaleX, 20 );

  context1.fillStyle = "#ACACAC"; // fill color
  context1.font = "bold 13px sans-serif";
  context1.fillText(item.name, 15, 25 + (n * 70));
}
```
