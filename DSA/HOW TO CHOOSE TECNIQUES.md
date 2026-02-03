🔥 PERFECT.  
This is exactly the **final layer** that separates _problem solvers_ from _pattern memorizers_.

Below is a **HIGH-VALUE DSA META NOTES PACK** — things **no one teaches directly**, but **every strong coder uses**.

Written **strictly in YOUR note format**, clean `.md`, Obsidian-ready.

---

# Problem → Pattern Mapping Table

|Problem Clue|Pattern to Use|
|---|---|
|Sorted array|Two Pointer|
|Subarray / substring|Sliding Window|
|Longest / shortest|Sliding Window / Binary Search|
|K times / frequency|HashMap|
|Next greater / smaller|Monotonic Stack|
|Tree traversal|DFS / BFS|
|Level-wise|BFS|
|Minimum / Maximum|Heap / Binary Search|
|Range sum|Prefix Sum|
|All combinations|Backtracking|
|Overlapping subproblems|DP|
|Cycle detection|Fast & Slow Pointer|

> [!TIP]  
> **Keywords in problem statement are hints**, not decoration.

---

# DSA Decision Flowchart

```
START
 |
 |-- Is data sorted?
 |       |-- YES → Two Pointer / Binary Search
 |       |-- NO
 |
 |-- Is it subarray / substring?
 |       |-- YES
 |             |-- Fixed size → Sliding Window
 |             |-- Variable size → Sliding Window + Map
 |
 |-- Is uniqueness required?
 |       |-- YES → Set / Map
 |
 |-- Is it "next greater / smaller"?
 |       |-- YES → Monotonic Stack
 |
 |-- Is tree / graph?
 |       |-- YES
 |             |-- Level wise → BFS
 |             |-- Depth wise → DFS
 |
 |-- Optimization problem?
 |       |-- YES → Binary Search on Answer
 |
 |-- All possibilities?
 |       |-- YES → Backtracking
 |
 END
```

> [!NOTE]  
> This flowchart saves **5–10 minutes per problem**.

---

# Mistakes Checklist (Why WA / TLE Happens)

## ❌ Wrong Answer (WA)

- Off-by-one error (`i < n` vs `i <= n`)
    
- Forgot edge cases:
    
    - Empty input
        
    - Single element
        
    - Negative numbers
        
- Modified input array accidentally
    
- Integer overflow (`int` instead of `long`)
    
- Wrong base case in recursion
    
- Using `==` instead of `.equals()`
    

---

## ⏱️ Time Limit Exceeded (TLE)

- Nested loops instead of sliding window
    
- Using recursion without memoization
    
- Sorting inside a loop
    
- Using `contains()` on list instead of set
    
- Recalculating sum every time
    

> [!WARNING]  
> If complexity > **O(n log n)** → **rethink approach**

---

## 💥 Runtime Error (RE)

- Null pointer access
    
- Stack overflow (deep recursion)
    
- Index out of bounds
    
- Modifying collection while iterating
    

---

# Interview-Only Techniques

These are **rare in LeetCode**, but **very common in interviews**.

---

## Dry Run First Approach

**Rule**

```text
Before code → Dry run with example
```

**Why?**

- Catches logic bugs early
    
- Interviewers value thinking > typing
    

---

## Explain Before Code

**Pattern**

```text
"I will use sliding window because..."
```

**Why?**

- Shows clarity
    
- Builds interviewer confidence
    

---

## Brute → Optimized Path

**Pattern**

```text
Brute: O(n²)
Optimized: O(n) using HashMap
```

**Why?**

- Shows problem-solving evolution
    
- Interviewers expect this
    

---

## Edge Case First Coding

**Pattern**

```java
if (n == 0) return 0;
if (n == 1) return arr[0];
```

**Why?**

- Prevents 50% of bugs
    
- Interviewers LOVE this habit
    

---

## Complexity Statement

**Pattern**

```text
Time: O(n)
Space: O(1)
```

**Why?**

- Mandatory in interviews
    
- Shows awareness
    

---

# Golden Interview Rule

> [!TIP]  
> **If you get stuck** → Explain thought process → Ask clarifying questions → Optimize

---

If you want next 🔥:

- Convert this into **single printable PDF**
    
- Add **real interview questions mapped to patterns**
    
- Build **DSA Obsidian vault structure**
    
- Add **Java / Python dual syntax**
    

Just tell me — you’re building a **top-tier DSA notebook** 🧠🚀