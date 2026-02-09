You’re thinking exactly like a placement topper now 🔥  
Below is a **COMPLETE, end-to-end GRAPH CHEAT SHEET** tailored for **placements + LeetCode**, with **patterns, tricks, edge cases, and interview talk-points**.

👉 You can paste this **as-is into Obsidian** and revise before coding rounds.

---

# 🧠 GRAPH CHEAT SHEET

### (Placements + LeetCode + Coding Rounds)

---

## 1️⃣ How to Identify a Graph Problem (MOST IMPORTANT)

If the problem mentions:

- connections / links / roads
    
- neighbors / adjacent
    
- dependencies / prerequisites
    
- transformations (word → word)
    
- grid / matrix movement
    
- minimum steps / hops
    
- reachability
    

✅ **IT IS A GRAPH PROBLEM**

---

## 2️⃣ Graph Types → What Algorithm to Use

|Graph Type|Examples|Best Algorithm|
|---|---|---|
|Unweighted|Friends, jumps|BFS|
|Weighted (+ve)|Maps, cost|Dijkstra|
|Weighted (−ve)|Currency exchange|Bellman-Ford|
|Directed|Course Schedule|Topo Sort|
|Undirected|Network|DFS / Union Find|
|DAG|Build system|Topo Sort|
|Grid (Matrix)|Islands, Maze|BFS / DFS|
|Tree|Hierarchy|DFS / BFS|

---

## 3️⃣ Representation (ALWAYS SAY THIS)

> “I’ll use an **adjacency list** for space efficiency.”

```java
ArrayList<ArrayList<Integer>> adj;
```

Grid → no need to build graph explicitly.

---

## 4️⃣ BFS vs DFS (Interview Gold)

|BFS|DFS|
|---|---|
|Queue|Recursion / Stack|
|Shortest path|Explore deeply|
|Level order|Backtracking|
|More memory|Less memory|

📌 **Shortest path in unweighted graph → BFS ALWAYS**

---

## 5️⃣ CORE GRAPH PATTERNS (90% Problems)

---

### 🔹 Pattern 1: Traversal / Connected Components

**Keywords:** count, reach, connected

Used in:

- Number of islands
    
- Provinces
    
- Graph connectivity
    

Algorithm:

```
for each node:
    if not visited:
        DFS/BFS
        count++
```

---

### 🔹 Pattern 2: Shortest Path

|Case|Algorithm|
|---|---|
|Unweighted|BFS|
|Weighted (+ve)|Dijkstra|
|Weighted (−ve)|Bellman-Ford|
|Grid shortest path|BFS|
|All pairs|Floyd-Warshall (rare)|

---

### 🔹 Pattern 3: Cycle Detection

|Graph|Technique|
|---|---|
|Undirected|DFS + parent|
|Directed|DFS + recursion stack|
|Directed|Topo sort fails|

📌 Cycle in directed graph = **no valid topo order**

---

### 🔹 Pattern 4: Topological Sort (VERY IMPORTANT)

Only works on **DAG**

Used in:

- Course Schedule
    
- Task scheduling
    
- Build dependencies
    

Algorithms:

- DFS + stack
    
- Kahn’s Algorithm (BFS + indegree)
    

---

### 🔹 Pattern 5: Grid / Matrix Problems

Grid = Graph (implicit)

Moves:

```java
int[] dx = {-1,0,1,0};
int[] dy = {0,1,0,-1};
```

Used in:

- Flood fill
    
- Rotten oranges
    
- Islands
    
- Shortest path in maze
    

---

## 6️⃣ Union Find (DISJOINT SET)

Used when:

- Dynamic connectivity
    
- Kruskal’s MST
    
- Cycle detection (undirected)
    

Optimizations:

- Path compression
    
- Union by rank
    

📌 **If graph edges are added dynamically → Union Find**

---

## 7️⃣ Minimum Spanning Tree (MST)

|Algorithm|Use|
|---|---|
|Kruskal|Sparse graph|
|Prim|Dense graph|

Rules:

- Undirected graph only
    
- Connect all nodes with min cost
    

---

## 8️⃣ MUST-KNOW LEETCODE GRAPH PROBLEMS

|Problem|Pattern|
|---|---|
|Number of Islands|DFS/BFS|
|Course Schedule|Topo Sort|
|Clone Graph|DFS|
|Rotten Oranges|Multi-source BFS|
|Word Ladder|BFS|
|Network Delay Time|Dijkstra|
|Accounts Merge|Union Find|
|Pacific Atlantic|DFS|
|Cheapest Flights|Dijkstra|

---

## 9️⃣ INTERVIEW TIPS (VERY IMPORTANT)

### 🔥 Tip 1: Always Ask

> “Is the graph directed or undirected?”

---

### 🔥 Tip 2: Mark Visited Immediately

```java
visited[node] = true; // before pushing
```

Prevents TLE.

---

### 🔥 Tip 3: BFS Level Trick

```java
int size = q.size();
while(size--) { ... }
```

Used in:

- Levels
    
- Time steps
    
- Minimum moves
    

---

### 🔥 Tip 4: Multi-Source BFS

Push **all sources first**.

Used in:

- Rotten Oranges
    
- Distance to nearest 0
    

---

### 🔥 Tip 5: Topo Sort Validation

If topo length < V → cycle exists.

---

### 🔥 Tip 6: Dijkstra Optimization

Ignore outdated PQ entries:

```java
if (dist > currDist) continue;
```

---

## 🔟 Common Mistakes (AVOID THESE)

❌ Using DFS for shortest path  
❌ Forgetting visited array  
❌ Not handling disconnected graph  
❌ Using Dijkstra with negative weights  
❌ Building graph unnecessarily for grid

---

## 🔑 One-Line Decision Cheat

- **Min steps?** → BFS
    
- **Dependency?** → Topo sort
    
- **Cycle?** → DFS
    
- **Cost?** → Dijkstra
    
- **Grid?** → BFS/DFS
    
- **Dynamic edges?** → Union Find
    

---

## 🧪 Final Revision Strategy (Placements)

1️⃣ Master BFS + DFS  
2️⃣ Learn Topo Sort  
3️⃣ Learn Dijkstra  
4️⃣ Learn Union Find  
5️⃣ Practice grid problems  
6️⃣ Memorize patterns, not code

---

Locked in 🔥
Below is **everything you asked for**, optimized for **placements + LeetCode**, clean enough to **revise the night before interviews**.

---

# 📌 20 LeetCode Graph Problems (ORDERED BY DIFFICULTY & PATTERN)

### 🟢 EASY (Build confidence)

1. Number of Islands — DFS / BFS
2. Flood Fill — DFS / BFS
3. Find if Path Exists in Graph — DFS / BFS
4. Max Area of Island — DFS
5. Clone Graph — DFS / BFS

---

### 🟡 MEDIUM (PLACEMENT CORE 🔥)

6. Number of Provinces — DFS / Union Find
7. Rotting Oranges — Multi-source BFS
8. Course Schedule — Topological Sort
9. Course Schedule II — Topological Sort
10. Pacific Atlantic Water Flow — DFS
11. Keys and Rooms — DFS
12. Word Ladder — BFS
13. Accounts Merge — Union Find
14. Number of Connected Components — Union Find

---

### 🔴 HARD (INTERVIEW DIFFERENTIATOR)

15. Network Delay Time — Dijkstra
16. Cheapest Flights Within K Stops — Dijkstra / BFS
17. Reconstruct Itinerary — DFS + Backtracking
18. Alien Dictionary — Topo Sort
19. Shortest Path in Binary Matrix — BFS
20. Critical Connections in a Network — Tarjan (Advanced)

📌 **If you do 1–14 well → 90% graph questions covered**

---

# 🧩 GRAPH → ALGORITHM DECISION FLOWCHART

```
START
  |
  v
Does the problem mention connections / neighbors / grid?
  |
  YES
  |
Is it asking MINIMUM steps / distance?
  |
  ├── YES
  |     |
  |   Is graph weighted?
  |     |
  |   ├── NO  → BFS
  |   └── YES
  |         |
  |       Negative weights?
  |         |
  |       ├── YES → Bellman-Ford
  |       └── NO  → Dijkstra
  |
  └── NO
        |
      Is it about dependency / order?
        |
      ├── YES → Topological Sort
      |
      └── NO
            |
          Cycle detection?
            |
          ├── Directed   → DFS + Rec Stack
          └── Undirected → DFS + Parent
```

📌 **Memorize this flowchart → instant clarity in interviews**

---

# 💡 JAVA ONE-FILE GRAPH TEMPLATE (COPY–PASTE READY)

```java
import java.util.*;

public class GraphTemplate {

    // ---------- Graph ----------
    static ArrayList<ArrayList<Integer>> adj;

    static void buildGraph(int V, int[][] edges, boolean directed) {
        adj = new ArrayList<>();
        for (int i = 0; i < V; i++) adj.add(new ArrayList<>());

        for (int[] e : edges) {
            adj.get(e[0]).add(e[1]);
            if (!directed)
                adj.get(e[1]).add(e[0]);
        }
    }

    // ---------- BFS ----------
    static void bfs(int V, int start) {
        boolean[] vis = new boolean[V];
        Queue<Integer> q = new LinkedList<>();
        q.add(start);
        vis[start] = true;

        while (!q.isEmpty()) {
            int node = q.poll();
            for (int nei : adj.get(node)) {
                if (!vis[nei]) {
                    vis[nei] = true;
                    q.add(nei);
                }
            }
        }
    }

    // ---------- DFS ----------
    static void dfs(int node, boolean[] vis) {
        vis[node] = true;
        for (int nei : adj.get(node))
            if (!vis[nei])
                dfs(nei, vis);
    }

    // ---------- Topological Sort (Kahn) ----------
    static int[] topoSort(int V) {
        int[] indeg = new int[V];
        for (int i = 0; i < V; i++)
            for (int v : adj.get(i))
                indeg[v]++;

        Queue<Integer> q = new LinkedList<>();
        for (int i = 0; i < V; i++)
            if (indeg[i] == 0) q.add(i);

        int[] topo = new int[V];
        int idx = 0;

        while (!q.isEmpty()) {
            int u = q.poll();
            topo[idx++] = u;
            for (int v : adj.get(u)) {
                if (--indeg[v] == 0)
                    q.add(v);
            }
        }
        return topo;
    }
}
```

📌 **This single file solves 70% graph questions**

---

# 🧠 LAST-DAY GRAPH REVISION (1 PAGE)

### 🔑 One-Liners to Remember

* Min steps → **BFS**
* Cost involved → **Dijkstra**
* Dependency → **Topo sort**
* Cycle → **DFS**
* Grid → **BFS / DFS**
* Dynamic connectivity → **Union Find**

---

### 🔥 Interview Power Tips

* Mark `visited` **when adding to queue**
* BFS = Queue, DFS = Stack/Recursion
* If topo size < V → cycle exists
* Multi-source BFS → push all sources first
* Dijkstra ❌ negative weights

---

### ❌ Common Mistakes

* DFS for shortest path ❌
* Forgetting disconnected components ❌
* Using Dijkstra with negative edges ❌
* Rebuilding graph for grid ❌

---

### ✅ Final Prep Checklist

✔ BFS
✔ DFS
✔ Topo Sort
✔ Dijkstra
✔ Union Find
✔ Grid problems

---

If you want next (HIGHLY recommended):

* 🧠 **Graph patterns → 5 templates only**
* 🧪 **Company-wise graph questions**
* 🧩 **Dry-run strategy for interviews**
* 📒 **Obsidian backlinks setup**

Say the word 🚀

