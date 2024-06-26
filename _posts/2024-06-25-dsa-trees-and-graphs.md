# Data Structure: Trees and Graphs

## Binary Trees
Like a linked list, a **tree** is a type of graph. Also like a linked list, there are multiple types of trees. We will be focusing on **binary trees**.   
Just like with a linked list, binary trees are implemented using objects of a custom class. This is the typical class definition that will be provided to you in algorithm problems: 
```js
class TreeNode {
    constructor(val) {
        this.val = val;
        this.left = null;
        this.right = null;
    }
}
```

### 100. Same Tree 
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

## Graphs
A **graph** is any collection of nodes and their pointers to other nodes. In fact, linked lists and trees are both types of graphs. 

### 133. Clone Graph
```ts
/**
 * Definition for _Node.
 * class _Node {
 *     val: number
 *     neighbors: _Node[]
 * 
 *     constructor(val?: number, neighbors?: _Node[]) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.neighbors = (neighbors===undefined ? [] : neighbors)
 *     }
 * }
 * 
 */


function cloneGraph(node: _Node | null): _Node | null {
    if (!node) return null 
    let res = new _Node(node.val)
    let queue = [node] 
    let seen = new Map([
        [node.val, res]
    ])
    while(queue.length) {
        const currNode = queue.shift()
        // console.log(currNode.val)
        const copyNode = seen.get(currNode.val)
        for (const neighbor of currNode.neighbors) {
            // Don't add already seen nodes, otherwise it will be infinite loop 
            if (!seen.has(neighbor.val)) {
                const newNode = new _Node(neighbor.val)
                queue.push(neighbor)
                seen.set(neighbor.val, newNode)
            }
            // this should not be inside of if, because it is possible the neighbors of current node is already seen 
            // adding it to if will result in partial copied graph 
            copyNode.neighbors.push(seen.get(neighbor.val))  
        }
    }
    
	return res
};
```
