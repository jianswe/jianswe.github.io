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
