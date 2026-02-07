# 🌳 Segment Tree – Range Maximum Query (RMQ)

## 🧠 Concept

A **Segment Tree** is a binary tree (stored using an array) that allows answering range queries efficiently.

For **RMQ (Range Maximum Query)**, each node stores the **maximum value** of a subarray.

---

## 📌 Problem Statement

Given an array `arr[]` of size `n`, answer multiple queries of the form:

> What is the **maximum element** in the range `[L, R]`?

---

## 🏗️ Data Structure Used

- Array-based Segment Tree
    
- Tree stored in an array `seg[]`
    

### Index Mapping

- Root → `seg[0]`
    
- Left child of index `i` → `2*i + 1`
    
- Right child of index `i` → `2*i + 2`
    

---

## 🧮 Space Allocation

```text
seg[] size = 4 * n
```

Reason: Safe upper bound to store the full segment tree.

---

## 🚀 Algorithm: Build Segment Tree

### Step 1: Read Input

- Let input array be `arr[]`
    
- Let `n = arr.length`
    

---

### Step 2: Create Segment Tree Array

- Create an integer array `seg[]` of size `4 * n`
    
- `seg[0]` will store the maximum of the entire array
    

---

### Step 3: Build Tree Recursively

#### Build Function Parameters

- `idx` → current index in `seg[]`
    
- `low` → start index of range
    
- `high` → end index of range
    

---

#### Step 3.1: Base Case (Leaf Node)

- If `low == high`
    
    - Store `arr[low]` in `seg[idx]`
        
    - Return
        

---

#### Step 3.2: Recursive Case (Internal Node)

- Compute `mid = (low + high) / 2`
    
- Recursively build left subtree:
    
    - `build(2*idx + 1, low, mid)`
        
- Recursively build right subtree:
    
    - `build(2*idx + 2, mid + 1, high)`
        
- Store the maximum of both children:
    
    - `seg[idx] = max(seg[left], seg[right])`
        

---

## 🔍 Algorithm: Range Maximum Query (RMQ)

### Query Function Parameters

- `idx` → current index in `seg[]`
    
- `low, high` → range covered by current node
    
- `l, r` → query range
    

---

### Step 4.1: No Overlap Case

- If `high < l` OR `low > r`
    
    - Return `-∞` (identity value for maximum)
        

---

### Step 4.2: Complete Overlap Case

- If `[low, high]` lies completely inside `[l, r]`
    
    - Return `seg[idx]`
        

---

### Step 4.3: Partial Overlap Case

- Compute `mid = (low + high) / 2`
    
- Query left subtree
    
- Query right subtree
    
- Return `max(leftResult, rightResult)`
    

---

## 🧾 Output

- The value returned by the query function is the **maximum element in the range `[l, r]`**
    

---

## ⏱️ Complexity Analysis

|Operation|Time Complexity|
|---|---|
|Build Segment Tree|O(n)|
|Range Query|O(log n)|
|Space Used|O(4n)|

---

## 🧠 Key Observations

- Segment Tree divides the array recursively
    
- Each node stores precomputed information
    
- Only relevant branches are visited during query
    

---

## 🎯 Interview One-Liner

> "Segment Tree stores range maximums in a tree-like array structure and answers RMQ using overlap logic in logarithmic time."

---

## 🔗 Tags

#segment-tree #rmq #data-structures #leetcode #competitive-programming