Directed graph 
Undirected graph
# Cycle 
Starts from the node and reach to same node
![[Pasted image 20260211205333.png]]
A node cannot appear twice in a path
Adjacent node should have an edges
Degree of graph - no of edges attached to the graph in UD graph
Degree of graph = 2* E(UD)
Directed Graph- Indegree outdegree
representation of Graph 
m represents edges and n represent nodes
Two ways to store a graph 
1. matrix way -n*m;
   ```
   int [n][m];
   ```
2. list way - 2*n(edges)

```java

```
connected components  graph
Here are notes on the Introduction to Graph Data Structures based on the provided video transcript.

### **Introduction to Graphs**

- **Structure:** A graph is a data structure composed of **nodes** (also called vertices) and **edges**.
- **Nodes (Vertices):**
    - Represented generically as circular objects.
    - Typically labeled with numbers (e.g., 1, 2, 3...), though the numbering order does not matter.
    - **$V$** is often used to denote the total count of vertices/nodes.
- **Edges:**
    - The lines connecting two nodes.
    - Edges determine if and how you can travel between nodes.

---

### **Types of Graphs**

#### **1. Undirected Graph**

- **Definition:** A graph where the edges do not have arrows or direction.
- **Bi-directional:** An edge between node $u$ and node $v$ means you can travel from $u$ to $v$ **and** from $v$ to $u$.
- **Connectivity:** It represents a two-way connection.

#### **2. Directed Graph**

- **Definition:** A graph where edges have arrows indicating a specific direction.
- **Uni-directional:** An edge from $1 \to 4$ allows travel from 1 to 4, but **not** from 4 to 1.
- **Bi-directional Simulation:** To have a two-way connection in a directed graph, you must have two separate edges (one from $1 \to 4$ and another from $4 \to 1$).

---

### **Key Concepts & Terminology**

#### **Cycles**

- **Definition:** A cycle occurs when you start at a specific node, travel through the graph via edges, and **end at the same node**.
- **Undirected Cyclic Graph:** An undirected graph that contains at least one cycle.
- **Directed Acyclic Graph (DAG):** A directed graph that contains **no cycles**.
- **Note on Structure:** A graph does not have to be a closed circle; open structures (like binary trees) are also considered graphs as long as they have nodes and edges.

#### **Path**

- **Definition:** A sequence of nodes where every adjacent pair of nodes is connected by an edge.
- **Constraint:** A node **cannot appear twice** in a path.
- **Reachability:** A valid path requires that each node in the sequence is reachable from the previous one via an edge.

#### **Degree of a Node**

- **In Undirected Graphs:**
    - The degree is the **total number of edges** attached to a specific node.
    - **Property:** The total degree of a graph is equal to **twice the number of edges** ($2 \times E$) because every edge connects two nodes.
- **In Directed Graphs:**
    - **In-degree:** The number of **incoming** edges (pointing toward the node).
    - **Out-degree:** The number of **outgoing** edges (pointing away from the node).

#### **Edge Weights**

- **Definition:** A numerical value assigned to an edge.
- **Usage:** Used to represent costs, distances, or other metrics between nodes (e.g., weight 3, weight 5).
- **Unit Weights:** If no weights are explicitly assigned, the convention is to assume **unit weights** (a value of 1).
  Here are comprehensive notes on Graph Data Structures, Traversal Algorithms, and problem-solving applications based on the provided sources.

### **1. Fundamentals of Graphs**

**Basic Structure**

- **Definition:** A graph consists of **Nodes** (vertices) and **Edges** (lines connecting nodes).
- **Notation:** Nodes are often numbered (e.g., 1, 2, 3), but the order does not matter. $V$ denotes the number of vertices.
- **Connectivity:** Graphs do not need to be enclosed circles; open structures like trees are also considered graphs.

**Types of Graphs**

- **Undirected Graph:** Edges have no direction. An edge between $u$ and $v$ is bi-directional (you can travel $u \to v$ and $v \to u$).
- **Directed Graph:** Edges have arrows. An edge $u \to v$ allows travel only from $u$ to $v$. To have a bi-directional connection, two separate directed edges are required.

**Key Terminology**

- **Cycle:** A path that starts at a node and ends at the same node.
    - **DAG (Directed Acyclic Graph):** A directed graph with no cycles.
- **Path:** A sequence of reachable nodes where **no node appears twice**. Adjacent nodes in a path must have an edge connecting them.
- **Degree:**
    - **Undirected:** The number of edges attached to a node.
    - **Property:** The total degree of a graph is $2 \times E$ (twice the number of edges) because every edge connects two nodes.
    - **Directed:** Split into **In-degree** (incoming edges) and **Out-degree** (outgoing edges).
- **Edge Weights:** Numerical values assigned to edges (e.g., distance, cost). If not assigned, assume **unit weights** (value of 1).

---

### **2. Traversal Algorithms**

#### **Breadth-First Search (BFS)**

- **Concept:** A **level-wise** traversal. It visits neighbors at distance 1, then distance 2, and so on (Breadth).
- **Data Structures:**
    - **Queue (FIFO):** Stores nodes to be processed.
    - **Visited Array:** Tracks processed nodes to prevent cycles (size $N+1$ for 1-based indexing).
- **Algorithm Steps:**
    1. Push the **starting node** into the Queue and mark it as visited.
    2. While the Queue is not empty, remove (pop) the front node.
    3. Iterate through the node's neighbors (using an adjacency list).
    4. If a neighbor has not been visited, add it to the Queue and mark it as visited.
- **Complexity:**
    - **Time:** $O(N) + O(2E)$ (Visiting every node once + traversing total degrees).
    - **Space:** $O(N)$ (Queue + Visited Array).

#### **Depth-First Search (DFS)**

- **Concept:** A **depth-wise** traversal. It goes as deep as possible down a path before backtracking.
- **Mechanism:** Uses **Recursion** to visit neighbors, effectively using the system stack.
- **Algorithm Steps:**
    1. Start at a node and mark it as visited.
    2. Access the adjacency list for neighbors.
    3. For each unvisited neighbor, recursively call the DFS function for that neighbor.
    4. When a node has no unvisited neighbors, the function returns (backtracks) to the previous node.
- **Complexity:**
    - **Time:** $O(N) + O(2E)$ (Summation of degrees).
    - **Space:** $O(N)$ (Visited Array + Recursion Stack height in worst-case skewed graphs).

---

### **3. Application: Rotten Oranges Problem**

**Problem Statement**

- Given a grid ($N \times M$) where:
    - 0 = Empty cell.
    - 1 = Fresh orange.
    - 2 = Rotten orange.
- **Goal:** Find the **minimum time** to rot all fresh oranges. A rotten orange rots adjacent fresh neighbors (up, down, left, right) in 1 unit of time.

**Solution Logic**

- **Algorithm Choice:** **BFS** is required because oranges rot simultaneously level-by-level (uniform pace). DFS is incorrect here as it would explore depth first, failing to track minimum time.
- **Multi-Source BFS:** Since multiple oranges can be rotten initially, all of them are pushed into the Queue at time $t=0$.
- **Data Structures:**
    - **Queue:** Stores `{{row, col}, time}`.
    - **Visited Array:** Matches grid dimensions to track rotten status.
    - **Delta Arrays:** Used to calculate neighbor coordinates easily: `dRow = {-1, 0, 1, 0}` and `dCol = {0, 1, 0, -1}`.

**Execution Steps**

1. **Initialization:** Scan grid. Push all initially rotten oranges (`2`) to Queue with time 0. Count total fresh oranges.
2. **BFS Loop:**
    - Pop the current orange. Update `maxTime`.
    - Check 4 directions. If a valid, unvisited fresh orange (`1`) is found:
        - Mark as visited/rotten.
        - Push to Queue with `time + 1`.
        - Decrement fresh orange count.
3. **Final Check:** If the count of fresh oranges remaining is not zero, return `-1` (impossible to rot all). Otherwise, return `maxTime`.

**Complexity**

- **Time:** $O(N \times M)$ (Each cell is processed at most once).
- **Space:** $O(N \times M)$ (Queue and Visited array size).
  Based on the provided sources, here is the Java code implementing the three core concepts discussed: **Breadth-First Search (BFS)**, **Depth-First Search (DFS)**, and the **Rotten Oranges** problem (an application of BFS).

### 1. BFS and DFS Traversals

The following class demonstrates how to traverse a graph using an Adjacency List `ArrayList<ArrayList<Integer>>`, as described in the sources.

```
import java.util.*;

public class GraphTraversals {

    // BREADTH-FIRST SEARCH (BFS)
    // Concept: Level-wise traversal using a Queue.
    public ArrayList<Integer> bfsOfGraph(int V, ArrayList<ArrayList<Integer>> adj) {
        ArrayList<Integer> bfs = new ArrayList<>();
        boolean[] visited = new boolean[V]; // Visited array to track nodes
        Queue<Integer> q = new LinkedList<>(); // Queue for FIFO operations

        // Initial configuration: Push starting node (0) and mark as visited
        q.add(0);
        visited = true;

        // Iterate until queue is empty
        while (!q.isEmpty()) {
            Integer node = q.poll(); // Take the node out
            bfs.add(node); // Add to result list

            // Traverse all neighbors of the current node
            for (Integer neighbor : adj.get(node)) {
                // If neighbor is not visited, add to queue and mark visited
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    q.add(neighbor);
                }
            }
        }
        return bfs;
    }

    // DEPTH-FIRST SEARCH (DFS)
    // Concept: Depth-wise traversal using Recursion.

    // Main DFS function to initialize variables
    public ArrayList<Integer> dfsOfGraph(int V, ArrayList<ArrayList<Integer>> adj) {
        boolean[] visited = new boolean[V]; // Visited array
        ArrayList<Integer> ls = new ArrayList<>(); // List to store DFS result

        // Assuming 0 is the starting node for 0-based indexing
        dfs(0, visited, adj, ls);
        return ls;
    }

    // Recursive helper function
    private void dfs(int node, boolean[] visited, ArrayList<ArrayList<Integer>> adj, ArrayList<Integer> ls) {
        visited[node] = true; // Mark node as visited
        ls.add(node); // Add node to the list

        // Traverse neighbors
        for (Integer neighbor : adj.get(node)) {
            // Only make a recursive call if the neighbor is unvisited
            if (!visited[neighbor]) {
                dfs(neighbor, visited, adj, ls);
            }
        }
    }
}
```

---

### 2. Rotten Oranges (Grid BFS)

This solution solves the "Rotten Oranges" problem using BFS because oranges rot simultaneously level-by-level.

```
import java.util.*;

public class RottenOranges {

    // Helper class to store coordinates and time
    static class Pair {
        int row;
        int col;
        int tm;

        Pair(int row, int col, int tm) {
            this.row = row;
            this.col = col;
            this.tm = tm;
        }
    }

    public int orangesRotting(int[][] grid) {
        int n = grid.length;
        int m = grid.length;

        // Queue stores {row, col, time}
        Queue<Pair> q = new LinkedList<>();

        // Visited array to keep track of rotten oranges
        int[][] visited = new int[n][m];

        int cntFresh = 0; // Count fresh oranges to check validity later

        // Step 1: Initialize Queue with all initially rotten oranges
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                // If cell contains rotten orange (2)
                if (grid[i][j] == 2) {
                    q.add(new Pair(i, j, 0)); // Push with time 0
                    visited[i][j] = 2; // Mark as visited
                } else {
                    visited[i][j] = 0;
                }

                // If cell contains fresh orange (1), count it
                if (grid[i][j] == 1) {
                    cntFresh++;
                }
            }
        }

        int tm = 0; // Variable to track maximum time

        // Delta arrays for 4 directions: top, right, bottom, left
        int[] dRow = {-1, 0, 1, 0};
        int[] dCol = {0, 1, 0, -1};
        int cnt = 0; // Count of fresh oranges converted to rotten

        // Step 2: BFS Traversal
        while (!q.isEmpty()) {
            int r = q.peek().row;
            int c = q.peek().col;
            int t = q.peek().tm; // Get current time
            tm = Math.max(tm, t); // Update max time
            q.remove();

            // Check all 4 neighbors
            for (int i = 0; i < 4; i++) {
                int nrow = r + dRow[i];
                int ncol = c + dCol[i];

                // Check boundary validity and if the neighbor is a fresh orange
                if (nrow >= 0 && nrow < n && ncol >= 0 && ncol < m &&
                    visited[nrow][ncol] == 0 && grid[nrow][ncol] == 1) {

                    // Push to queue with time + 1
                    q.add(new Pair(nrow, ncol, t + 1));

                    // Mark as visited/rotten
                    visited[nrow][ncol] = 2;

                    cnt++; // Increment count of converted oranges
                }
            }
        }

        // Step 3: Validation
        // If the number of oranges we rotted != initial fresh count, return -1
        if (cnt != cntFresh) {
            return -1;
        }

        return tm; // Return the minimum time required
    }
}
```

### Key Logic Summary from Sources:

- **BFS (Breadth-First Search):** Uses a **Queue**. It traverses neighbors (breadth) before moving deeper. Time Complexity is $O(N + 2E)$.
- **DFS (Depth-First Search):** Uses **Recursion** (Stack). It traverses deep into one path before backtracking. Time Complexity is $O(N + 2E)$ (Summation of degrees).
- **Rotten Oranges:** Uses **Multi-source BFS**. We push _all_ initially rotten oranges into the queue at time 0. We cannot use DFS because we need the _minimum_ time, which implies simultaneous level-wise processing.