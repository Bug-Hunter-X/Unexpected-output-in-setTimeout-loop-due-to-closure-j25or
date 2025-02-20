# JavaScript Closure Bug

This repository demonstrates a common JavaScript bug related to closures and the `setTimeout` function.  The code intends to log the numbers 0 through 9 with a one-second delay between each. However, due to how closures work, it produces unexpected results.  This example highlights the importance of understanding how variables are captured in JavaScript closures.

## Bug Description

The `myFunction` uses a `for` loop and `setTimeout`.  You might expect the output to be:

```
0
1
2
3
4
5
6
7
8
9
```

However, due to the asynchronous nature of `setTimeout` and how the loop variable `i` is captured, the output will be:

```
10
10
10
10
10
10
10
10
10
10
```

This happens because the callbacks created by `setTimeout` don't capture the value of `i` at the time they are created. Instead, they capture a reference to `i`. By the time the `setTimeout` callbacks finally execute, the loop has already completed, and `i` is equal to 10.

## Solution

The solution involves using a closure to capture the value of `i` at each iteration of the loop. This can be achieved by creating an immediately invoked function expression (IIFE):