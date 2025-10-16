# Class 7 Exercises
Here are some of the scripts that were used during class (use the HTML Boilerplate files from Class 7 to work with these):

### Blocking Sync Code
```
// do NOT attempt this!!
while( 1 ) {
	console.log('a');
} // DO NOT RUN THIS - YOU WILL CRASH YOUR BROWSER!!
```

### Non-blocking Async Code
```
console.log('start');

setTimeout( function() {
  console.log('it is now 3 secs later');
  }, 3000);
console.log('end?'); // this runs before 'it is now 3 secs later'
```

### Async behaviour - 3 will print before 2 and 4.
```
console.log("1");
setTimeout(function(){console.log("2");},3000);

console.log("3");
setTimeout(function(){console.log("4");},1000);
```

### Ajax testing with https://reqres.in/ and XMLHttpRequest()
```
let button = document.getElementById('GetUsers');
button.addEventListener("click", getUserData);

function getUserData() {
	let url = "https://reqres.in/api/users";
	let xhr = new XMLHttpRequest();
	xhr.onerror = function() {
		document.getElementById("Output").innerHTML = "There was an error";
	}

	xhr.onprogress = function(event) {
		console.log(event);
		document.getElementById("Output").innerHTML = "In progress";
	}

	xhr.onload = function() {
		if (xhr.status === 200) {
				let authors = JSON.parse(xhr.responseText); // Getresults
				for (key in authors.data) { // loop through theresults
						let author = authors.data[key]; //assign current row to author var
						console.log(author);
				}
		} else {
			document.getElementById("Output").innerHTML = "There was an error";
		}
	}

	xhr.open("GET", url, true);
  xhr.setRequestHeader( 'x-api-key', 'reqres-free-v1');
	xhr.send();
	console.log(xhr);
}
```

### Another Ajax testing with JokeAPI and XMLHttpRequest()

```
let button = document.getElementById('GetUsers');
button.addEventListener("click", getUserData);

function getUserData() {
  let url = "https://v2.jokeapi.dev/joke/Any?blacklistFlags=nsfw,religious,political,racist,sexist,explicit";
  let xhr = new XMLHttpRequest();
  xhr.onerror = function() {
    document.getElementById("Output").innerHTML = "There was an error";
  }

  xhr.onprogress = function(event) {
    console.log(event.loaded, event.total);
    document.getElementById("Output").innerHTML = "In progress";
  }

  xhr.onload = function() {
    if (xhr.status === 200) {
        let joke = JSON.parse(xhr.responseText); // Getresults
        console.log(joke);
        let content = `SETUP: ${joke.setup} <br>
        DELIVERY: ${joke.delivery}`;
        document.getElementById("Output").innerHTML = content;

    } else {
      document.getElementById("Output").innerHTML = "There was an error";
    }
  }

  xhr.open("GET", url, true);
  xhr.send();
  console.log(xhr);
}
```

###  Sending data using XMLHttpRequest() and POST
```
const form = document.getElementById('createUser')

form.addEventListener("submit", saveUserData);

function saveUserData(e) {
	e.preventDefault();

	let url = "https://reqres.in/api/users";

	let xhr = new XMLHttpRequest();
	let user = {}; // create an empty object
	user.name = form.first_name.value + ' ' + form.last_name.value;
	console.log(user, JSON.stringify(user));

	xhr.onload = function() {
		if (xhr.status === 200  || xhr.status === 201) {
				let resp = JSON.parse(xhr.response);
				document.getElementById("Output").innerHTML = "Successfully created id: "+resp.id;
		} else {
				document.getElementById("Output").innerHTML = "There was an error";
		}
	}

	xhr.open("POST", url, true);
	xhr.setRequestHeader("Content-Type", "application/json");
  xhr.setRequestHeader( 'x-api-key', 'reqres-free-v1');
  xhr.send(JSON.stringify(user));
	console.log(xhr);
}
```

### Using formData to send data
```
const form = document.getElementById('createUser')
form.addEventListener("submit", saveUserData);

function saveUserData(e) {
	e.preventDefault();

	let url = "https://reqres.in/api/users";

	let xhr = new XMLHttpRequest();
	
  const FD  = new FormData(form);
	FD.append("name",form.first_name.value + ' ' + form.last_name.value);
	let jsonObject = {};
	for (let pair  of FD.entries()) {
			jsonObject[pair[0]] = pair[1];
	}

	xhr.onload = function() {
		if (xhr.status === 200  || xhr.status === 201) {
				let resp = JSON.parse(xhr.response);
				document.getElementById("Output").innerHTML = "Successfully created id: "+resp.id;
		} else {
				document.getElementById("Output").innerHTML = "There was an error";
		}
	}

	xhr.open("POST", url, true);
	xhr.setRequestHeader("Content-Type", "application/json");
  xhr.setRequestHeader( 'x-api-key', 'reqres-free-v1');
  xhr.send(JSON.stringify(jsonObject));
	console.log(xhr);
}
```
### Class exercise: use above to get data from reqres and then format in the DOM.
```
let button = document.getElementById('GetUsers');
button.addEventListener("click", getUserData);

function getUserData() {

	const ul = document.createElement('ul');
	const url = 'https://reqres.in/api/users';
	const xhr = new XMLHttpRequest();
	xhr.onload = function() {
		if (xhr.status === 200  || xhr.status === 201) {
			let authors = JSON.parse(xhr.responseText); // Get results
			console.log(authors)
			for (key in authors.data) { // loop through the results
				let author = authors.data[key]; //assign current row to author var
				let li = document.createElement('li'), //  Create the elements we need
						img = document.createElement('img'),
						span = document.createElement('span');
				img.src = author.avatar;  // Add the source of the image to be the src of the img element
				span.innerHTML = author.first_name + ' ' +author.last_name; // Make the HTML of our span to be the first and last name of our author
				li.appendChild(img); // Append img element back tocontaining li
				li.appendChild(span); // Append span element back tocontaining li
				ul.appendChild(li); // Append li element back tocontaining ul
			}
			const sect = document.getElementsByTagName("section")[0];
			sect.append(ul); //Append the new ul to body
		}
	}
	xhr.open('GET', url, true);
  xhr.setRequestHeader( 'x-api-key', 'reqres-free-v1');
	xhr.send(null);
}
```

### Callback explanation - nothing is in order.
```
function printString(string) {
	const delay = Math.floor(Math.random() * 1000) + 1;
	setTimeout( function() {
			console.log(string, delay);
		},
		delay
	)
}
// in parallel(ish)
function printAll(){
	printString("A");
	printString("B");
	printString("C");
}
printAll();
printAll(); // again - prints in a diff order everytime you run it.
```
```
//simple callback hell when trying to set them to run in a specific sequence
function printString(string, callback){
	const delay = Math.floor(Math.random() * 1000) + 1;
	setTimeout( function() {
			console.log(string, delay);
			callback();
		},
		delay
	)
}

// in seq - works but the code is ugly and confusing!
function printAll(){
	printString("A", function() {
		printString("B", function() {
			printString("C", function(){} )
		})
	})
}
```

## Converting into a promise 
```
function printString(string){
	return new Promise( function(resolve, reject) {
		const delay = Math.floor(Math.random() * 1000) + 1;
		setTimeout( function() {
			 console.log(string);
			 resolve();
			},
			delay
		)
	})
}

function printAll() {
		const a = printString("A");
		const b = a.then( function() {
			return printString("B");
		});
		const c = b.then( function() {
			return printString("C");
		});
}

printAll();

//cleaned up: - by chaining them together - reads better!
function printAll() {
		printString("A")
			.then( function() {
				return printString("B");
			})
			.then( function() {
				return printString("C");
			});
}
```
### An example of embedded callbacks - callback hell in actual use when making a 2nd ajax call after the first one is completed
```
let button = document.getElementById('GetUsers');
button.addEventListener("click", getUserData);

function getUserData() {
  const url = 'https://randomuser.me/api/?results=1';
  const xhr = new XMLHttpRequest();
  xhr.onload = function() {
      if (xhr.status === 200) {
      const author = JSON.parse(xhr.responseText); // Getresults
      const name = author.results[0].id.name;
      const coords = author.results[0].location.coordinates;
      document.getElementById("Output").innerHTML = `${name} is located at ${coords.latitude} / ${coords.longitude} `;

      // check next call - this can only happen after the first request IS COMPLETE
      const xhr1 = new XMLHttpRequest();
      const url = 'http://api.open-notify.org/iss-now.json';
      xhr1.onload = function() {
        const iss = JSON.parse(xhr1.responseText);
        if (xhr1.status === 200) {
          document.getElementById("Output").innerHTML += `<br>ISS position is: ${iss.iss_position.latitude} / ${iss.iss_position.longitude}`;
          //calculate difference
          const dist = distance( coords.latitude, coords.longitude, iss.iss_position.latitude, iss.iss_position.longitude);
          document.getElementById("Output").innerHTML += `<br>Current distance between the two  is: ${dist} miles`;

        } else {
          document.getElementById("Output").innerHTML = "There was an error" + xhr1.error;
        }
      }
      xhr1.open('GET', url, true);
      xhr1.setRequestHeader("Accept", 'application/json');
      xhr1.send(null);

    } else {
      document.getElementById("Output").innerHTML = "There was an error" + xhr1.error;
    }
  }
  xhr.open('GET', url, true);
  xhr.send(null);
}

// helper function for above
function distance(lat1, lon1, lat2, lon2, unit) {
	if ((lat1 == lat2) && (lon1 == lon2)) {
		return 0;
	}
	else {
		let radlat1 = Math.PI * lat1/180;
		let radlat2 = Math.PI * lat2/180;
		let theta = lon1-lon2;
		let radtheta = Math.PI * theta/180;
		let dist = Math.sin(radlat1) * Math.sin(radlat2) + Math.cos(radlat1) * Math.cos(radlat2) * Math.cos(radtheta);
		if (dist > 1) {
			dist = 1;
		}
		dist = Math.acos(dist);
		dist = dist * 180/Math.PI;
		dist = dist * 60 * 1.1515;
		if (unit=="K") { dist = dist * 1.609344 }
		if (unit=="N") { dist = dist * 0.8684 }
		return dist;
	}
}
```

### Reworking AJAX into a promise
```
function xhrRequest( url ) {
	return new Promise( function(resolve, reject) {
		const xhr = new XMLHttpRequest();
		xhr.open( 'GET', url, true );
		xhr.send();
		xhr.onload = function () {
			if (xhr.status === 200) {
					const response = JSON.parse(xhr.responseText);
					resolve(response);
			} else {
					const error = xhr.statusText || 'The reason is mysterious. Call Yoda!';
					reject(error);
			}
		}

	}
)};

let coords;
const button = document.getElementById('GetUsers');

button.addEventListener("click", function() {
	xhrRequest('https://randomuser.me/api/?results=1')
		.then(function(resp) {
			let name = resp.results[0].id.name;
			coords = resp.results[0].location.coordinates;
			document.getElementById("Output").innerHTML = `${name} is located at ${coords.latitude} / ${coords.longitude} `;
			return xhrRequest('http://api.open-notify.org/iss-now.json')
		})
		.then( function(resp) {
			let iss = resp.iss_position;
			document.getElementById("Output").innerHTML += `<br>ISS position is: ${iss.latitude} / ${iss.longitude}`;
			 let dist = distance( coords.latitude, coords.longitude, iss.latitude, iss.longitude);
			document.getElementById("Output").innerHTML += `<br>Current distance between the two  is: ${dist} miles`;
		})
		.catch(function(error){
				document.getElementById("Output").innerHTML = "There was an error in the api: " + error;
		});
});

function distance(lat1, lon1, lat2, lon2, unit) {
	if ((lat1 == lat2) && (lon1 == lon2)) {
		return 0;
	}
	else {
		let radlat1 = Math.PI * lat1/180;
		let radlat2 = Math.PI * lat2/180;
		let theta = lon1-lon2;
		let radtheta = Math.PI * theta/180;
		let dist = Math.sin(radlat1) * Math.sin(radlat2) + Math.cos(radlat1) * Math.cos(radlat2) * Math.cos(radtheta);
		if (dist > 1) {
			dist = 1;
		}
		dist = Math.acos(dist);
		dist = dist * 180/Math.PI;
		dist = dist * 60 * 1.1515;
		if (unit=="K") { dist = dist * 1.609344 }
		if (unit=="N") { dist = dist * 0.8684 }
		return dist;
	}
}
```

### Fetch GET - cleaner and intuitive
```
let button = document.getElementById('GetUsers');
button.addEventListener("click", getUserData);

function getUserData() {
  let url = "https://reqres.in/api/users";
    fetch(url)
      .then(function(response) { // first then processes raw data into JSON - always needed
        return response.json();
      })
      .then(function(resp) { // 2nd then processes JSON data into whatever you need it to do
        console.log(resp);
        document.getElementById("Output").innerHTML = JSON.stringify(resp.data);
      })
      .catch(function(resp) { // catches any error in the above
        document.getElementById("Output").innerHTML = "There was an error";
      });
}

function getCoordData( coord ) {
	let url = "http://api.open-notify.org/iss-now.json";
	fetch(url)
		.then(function(response) {
			return response.json();
		})
		.then(function(resp) {
			console.log(resp);
			let iss = resp.iss_position;
			document.getElementById("Output").innerHTML += `<br>ISS position is: ${iss.latitude} / ${iss.longitude}`;
			let dist = distance( coords.latitude, coords.longitude, iss.latitude, iss.longitude);
			document.getElementById("Output").innerHTML += `<br>Current distance between the two  is: ${dist} miles`;
		})
		.catch(function(error) {
			document.getElementById("Output").innerHTML += "There was an error "+error;
		});
}
```

### Fetch GET - combining the above and chaining them further
```
let button = document.getElementById('GetUsers');
button.addEventListener("click", getUserData);

function getUserData(e) {
  e.preventDefault();

  const url = "https://randomuser.me/api/?results=1";
  const url2 = "http://api.open-notify.org/iss-now.json";
  let coords; // this is needed still.

  fetch(url)
    .then(function(response) {
        return response.json();
    })
    .then( function(data) {
        console.log('raw data',data);
        document.getElementById("Output").innerHTML = JSON.stringify(data.results[0]);
        coords = data.results[0].location.coordinates;

       return fetch(url2); // this returns a NEW fetch object so you can then append another 2 then() to it!
    } )
    .then( function(response) {
        return response.json();
    })
    .then(function(resp) {
        console.log('raw data',resp);
        let iss = resp.iss_position;
        document.getElementById("Output").innerHTML += `<br>ISS position is: ${iss.latitude} / ${iss.longitude}`;
        let dist = distance( coords.latitude, coords.longitude, iss.latitude, iss.longitude);
        document.getElementById("Output").innerHTML += `<br>Current distance between the two  is: ${dist} miles`;
    })
    .catch(function(error) {
        document.getElementById("Output").innerHTML = "There was an error "+error;
    });
}
```

### Fetch POST
```
const form = document.getElementById('createUser')
form.addEventListener("submit", saveUserData);

function saveUserData(e) {
	e.preventDefault();

	const url = "https://reqres.in/api/users";
	const FD  = new FormData(form);
	FD.append("name",form.first_name.value + ' ' + form.last_name.value);
	let jsonObject = {};
	for (let pair  of FD.entries()) {
			jsonObject[pair[0]] = pair[1];
	}
	console.log(jsonObject);
	//console.log(req);
	fetch(url, {
		method: 'POST',
		headers: {'Content-Type': 'application/json'},
		body: JSON.stringify(jsonObject)
	})
		.then(function(response) {
				console.log(response.json());
				return response.json();
		})
		.then(function(data) {
				console.log('raw data',data);
				document.getElementById("Output").innerHTML = "Successfully created id: "+data.id;
		})
		.catch(function(error) {
				document.getElementById("Output").innerHTML = "Th1ere was an error "+error;
		});
}
```

### Using Async Await - flattens all calls within the same scope:
```

function xhrRequest( url ) {
	return new Promise( function(resolve, reject) {
		const xhr = new XMLHttpRequest();
		xhr.open( 'GET', url, true );
		xhr.send();
		xhr.onload = function () {
			if (xhr.status === 200) {
				 console.log(url);
				 const response = JSON.parse(xhr.responseText);
					resolve(response);
			} else {
					const error = xhr.statusText || 'The reason is mysterious. Call Yoda!';
					reject(error);
			}
		}

	}
)};

const button = document.getElementById('GetUsers');
button.addEventListener("click", processCall);

async function processCall() {
	// 1st step
	const first_resp = await xhrRequest('https://randomuser.me/api/?results=1');
	const name = first_resp.results[0].id.name;
	const coords = first_resp.results[0].location.coordinates;
	document.getElementById("Output").innerHTML = `${name} is located at ${coords.latitude} / ${coords.longitude} `;

	// 2nd step
	const second_resp = await xhrRequest('http://api.open-notify.org/iss-now.json');
	const iss = second_resp.iss_position;
	document.getElementById("Output").innerHTML += `<br>ISS position is: ${iss.latitude} / ${iss.longitude}`;
	const dist = distance( coords.latitude, coords.longitude, iss.latitude, iss.longitude);
	document.getElementById("Output").innerHTML += `<br>Current distance between the two  is: ${dist} miles`;
}
```

### Reworking the class exercise using fetch:
```
const button = document.getElementById('GetUsers');
button.addEventListener("click", getUserData);

function getUserData(e) {
  e.preventDefault();

  const url = 'https://randomuser.me/api/?results=10';
  const ul = document.createElement('ul');

  fetch(url)
    .then(function(response) {
        return response.json();
    })
    .then( function(data) {
        console.log('raw data',data);

        let authors = data.results; // Getresults
        for (author of authors) { // loop through theresults
            console.log(author);
            let li = document.createElement('li'); //  Create theelements we need
            let img = document.createElement('img');
            let span = document.createElement('span');

            img.src = author.picture.medium;  // Add the source ofthe image to be the src of the img element
            span.innerHTML = author.name.first + ' ' +author.name.last; // Make the HTML of our span to be the firstand last name of our author
            li.appendChild(img); // Append img element back tocontaining li
            li.appendChild(span); // Append span element back tocontaining li
            ul.appendChild(li); // Append li element back tocontaining ul
            document.body.append(ul); //Append the new ul to body
        }

    } )
    .catch(function(error) {
        document.getElementById("Output").innerHTML = "There was an error "+error;
    });
}
```

### AI Example 1 (may not work as my quota is over the limit):
```
// fetch get
const button = document.getElementById('GetUsers');
button.addEventListener("click", getUserData);

// EDEN AI:
function getUserData(e) {
    e.preventDefault();
    // start the form event handler on submit
    console.log('sending to EDEN AI');

    // get the prompt value
    const prompt = document.getElementById('aiQ').value;

    // build the generator params
    let json = JSON.stringify({
        texts: [
          "Linux is a family of open-source Unix-like operating systems based on the Linux kernel, an operating system kernel first released on September 17.",
        ],
        temperature: 0.8,
        providers: "openai",
        question: prompt,
        examples: [
          ["What is human life expectancy in the United States?", "78 years."],
        ],
        examples_context: "In 2017, U.S. life expectancy was 78.6 years.",
        fallback_providers: "",
    });

    const apiKey = 'sk-sXqFPCq8PgwBE1JtPeSkFhGJ1djMlIR8maSi8wvQvYvnHtY3';

    fetch( `https://api.edenai.run/v2/text/question_answer`,
        {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json',
                Accept: 'application/json',
                authorization: `Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyX2lkIjoiOTY5MTU0ODMtMTE5Mi00YTRmLThhNTgtMjk0NWQ2NzQyMWJjIiwidHlwZSI6ImFwaV90b2tlbiJ9.FleD1FY5eVEwKKBWtAVCJXAfFOtMEUdMcQAjSn-AZE8`,
            },
            body: json,
        })
        .then(response => response.json())
        .then(json => {
            // once received, assign to img element and render
            console.log(json);

            document.getElementById("Output").innerHTML += `<br>Current distance between the two  is: ${json.openai.answers[0]} miles`;

        });
}
```

### AI Example 2:
```
// fetch get
const button = document.getElementById('GetUsers');
button.addEventListener("click", getUserData);


// OPEN AI:
function getUserData(e) {
    e.preventDefault();
    // start the form event handler on submit
    console.log('sending to OPEN AI');
    // get the prompt value
    const prompt = document.getElementById('aiQ').value;

    // build the generator params
    let json = JSON.stringify({
        "model": "gpt-3.5-turbo",
        "messages": [
          {
            "role": "user",
            "content": "Hello!"
          },
          {
            "role": "user",
            "content": prompt,
          }
        ]
    });
    // sorry I cannot share my api key here, as GIthub will delete it to avoid possible exposure. So you will need to generate your own and use here to run this test:
    const apiKey = 'sk-proj-***';

    fetch( `https://api.openai.com/v1/chat/completions`,
        {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json',
                Accept: 'application/json',
                authorization: `Bearer ${apiKey}`,
            },
            body: json,
        })
        .then(response => response.json())
        .then(json => {
            // once received, assign to img element and render
            console.log(json);

            const message = json.choices[0].message.content.replace(/\n/g, "<br />");

            document.getElementById("Output").innerHTML += `<br> ${message}`;

        });
}
```
