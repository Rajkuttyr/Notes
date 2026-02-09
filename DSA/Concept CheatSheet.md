Got you. Since the test is **tomorrow**, this is a **last-day, recall-focused Obsidian notes pack** — **short, sharp, and exam-oriented**.
Think of this as **mental triggers**, not textbook theory.

I’ll give you:

1. 📓 **Obsidian-ready notes (copy–paste)**
2. 🧠 **Algorithm decision cues**
3. 🔥 **Hand-picked LeetCode for Level 2 & 3**

---

# 📓 OBSIDIAN NOTES (LAST-DAY REVISION)

---

## 🟢 LEVEL 1 — Core DSA (2 Questions)

### 📦 Arrays

```md
## Arrays
- Contiguous memory
- O(1) access
- Watch for overflow in sum (use long)

Patterns:
- Prefix Sum
- Sliding Window
- Two Pointers

Trick:
- Sorting → Two pointers
- Subarray sum → Prefix + HashMap
```

---

### 🔤 Strings

```md
## Strings
- Immutable (Java)
- Use StringBuilder for edits

Patterns:
- Frequency map (int[26])
- Sliding window for substrings
- Palindrome → two pointers
```

---

### 👉 Two Pointers

```md
## Two Pointers
Used when:
- Sorted array
- Pair / triplet problems

Types:
- Left & Right
- Fast & Slow (cycle detection)
```

---

### 🪟 Sliding Window

```md
## Sliding Window
Used for:
- Subarrays / substrings
- Max / min length

Template:
- Expand right
- Shrink left when invalid
```

---

### 🔍 Search / Sort

```md
## Search & Sort
Binary Search:
- Sorted data
- Mid = l + (r-l)/2

Sorting:
- Arrays.sort() → O(n log n)
- Useful before two pointers
```

---

### 📚 Stack

```md
## Stack
LIFO

Used in:
- Next Greater Element
- Valid Parentheses
- Monotonic Stack
```

---

### 🚶 Queue

```md
## Queue
FIFO

Used in:
- BFS
- Sliding window
```

---

### 🗂 HashMap

```md
## HashMap
Key → Value (O(1) avg)

Used in:
- Frequency count
- Prefix sum
- Index tracking
```

---

## 🟡 LEVEL 2 — Trees / Segment Tree / Trie (1 Question)

### 🌳 Binary Tree

```md
## Binary Tree
Traversals:
- Inorder → LNR
- Preorder → NLR
- Postorder → LRN
- Level Order → BFS

DFS → Recursion
BFS → Queue
```

---

### 📏 Segment Tree

```md
## Segment Tree
Used for:
- Range Query
- Update + Query both

Build → O(n)
Query → O(log n)

Common:
- Range Sum
- Range Min/Max
```

---

### 🔤 Trie

```md
## Trie
Used for:
- Prefix search
- Dictionary problems

Time:
- Insert/Search → O(length of word)

Node:
- children[26]
- isEnd
```

---

## 🔴 LEVEL 3 — Graphs (1 Question)

### 🌐 Graph Basics

```md
## Graph
Types:
- Directed
- Undirected

Representation:
- Adjacency List (preferred)
```

---

### 🚶 BFS

```md
## BFS
- Queue
- Shortest path (unweighted)
- Level order traversal
```

---

### 🧗 DFS

```md
## DFS
- Recursion / Stack
- Cycle detection
- Components
```

---

### 🔁 Cycle Detection

```md
## Cycle Detection
Undirected:
- DFS + parent check

Directed:
- DFS + recursion stack
```

---

### 📐 Topological Sort

```md
## Topological Sort
Used for:
- Dependency problems

Only for DAG

Algorithms:
- Kahn's (BFS + indegree)
- DFS stack
```

---

# 🧠 QUICK DECISION FLOW

```
Array + subarray? → Sliding Window
Pair sum? → HashMap / Two Pointers
Tree depth/path? → DFS
Shortest path? → BFS
Dependency order? → Topo Sort
Range query? → Segment Tree
Prefix words? → Trie
```

---

# 🔥 LEETCODE QUESTIONS (FOCUSED)

## 🟡 LEVEL 2 (Trees / Trie / Segment Tree)

1. **Binary Tree**

   * `104` Maximum Depth of Binary Tree
   * `226` Invert Binary Tree
   * `543` Diameter of Binary Tree
   * `199` Binary Tree Right Side View

2. **Trie**

   * `208` Implement Trie
   * `211` Design Add and Search Words

3. **Segment Tree**

   * `307` Range Sum Query – Mutable

---

## 🔴 LEVEL 3 (Graphs)

1. **BFS / DFS**

   * `200` Number of Islands
   * `695` Max Area of Island

2. **Cycle Detection**

   * `207` Course Schedule
   * `210` Course Schedule II

3. **Topological Sort**

   * `210` Course Schedule II
   * `269` Alien Dictionary

4. **Shortest Path**

   * `994` Rotting Oranges
   * `127` Word Ladder

---

# 🚀 NIGHT-BEFORE STRATEGY

✅ Revise **decision flow**
✅ Solve **1 tree + 1 graph** problem
✅ Don’t learn new patterns now
✅ Sleep (seriously)

If you want, I can give you:

* 🧠 **1-page printable cheat sheet**
* 💻 **Java one-file templates (Tree + Graph)**
* ⏱ **Mock test (4 questions, timed)**

Just tell me 👍
