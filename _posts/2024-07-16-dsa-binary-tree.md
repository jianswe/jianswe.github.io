# Data Structure: Binary Tree

## Overview 
Like a linked list, a **tree** is a type of graph. Also like a linked list, there are multiple types of trees. We will be focusing on **binary trees**.   
Just like with a linked list, binary trees are implemented using objects of a custom class. This is the typical class definition that will be provided to you in algorithm problems: 
```ts
class TreeNode {
    val: number
    left: TreeNode | null
    right: TreeNode | null
    constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
        this.val = (val===undefined ? 0 : val)
        this.left = (left===undefined ? null : left)
        this.right = (right===undefined ? null : right)
    }
}
```

## Traversal 
### DFS (Depth-First Search)   
#### 144. Binary Tree Preorder Traversal 
Pre-order traversal is to visit the root frist. Then traverse the left subtree. Finally, traverse the right subtree. 
##### Solution 1: Recursion
```ts
function preorderTraversal(root: TreeNode | null): number[] {
    if (!root) return []
    let ans = [root.val]
    ans.push(...preorderTraversal(root.left))
    ans.push(...preorderTraversal(root.right))
    return ans 
};
```

##### Solution 2: Stack
```ts
function preorderTraversal(root: TreeNode | null): number[] {
    let stack = [root], ans = []
    while (stack.length>0) {
        const current = stack.pop()
        if (!current) continue 
        ans.push(current.val)
        if (current.right) stack.push(current.right)
        if (current.left) stack.push(current.left)
    }
    return ans 
};
```

#### 94. Binary Tree Inorder Traversal 
In-order traversal is to traverse the left subtree first. Then visit the root. Finally, traverse the right subtree. 
##### Solution 1: Recursion 
```ts
function inorderTraversal(root: TreeNode | null): number[] {
    if (!root) return []
    let ans = []
    ans.push(...inorderTraversal(root.left))
    ans.push(root.val)
    ans.push(...inorderTraversal(root.right))
    return ans 
};
```

##### Solution 2: Stack 
```ts

```

##### Use Cases
Typically, for **binary search tree**, we can retrieve all the data in sorted order using in-order traversal.  
#### Post-order Traversal 
Post-order traversal is to traverse the left subtree first. Then traverse the right subtree. Finally, visit the root. 
##### Use Cases 
* When you delete nodes in a tree, deletion process will be in post-order.
* Post-order is widely used in mathematical expressions. You can easily handle the expression using a stack. Each time when you meet a operator, you can just pop 2 elements from the stack, calculate the result and push the result back into the stack.  

### BFS (Breadth-First Search)

### [100. Same Tree](https://leetcode.com/problems/same-tree) 
```ts
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     val: number
 *     left: TreeNode | null
 *     right: TreeNode | null
 *     constructor(val?: number, left?: TreeNode | null, right?: TreeNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.left = (left===undefined ? null : left)
 *         this.right = (right===undefined ? null : right)
 *     }
 * }
 */

function isSameTree(p: TreeNode | null, q: TreeNode | null): boolean {
    if (p === null && q === null) return true
    if (p === null || q === null) return false 
    if (p.val !== q.val) return false
    // we don't check if p.val === q.val since if that check return true, there will be no check for left and right children. 
    return isSameTree(p.left, q.left) && isSameTree(p.right, q.right)
};
```
