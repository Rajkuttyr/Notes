```java
import java.util.*;

// =======================================================
// COMPLETE GRAPH TEMPLATE FOR PLACEMENTS & LEETCODE
// =======================================================

public class GraphComplete {

    // ---------- BASIC GRAPH ----------
    static class Graph {
        int V;
        ArrayList<ArrayList<Integer>> adj;

        Graph(int V) {
            this.V = V;
            adj = new ArrayList<>();
            for (int i = 0; i < V; i++)
                adj.add(new ArrayList<>());
        }

        void addEdge(int u, int v, boolean directed) {
            adj.get(u).add(v);
            if (!directed)
                adj.get(v).add(u);
        }
    }

    // ---------- BFS ----------
    static void bfs(Graph g, int src) {
        boolean[] vis = new boolean[g.V];
        Queue<Integer> q = new LinkedList<>();

        q.add(src);
        vis[src] = true;

        while (!q.isEmpty()) {
            int node = q.poll();
            System.out.print(node + " ");

            for (int nei : g.adj.get(node)) {
                if (!vis[nei]) {
                    vis[nei] = true;
                    q.add(nei);
                }
            }
        }
        System.out.println();
    }

    // ---------- DFS ----------
    static void dfs(int node, boolean[] vis, Graph g) {
        vis[node] = true;
        System.out.print(node + " ");

        for (int nei : g.adj.get(node)) {
            if (!vis[nei])
                dfs(nei, vis, g);
        }
    }

    // ---------- CYCLE DETECTION (UNDIRECTED) ----------
    static boolean hasCycleUndirected(int node, int parent,
                                      boolean[] vis, Graph g) {
        vis[node] = true;

        for (int nei : g.adj.get(node)) {
            if (!vis[nei]) {
                if (hasCycleUndirected(nei, node, vis, g))
                    return true;
            } else if (nei != parent) {
                return true;
            }
        }
        return false;
    }

    // ---------- CYCLE DETECTION (DIRECTED) ----------
    static boolean hasCycleDirected(int node,
                                    boolean[] vis,
                                    boolean[] recStack,
                                    Graph g) {
        vis[node] = true;
        recStack[node] = true;

        for (int nei : g.adj.get(node)) {
            if (!vis[nei] && hasCycleDirected(nei, vis, recStack, g))
                return true;
            else if (recStack[nei])
                return true;
        }

        recStack[node] = false;
        return false;
    }

    // ---------- TOPOLOGICAL SORT (DFS) ----------
    static void topoDFS(int node, boolean[] vis,
                        Stack<Integer> st, Graph g) {
        vis[node] = true;

        for (int nei : g.adj.get(node))
            if (!vis[nei])
                topoDFS(nei, vis, st, g);

        st.push(node);
    }

    // ---------- TOPOLOGICAL SORT (KAHN BFS) ----------
    static int[] topoKahn(Graph g) {
        int[] indeg = new int[g.V];

        for (int i = 0; i < g.V; i++)
            for (int nei : g.adj.get(i))
                indeg[nei]++;

        Queue<Integer> q = new LinkedList<>();
        for (int i = 0; i < g.V; i++)
            if (indeg[i] == 0)
                q.add(i);

        int[] topo = new int[g.V];
        int idx = 0;

        while (!q.isEmpty()) {
            int node = q.poll();
            topo[idx++] = node;

            for (int nei : g.adj.get(node)) {
                if (--indeg[nei] == 0)
                    q.add(nei);
            }
        }
        return topo;
    }

    // ---------- SHORTEST PATH (UNWEIGHTED BFS) ----------
    static int[] shortestPathUnweighted(Graph g, int src) {
        int[] dist = new int[g.V];
        Arrays.fill(dist, -1);

        Queue<Integer> q = new LinkedList<>();
        q.add(src);
        dist[src] = 0;

        while (!q.isEmpty()) {
            int node = q.poll();
            for (int nei : g.adj.get(node)) {
                if (dist[nei] == -1) {
                    dist[nei] = dist[node] + 1;
                    q.add(nei);
                }
            }
        }
        return dist;
    }

    // ---------- DIJKSTRA ----------
    static class Pair {
        int node, dist;
        Pair(int n, int d) {
            node = n;
            dist = d;
        }
    }

    static int[] dijkstra(int V,
            ArrayList<ArrayList<Pair>> adj, int src) {

        int[] dist = new int[V];
        Arrays.fill(dist, Integer.MAX_VALUE);

        PriorityQueue<Pair> pq =
            new PriorityQueue<>((a, b) -> a.dist - b.dist);

        pq.add(new Pair(src, 0));
        dist[src] = 0;

        while (!pq.isEmpty()) {
            Pair cur = pq.poll();

            if (cur.dist > dist[cur.node]) continue;

            for (Pair nei : adj.get(cur.node)) {
                if (dist[cur.node] + nei.dist < dist[nei.node]) {
                    dist[nei.node] = dist[cur.node] + nei.dist;
                    pq.add(new Pair(nei.node, dist[nei.node]));
                }
            }
        }
        return dist;
    }

    // ---------- UNION FIND ----------
    static class DSU {
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

    // ---------- MAIN (TEST) ----------
    public static void main(String[] args) {

        Graph g = new Graph(5);

        g.addEdge(0, 1, false);
        g.addEdge(0, 2, false);
        g.addEdge(1, 3, false);
        g.addEdge(2, 4, false);

        System.out.println("BFS:");
        bfs(g, 0);

        System.out.println("DFS:");
        boolean[] vis = new boolean[g.V];
        dfs(0, vis, g);
        System.out.println();

        System.out.println("Shortest Path:");
        System.out.println(Arrays.toString(shortestPathUnweighted(g, 0)));
    }
}

```