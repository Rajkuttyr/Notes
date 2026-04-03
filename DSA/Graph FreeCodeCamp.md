Reprsentaion of graph as 
1. Adjacency List 
2. Adjacency matrix
3. less edges - adjacency list
   more edges - matrix

22 leetcode problems 
1.No of provicences - amazon bloomberg google
547 provicences 
a provinces is group of directly connected or inderctly and no othe
n*n matrix is connected isConnected[i][j]=1 they are connected

```java
class Solution {

public int findCircleNum(int[][] isConnected) {

int n = isConnected.length;

boolean[] vis = new boolean[n];

int res =0;

for(int i=0;i<n;i++){

if(!vis[i]){

bfs(i,isConnected,vis);

res++;

}

}

return res;

}

public void bfs(int start,int[][] matrix,boolean[] vis){

Queue<Integer> q = new LinkedList<>();

q.offer(start);

vis[start]=true;

while(!q.isEmpty()){

int city = q.poll();

for(int i=0;i<matrix.length;i++){

if(matrix[city][i]==1&& !vis[i]){

q.offer(i);

vis[i]=true;

}

}

}

}

}
```

200 number of island-apple google amazon facebook

input - n*n grid - filled with 1 or 0 1- land 0- water we need to find total no island in the grid 
Island - a land covered four sides by water
All land can be conected together and can be consider as land 
travers the input array  and find matrix = 1; 
DFS 
```java
class Solution {

public int numIslands(char[][] grid) {

int n = grid.length;

int m = grid[0].length;

int res =0;

for(int i=0;i<n;i++){

for(int j=0;j<m;j++){

if(grid[i][j]=='1'){

res++;

dfs(i,j,grid);

}

}

}

return res;

}

public void dfs(int i,int j,char[][] grid){

int n =grid.length;

int m = grid[0].length;

if(i<0 ||j<0||i>=n||j>=m ||grid[i][j]=='0') return;

grid[i][j]='0';

dfs(i-1,j,grid);

dfs(i+1,j,grid);

dfs(i,j-1,grid);

dfs(i,j+1,grid);

}

}
```

lc -695 max area of island
```java
class Solution {

public int maxAreaOfIsland(int[][] grid) {

int n = grid.length;

int m = grid[0].length;

int res=0;

for(int i=0;i<n;i++){

for(int j=0;j<m;j++){

if(grid[i][j]==1){

int val = dfs(i,j,grid);

res=Math.max(res,val);

}

}

}

return res;

}

public int dfs(int i,int j,int[][] grid){

int n = grid.length;

int m = grid[0].length;

int area=1;

if(i<0||j<0||i>=n||j>=m||grid[i][j]==0)return 0;

grid[i][j]=0;

area+=dfs(i-1,j,grid);

area+=dfs(i+1,j,grid);

area+=dfs(i,j-1,grid);

area+=dfs(i,j+1,grid);

return area;

}

}
```

323 Number of Connected Components in Undirescted Graph - google amazon facebook

give n nodes and array of edges of undirected graph based on the input we have to return number of connected omponnets exsist 
dfs;
when edges are given 
convert edges to 
```java
import java.util.*;

class Solution {
    public int countComponents(int n, int[][] edges) {
        List<List<Integer>> adj = new ArrayList<>();

        // Step 1: Build graph
        for(int i = 0; i < n; i++){
            adj.add(new ArrayList<>());
        }

        for(int[] edge : edges){
            adj.get(edge[0]).add(edge[1]);
            adj.get(edge[1]).add(edge[0]);
        }

        boolean[] visited = new boolean[n];
        int res = 0;

        // Step 2: DFS traversal
        for(int i = 0; i < n; i++){
            if(!visited[i]){
                dfs(i, adj, visited);
                res++;
            }
        }

        return res;
    }

    public void dfs(int node, List<List<Integer>> adj, boolean[] visited){
        visited[node] = true;

        for(int nei : adj.get(node)){
            if(!visited[nei]){
                dfs(nei, adj, visited);
            }
        }
    }
}
```
261- Graph valid tree -google facebook 

