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
Every tree is a graph but every graph is not tree
Node n edges =n-1;
To determine nodes are cyclic if nodes = n and edges=n-1
```java
class Solution {

public boolean validTree(int n, int[][] edges) {

if(n-1!=edges.length)return false;

List<List<Integer>> adj = new ArrayList<>();

for(int i=0;i<n;i++){

adj.add(new ArrayList<>());

}

for(int[] node : edges){

adj.get(node[0]).add(node[1]);

adj.get(node[1]).add(node[0]);

}

int[] vis = new int[n];

dfs(0,vis,adj);

int count=0;

for(int i:vis){

if(i==1)count++;

}

return count==n ? true:false;

  

}

public void dfs(int start, int[] vis, List<List<Integer>> adj){

vis[start]=1;

for(int i :adj.get(start)){

if(vis[i]==0)dfs(i,vis,adj);

}

}

}


```
lc -133
Clone graph
Facebook -44 amazon google 
given conected undirected graph  we can reach to any node by traversing from any node return deep copy 
lc 994 rotting oranges
0 representing empty cell
1 representing fresh orange 
2 rotten ornage
Every minutes a fresh oranges thatis 4 directionaly adjacent to each will rotten 
returm minimu numer of time to rott all orange if not possible return 0
BFS traversal for evry bfs call increase the min 
```java
class Solution {

public int orangesRotting(int[][] grid) {

if(grid==null||grid.length==0) return -1;

int n = grid.length,m=grid[0].length;

Queue<int[]> q = new LinkedList<>();

int fc=0;

for(int i=0;i<n;i++){

for(int j=0;j<m;j++){

if(grid[i][j]==1)fc++;

else if(grid[i][j]==2)q.offer(new int[]{i,j});

  

}

}

if(fc==0)return 0;

int min=0;

int[][] dir = new int[][]{{1,0},{-1,0},{0,1},{0,-1}};

while(!q.isEmpty()){

int size = q.size();

for(int i=0;i<size;i++){

int[] rotten = q.poll();

for(int[] d :dir){

int x = rotten[0]+d[0];

int y = rotten[1]+d[1];

if(x>=0 && y>=0 && x<n&& y<m &&grid[x][y]==1){

grid[x][y]=2;

fc--;

q.offer(new int[]{x,y});

}

}

}

min++;

}

return fc==0 ? min-1:-1;

}

}

```

lc - 684 
graph tree dsu
tree is a undirected graph without cycle 
given graph may be a tree that contains total nodes and edges array
we need to return a that can be removed to be a tree
disjointed set union data structue
1. find - return it belongs to which group
2. merges - if two it will merge into single group


