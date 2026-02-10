Nice choice 😄
Here are **clean, exam-ready Dynamic Programming notes**, **structured perfectly for Obsidian** (Markdown, backlinks friendly, quick revision).

You can **copy-paste directly into Obsidian**.

---

# 🧠 Dynamic Programming (DP)

## 📌 What is Dynamic Programming?

Dynamic Programming is an optimization technique used to solve problems by:

* Breaking them into **overlapping subproblems**
* Solving each subproblem **once**
* Storing results to avoid recomputation

---

## 🔑 When to Use DP?

A problem can be solved using DP if it has:

1. **Optimal Substructure**
2. **Overlapping Subproblems**

---

## 🧩 Types of Dynamic Programming

### 1️⃣ Top-Down (Memoization)

* Recursive
* Uses cache (array / map)
* Easier to write

```java
int dp[] = new int[n+1];

int fib(int n) {
    if (n <= 1) return n;
    if (dp[n] != 0) return dp[n];
    return dp[n] = fib(n-1) + fib(n-2);
}
```

---

### 2️⃣ Bottom-Up (Tabulation)

* Iterative
* No recursion
* More efficient

```java
int fib(int n) {
    int dp[] = new int[n+1];
    dp[0] = 0;
    dp[1] = 1;
    for(int i = 2; i <= n; i++)
        dp[i] = dp[i-1] + dp[i-2];
    return dp[n];
}
```

---

## 🧠 DP Problem-Solving Steps (MUST MEMORIZE)

1. **Define the state**

   * `dp[i]` = answer till index `i`
2. **Write the recurrence**
3. **Identify base cases**
4. **Decide order of computation**
5. **Optimize space (if possible)**

---

## 🧮 Common DP Patterns

---

### 🔹 1. 1D DP (Linear DP)

#### Fibonacci

```
dp[i] = dp[i-1] + dp[i-2]
```

#### Climbing Stairs

```
dp[i] = dp[i-1] + dp[i-2]
```

---

### 🔹 2. 2D DP

#### Longest Common Subsequence (LCS)

```
dp[i][j] = LCS of s1[0..i-1], s2[0..j-1]
```

Recurrence:

```
if s1[i-1] == s2[j-1]:
    dp[i][j] = 1 + dp[i-1][j-1]
else:
    dp[i][j] = max(dp[i-1][j], dp[i][j-1])
```

---

### 🔹 3. Knapsack Pattern

#### 0/1 Knapsack

```
dp[i][w] = max(
    dp[i-1][w],
    val[i] + dp[i-1][w-wt[i]]
)
```

---

### 🔹 4. Unbounded Knapsack

* Coin Change
* Rod Cutting

```
dp[w] = min(dp[w], dp[w - coin] + 1)
```

---

### 🔹 5. DP on Grid

#### Unique Paths

```
dp[i][j] = dp[i-1][j] + dp[i][j-1]
```

---

### 🔹 6. DP on Subsequences

| Problem       | Key Idea                  |
| ------------- | ------------------------- |
| LIS           | `dp[i] = 1 + max(dp[j])`  |
| LCS           | 2D DP                     |
| Edit Distance | Replace / Insert / Delete |

---

### 🔹 7. DP on Trees

#### Tree DP Template

```java
int dfs(TreeNode root) {
    if(root == null) return 0;
    int left = dfs(root.left);
    int right = dfs(root.right);
    return Math.max(left, right) + 1;
}
```

---

## ⚡ Space Optimization Trick

If `dp[i]` depends only on last few states:

```java
prev2 = 0;
prev1 = 1;
for(int i = 2; i <= n; i++){
    curr = prev1 + prev2;
    prev2 = prev1;
    prev1 = curr;
}
```

---

## 🧠 Classic DP Problems (MUST PRACTICE)

* Fibonacci
* Climbing Stairs
* House Robber
* Coin Change
* Knapsack (0/1 & Unbounded)
* LIS
* LCS
* Edit Distance
* Matrix Chain Multiplication
* Subset Sum
* Palindromic Substrings

---

## 🎯 DP Interview One-Liners

* “DP is used when subproblems overlap.”
* “Memoization is top-down, tabulation is bottom-up.”
* “Define the state clearly before coding.”
* “Try space optimization if only previous states are needed.”

---

## 🧩 Obsidian Tips (Highly Recommended)

* Create backlinks like:

  * `[[Knapsack DP]]`
  * `[[LCS]]`
* Use tags:

  * `#dp`
  * `#patterns`
* One problem = one note
* Add **recurrence + code + dry run**

---

If you want next:

* 🔥 **DP Patterns cheat sheet**
* 🔥 **DP vs Greedy**
* 🔥 **LeetCode DP roadmap**
* 🔥 **Visual DP explanations**

Just say 😄
Perfect 😄
Here’s the **full DP master pack**, written **cleanly in Obsidian-friendly Markdown**, exactly how toppers maintain their notes.

You can split these into **4 separate notes** or keep them in one vault section.

---

# 🔥 DP PATTERNS – CHEAT SHEET

## 🧠 1️⃣ Linear / 1D DP

**State depends on previous indices**

### Pattern

```
dp[i] = f(dp[i-1], dp[i-2], ...)
```

### Problems

* Fibonacci
* Climbing Stairs
* House Robber
* Decode Ways

---

## 🧠 2️⃣ 2D DP (Strings / Sequences)

### Pattern

```
dp[i][j] = answer using first i chars of s1 and j chars of s2
```

### Problems

* LCS
* Edit Distance
* Longest Palindromic Subsequence

---

## 🧠 3️⃣ Knapsack Pattern

### 0/1 Knapsack

```
dp[i][w] = max(
  dp[i-1][w],
  val[i] + dp[i-1][w-wt[i]]
)
```

### Unbounded Knapsack

```
dp[w] = max(dp[w], dp[w-wt[i]] + val[i])
```

### Problems

* Subset Sum
* Coin Change
* Rod Cutting

---

## 🧠 4️⃣ LIS Pattern (Pick / Not Pick)

```
dp[i] = max(dp[j] + 1) where j < i and arr[j] < arr[i]
```

### Problems

* LIS
* Russian Doll Envelopes

---

## 🧠 5️⃣ Grid DP

```
dp[i][j] = dp[i-1][j] + dp[i][j-1]
```

### Problems

* Unique Paths
* Minimum Path Sum
* Dungeon Game

---

## 🧠 6️⃣ Interval DP

```
dp[i][j] = min/max over k between i and j
```

### Problems

* Matrix Chain Multiplication
* Burst Balloons
* Palindrome Partitioning

---

## 🧠 7️⃣ Tree DP

```
solve(node) = combine(solve(left), solve(right))
```

### Problems

* Diameter of Tree
* House Robber III
* Binary Tree Maximum Path Sum

---

## 🧠 8️⃣ Bitmask DP

```
dp[mask] = answer for chosen set
```

### Problems

* Traveling Salesman
* Assignment Problem

---

# 🔥 DP vs GREEDY (VERY IMPORTANT)

| Feature              | DP       | Greedy             |
| -------------------- | -------- | ------------------ |
| Future consideration | ✅ Yes    | ❌ No               |
| Local optimum        | ❌        | ✅                  |
| Guarantees optimal   | ✅        | ❌                  |
| Complexity           | Higher   | Lower              |
| Example              | Knapsack | Activity Selection |

### Key Rule

> If a greedy choice always leads to optimal → use Greedy
> Otherwise → use DP

---

# 🔥 LEETCODE DP ROADMAP (STEP-BY-STEP)

## 🟢 Beginner (MUST DO)

* Fibonacci (509)
* Climbing Stairs (70)
* House Robber (198)
* Maximum Subarray (53)

---

## 🟡 Intermediate

* Coin Change (322)
* LIS (300)
* LCS (1143)
* Unique Paths (62)
* Minimum Path Sum (64)

---

## 🔴 Advanced

* Edit Distance (72)
* Matrix Chain Multiplication
* Burst Balloons (312)
* Palindrome Partitioning II (132)
* Word Break (139)

---

## 🔥 HARDCORE DP

* DP with Bitmask
* DP on Trees
* Digit DP
* State Compression DP

---

# 🔥 VISUAL DP EXPLANATIONS (MENTAL MODELS)

## 🎯 Fibonacci (State Flow)

```
f(5)
 ├── f(4)
 │    ├── f(3)
 │    └── f(2)
 └── f(3)
```

→ overlapping subproblems ⇒ DP

---

## 🎯 Knapsack (Choice Tree)

```
Item i:
 ├── take → capacity - wt[i]
 └── skip → capacity unchanged
```

---

## 🎯 Grid DP

```
Start → → →
  ↓
  ↓
```

Each cell = ways from top + left

---

## 🎯 LIS Visualization

```
Index:  0  1  2  3
Array: 10  9  2  5
dp:     1  1  1  2
```

---

# 🧠 DP PROBLEM SOLVING TEMPLATE (SAVE THIS)

```text
1. Define dp state
2. Write recurrence
3. Identify base case
4. Decide iteration order
5. Optimize space
```

---

# 🏷️ OBSIDIAN TAGGING SUGGESTION

```text
#dp
#patterns
#leetcode
#dynamic-programming
```

Backlinks:

* `[[Knapsack DP]]`
* `[[LCS]]`
* `[[Tree DP]]`

---

## 🎯 Final Tip (EXAM + INTERVIEW GOLD)

> If you cannot explain your dp state in one sentence, you don’t understand the DP yet.

---

If you want next 🔥

* **Digit DP notes**
* **DP dry-run tricks**
* **DP → recursion conversion**
* **Company-wise DP questions**

Just say 🚀
#dp
#leetcode 
#algorithm