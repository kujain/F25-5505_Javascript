#### SESSION #12

# JS & STORAGE
# JS IN THE BACKEND

## BROWSER STORAGE

- Purpose is to learn about the users, store and then use that data gained about them to personalize the site.
- Used to greet returning users, store browsing history on a site etc.
- Not secure as it is usually not encrypted and accessible.
- This data needs to be stored somewhere between browser sessions.
- Local file system is off limits to browsers, except in a restricted disk space called cookies or in the browser's through web storage.

## COOKIES

- Small text files stored in a web user’s browser directory or data folder. 
- Sites use cookies on users' browsers to store login credentials, identify customers, and provide a customized shopping/browsing experience within their sites.
- Convenient for retaining information from one session on a website to another, or between sessions on related websites, without having to do this on a server.
- Cookies are local to a specific browser/pc only. They cannot be transferred.
- Cookies can be set to last/expire as needed. They can persist beyond browser sessions.
- Cookies can be accessed based on its domain and path settings. It's usually defaults to be accessed by any script on the domain that set it in the first place.
- Cookies are created through javascript.



## COOKIE SECURITY

- Cookies are stored in plain text in the browser system in a system folder on the computer and should not store sensitive data.
- It is possible that third party code on sites (ads) can have access to these cookies and process them for their use, along with adding their own cookies (3rd party cookies) that is used across the ad network, leading to  user targeting/re-targeting schemes/scams.
- Cookies can be accessed by the server-side as well - they can be set and accessed, allowing for a channel for the backend code (php, ruby, python, node) to communicate (indirectly) with the frontend code (javascript/html).



## COOKIE CREATION

Cookies is a component of the DOM:

```
document.cookie = "user_name=Dave;expires=Tue, 28 Dec 2024 00:00:00;";
document.cookie = "user_age=12;expires=Tue, 28 Dec 2024 00:00:00; path=/;";
document.cookie = "user_gender=Male;expires=Tue, 28 Dec 2024 00:00:00; domain=localhost;";
document.cookie = "user_geo=Oxford;expires=Tue, 28 Dec 2024 00:00:00; domain=/localhost; secure=true";
```

## COOKIE  COMPONENTS AND SETUP

Name/value string pair: required
```
"user_name=Dave;"
"user_name="+escape("Dave Bowman")+";"
```

Expiry: follows UTC time format. If not set, cookies expires when browser is closed.
```
"expires=Tue, 28 Dec 2020 00:00:00;"

const expire = new Date();
expire.setMonth(expire.getMonth() + 6);
document.cookie = "UserName=Dave;expires=" + expire.toUTCString() + ";";
```

Path: restricts cookie access by actual path of the file currently loaded in browser:
```
// cookie is set and get by file/folders inside /get_user eg. /get_user/index, /get_user etc.
"path=/get_user;"

// cookie is set and get by all files/folder inside current domain:
"path=/;"
```

Domain: restricts cookie access by specified domain - defaults to current domain:
```
"domain=mydomain.com;"
"domain=sub.mydomain.com;"
```

Secure: sets it so cookie can be accessed only through SSL


## COOKIE CREATION FUNCTION
```
function setCookie(name, value, expires, path) {
  value = escape(value);
  if (!expires) {
    let now = new Date();
    now.setMonth(now.getMonth() + 6);
    expires = now.toUTCString();
  }
  if (path) {
    path = ";Path=" + path;
  }
  document.cookie = name + "=" + value + ";expires=" + expires + path;
}

setCookie('user_name','you');


// custom expiry
let now = new Date();
now.setHours(now.getHours() + 24);
let expiry = now.toUTCString();

setCookie('user_name','Dave Bowman', expiry);
```


 
## GETTING COOKIE VALUES

Cookies are stored in the DOM as one long string so a parsing function is needed:
```
function getCookieValue(name) {
  let cookie_value;
  const cookie_arr = document.cookie.split('; ');

  cookie_arr.forEach( val => {
    // console.log(val);
    if (val.indexOf(name) === 0) {
      cookie_value = val.substring(name.length+1);
    }
  })

  return unescape(cookie_value);
}
```

To delete, set expiry to now or past
```
// custom expiry
let now = new Date();
let expiry = now.toUTCString();

setCookie('user_name','Dave Bowman', expiry);
```


## WEB STORAGE

Issues with cookies:
- Cookies are from a much earlier age of browsers and have limits to their access in modern javascript environments.
- They are not useful for server-based applications, but mostly for browser-based applications.
- Size limitations on cookies: 4KB per cooke and at most ~40 cookies per domain.
- They have expiry settings by default.
- They are a little cumbersome to remove.

Web Storage allows a way around many of the above:
- stays within the browser and not transmitted to the server- only for javascript usage.
- Upto 5MB - 10MB storage per domain.
- Local storage data never expires.

LocalStorage object is a component of the Web Storage API that is persistent (as compared with Session Storage).

However, LocalStorage is client side only so server-side scripts cannot access it, unlike cookie.



## LOCAL STORAGE

```
// set storage data
localStorage.setItem("user_name", "Dave Bowman");

localStorage.user_name = "Frank Poole";


// get storage data
let name = localStorage.getItem("user_name");

let name = localStorage.user_name;

// remove storage data
localStorage.removeItem("user_name");

localStorage.user_name = null;

// storing more complex data
let user_details = { firstName: "John", lastName: "Doe", age: 35 };
localStorage.person = JSON.stringify(user_details);

let person_detail = JSON.parse(localStorage.person);


// clear everything
localStorage.clear();
```


## CLOUD DATABASE 

- Many new BaaS providers that allow API-based backend services in the cloud eg. Databases, Servers etc.
- A few popular BaaS: AWS (Lambda), Google Cloud Run, Firebase etc.
- Firebase Cloud DB allows API access to storage
- Firebase's Javascript SDK allows its use directly from JS without a need for a backend server-based API
- https://firebase.google.com


## SETUP

### WEB: 
https://firebase.google.com/docs/web/setup
https://console.firebase.google.com/u/0/?pli=1
Setup Database (Choose Realtime DATABASE - free tier)

- Set permission to read/write

- Copy code and import.

- Start local server (or use Code's built-in or use the gulp flow): 
```
npm install -g http-server
http-server
```

- Base code: (Get them from the console above)
```
const config = {
  apiKey: "**use your key here**",
  authDomain: "dt-webadvanced-js.firebaseapp.com",
  databaseURL: "https://dt-webadvanced-js.firebaseio.com",
  projectId: "dt-webadvanced-js",
  storageBucket: "dt-webadvanced-js.appspot.com",
  messagingSenderId: "339163927955",
  appId: "1:339163927955:web:4fc1ebd6aaba743d6ac466"
};
const db = firebase.initializeApp(config);
const st_ref = db.database().ref('students');
```





## USAGE

- INITIALIZE
```
const db = firebase.initializeApp(config);
const st_ref = db.database().ref('students');
```

- GET LIST
```
st_ref.on("value", function(snapshot) {    console.log(snapshot.val()); }
```

- SAVE LIST
```
let jsonObject = {
    first_name: form.first_name.value,
    last_name: form.last_name.value,
    email: form.email.value
};

st_ref.push(jsonObject);
```

**NOTE**: Latest version 9 requires node or modular design. But 8 can still be used more conventionally (see boilerplate for both examples)





## JS IN THE BACKEND

- Frontend deals with the client side - ie the browser 
- Where a user interacts with an app:  part of the web that you can see and interact with
- Traditionally 3 components: HTML / CSS / JS
- Backend deals with what happens at the server end ie where the frontend requests come from and are made:
- Backend processes info sent to it and stores it
- Traditionally 3 layers: SERVER / APPLICATION / DATABASE  
- Popular servers: Apache, nGINX, NodeJS
- Popular languages and platforms for Backend: PHP, Ruby, Python, JS 
- Popular Databases: mySQL, PostgreSQL, MongoDB


## API - INTERFACE BETWEEN Frontend and Backend

- APIs allow connection between completely different and unfamiliar frontend and backend systems (or between different backend systems)
- Exposes a part of the backend application through its methods and options that allow a client application to make requests to send and receive data
- APIs are needed to allow storing data at the server-side. Web storage (local storage and cookies) cannot be used for anything permanent or secure.

 


## NODEJS

- NodeJS - Backend server that uses Javascript as its language. 
- Intended for use outside of a browser context (i.e. running directly on a computer or server OS) in a headless capacity.
- Many plugins/modules to extend it for many uses- from preprocessing to server tasks
- Used for frontend and backend development workflows
- Event driven code
- Access to filesystem etc. through module

### Build a module
```
// testmodule.js

function TestFunction() {
  console.log('Hello from TestFunction!');
}
module.exports = TestFunction;

// app.js
const TestFunction = require('./testmodule);
TestFunction(); // logs 'Hello from TestFunction!'
```

**In terminal:** `node ./app.js`



### NodeJS - Basic Server setup
```
const http = require("http");

const hostname = "localhost";
const port = 8000;

// Create HTTP server 
const server = http.createServer((req, res) => {

   // Set the response HTTP header with HTTP status and Content type
   res.writeHead(200, {'Content-Type': 'text/html'});

   // Send the response body
   res.end('<h1>Hello Class</h1> \n');
});

// Logs once the server starts listening
server.listen(port, hostname, () => {
   console.log(`NODE Server running at http://${hostname}:${port}/`);
})
```

**In terminal:** `node ./server.js`


## NODEJS with MONGODB

- Setup MongoDB Atlas Cloud account (free tier)

- Install mongodb module: 
```
npm install mongodb
```

- Create Database and table and connect 
```
const { MongoClient, ServerApiVersion } = require('mongodb');

const uri = "mongodb+srv://kunal:<password>@parsons.rv7ow9n.mongodb.net/?retryWrites=true&w=majority&appName=Parsons";

// Create a MongoClient with a MongoClientOptions object to set the Stable API version
const client = new MongoClient(uri, {
  serverApi: {
    version: ServerApiVersion.v1,
    strict: true,
    deprecationErrors: true,
  }
});
```

**In terminal:** `node ./server.js`





## EXPRESS

- A popular node web framework to handle basic server tasks like GET, POST requests etc. as well as serve basic static files (html, css etc.)
- Allows building an API endpoint easily.
- Allows defining routes (different endpoints)
- Can be extended through various npm modules to handle pretty much any common (or uncommon) web server requirements.
- An un-opinionated framework - complete flexibility in how to implement it across any requirement.  
```
$ npm init -y
$ npm install --save express
```

```
const express = require('express');
const app = express();

app.get('/', function(req, res) {
  res.send('Hello Class!');
});

app.get('/users', function(req, res) {
  res.send('Hello User!');
});

app.listen(8002, function() {
  console.log('Example app listening on port 8002!');
});
```

**In terminal:** `node ./server.js`




## SIMPLE NODEJS API SERVER

- JSON SERVER - allows using a json file as a database
- https://github.com/typicode/json-server

```
npm init -y
npm install --save json-server
npm install -g json-server
touch db.json
npm run start
```

- GET example returns a student object with the id=2 `http://localhost:8002/students/2`

- GET example returns a response object with the id=2 `http://localhost:8002/responses/2`

- Other methods:
```
GET  /students // get data
GET  /students/{id} // get one student data with id={id}
POST /students // save student data
```

- SAMPLE FETCH
```
async function processCall() {
  try {
    const first_resp = await getData('http://localhost:8002/students/');
    console.log(first_resp);
    document.getElementById("Output").innerHTML += `Data returned is: ${JSON.stringify(first_resp)}`;
  } catch(error) {
    document.getElementById("Output").innerHTML = error; // TypeError: failed to fetch
  }
  console.log('done');
}

function getData( url ) {
  return new Promise( function(resolve, reject) {
    const xhr = new XMLHttpRequest();
    xhr.open( 'GET', url, true );
    xhr.send();
    xhr.onload = function () {
      console.log(xhr);
      if (xhr.status === 200) {
         const response = JSON.parse(xhr.responseText);
          resolve(response);
      } else {
          const error = xhr.statusText || 'The reason is mysterious. Call Yoda!';
          reject(error);
      }
    }
  });
}
```

- SAMPLE SAVE
```
const form = document.getElementById('createUser')
form.addEventListener("submit", processSubmit);

async function processSubmit(e) {
  e.preventDefault();
  const FD  = new FormData(form);
  FD.append("first_name",form.first_name.value);
  FD.append("last_name",form.last_name.value);
  FD.append("email",form.email.value);
  let jsonObject = {};
  for (let pair  of FD.entries()) {
      jsonObject[pair[0]] = pair[1];
  }
  try {
    const first_resp = await saveData('http://localhost:8002/students/', jsonObject);
    console.log('sdsd',first_resp);
    document.getElementById("Output").innerHTML += `Saved. Data returned is: ${JSON.stringify(first_resp)}`;
  } catch(error) {
    document.getElementById("Output").innerHTML = error; // TypeError: failed to fetch
  }
  console.log('done');
}

function saveData( url, data ) {
  return new Promise( function(resolve, reject) {
    const xhr = new XMLHttpRequest();
    xhr.open( 'POST', url, true );
    xhr.setRequestHeader("Content-Type", "application/json;charset=UTF-8");
    xhr.send(JSON.stringify(data));
    xhr.onload = function () {
      if (xhr.status === 201) {
         const response = JSON.parse(xhr.responseText);
         resolve(response);
      } else {
          const error = xhr.statusText || 'The reason is mysterious. Call Yoda!';
          reject(error);
      }
    }
  });
};
```

## USING THE CLOUD TO RUN NODEJS

- Google CLoud Run provides serverless code hosting - needs docker.
- Amazon AWS Lambda - similar to Google Cloud to host node.js services.
- Heroku is a free hosting service for hosting small projects with easy setup and deployment from the command line through github and NPM.
- Vercel is similar and makes it easy to deploy serverless applications
- etc.


## FRAMEWORKS

- Javascript development frameworks can help speed up coding and simplify the written code, especially for larger apps.
- The amount of code written is lesser since the framework handles many of the typical functionalities and takes care of many assumptions/decisions/defaults.
- Examples: 
- React
- Next
- Angular
- Vue 
- Backbone
- Ember
- Meteor
- Svelte
- Gatsby
- etc. etc.

