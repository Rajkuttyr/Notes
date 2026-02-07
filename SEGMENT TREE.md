# Segment Tree

## Definition

A **Segment Tree** is a **binary tree–based data structure** used to efficiently handle:

- **Range Queries**
    
- **Point Updates / Range Updates**
    

on an array.

---

## Why Segment Tree?

|Operation|Array|Segment Tree|
|---|---|---|
|Range Query|O(n)|**O(log n)**|
|Update|O(1)|**O(log n)**|

---

# Segment Tree Structure

- Each node represents a **segment [l, r]**
    
- Root → entire array
    
- Leaves → single elements
    

---

## Size of Segment Tree

> [!NOTE]  
> Maximum size = **4 × n**

---

# Segment Tree Node Representation

**Syntax**

```java
int[] seg = new int[4 * n];
```

---

# Build Segment Tree

**Syntax**

```java
void build(int idx, int l, int r, int[] arr) {
    if (l == r) {
        seg[idx] = arr[l];
        return;
    }

    int mid = (l + r) / 2;
    build(2 * idx + 1, l, mid, arr);
    build(2 * idx + 2, mid + 1, r, arr);

    seg[idx] = seg[2 * idx + 1] + seg[2 * idx + 2];
}
```

# Important Ideas

1. Divide array into halves
    
2. Combine children
    
3. Build time: **O(n)**
    

---

# Range Query (Sum)

**Syntax**

```java
int query(int idx, int l, int r, int ql, int qr) {
    // No overlap
    if (r < ql || l > qr) return 0;

    // Complete overlap
    if (l >= ql && r <= qr) return seg[idx];

    // Partial overlap
    int mid = (l + r) / 2;
    return query(2 * idx + 1, l, mid, ql, qr)
         + query(2 * idx + 2, mid + 1, r, ql, qr);
}
```

# Important Ideas

1. Three overlap cases
    
2. Avoid unnecessary recursion
    
3. Time: **O(log n)**
    

---

# Point Update

**Syntax**

```java
void update(int idx, int l, int r, int pos, int val) {
    if (l == r) {
        seg[idx] = val;
        return;
    }

    int mid = (l + r) / 2;
    if (pos <= mid)
        update(2 * idx + 1, l, mid, pos, val);
    else
        update(2 * idx + 2, mid + 1, r, pos, val);

    seg[idx] = seg[2 * idx + 1] + seg[2 * idx + 2];
}
```

---

# Segment Tree for Min / Max

## Min Segment Tree

```java
seg[idx] = Math.min(left, right);
```

## Max Segment Tree

```java
seg[idx] = Math.max(left, right);
```

> [!TIP]  
> Only **merge logic changes**, structure stays same.

---

# Lazy Propagation (IMPORTANT)

## Why Lazy?

- Range update without updating all nodes
    
- Delay updates until needed
    

---

## Lazy Array

```java
int[] lazy = new int[4 * n];
```

---

## Range Update (Lazy)

**Syntax**

```java
void updateRange(int idx, int l, int r, int ql, int qr, int val) {
    if (lazy[idx] != 0) {
        seg[idx] += (r - l + 1) * lazy[idx];
        if (l != r) {
            lazy[2 * idx + 1] += lazy[idx];
            lazy[2 * idx + 2] += lazy[idx];
        }
        lazy[idx] = 0;
    }

    if (r < ql || l > qr) return;

    if (l >= ql && r <= qr) {
        seg[idx] += (r - l + 1) * val;
        if (l != r) {
            lazy[2 * idx + 1] += val;
            lazy[2 * idx + 2] += val;
        }
        return;
    }

    int mid = (l + r) / 2;
    updateRange(2 * idx + 1, l, mid, ql, qr, val);
    updateRange(2 * idx + 2, mid + 1, r, ql, qr, val);

    seg[idx] = seg[2 * idx + 1] + seg[2 * idx + 2];
}
```

---

# Lazy Range Query

**Syntax**

```java
int queryLazy(int idx, int l, int r, int ql, int qr) {
    if (lazy[idx] != 0) {
        seg[idx] += (r - l + 1) * lazy[idx];
        if (l != r) {
            lazy[2 * idx + 1] += lazy[idx];
            lazy[2 * idx + 2] += lazy[idx];
        }
        lazy[idx] = 0;
    }

    if (r < ql || l > qr) return 0;

    if (l >= ql && r <= qr) return seg[idx];

    int mid = (l + r) / 2;
    return queryLazy(2 * idx + 1, l, mid, ql, qr)
         + queryLazy(2 * idx + 2, mid + 1, r, ql, qr);
}
```

---

# When to Use Segment Tree

## Use Case

- Multiple range queries
    
- Dynamic updates
    
- Competitive programming
    

---

# Common Segment Tree Problems

### Leetcode / CP

1. [[307. Range Sum Query – Mutable]]
    
2. [[729. My Calendar I]]
    
3. [[715. Range Module]]
    
4. [[315. Count of Smaller Numbers After Self]] (advanced)
    

---

# Segment Tree vs Fenwick Tree

|Feature|Segment Tree|Fenwick Tree|
|---|---|---|
|Range Query|Yes|Yes|
|Range Update|Yes (Lazy)|No|
|Implementation|Complex|Simple|
|Power|High|Medium|

---

# Golden Segment Tree Rules

> [!TIP]  
> 1️⃣ Always think in **segments**  
> 2️⃣ Master overlap cases  
> 3️⃣ Lazy propagation is mandatory for range updates

---

## ✅ If you master THIS:

- You can solve **almost all CP range problems**
    
- Hard LeetCode becomes approachable
    
- Range update/query becomes intuitive
    

---

If you want next:

- Fenwick Tree (BIT) notes
    
- Persistent Segment Tree
    
- Segment Tree templates (copy-paste)
    
- CP problem list for Segment Tree
    

Just tell me 👊