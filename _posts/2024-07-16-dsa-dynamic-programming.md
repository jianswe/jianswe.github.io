# Algorithm: Dynamic Programming 
Dynamic Programming is a method of sovling a problem by dividing it into smaller problems.  
Usually, a problem where you need to solve by DP can only be solved by DP (in approved time complexity). If you don't know DP, it's probably impossbile to solve a DP problem, even an easy one. 

## Intro to Dynamic Programming 
### What is DP? 
1. The problem can be broken into "overlapping subproblems" - smaller versions of the original problem that are re-used multiple times.
2. The problem has an "optimal substructure" - an optimal solution can be formed from optimal solutions to the overlapping subproblems of the original problem.

### Concepts 
We define a recursive function, usually called `dp`, the return of the function is the answer to the original problem as if the arguments you passed to it were the input.  
**State**: The arguments that a recursive function takes represents a state. When we look at tree traversal, for example, DFS, a node is never visited twice, which means the state is never repeated.  
**Memoization**: But for DP, state can be revisited multiple times, so we need to cache the answer for a given state, this process is called memoization. 

### When to Use DP
1. The problem will ask for the optimum value (maximum or minimum) of something, or the number of ways there are to do something.
2. Future "decisions" depend on earlier decisions.

## Strategic Approach to DP 
### Framework for DP Problems
For this article, we're going to use [Coin Change](https://leetcode.com/problems/coin-change) as an example. We will start with a top-down solution.  
> You are given an integer array coins representing coins of different denominations and an integer amount representing a total amount of money.  
Return the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1.  
You may assume that you have an infinite number of each kind of coin.

To create any DP algorithm, there are 3 main components.   
1. **A function or data structure that will compute/contain the answer to the problem for any given state.**  
Since we're starting with top-down, we will be talking about a function here.
Let's define a function `dp(state)` that
* returns the minimum number of coins for a given state.
* The state would be the the amount of money (s).   

2. **A recurrence relation to transition between states.**  
`dp(s) = min(dp(s-c[i]))+1`, `c[i]` is the i's coin. 

3. **Base cases**, so that our recurrence relation doesn't go on infinitely.  
`dp(s)=-1, if s<0`
`dp(0)=0`

#### Implementation
```ts
function coinChange(coins: number[], amount: number): number {
    let memo = new Array(amount+1).fill(0)

    function dp(rem: number): number {
        
        if (rem<0) return -1
        if (rem===0) return 0
        if (memo[rem] !== 0) return memo[rem] 
        let min = Infinity
        for (const coin of coins) {
            const res = dp(rem-coin)
            if (res>=0 && res<min) min = 1 + res
        }
        memo[rem] = (min === Infinity) ? -1 : min
        return memo[rem]
    }

    return dp(amount)
};
```

#### Covert top-down solution to bottom-up
```ts
function coinChange(coins: number[], amount: number): number {
    let memo = new Array(amount+1).fill(0)
    for (let i=1; i<=amount; i++) {
        let min = Infinity
        for (const coin of coins) {
            if (i-coin>=0 && memo[i-coin] !==-1 && memo[i-coin]<min) {
                min = 1 + memo[i-coin]
            } 
        }
        memo[i] = (min === Infinity) ? -1 : min
    }
    return memo[amount]
};
```
