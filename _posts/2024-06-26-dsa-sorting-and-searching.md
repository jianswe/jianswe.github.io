# Algorithms: Sorting and Searching
## LeetCode 
### 56. Merge Intervals
https://leetcode.com/problems/merge-intervals
```ts
function merge(intervals: number[][]): number[][] {
    let ans = []
    intervals.sort((a, b) => a[0] - b[0])
    let start=intervals[0][0], end = intervals[0][1]
    for (const interval of intervals.slice(1)) {
        if(interval[0]<=end) {
            if (interval[1]>end) {
                end = interval[1]
            }
        } else {
            ans.push([start,end])
            start= interval[0]
            end = interval[1]
        }
    }
    ans.push([start,end])
    return ans 
};
```
