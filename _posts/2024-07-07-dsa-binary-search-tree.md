# Data Structure: Binary Search Tree 
## Introduction to BST
A **Binary Search Tree** is a special form of a binary tree. 
1. The value in each node must be *greater than* (or equal to) any values in its *left subtree*
2. The value in each node must be *less than* (or equal to) any values in its *right subtree*.

### 285. Inorder Successor in BST
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

function inorderSuccessor(root: TreeNode | null, p: TreeNode | null): TreeNode | null {
    let curr, parent 
    // if p has right child, then the right left most child will be p's successor 
	if (p.right) {
        curr = p.right
        while (curr.left) {
            curr = curr.left
        }
        return curr
    }
    
    // if p doesn't have right child, then p's parent could be p's successor 
    // but p has to be the parent's left child 
    // or p's parent is p's grandparent's left child, ... 
    curr = root
    let ans 
    while (curr) {
        if (curr.val === p.val) {
            return ans 
        } else if (curr.val < p.val) {
            parent = curr
            curr = curr.right
        } else {
            parent = curr 
            ans = curr
            curr = curr.left
        }
    }
    return null 
};
```


## Basic Operations in BST 
### 700. Search in a Binary Search Tree
```ts
function searchBST(root: TreeNode | null, val: number): TreeNode | null {
    let cur = root
    while(cur) {
        if (cur.val === val) {
            return cur 
        } else if (cur.val < val) {
            cur = cur.right
        } else {
            cur = cur.left
        }
    }
    return null
};
```

### 701. Insert into a Binary Search Tree
```ts
function insertIntoBST(root: TreeNode | null, val: number): TreeNode | null {
    if (!root) return new TreeNode(val)
    let cur = root
    while(cur) {
        if (cur.val < val) {
            if (cur.right) {
                cur = cur.right
            } else {
                cur.right = new TreeNode(val)
                break
            }
        } else {
            if (cur.left) {
                cur = cur.left
            } else {
                cur.left = new TreeNode(val)
                break
            }
        }
    }
    return root
};
```

### 450. Delete Node in a BST
```ts
function deleteNode(root: TreeNode | null, key: number): TreeNode | null {
    let curr = root, parent 
    while (curr) {
        if (curr.val === key) {
            break 
        } else if (curr.val < key) {
            parent = curr 
            curr = curr.right
        } else {
            parent = curr 
            curr = curr.left 
        }
    }
    if (!curr) return root // no node with val === key 
    if (!parent) { // root has val === key
        if (!curr.left && !curr.right) {
            return null
        } else if (!curr.left) {
            return curr.right
        } else if (!curr.right) {
            return curr.left
        } else {
            let rightLeft = curr.right, rightLeftParent
            while (rightLeft.left) {
                rightLeftParent = rightLeft
                rightLeft = rightLeft.left
            }
            curr.val = rightLeft.val 
            if (rightLeftParent) rightLeftParent.left = rightLeft.right
            else curr.right = rightLeft.right 
            return root 
        }
    }
    if (!curr.left && !curr.right) {
        if (parent.val < curr.val) {
            parent.right = null 
        } else {
            parent.left = null 
        }
    } else if (!curr.left) {
        if (parent.val < curr.val) {
            parent.right = curr.right
        } else {
            parent.left = curr.right
        }
    } else if (!curr.right) {
        if (parent.val < curr.val) {
            parent.right = curr.left
        } else {
            parent.left = curr.left
        }
    } else {
        let rightLeft = curr.right, rightLeftParent
        while (rightLeft.left) {
            rightLeftParent = rightLeft
            rightLeft = rightLeft.left
        }
        curr.val = rightLeft.val 
        if (rightLeftParent) rightLeftParent.left = rightLeft.right
        else curr.right = rightLeft.right  
    }
    return root 
};
```
