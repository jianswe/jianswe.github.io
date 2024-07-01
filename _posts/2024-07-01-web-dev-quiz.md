# Advanced Web Development Quiz 
## async & defer 
Q1: Put the scripts in the right order of execution  
  A. <script async src="async1.js" />         // Loads in 300ms    
  B. <script defer src="defer1.js" />         // Loads in 200ms    
  C. <script defer src="defer2.js" />         // Loads in 300ms   
  D. <script async src="async2.js" />         // Loads in 50ms  
  E. <script async defer="asyncdefer1.js" />  // Loads in 60ms  

Answer: D -> E -> A -> B -> C 

async: fetch the script, at the same time parsing the HTML.  
defer: only execute the script after HTML parsing is finished.  
When you have boht async and defer, the script will be async.  

Parse HTML -> async2.js -> asyncdefer1.js -> Parse HTML -> async1.js -> HTML parsing complete -> defer1.js -> defer2.js

## Rendering Pipeline & Compositing 
Q2: Which statements are true?  
  A. The render tree contains all elements from the DOM and CSSOM combined.  
  B. Compositing is the process of separating layers based on z-index, which are then combined to form the final image displayed on the screen.  
  C. The layout process assigns colors and images to the visual elements in the render tree.  
  D. The composting process happens on the compositor thread.  
  E. Elements that aren't visible on the page, for example `display: hidden`, aren't part of the DOM tree.  

Answer: D 

1. DOM Tree & CSSOM Tree
2. Render Tree: contains both DOM and CSSOM tree, but doesn't include elements that are not visible, like `head` elements, or `display:hidden`.
3. Layout: Calculate the position, size, viewport.
4. Paint: Screen resolution, assigns colors and images to the visual elments in the render tree. 
5. Composite: merge all layout together, but not based on z-index.

## Resolving Domain Requests 
Q3: Fill in the correct terms  
Browser sends request to A (Recursive DNS Resolver) 
A queries B (Root Name Server) 
B responds with C IP address  
A queries C (Top Level Domain Name Server) 
C responds with D IP address  
A queries D (Authoritative Name Server) 
D responds with website's E (IP Address)  

1. Recursive DNS Resolver
2. Root Name Server
3. IP Address
4. Top Level Domain Name Server
5. Authoritative Name Server 

Note: 
1. Root Name Server: .com, .net, .co.uk, .dev, etc.
2. Top Level Domain Name Server: google.com, twitter.com, website.com, facebook.com, etc.
3. Authoritative Name Server: www.website.com, api.website.com, etc.

## Call Stack & Event Loop 
Q4: What gets logged? 
```js
setTimeout(() => console.log(1)) // push () => console.log(1) to Macrotask Queue 
Promise.resolve().then(() => console.log(2)) // push () => console.log(2) to Microtask Queue
Promise.resolve().then(() => setTimeout(() => console.log(3))) // push () => setTimeout() to to Microtask Queue 
new Promise(() => console.log(4)) // Promise body run synchronously, it only returns a Promise. So () => console.log(4) get called on Call Stack right away
setTimeout(() => console.log(5)) // push () => console.log(5) to Macrotask Queue
```

answer: 4 2 1 5 3 

* **Call Stack**: Stack that keeps track of the sequence of function calls and their execution contexts. 
* **Web API**: API that enables web features like: DOM manipulaiton, Timers (setTimeout), Networking (fetch), etc. 
* **Macrotask Queue**: `setTimeout` callbacks, `setInterval` callbacks, UI rendering tasks, User input events, Network events. 
* **Microtask Queue**: Promise callbacks, queueMicrotask callbacks, async/await, MutationObserver callbacks. 
* **Event Loop**: Continuous loop that sends tasks from the task queue (Microtask first) to the Call Stack. 
