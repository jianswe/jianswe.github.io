# Interview: Apple Leetcode FAQ
## Arrays and Strings 
### 1. Two Sum
https://leetcode.com/problems/two-sum
```ts
function twoSum(nums: number[], target: number): number[] {
    let targetMap = new Map() // key: target num, value: index of current num
    for (let i=0; i<nums.length; i++) {
        if(targetMap.has(nums[i])) {
            return [targetMap.get(nums[i]), i]
        }
        targetMap.set(target-nums[i], i)
    }
};
```

### 15. 3Sum
https://leetcode.com/problems/3sum
```ts
function threeSum(nums: number[]): number[][] {
    let ans = [], ansSet = new Set()
    nums.sort((a,b)=>a-b) // don't forget to implement num sort
    for (let i=0; i<nums.length; i++) {
        const target = 0 - nums[i]
        let j=i+1, k=nums.length-1
        while (j<k) {
            if(nums[j]+nums[k]===target) {
                if (!ansSet.has(nums[i]+","+nums[j]+","+nums[k])) {
                    ans.push([nums[i], nums[j], nums[k]])
                    ansSet.add(nums[i]+","+nums[j]+","+nums[k])
                }
                j++
                k--
            } else if (nums[j]+nums[k] < target) {
                j++
            } else {
                k--
            }
        }
    }
    return ans 
};
```

### 42. Trapping Rain Water
```ts
function trap(height: number[]): number {
    let stack = [[height[0], 0]], ans  = 0
    for (let i=1; i<height.length; i++) {
        let [bottomH, bottomInd] = stack[stack.length-1]
        if (height[i]<=bottomH) {
            stack.push([height[i], i])
        } else {
            while(stack.length>0 && height[i]>bottomH) {
                 [bottomH, bottomInd] = stack.pop()
                 if (stack.length>0) {
                     const [leftH, leftInd] = stack[stack.length-1]
                     const waterH = Math.min(leftH, height[i]) - bottomH
                     ans += waterH*(i-leftInd-1);
                     [bottomH, bottomInd] = stack[stack.length-1];
                 }
            }
            stack.push([height[i], i])
            
        }
        
    }
    return ans 
};
```
