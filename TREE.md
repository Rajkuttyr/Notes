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
3. 
