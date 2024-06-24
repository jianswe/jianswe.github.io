# Algorithm: Backtracking 



## LeetCode 
### 39. Combination Sum
```ts 
function combinationSum(candidates: number[], target: number): number[][] {
    let ans = []
    
    function recursion(start: number, target: number, res: number[]) { // Time Complexity n 
        
        if (target < 0) return 
        if (target === 0) {
            ans.push(res)
            return 
        }
        for (let i = start; i < candidates.length; i++) { // Time Complexity n 
            res.push(candidates[i])
            recursion(i, target-candidates[i], [...res]) // Space Complexity n
            res.pop() // don't forget this step 
        }
    }
    
    recursion(0, target, [])
    
    return ans 
};
```
Time Complexity: O(n^2)
Space Complexity 
If we pass sliced candidates into recursion, O(2*n^2)
If we don't pass sliced candidates into recursion, just use start index, O(n^2) 
