# Algorithm: Dynamic Programming 
Dynamic Programming is a method of sovling a problem by dividing it into smaller problems.  
Usually, a problem where you need to solve by DP can only be solved by DP (in approved time complexity). If you don't know DP, it's probably impossbile to solve a DP problem, even an easy one. 

## Intro to Dynamic Programming 
### What is DP? 
1. The problem can be broken into "overlapping subproblems" - smaller versions of the original problem that are re-used multiple times.
2. The problem has an "optimal substructure" - an optimal solution can be formed from optimal solutions to the overlapping subproblems of the original problem. 

### When to Use DP
1. The problem will ask for the optimum value (maximum or minimum) of something, or the number of ways there are to do something.
2. Future "decisions" depend on earlier decisions. 

## Strategic Approach to DP 
### Framework for DP Problems
We define a recursive function, usually called `dp`, the return of the function is the answer to the original problem as if the arguments you passed to it were the input.  
The arguments the recursive funciton takes represent a **state**.  
When we look at tree traversal, for example, DFS, a node is never visited twice, which means the state is never repeated.   
But for DP, state can be revisited multiple times, so we need to cache the answer for a given state, this process is called **memoization**.  

Using DP to find the nth fibonacci number. 
```ts
/**
 * @param {number} n
 * @return {number}
 */
var fibonacci = function(n) {
    if (n == 0) {
        return 0;
    }
    
    if (n == 1) {
        return 1;
    }
    
    if (memo.has(n)) {
        return memo.get(n);
    }
    
    memo.set(n, fibonacci(n - 1) + fibonacci(n - 2));
    return memo.get(n);
}

let memo = new Map();
```
