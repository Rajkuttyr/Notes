Max depth

### FORMULA 
1+max(l,r);

```
if(root == null)return 0;
int lh = maxDepth(root.left);
int rh= maxDepth(root.right);

return 1+max(lh,rh);
```
# Level order
1. Also called as BFS 
2. Implemented using Queue;
3. VECTOR OF VECTOR AND LIST OF LIST
4. QUEUE
5. take root node and add to q
6. add left to q
7. add rigth to q
8. on one completion 
9. add node to list 
10. take the element in q
11. check left thenn right and both to q
12. then and so on
13. if q is empty print the list

```
Queue<TREE> queue = new Queue<>();
List<List<Integer>> a = new LinkeList<>();
if(root==null) return a;



```