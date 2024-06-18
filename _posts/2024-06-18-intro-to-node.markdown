# Introduction to Node.js
## CLI 
### Process & Environment 
#### Environment 
The environment in Node.js refers to the set of variables that are available to a program at runtime. These variables are stored in the `process.env` object, which is an object containing key-value pairs of environment variable names and values. 
Here is an example of how to use environment variable: 
```js
// script.js
console.log(process.env.NODE_ENV)
```
If we run this script with command `NODE_ENV=production node script.js`, the output will be: 
```
production
```
## Modules
```js
(function(){
  console.log('IIFE')
})()
```
### Module Types
#### User-created Modules 
#### Internal Modules 
##### fs 
```js
import fs from 'node:fs'
const data = fs.readFileSync('notes.json', 'utf-8')
```
Most commonly used methods:
* `fs.readFile()` to read the content of a file asynchronously and returns its content in a callback function.
* `fs.writeFile()` to write data to a file asynchronously.

Instead of returning content in a callback function, we can use promises. 
```js
import fs from 'node:fs/promises'

const pjsonPath = new URL('./package.json', import.meta.url).pathname
console.log(JSON.parse(await fs.readFile(pjsonPath, 'utf-8')))
```

Other frequently used methods include: 
* `fs.mkdir()` to create a new directory
* `fs.readdir()` to read the contents of a directory
* `fs.stat()` to get information about a file
* `fs.unlink()` to delete a file
* `fs.rename()` to rename a file 
##### http
```js
import http from 'node:http'

```
#### Third-party Modules 
Use npm to install third-party modules. 
### Module Standards
#### CommonJS 
#### ESM
## Async in Node
### Callbacks 
Callbaks are tranditional ways to handle async. 
```js
fs.readFile('file.txt', (err, data) => {
  if (err) {
    console.error(err)
    return 
  }
  console.log(data)
})
```
But not all callbacks are async. 
```js
new Array(20000).fill(0).map((_, i) => {
  console.log(i)
})
```
Three most common ways to introduce async:  
1. Interact with DB
2. Network call
3. setTimeout
### Promise 

