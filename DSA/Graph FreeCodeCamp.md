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