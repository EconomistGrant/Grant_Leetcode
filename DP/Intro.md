# Dynamic Programming
Definition:
dynamic programming (also known as dynamic optimization) is a method for solving a complex problem by breaking it down into a collection of simpler subproblems, solving each of those subproblems just once, and storing their solutions – ideally, using a memory-based data structure.

key feature of DP: solve each of the subproblem just once
basically by keeping a memo to read and update

# Fibonacci

## simple recursion
```python
def fib(n):
    if n == 0:
        return 0
    if n == 1:
        return 1
    return fib(n - 1) + fib(n - 2)
```

a lot of repeated computation of fib(i)

## keep a memo
```python
memo = None

def _fib(n):
    if memo[n] != -1:
        return memo[n]
    if n == 0:
        return 0
    if n == 1:
        return 1
    memo[n] = _fib(n - 1) + _fib(n - 2)
    return memo[n]

def fib(n):
    global memo
    memo = [-1] * (n + 1)
    return _fib(n)
```

## Dynamic Programming
```python
def fib(n):
    memo = [-1] * (n + 1)
    memo[0] = 0
    memo[1] = 1

    for i in range(2, n + 1):
        memo[i] = memo[i - 1] + memo[i - 2]
    return memo[n]
```

