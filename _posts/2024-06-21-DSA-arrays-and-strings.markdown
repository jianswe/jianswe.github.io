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
