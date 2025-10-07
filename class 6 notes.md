# FORMS & FORM EVENTS

## DOM FOR FORMS
The original way to interact with a web page.
Form Elements
Form Properties & Methods
Form Events
Validation


## CLIENT/SERVER ARCHITECTURE
- Client: Web browser
- Server: web server (nginx, apache, node, IIS)
- HTTP protocol: the process used to send data between the client and server.
- Forms: allows user to initiate sending data from client to server

## THE FORM STRUCTURE
- Name: identifier for the form element
- Action: define the server url to send data to. Once processed, server responds by loading that url.
- Method: GET/POST define HOW to send the data
```
<form name="search" action="https://google.com/search" id="searchForm" method="GET">
    <input type="text" name="searchBox">
    <button type="submit">Search</button>
  </form>
```

## THE FORM ELEMENTS

- Text
- Number
- Password
- Radio
- Checkbox
- Select
- Textarea
- Button
- Label

 ```
 <form name="search" action="search" id="searchForm">
    
    <label for="SearchBox">Type your search term here:</label>
    <input type="text" name="searchBox" id="SearchBox">

    <label for="searchType">Select your search type:</label>
    <select name="searchType" id="searchType">
        <option value="quick">Quick Search</option>
        <option value="detail">Detailed Search</option>
    </select>

      <label for="searchArea">Fields to search in:</label>
      <label><input type="checkbox" name="searchArea" value="local" required-field>Local Sites</label>
      <label><input type="checkbox" name="searchArea" value="wide" required-field>Wide Sites</label>
      <label><input type="checkbox" name="searchArea" value="global" required-field>Global Sites</label>

    <label>Select your search location:</label>
    <label><input type="radio" name="searchScope" value="1">Inside Site</label>
    <label><input type="radio" name="searchScope" value="2">Outside Site</label>

      <label for="SearchPass">What's your age:</label>
      <input type="number" name="searchAge" id="SearchAge" required-field>

	<textarea>this is a test</textarea>

    <button type="submit">Search</button>

</form>
```

## THE DOM FOR FORMS
```
const form = document.forms[0];
const form =  document.getElementById('searchForm');
const form = document.querySelector('form#searchForm');
const form = document.forms["search"];
const form = document.forms.search;

const inp = document.getElementsByName("searchBox");
const inp = form.elements[0];
const inp = form.elements.searchBox;
const inp = form["searchBox"];
const inp_attribute = inp.type;
```

## FORM METHODS

```
form.submit(); //submits the form
form.reset(); //resets all input data
```

## FORM/INPUT EVENTS

```
const form = document.forms[0];
const inp = form.elements.searchBox;
```
Input events:
```
inp.addEventListener( 'focus', function() { console.log( "focused on", this.name ) } );
inp.addEventListener( 'blur', function() { console.log( "leaving", this.name ) } );
inp.addEventListener( 'change', function() { console.log( "leaving after changing", this.name ) } );
```

Form events:
```
form.addEventListener('submit', function(){ 
  console.log("submitting form", this.name);
});
```

## FORM DATA

Get value:
```
const inp = form.elements.searchBox;

inp.addEventListener( 'change', function() { 
console.log( "leaving after changing", this.value );
});
```

Set value:
```
const inp = form.elements.searchBox;
inp.value = "Enter your search term here";
```

Get/Set Attributes:
```
inp.getAttribute( "required" );
inp.hasAttribute( "required" );

inp.setAttribute( "required", 1 );

inp.required = 1;
```

## 9. FORM DATA

Password field values:
```
let input_pass = form.elements.SearchPass.value;
```

Checkbox values:
```
let input_area = form.elements.searchArea;
const form_area_vals = [];
for (i=0; i < input_area.length; i++) {
  if (input_area[i].checked) {
    form_area_vals.push(input_area[i].value);
}};
```

Alternative:
```
const form_area_vals = Array.from(input_area)
.filter(function(input_area) { 
        return input_area.checked
  })
  .map( function(item) { 
    return item.value
  });
```

Radio button values:
```
let input_scope = form.elements.searchScope.value;
```

Dropdown values:
```
let input_type = form.elements.searchType.value;
```

## BLOCKING SUBMISSIONS
```
form.addEventListener('submit', function(){ 
console.log("submitting form", this.name);
});
```

Becomes:
```
form.addEventListener('submit', function(e){ 
console.log("submitting form", this.name);
    e.preventDefault();
});
```

## FORMDATA OBJECT

FormData object: collects all data in a form in an object to be sent with the form submission:

```
const data = new FormData(form);
xhr.send(data);
```

To append:
```
data.append("name","name of person");
```

To loop through existing values:
```
const jsonObject = [];
for (let [key, value] of data.entries()) {
     jsonObject[key] = key;
}
```

## 12. FORM SUBMISSIONS

- Blocking
- HTTP clients and servers.
- Client: Javascript, HTML ...
- Server: Apache, Nginx, PHP, Ruby ...
- HTTP Requests and transfers
