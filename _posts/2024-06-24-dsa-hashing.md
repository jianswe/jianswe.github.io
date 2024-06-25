# Data Structure: Hashing 
## JavaScript Hash Data Structures 
### Set 
### Map 
#### constructor 
```ts
new Map(iterable)

const myMap = new Map([
  [1, "one"],
  [2, "two"],
  [3, "three"],
])
```

#### entries() 
```js
const map1 = new Map();

map1.set('0', 'foo');
map1.set(1, 'bar');

const iterator1 = map1.entries();

console.log(iterator1.next().value);
// Expected output: Array ["0", "foo"]

console.log(iterator1.next().value);
// Expected output: Array [1, "bar"]

const array1 = [...map1.entries()] // convert map entries iterable to array 
```

### Object {}
