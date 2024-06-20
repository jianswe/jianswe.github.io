# Node Web Server 
## Node Overview 
sending the right data back requires using multiple features of the computer. 
- Network socket - Receive and send back messages over the internet.
- Filesystem - that's where the html/css/javascript code is stored in files.
- CPU - for cryptography and optimizing hashing passwords.
- Kernel - I/O management

Javascript doesn't have access to all of those, but C++ does. So Node.js is written in C++. 

## http Module 
`Next.js` is heavily based of `Express`.   
`Express` is built on top of `http`
```js
import http from "http"

const server = http.createServer((req, res) => {
  if(req.method === 'GET' && req.url === '/') {
    console.log('hello from server')
    res.statusCode = 200
    res.end()
  }
})

server.listen(3001, () => {
  console.log('server on http://localhost:3001')
})
```

## API Basics
### Route 
A route is a unique combination of a URL and a HTTP Method.
#### HTTP Method
An HTTP method or Verb are constants that are used by API developers and HTTP to help determine intent of an API call. 
* GET - used to get information from an API
* POST - used to mutate or create new information on an API.
* PUT - used to replace existing information on an API.
* PATCH - used to update existing information on an API.
* DELETE - used to remove existing information on an API.
* OPTIONS - used with CORS by browsers to check to see if the client is able to actually communicate with an API.

#### Route Handlers 
A route handler is a function that executes when a certain route is triggered from an incoming request. 
