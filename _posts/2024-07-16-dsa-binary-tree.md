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
#### <a href="https://leetcode.com/problems/binary-tree-preorder-traversal/" target="_blank">144. Binary Tree Preorder Traversal</a> 
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
        if (current.right) stack.push(current.right) // we push right node first so it can be poped later than left node  
        if (current.left) stack.push(current.left)
    }
    return ans 
};
```

#### <a href="https://leetcode.com/problems/binary-tree-inorder-traversal/" target="_blank">94. Binary Tree Inorder Traversal</a> 
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
function inorderTraversal(root: TreeNode | null): number[] {
    let stack = [], curr = root, ans = []
    while (curr || stack.length>0) {
        while (curr) {
            stack.push(curr)
            curr = curr.left
        }
        curr = stack.pop()
        ans.push(curr.val)
        curr = curr.right
    }
    return ans 
};
```

##### Use Cases
Typically, for **binary search tree**, we can retrieve all the data in sorted order using in-order traversal.  
#### <a href="https://leetcode.com/problems/binary-tree-postorder-traversal/" target="_blank">145. Binary Tree Postorder Traversal</a> 
Post-order traversal is to traverse the left subtree first. Then traverse the right subtree. Finally, visit the root. 
##### Solution 1: Recursion
```ts
function postorderTraversal(root: TreeNode | null): number[] {
    if (!root) return []
    let ans = []
    ans.push(...postorderTraversal(root.left))
    ans.push(...postorderTraversal(root.right))
    ans.push(root.val)
    return ans 
};
```

##### Solution 2: Stack
```ts
function postorderTraversal(root: TreeNode | null): number[] {
    if (!root) return []
    let stack = [root], ans = []
    while(stack.length>0) {
        const curr = stack.pop()
        if (curr.left) stack.push(curr.left) // notice: we push left node first, this is different than in order traversal
        if (curr.right) stack.push(curr.right)
        ans.push(curr.val)
    }
    return ans.reverse() 
};
```

##### Use Cases 
* When you delete nodes in a tree, deletion process will be in post-order.
* Post-order is widely used in mathematical expressions. You can easily handle the expression using a stack. Each time when you meet a operator, you can just pop 2 elements from the stack, calculate the result and push the result back into the stack.  

### BFS (Breadth-First Search)
#### <a href="https://leetcode.com/problems/binary-tree-level-order-traversal/" target="_blank">102. Binary Tree Level Order Traversal</a>
```ts
function levelOrder(root: TreeNode | null): number[][] {
    if (!root) return []
    let level = 0, queue = [root], ans = []
    while (queue.length>0) {
        ans[level] = []
        let newQueue = []
        for (const node of queue) {
            ans[level].push(node.val)
            if (node.left) newQueue.push(node.left)
            if (node.right) newQueue.push(node.right)
        }
        queue = newQueue
        level++
    }
    return ans 
};
```

## Other Common LeetCode Questions
#### <a href="https://leetcode.com/problems/same-tree/" target="_blank">100. Same Tree</a>
```ts
function isSameTree(p: TreeNode | null, q: TreeNode | null): boolean {
    if (p === null && q === null) return true
    if (p === null || q === null) return false 
    if (p.val !== q.val) return false
    // we don't check if p.val === q.val since if that check return true, there will be no check for left and right children. 
    return isSameTree(p.left, q.left) && isSameTree(p.right, q.right)
};
```

#### <a href="https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree" target="_blank">236. Lowest Common Ancestor of a Binary Tree</a>
```ts
function lowestCommonAncestor(root: TreeNode | null, p: TreeNode | null, q: TreeNode | null): TreeNode | null {
	if (root === null || root === p || root === q) {
        return root 
    }
    const left = lowestCommonAncestor(root.left, p, q)
    const right = lowestCommonAncestor(root.right, p, q)
    if (left && right) return root 
    if (left) return left
    return right 
};
```
