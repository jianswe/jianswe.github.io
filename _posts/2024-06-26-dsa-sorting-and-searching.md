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

### 349. Intersection of Two Arrays
```ts
function intersection(nums1: number[], nums2: number[]): number[] {
    // const nums1Set = new Set(nums1), nums2Set = new Set(nums2)
    // const interSet = nums1Set.intersection(nums2)
    // return [...interSet]
    
    nums1.sort((a,b)=>a-b)
    nums2.sort((a,b)=>a-b)
    let i=0, j=0, ans = []
    while (i<nums1.length && j<nums2.length) {
        if (nums1[i] === nums2[j]) {
            if (ans[ans.length-1] !==nums1[i]) {
                ans.push(nums1[i])
            } 
            i++
            j++
        } else if (nums1[i] > nums2[j]) {
            j++
        } else {
            i++
        }
    }
    return ans 
};
```
