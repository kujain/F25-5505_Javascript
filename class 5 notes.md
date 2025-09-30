
#### SESSION #5

# THE DOCUMENT OBJECT MODEL & EVENT HANDLING

## WEB STANDARDS

WEB LIVING STANDARDS

- HTML standard (current HTML5)
- W3C.org
- https://www.w3.org/TR/html52/

- ECMAscript  (current ES2022)
- ecma-international.org
- https://262.ecma-international.org/13.0/

- CSS (current CSS 3 - no new version since then)
- W3C.org


## DOCUMENT OBJECT MODEL
- Abstract and standardized representation of the HTML document independent of the browser render of the page but fully linked (live).
- DOM Standards and Levelshttps://caniuse.com/#search=dom
- Some browsers do add in variations to the model  eg. https://quirksmode.org/dom/html
- Basically a collection of objects within objects (called Nodes and NodeLists)
```
<!DOCTYPE html>
<html lang="en">
<head></head>
<body>
<h1>My Heading</h1>
<p>This is some text in a paragraph.</p>
</body>
</html>
```

# THE DOM TREE

```
<!DOCTYPE html>
<html lang="en">
<head>
  <title>This is the Page Title</title> 
</head>
<body>
<!-- this is a comment -->
  <h1 id="title">Main Title</h1>
  <span>Below is a <strong>table</strong></span> 
  <table class="primary_table">
    		<tr>
        		<td>Row 1 Cell 1</td> 
<td>Row 1 Cell 2</td>
    		</tr> 
  </table>
  <span>Above is a table</span> 
</body>
</html>
```


## DOM NODES

DOM has different types of nodes. Some common ones:
- Element node: 1
- Text node: 3
- Comment node: 8
- The top level node, which is document: 9

## DOM PROPERTIES

Accessing the document object:  document
```
const body = document.body;		// returns node object - level 1
console.log( body.nodeType);	// returns integer
console.log( body.nodeName);	// returns name "BODY"
console.log( body.nodeValue);	// returns nothing since it only has childnodes
console.log( typeof(body) ); // returns object
console.log( document.documentElement);	// returns top level (usually HTML)
const images = document.images; 	// returns a list of image nodes
const forms = document.forms; 	// returns a list of forms
const links = document.links; 	// returns a list of links inside anchors
```


## DOM METHODS

Getting elements
```
const title = document.getElementById('title');				// returns node object
const table = document.getElementsByClassName('primary_table'); 	// list of table objects by classname
let spans = document.getElementsByTagName('span');			// list of span objects
```
Element list - similar to array (has length property) and can be iterated. eg.
```
for (let i = 0; i < spans.length; i++) {
  let item = spans[i];
  console.log( item.nodeType );
}
```

querySelector: returns first match on any element based on the css query
```const spans = document.querySelector('.primary_table td');	// the first table with the class
```

querySelectorAll - returns the node list
```
const spans = document.querySelectorAll('span');			// list of span objects
```

## TRAVERSING THE DOM

childNodes returns ALL nodes that are children of a DOM object node:
```
const tables = document.querySelector('.primary_table');	// list of table objects by class
tables.childNodes;
```

children returns all ELEMENT nodes that are children of a DOM object node:
```
tables.children; // returns only child element Nodes
```

parentNode returns the parent node of a DOM object node:
```
tables.parentNode;
```


nodeValue returns  value inside a DOM object node containing text:
```
tables.nodeValue;	//returns null
tables.getElementsByTagName('td')[0].childNodes[0].nodeValue; //returns content
document.querySelector('h1').childNodes[0].nodeValue; //returns content
```

textContent/innerHTML returns  values inside a DOM object node:
```
const tables = document.querySelector('.primary_table');	// list of objects inside table
tables.textContent;
tables.innerHTML;
```

## DOM ATTRIBUTES

All HTML elements have attributes such as class, id, src, and href:
```
tables.getAttribute("class");	// return "primary_table"
tables.getAttribute("id");		// return null

const metas = document.getElementsByTagName("meta");
for (let i=0; i<metas.length; i++) { 
if (metas[i].getAttribute("charset")) { 
    	console.log ( metas[i].getAttribute("charset") ); 
      }
} 
// OR
console.log(document.querySelector("meta[charset]").getAttribute("charset"));
```

Custom Data Attributes:
```
tables.dataset["columns"];	// return value of data-columns attribute
```


Class attributes:
```
tables.className;   // return "primary_table"
```
More flexible:
```
// returns a object list of all classes
tables.classList.contains("primary_table");

tables.classList
```

## SETTING DOM ATTRIBUTES

Using generic attributes:
```
tables.className;		// return "primary_table"
tables.setAttribute("class", "sec_table");
tables.setAttribute("id", "FirstTable");
document.querySelector("meta[charset]").setAttribute("charset","ASCII");
```

For Class attributes only:
```
tables.className = tables.className + "sec_table";		// return "primary_table"
tables.classList.add("third_table");	// returns a object list of all classes
tables.classList.remove("sec_table");
tables.classList.toggle("enabled");
```

## UPDATING DOM 

Create a new element:
```
const new_para = document.createElement('p');
const text = document.createTextNode('This is the end.');
new_para.appendChild(text);
```

OR
```
const new_para = document.createElement('p');
new_para.textContent = "This is the end.";
```

Add to Page:
```
document.body.appendChild(new_para); //adds to end of body

const top_head = document.getElementsByTagName('h1')[0];
top_head.appendChild(new_para); //adds to end of h1 tag

const sect = document.getElementsByTagName('section')[0];
const title = sect.getElementsByTagName('h1')[0];
sect.insertBefore(new_para,title); // //adds before h1 tag
```

Removing elements:
```
sect.removeChild(new_para);
// reference still exists so it can be reinserted.
sect.insertBefore(new_para,title);
```

Replacing elements:
```
h1 = document.getElementById("title");
let oldText = h1.firstChild;
let newText = document.createTextNode("New Title");
h1.replaceChild(newText,oldText)

// alternative non-standard but accepted approach
h1.innerHTML = "New Title"; 
```

Playing with Styles:
```
const h1 = document.getElementById("title");

h1.style.border = "2px solid red";

h1.style.backgroundColor = "lightgrey"; //props are in lower camel case

h1.style.display = "none";
```

## EVENTS
- Connects user interactions with the DOM.
- Events occur whenever user clicks, types, moves the mouse.
- Custom events can also be defined in javascript.
- Event listeners informs javascript when the event happens.

Events list: https://developer.mozilla.org/en-US/docs/Web/Events
OR
https://w3c.github.io/uievents/#event-types-list



## EVENT LISTENERS

Event listener is a DOM method that listens out for any specified event on the page:
```
document.addEventListener(event_type, callback_function);

const an = document.getElementsByTagName('a')[0];
an.addEventListener("click", function() {    alert('xx')});
```

Adding Event listeners to the root (document):
```
addEventListener("click", function() { 
  alert("yy");
}); //click anywhere on the document
```


## EVENT PARAMETER OBJECT

An event object is sent to the callback function:
```
const an = document.getElementsByTagName('a')[0];
const clickFunction = function(e) {
	console.log(e.type); // contains all properties of the event that occurs
	console.log(e.taget); // contains the element that was clicked
}
an.addEventListener("click", clickFunction);
```

## TYPES: MOUSE EVENTS

The mouseover event occurs when the mouse pointer is placed over the element to which the event listener is attached.The mouseout event occurs when the mouse pointer moves away from an element. The mouseover event occurs when the mouse pointer is placed over the element The mouseout event occurs when the mouse pointer moves away from an element.
```
const an = document.getElementsByTagName('a')[1];
an.addEventListener("click",function(e){ console.log("click") });
an.addEventListener("mousedown",function(e){ console.log("down") });
an.addEventListener("mouseup",function(e){ console.log("up") });
an.addEventListener("mouseover",function(e){ console.log("over") });
an.addEventListener("mouseout",function(e){ console.log("out") });
```

## BLOCK DEFAULT BEHAVIOUR

Prevent redirecting to a link on clicking an anchor:
```
const an = document.getElementsByTagName('a')[1];
an.addEventListener("click",function(e){ 
  console.log("click");
  e.preventDefault();
});
```  

## EVENT PROPAGATION

An event is inherited by all child nodes of the node the listener is added to.
**Bubbling** - when an event type goes up the tree in sequence of priority, firing on elements with more specific event handler to less specific - default
**Capturing** -when  the event is first captured by the outermost element and propagated to the inner elements - also known as trickle down

```
const an = document.getElementsByTagName('a')[1];
an.addEventListener("click",function(e){ 
  console.log("click a");
  e.preventDefault();
});

const ap = document.getElementsByTagName('p')[0];
ap.addEventListener("click",function(e){ 
  console.log("click p");
  e.preventDefault();
});

To stop propagation:
e.stopPropagation();
```


## EVENT DELEGATION

An event is inherited by all child nodes of the node the listener is added to.
```
const list = document.getElementsByTagName('ul')[0];
list.addEventListener("click",function(e){ 
  console.log("click");
  e.preventDefault();
});
```
