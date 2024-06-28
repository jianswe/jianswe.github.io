# Algorithm: Binary Search 
## Implementation template
```js
let binarySearch = (arr, target) => {
    let left = 0;
    let right = arr.length - 1;
    while (left <= right) {
        let mid = Math.floor((left + right) / 2);
        if (arr[mid] == target) {
            // do something
            return;
        }
        if (arr[mid] > target) {
            right = mid - 1;
        } else {
            left = mid + 1;
        }
    }

    // target is not in arr, but left is at the insertion point
    return left;
}
```

## Duplicate elements 
If your input has duplicates, you can modify the binary search template to find either the first or the last position of a given element. If `target` appears multiple times, then the following template will find the left-most index:
```ts
let binarySearch = (arr, target) => {
    let left = 0;
    let right = arr.length; // right index is exclusive 
    while (left < right) {
        let mid = Math.floor((left + right) / 2);
        if (arr[mid] >= target) { 
            right = mid; // since right index is exclusive, we don't need `mid - 1` here 
        } else { // since we want the left-most index, we don't increase left when arr[mid] === target 
            left = mid + 1;
        }
    }

    return left;
}
```
The following template will find the right-most insertion point (the index of the right-most element plus one):
```js
let binarySearch = (arr, target) => {
    let left = 0;
    let right = arr.length;
    while (left < right) {
        let mid = Math.floor((left + right) / 2);
        if (arr[mid] > target) { // since we want the right-most index, we don't decrease right when arr[mid] === target
            right = mid;
        } else {
            left = mid + 1;
        }
    }

    return left;
}
```
If the element you are searching for does not exist, then `left` will be at the index where the element should be inserted to maintain sorted order (just like in a normal binary search).
