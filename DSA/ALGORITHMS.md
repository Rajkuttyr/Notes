

---

# Binary Search

**Syntax**

```java
int l = 0, r = n - 1;

while (l <= r) {
    int mid = l + (r - l) / 2;
    if (arr[mid] == target) return mid;
    else if (arr[mid] < target) l = mid + 1;
    else r = mid - 1;
}
```

# Important Ideas

1. Works on sorted data
    
2. Reduces search space by half
    
3. O(log n) time
    

## Use Case

- Search problems
    
- Lower/upper bound
    
- Binary search on answer
    

### Leetcode problem number and name to check

1. [[704. Binary Search]]
    
2. [[35. Search Insert Position]]
    

---

# Merge Sort

**Syntax**

```java
void mergeSort(int[] arr, int l, int r) {
    if (l >= r) return;
    int mid = (l + r) / 2;
    mergeSort(arr, l, mid);
    mergeSort(arr, mid + 1, r);
    merge(arr, l, mid, r);
}
```

# Important Ideas

1. Divide and conquer
    
2. Stable sort
    
3. O(n log n)
    

## Use Case

- Sorting large data
    
- Linked list sorting
    
- Inversion count
    

### Leetcode

1. [[912. Sort an Array]]
    
2. [[148. Sort List]]
    

---

# Quick Sort

**Syntax**

```java
int partition(int[] arr, int l, int r) {
    int pivot = arr[r];
    int i = l - 1;
    for (int j = l; j < r; j++) {
        if (arr[j] < pivot) {
            i++;
            swap(arr, i, j);
        }
    }
    swap(arr, i + 1, r);
    return i + 1;
}
```

# Important Ideas

1. In-place sorting
    
2. Average O(n log n)
    
3. Worst O(n²)
    

## Use Case

- Fast sorting
    
- Competitive programming
    

---

# Breadth First Search (BFS)

**Syntax**

```java
Queue<Integer> q = new LinkedList<>();
q.offer(start);
visited[start] = true;

while (!q.isEmpty()) {
    int node = q.poll();
    for (int nei : adj[node]) {
        if (!visited[nei]) {
            visited[nei] = true;
            q.offer(nei);
        }
    }
}
```

# Important Ideas

1. Level-wise traversal
    
2. Shortest path (unweighted)
    
3. Uses queue
    

## Use Case

- Tree level order
    
- Graph shortest path
    

### Leetcode

1. [[102. Binary Tree Level Order Traversal]]
    
2. [[994. Rotting Oranges]]
    

---

# Depth First Search (DFS)

**Syntax**

```java
void dfs(int node) {
    visited[node] = true;
    for (int nei : adj[node]) {
        if (!visited[nei]) dfs(nei);
    }
}
```

# Important Ideas

1. Depth traversal
    
2. Recursion / stack
    
3. Backtracking base
    

## Use Case

- Connected components
    
- Cycle detection
    
- Tree traversal
    

---

# Dijkstra’s Algorithm

**Syntax**

```java
PriorityQueue<int[]> pq = new PriorityQueue<>(
    (a,b) -> a[1] - b[1]
);
pq.offer(new int[]{src, 0});
```

# Important Ideas

1. Shortest path (weighted)
    
2. Greedy + heap
    
3. No negative weights
    

## Use Case

- Navigation problems
    
- Weighted graphs
    

### Leetcode

1. [[743. Network Delay Time]]
    
2. [[1631. Path With Minimum Effort]]
    

---

# Union Find (Disjoint Set)

**Syntax**

```java
int find(int x) {
    if (parent[x] != x)
        parent[x] = find(parent[x]);
    return parent[x];
}
```

# Important Ideas

1. Path compression
    
2. Union by rank
    
3. Almost O(1)
    

## Use Case

- Connected components
    
- Cycle detection
    
- Kruskal MST
    

### Leetcode

1. [[547. Number of Provinces]]
    
2. [[684. Redundant Connection]]
    

---

# Dynamic Programming (1D)

**Syntax**

```java
dp[0] = 1;
dp[1] = 1;

for (int i = 2; i <= n; i++) {
    dp[i] = dp[i - 1] + dp[i - 2];
}
```

# Important Ideas

1. Overlapping subproblems
    
2. Optimal substructure
    
3. Cache results
    

## Use Case

- Fibonacci
    
- Climbing stairs
    
- House robber
    

---

# Topological Sort

**Syntax**

```java
Queue<Integer> q = new LinkedList<>();

while (!q.isEmpty()) {
    int node = q.poll();
    for (int nei : adj[node]) {
        indegree[nei]--;
        if (indegree[nei] == 0) q.offer(nei);
    }
}
```

# Important Ideas

1. DAG only
    
2. Dependency resolution
    
3. BFS based
    

## Use Case

- Course schedule
    
- Build systems
    

### Leetcode

1. [[207. Course Schedule]]
    
2. [[210. Course Schedule II]]
    

---

# Final Advice

> [!TIP]  
> You don’t need to **master everything**.  
> You need to **recognize which algorithm applies**.

---

If you want next:

- 🔥 **Graph algorithms cheat sheet**
    
- 🔥 **DP patterns cheat sheet**
    
- 🔥 **Company-wise must-know algorithms**
    
- 🔥 **Printable algorithm template PDF**
    

Just tell me 👊