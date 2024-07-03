# Data Structure: Stack and Queue
## Implement Queue using Two Stacks 
```js
class Queue {
    stack1 = []
    stack2 = []
    enqueue(num) {
        this.stack1.push(num)
    }
    dequeue() {
        if (this.stack2.length === 0) { // we don't need to push stack1 into stack2 until stack2 is empty
            while (this.stack1.length) {
                this.stack2.push(this.stack1.pop())
            }
        }
        return this.stack2.pop()
    }
    peek() {
        if (this.stack2.length === 0) {
            while (this.stack1.length) {
                this.stack2.push(this.stack1.pop())
            }
        }
        return this.stack2[this.stack2.length-1]
    }
}
```
