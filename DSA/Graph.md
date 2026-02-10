Perfect 👍 here are **clean, interview-ready Java Graph templates** you can **directly paste into Obsidian** and reuse in LeetCode / GFG / contests.

---

# 🧠 Java Graph Templates (DSA Ready)

---

## 🔹 Adjacency List (Generic Graph)

```java
import java.util.*;

class Graph {
    int V;
    ArrayList<ArrayList<Integer>> adj;

    Graph(int V) {
        this.V = V;
        adj = new ArrayList<>();
        for (int i = 0; i < V; i++)
            adj.add(new ArrayList<>());
    }

    void addEdge(int u, int v) {
        adj.get(u).add(v);
        adj.get(v).add(u); // remove for directed graph
    }
}
```

---

## 🔹 BFS (Breadth First Search)

```java
void bfs(int V, ArrayList<ArrayList<Integer>> adj, int start) {
    boolean[] visited = new boolean[V];
    Queue<Integer> q = new LinkedList<>();

    visited[start] = true;
    q.add(start);

    while (!q.isEmpty()) {
        int node = q.poll();
        System.out.print(node + " ");

        for (int nei : adj.get(node)) {
            if (!visited[nei]) {
                visited[nei] = true;
                q.add(nei);
            }
        }
    }
}
```

📌 **Use when**: shortest path (unweighted), level order traversal

---

## 🔹 DFS (Recursive)

```java
void dfs(int node, boolean[] visited, ArrayList<ArrayList<Integer>> adj) {
    visited[node] = true;
    System.out.print(node + " ");

    for (int nei : adj.get(node)) {
        if (!visited[nei]) {
            dfs(nei, visited, adj);
        }
    }
}
```

---

## 🔹 DFS (Iterative – Stack)

```java
void dfsIterative(int start, ArrayList<ArrayList<Integer>> adj, int V) {
    boolean[] visited = new boolean[V];
    Stack<Integer> stack = new Stack<>();

    stack.push(start);

    while (!stack.isEmpty()) {
        int node = stack.pop();

        if (!visited[node]) {
            visited[node] = true;
            System.out.print(node + " ");

            for (int nei : adj.get(node)) {
                if (!visited[nei])
                    stack.push(nei);
            }
        }
    }
}
```

---

## 🔹 Cycle Detection (Undirected Graph – DFS)

```java
boolean hasCycle(int node, int parent, boolean[] visited,
                 ArrayList<ArrayList<Integer>> adj) {

    visited[node] = true;

    for (int nei : adj.get(node)) {
        if (!visited[nei]) {
            if (hasCycle(nei, node, visited, adj))
                return true;
        } else if (nei != parent) {
            return true;
        }
    }
    return false;
}
```

---

## 🔹 Cycle Detection (Directed Graph)

```java
boolean isCyclicUtil(int node, boolean[] visited,
                     boolean[] recStack,
                     ArrayList<ArrayList<Integer>> adj) {

    visited[node] = true;
    recStack[node] = true;

    for (int nei : adj.get(node)) {
        if (!visited[nei] && isCyclicUtil(nei, visited, recStack, adj))
            return true;
        else if (recStack[nei])
            return true;
    }

    recStack[node] = false;
    return false;
}
```

---

## 🔹 Topological Sort (DFS)

```java
void topoDFS(int node, boolean[] visited,
             Stack<Integer> stack,
             ArrayList<ArrayList<Integer>> adj) {

    visited[node] = true;

    for (int nei : adj.get(node)) {
        if (!visited[nei])
            topoDFS(nei, visited, stack, adj);
    }

    stack.push(node);
}
```

---

## 🔹 Topological Sort (Kahn’s Algorithm – BFS)

```java
int[] topoSort(int V, ArrayList<ArrayList<Integer>> adj) {
    int[] indegree = new int[V];

    for (int i = 0; i < V; i++)
        for (int nei : adj.get(i))
            indegree[nei]++;

    Queue<Integer> q = new LinkedList<>();
    for (int i = 0; i < V; i++)
        if (indegree[i] == 0)
            q.add(i);

    int[] topo = new int[V];
    int idx = 0;

    while (!q.isEmpty()) {
        int node = q.poll();
        topo[idx++] = node;

        for (int nei : adj.get(node)) {
            if (--indegree[nei] == 0)
                q.add(nei);
        }
    }
    return topo;
}
```

---

## 🔹 Shortest Path (Unweighted – BFS)

```java
int[] shortestPath(int V, ArrayList<ArrayList<Integer>> adj, int src) {
    int[] dist = new int[V];
    Arrays.fill(dist, -1);

    Queue<Integer> q = new LinkedList<>();
    q.add(src);
    dist[src] = 0;

    while (!q.isEmpty()) {
        int node = q.poll();
        for (int nei : adj.get(node)) {
            if (dist[nei] == -1) {
                dist[nei] = dist[node] + 1;
                q.add(nei);
            }
        }
    }
    return dist;
}
```

---

## 🔹 Dijkstra (Weighted Graph)

```java
class Pair {
    int node, dist;
    Pair(int n, int d) {
        node = n;
        dist = d;
    }
}

int[] dijkstra(int V, ArrayList<ArrayList<Pair>> adj, int src) {
    PriorityQueue<Pair> pq =
        new PriorityQueue<>((a, b) -> a.dist - b.dist);

    int[] dist = new int[V];
    Arrays.fill(dist, Integer.MAX_VALUE);

    pq.add(new Pair(src, 0));
    dist[src] = 0;

    while (!pq.isEmpty()) {
        Pair cur = pq.poll();

        for (Pair nei : adj.get(cur.node)) {
            if (dist[cur.node] + nei.dist < dist[nei.node]) {
                dist[nei.node] = dist[cur.node] + nei.dist;
                pq.add(new Pair(nei.node, dist[nei.node]));
            }
        }
    }
    return dist;
}
```

---

## 🔹 Disjoint Set (Union Find – for Kruskal)

```java
class DSU {
    int[] parent, rank;

    DSU(int n) {
        parent = new int[n];
        rank = new int[n];
        for (int i = 0; i < n; i++)
            parent[i] = i;
    }

    int find(int x) {
        if (parent[x] != x)
            parent[x] = find(parent[x]);
        return parent[x];
    }

    void union(int x, int y) {
        int px = find(x);
        int py = find(y);

        if (px == py) return;

        if (rank[px] < rank[py])
            parent[px] = py;
        else if (rank[px] > rank[py])
            parent[py] = px;
        else {
            parent[py] = px;
            rank[px]++;
        }
    }
}
```

---

## 🔹 Graph Patterns Cheat Sheet

* **Islands / Connected components** → DFS / BFS
* **Shortest path** → BFS / Dijkstra
* **Cycle detection** → DFS + visited
* **Scheduling** → Topological sort
* **Minimum cost network** → Kruskal / Prim

---

If you want next:

* 🔥 **LeetCode graph templates only**
* 📌 **GFG-style function signatures**
* 🧩 **Graph problems by pattern**
* 📒 **Obsidian backlinks setup for DSA**

Just say the word 👀

---

# 📊 Graph Data Structure

## 🔹 What is a Graph?

A **Graph** is a non-linear data structure consisting of:

* **Vertices (Nodes)** → entities
* **Edges** → connections between nodes

Formally:

```
Graph G = (V, E)
V → set of vertices
E → set of edges
```

---

## 🔹 Types of Graphs

### 1. Based on Direction

* **Undirected Graph**
  Edge has no direction
  `(u — v)`

* **Directed Graph (Digraph)**
  Edge has direction
  `(u → v)`

---

### 2. Based on Weight

* **Unweighted Graph**
  All edges equal cost

* **Weighted Graph**
  Each edge has a weight/cost
  `(u → v, weight = 5)`

---

### 3. Based on Connectivity

* **Connected Graph**
  Path exists between every pair of vertices

* **Disconnected Graph**
  At least one vertex is unreachable

---

### 4. Special Graphs

* **Cyclic Graph** → Contains a cycle
* **Acyclic Graph** → No cycles
* **DAG (Directed Acyclic Graph)** → Very important for scheduling
* **Complete Graph** → Every vertex connected to every other
* **Bipartite Graph** → Vertices divided into two sets

---

## 🔹 Graph Representations

### 1. Adjacency Matrix

* 2D array `V x V`
* `matrix[i][j] = 1` if edge exists

**Pros**

* Fast edge lookup `O(1)`

**Cons**

* High space `O(V²)`

---

### 2. Adjacency List ✅ (Most Used)

* Each vertex stores list of neighbors

**Pros**

* Space efficient `O(V + E)`
* Easy traversal

**Cons**

* Edge lookup slower than matrix

---

## 🔹 Graph Traversal

### 🔸 Breadth First Search (BFS)

* Uses **Queue**
* Level-wise traversal
* Finds **shortest path in unweighted graph**

**Time:** `O(V + E)`

---

### 🔸 Depth First Search (DFS)

* Uses **Recursion / Stack**
* Goes deep before backtracking
* Used for cycle detection, components

**Time:** `O(V + E)`

---

## 🔹 Cycle Detection

### Undirected Graph

* DFS with **parent tracking**

### Directed Graph

* DFS with **recursion stack**
* Or **Topological Sort**

---

## 🔹 Topological Sorting

* Linear ordering of vertices
* Only possible in **DAG**

**Methods**

* DFS based
* Kahn’s Algorithm (BFS + indegree)

---

## 🔹 Shortest Path Algorithms

| Algorithm      | Works On               | Notes    |
| -------------- | ---------------------- | -------- |
| BFS            | Unweighted             | Fastest  |
| Dijkstra       | Weighted (no negative) | Greedy   |
| Bellman-Ford   | Negative weights       | Slower   |
| Floyd-Warshall | All-pairs              | DP based |

---

## 🔹 Minimum Spanning Tree (MST)

* Spans all vertices with minimum cost
* Only for **undirected graphs**

**Algorithms**

* **Kruskal’s Algorithm** (Union Find)
* **Prim’s Algorithm** (Priority Queue)

---

## 🔹 Graph Concepts

* **Degree** → number of edges
* **Indegree / Outdegree** → directed graphs
* **Path** → sequence of vertices
* **Cycle** → path that starts & ends at same vertex
* **Component** → connected subgraph

---

## 🔹 Common Graph Problems

* Number of islands 🌊
* Course schedule 📚
* Shortest path 🚦
* Detect cycle 🔁
* Bipartite check ⚖️
* Network delay ⏱️

---

## 🔹 Graph vs Tree

| Tree         | Graph               |
| ------------ | ------------------- |
| No cycles    | Cycles possible     |
| Connected    | May be disconnected |
| n-1 edges    | Any number of edges |
| Hierarchical | Non-hierarchical    |

---

## 🔹 When to Use Graph?

* Social networks
* Maps & navigation
* Dependency resolution
* Computer networks
* Scheduling problems

---

## 🔹 Quick Revision

* Graph = nodes + edges
* Adjacency List preferred
* BFS → shortest path
* DFS → cycles & components
* DAG → topological sort

---

If you want, I can also give:

* 🔥 **LeetCode graph patterns**
* 🧠 **Graph intuition cheatsheet**
* 🧪 **Java / C++ graph templates**
* 📌 **Obsidian-linked notes (with backlinks)**

Just tell me 👀

---
---
---
```java
```



