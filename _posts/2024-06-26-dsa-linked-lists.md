# Data Structure: Linked List
## LeetCode 
### 2. Add Two Numbers
https://leetcode.com/problems/add-two-numbers
```ts
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     val: number
 *     next: ListNode | null
 *     constructor(val?: number, next?: ListNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.next = (next===undefined ? null : next)
 *     }
 * }
 */

function addTwoNumbers(l1: ListNode | null, l2: ListNode | null): ListNode | null {
    let plusOne = 0
    let ans = new ListNode()
    let c1 = l1, c2 = l2, c3 = ans
    while(c1 || c2) {
        const c1Val = c1? c1.val : 0
        const c2Val = c2? c2.val : 0
        const tempSum = c1Val + c2Val + plusOne
        if(tempSum>9) {
            c3.val = tempSum - 10
            plusOne = 1
        } else {
            c3.val = tempSum
            plusOne = 0
        }
        
        if (c1) c1 = c1.next
        if (c2) c2 = c2.next
        if (c1||c2||plusOne) {
            c3.next = new ListNode()
            c3 = c3.next
        }
    }
    if(plusOne) {
        c3.val = 1
    } 
    return ans 
};
```

### 21. Merge Two Sorted Lists
https://leetcode.com/problems/merge-two-sorted-lists/
```ts
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     val: number
 *     next: ListNode | null
 *     constructor(val?: number, next?: ListNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.next = (next===undefined ? null : next)
 *     }
 * }
 */

function mergeTwoLists(list1: ListNode | null, list2: ListNode | null): ListNode | null {
    if (!list1 && !list2) return null
    let ans = new ListNode()
    let node1=list1, node2=list2, node3=ans
    while(node1 && node2) {
        if(node1.val<node2.val) {
            node3.val = node1.val
            node1 = node1.next
        } else {
            node3.val = node2.val
            node2 = node2.next
        }
        if (node1 || node2) {
            node3.next = new ListNode()
            node3 = node3.next
        }   
    }
    while(node1) {
        node3.val = node1.val
        node1 = node1.next
        if (node1) {
            node3.next = new ListNode()
            node3 = node3.next
        }
    }
    while(node2) {
        node3.val = node2.val
        node2 = node2.next
        if (node2) {
            node3.next = new ListNode()
            node3 = node3.next
        }
    }
    return ans 
};
```
