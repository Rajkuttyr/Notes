

---

# <font color="Red">Recursion</font>

**Syntax**

```java
void solve(params) {
    // 1. Base Case
    if (condition) return;

    // 2. Work / Logic
    // process current state

    // 3. Recursive Call
    solve(modifiedParams);
}
```

# Important Concepts

1. Function calls itself
    
2. Problem broken into smaller sub-problems
    
3. Must have **base case**
    
4. Uses **call stack**
    
5. Can lead to stack overflow if not controlled
    

---

## Types of Recursion

### 1. Tail Recursion

```java
void print(int n) {
    if (n == 0) return;
    System.out.println(n);
    print(n - 1);
}
```

### 2. Head Recursion

```java
void print(int n) {
    if (n == 0) return;
    print(n - 1);
    System.out.println(n);
}
```

---

# Important Steps to Write Recursion

1. Identify **base case**
    
2. Assume recursion works for smaller input
    
3. Modify input toward base case
    
4. Combine result (if required)
    

> [!TIP]  
> Always write **base case first**, then recursion

---

## Use Case

- Tree traversal
    
- Divide and conquer
    
- Backtracking
    
- DFS in graphs
    
- Mathematical problems
    

---

# Recursion Tree Understanding

**Example**

```java
f(3)
 ├── f(2)
 │    ├── f(1)
 │    │    └── f(0)
 │    └── f(1)
 └── f(2)
```

> [!NOTE]  
> Time complexity depends on **branching factor × depth**

---

# Common Recursion Problems

### Leetcode problem number and name to check

1. [[509. Fibonacci Number]]
    
2. [[206. Reverse Linked List]]
    
3. [[104. Maximum Depth of Binary Tree]]
    
4. [[78. Subsets]]
    
5. [[46. Permutations]]
    

---

# Common Mistakes

- Missing base case
    
- Wrong base condition
    
- Infinite recursion
    
- Modifying global variables incorrectly
    
- Forgetting to return value
    

> [!WARNING]  
> If recursion depth is large → convert to iteration

---

# Recursion vs Iteration

|Recursion|Iteration|
|---|---|
|Simple code|Faster|
|Uses stack|No extra stack|
|Risk of overflow|Safe for large input|

---

# How to Debug Recursion

1. Dry run with small input
    
2. Print parameters
    
3. Draw recursion tree
    
4. Check base case hit
    

---

# Golden Recursion Rule

> [!TIP]  
> **If you cannot explain the recursion in words, do not code it.**

---

If you want next:

- Backtracking notes (same format)
    
- DP vs Recursion comparison
    
- Recursion → Iteration conversion tricks
    
- Java recursion templates collection
    

Just say the word 🚀
hl
jjfff,k
jjj
jjjfofofkdkd