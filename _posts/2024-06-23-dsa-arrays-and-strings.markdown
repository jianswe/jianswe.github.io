# Data Structures: Arrays and Strings 

## Big O

| Operation      | Array      | String(Immutable)
| ------------- | ------------- | -------------------- |
| Appending to end | O(1) | O(n) |
| popping from end | O(1) | O(n) |
| Insertion, not from end | O(n) | O(n) |
| Deletion, not from end | O(n) | O(n) |
| Modifying an element | O(1) | O(n) |
| Random access | O(1) | O(1) | 
| Checking if element exists | O(n) | O(n) |

## JavaScript Common methods
### Array
`slice(start?, end?)`: returns a shallow copy of a portion of an array into a new array object selected from `start` to `end` (`end` not included). It support negative index. 
```js
const animals = ['ant', 'bison', 'camel', 'duck', 'elephant'];

console.log(animals.slice(1, 5));
// Expected output: Array ["bison", "camel", "duck", "elephant"]

console.log(animals.slice(-2));
// Expected output: Array ["duck", "elephant"]

console.log(animals.slice(2, -1));
// Expected output: Array ["camel", "duck"]

console.log(animals.slice());
// Expected output: Array ["ant", "bison", "camel", "duck", "elephant"]
```
`splice(start, deleteCount, item1, item2, /* …, */ itemN))`: changes the contents of an array by removing or replacing existing elements and/or adding new elements *in place*.   

### String 
`slice(start, end?)`: works the same as Array `slice`    
`substr()`: **deprecated**   
`substring(start, end?)`: returns the part of this string from the start index up to and excluding the end index, or to the end of the string if no end index is supplied.   


## Two Pointers 
### 4Sum 
Given an array `nums` of `n` integers, return an array of all the unique quadruplets `[nums[a], nums[b], nums[c], nums[d]]` such that:
* `0 <= a, b, c, d < n`
* `a`, `b`, `c`, and `d` are distinct.
* `nums[a] + nums[b] + nums[c] + nums[d] == target`

You may return the answer in any order.

Example 1:   
Input: nums = [1,0,-1,0,-2,2], target = 0   
Output: [[-2,-1,1,2],[-2,0,0,2],[-1,0,0,1]]   
Example 2:   
Input: nums = [2,2,2,2,2], target = 8   
Output: [[2,2,2,2]]   

```ts
function fourSum(nums: number[], target: number): number[][] {
    let ans = new Set<string>()
    nums.sort((a,b)=>a-b)
    for (let i=0; i<nums.length-3; i++) {
        for (let j=i+1; j<nums.length-2; j++) {
            let left = j+1, right = nums.length-1, targetSum = target - nums[i] - nums[j]
            while (left<right) {
                if (nums[left] + nums[right] === targetSum) {
                    ans.add(nums[i] + "," + nums[j] + "," + nums[left] + "," + nums[right])
                    left++
                    right--
                } else if (nums[left] + nums[right] < targetSum) {
                    left++
                } else {
                    right--
                }
            }
        }
    }
    return [...ans].map(str => str.split(',').map(strNum => parseInt(strNum)))
};
```

## Binary Array
### 3191. Minimum Operations to Make Binary Array Elements Equal to One I
You are given a binary array `nums`.    
You can do the following operation on the array any number of times (possibly zero):   
* Choose any 3 consecutive elements from the array and flip all of them.

Flipping an element means changing its value from 0 to 1, and from 1 to 0.  
Return the minimum number of operations required to make all elements in nums equal to 1. If it is impossible, return -1.

Example 1:

Input: nums = [0,1,1,1,0,0]

Output: 3

Explanation:
We can do the following operations:

Choose the elements at indices 0, 1 and 2. The resulting array is nums = [1,0,0,1,0,0].
Choose the elements at indices 1, 2 and 3. The resulting array is nums = [1,1,1,0,0,0].
Choose the elements at indices 3, 4 and 5. The resulting array is nums = [1,1,1,1,1,1].
Example 2:

Input: nums = [0,1,1,1]

Output: -1

Explanation:
It is impossible to make all elements equal to 1.
```ts
function minOperations(nums: number[]): number {
    let ans = 0
    for (let i =0; i< nums.length-2; i++) {
        if (nums[i] === 0) {
            nums[i] = 1
            nums[i+1] = 1 - nums[i+1]
            nums[i+2] = 1 - nums[i+2]
            ans++
        }
    }
    if (nums[nums.length-2] === 1 && nums[nums.length-1] === 1) {
        return ans 
    }
    return -1
};
```

### 3192. Minimum Operations to Make Binary Array Elements Equal to One II
You are given a 
binary array
 nums.

You can do the following operation on the array any number of times (possibly zero):

Choose any index i from the array and flip all the elements from index i to the end of the array.
Flipping an element means changing its value from 0 to 1, and from 1 to 0.

Return the minimum number of operations required to make all elements in nums equal to 1.

 

Example 1:

Input: nums = [0,1,1,0,1]

Output: 4

Explanation:
We can do the following operations:

Choose the index i = 1. The resulting array will be nums = [0,0,0,1,0].
Choose the index i = 0. The resulting array will be nums = [1,1,1,0,1].
Choose the index i = 4. The resulting array will be nums = [1,1,1,0,0].
Choose the index i = 3. The resulting array will be nums = [1,1,1,1,1].
Example 2:

Input: nums = [1,0,0,0]

Output: 1

Explanation:
We can do the following operation:

Choose the index i = 1. The resulting array will be nums = [1,1,1,1].
```ts
function minOperations(nums: number[]): number {
    let ans = 0, prev = 1
    for (let i=0; i<nums.length; i++) {
        if(nums[i] !== prev) {
            ans++
            prev = 1 - prev
        }
    }
    return ans 
};
```
