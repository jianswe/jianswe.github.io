# Data Structure: Binary Search Tree 
A **Binary Search Tree** is a special form of a binary tree. 
1. The value in each node must be *greater than* (or equal to) any values in its *left subtree*
2. The value in each node must be *less than* (or equal to) any values in its *right subtree*. 

## Basic Operations in BST 
### 700. Search in a Binary Search Tree
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
