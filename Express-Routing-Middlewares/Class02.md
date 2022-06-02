#   Express REST API


-  ES6 Classes
- Using Express Routing
- Express Routing

## ES6 Classes

Classes  are a template for creating objects , Classes are in fact "special functions", 

the  syntax has two components: 
- class expressions  can be named or unnamed ,

 The name given to a named class expression is local to the class's body.

```
// unnamed
let Rectangle = class {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
};
console.log(Rectangle.name);
// output: "Rectangle"

// named
let Rectangle = class Rectangle2 {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
};
console.log(Rectangle.name);
// output: "Rectangle2"
```

- class declarations To declare a class, you use the class keyword with the name of the class

```
class Rectangle {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
}
```
classes must be defined before they can be constructed .

---
The body of a class is the part that is in curly brackets {}. This is where you define class members, such as methods or constructor.

- Strict mode

- Constructor : The constructor method is a special method for creating and initializing an object created with a class


### Prototype methods

```
class Rectangle {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
  // Getter
  get area() {
    return this.calcArea();
  }
  // Method
  calcArea() {
    return this.height * this.width;
  }
}

const square = new Rectangle(10, 10);

console.log(square.area); // 100
```

### Generator methods

```
class Polygon {
  constructor(...sides) {
    this.sides = sides;
  }
  // Method
  *getSides() {
    for(const side of this.sides){
      yield side;
    }
  }
}

const pentagon = new Polygon(1,2,3,4,5);

console.log([...pentagon.getSides()]); // [1,2,3,4,5]
```

### Sub classing with extends
```
class Animal {
  constructor(name) {
    this.name = name;
  }

  speak() {
    console.log(`${this.name} makes a noise.`);
  }
}

class Dog extends Animal {
  constructor(name) {
    super(name); // call the super class constructor and pass in the name parameter
  }

  speak() {
    console.log(`${this.name} barks.`);
  }
}

let d = new Dog('Mitzie');
d.speak(); // Mitzie barks.
```
---

# Routing

Routing refers to how an application’s endpoints (URIs) respond to client requests. For an introduction to routing,

app.get() to handle GET requests and app.post to handle POST request and app.use() to specify middleware as the callback function

```
const express = require('express')
const app = express()

// respond with "hello world" when a GET request is made to the homepage
app.get('/', (req, res) => {
  res.send('hello world')
})

```

Route methods

```// GET method route
app.get('/', (req, res) => {
  res.send('GET request to the homepage')
})

// POST method route
app.post('/', (req, res) => {
  res.send('POST request to the homepage')
})
```
Route handlers : You can provide multiple callback functions that behave like middleware to handle a request

```
app.get('/example/b', (req, res, next) => {
  console.log('the response will be sent by the next function ...')
  next()
}, (req, res) => {
  res.send('Hello from B!')
})
```
An array of callback functions

```
const cb0 = function (req, res, next) {
  console.log('CB0')
  next()
}

const cb1 = function (req, res, next) {
  console.log('CB1')
  next()
}

const cb2 = function (req, res) {
  res.send('Hello from C!')
}

app.get('/example/c', [cb0, cb1, cb2])
```
```
const cb0 = function (req, res, next) {
  console.log('CB0')
  next()
}

const cb1 = function (req, res, next) {
  console.log('CB1')
  next()
}

app.get('/example/d', [cb0, cb1], (req, res, next) => {
  console.log('the response will be sent by the next function ...')
  next()
}, (req, res) => {
  res.send('Hello from D!')
})
```
Response methods
```
Method	         Description
res.download()	Prompt a file to be downloaded.
res.end()	    End the response process.
res.json()    	Send a JSON response.
res.jsonp()	    Send a JSON response with JSONP support.
res.redirect()	Redirect a request.
res.render()	Render a view template.
res.send()	    Send a response of various types.
res.sendFile()	Send a file as an octet stream.
res.sendStatus()	Set the response status code and send its string representation as the response body.
```
## app.route()

You can create chainable route handlers for a route path by using app.route().

```
app.route('/book')
  .get((req, res) => {
    res.send('Get a random book')
  })
  .post((req, res) => {
    res.send('Add a book')
  })
  .put((req, res) => {
    res.send('Update the book')
  })
  ```
  ## express.Router

  Use the express.Router class to create modular

  ```
  const express = require('express')
const router = express.Router()

// middleware that is specific to this router
router.use((req, res, next) => {
  console.log('Time: ', Date.now())
  next()
})
// define the home page route
router.get('/', (req, res) => {
  res.send('Birds home page')
})
// define the about route
router.get('/about', (req, res) => {
  res.send('About birds')
})

module.exports = router
```
Then, load the router module in the app:

```
const birds = require('./birds')

// ...

app.use('/birds', birds)
```