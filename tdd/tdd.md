#  Node js

`What is Node ?` 

is an open-source , cross-platform runtime environment that allows developers to create all kinds of server-side tools and applications in JavaScript. 


`Benefits of node js`
- Great performance
- Code is written in "plain old JavaScript"
- access to hundreds of thousands of reusable packages using (npm) node package manager .


 - Node.js is portable. It is available on Microsoft Windows, macOS, Linux, Solaris, FreeBSD, OpenBSD, WebOS, and NonStop OS. You can use Node.js 
it is well-supported by many web hosting providers.
- It has a very active third party ecosystem and developer community, with lots of people who are willing to help.

You can use Node.js to create a simple web server using the Node HTTP package.


create a file called hello.js in your project


`in terminal type node file name ,  you can use nodemon package`

---

# Express

###  is the most popular Node web framework

` was initially released in November 2010 `

- There are mothods ( POST , GET , SET, etc….) also there are many of packeges .

- Integrate with "view" rendering engines in order to generate responses by inserting data into templates.



`Hello world Express`

```const express = require('express');
const app = express();
const port = 3000;

app.get('/', function(req, res) {
  res.send('Hello World!')
});

app.listen(port, function() {
  console.log(`Example app listening on port ${port}!`)
});
 
 ```

### Middleware 

 is functions end the HTTP request-response cycle by returning some response to the HTTP client . 

 - I can use third party middleware but before that I need Install it into my app using npm ( $ npm install morgan )
 
 - You can use the express.static middleware to serve static files, including your images, CSS and JavaScript (static() is the only middleware function that is actually part of Express).

---

# NPM
## node package manager

npm is the world's largest software registry. 

Open source developers from every continent use npm to share and borrow packages, and many organizations use npm to manage private development as well.
### npm consists of three distinct components:


- the website to discover packages
- the Command Line Interface (CLI)  runs from a terminal
- the registry  is a large public database of JavaScript software
---
#  TDD

## Test-driven development

refers to a style of programming in which three activities are tightly interwoven

- coding and testing : *in the form of writing unit test*
- design : *in the form of refactoring*

- write descrption
- run the test for enhanced.
- the code until it conforms to the simplicity criteria
repeat

---

# CI/CD

- CI  "Continuous Integration": is a workflow strategythat helps ensure everyone's changes will integrate with the current version of the project. This lets you catch bugs, reduce merge conflicts, and have confidence your software is working. 

 - CD "Continuous Delivery": is the practice of developing software in such a way that you could release it at any time. When coupled with CI, continuous delivery lets you develop features with modular code in more manageable increments.