🔥 **Excellent choice.**  
Below is a **COMPLETE, SELF-SUFFICIENT NOTES SET** for **Binary Tree & Binary Search Tree (BST)** — concepts, techniques, and algorithms — written **strictly in your exact format**, clean `.md`, easy to learn, revise, and apply.

If you master **only these notes**, you can solve **90%+ tree problems** confidently.

---

# Binary Tree

## Definition

A **Binary Tree** is a tree data structure where each node has **at most two children**:

- Left child
    
- Right child
    

---

## Node Structure

**Syntax**

```java
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;

    TreeNode(int val) {
        this.val = val;
    }
}
```

---

# Binary Tree Traversals

---

## Inorder Traversal (L → Root → R)

**Syntax**

```java
void inorder(TreeNode root) {
    if (root == null) return;
    inorder(root.left);
    System.out.print(root.val);
    inorder(root.right);
}
```

## Use Case

- BST gives sorted order
    
- Validate BST
    

### Leetcode

1. [[94. Binary Tree Inorder Traversal]]
    

---

## Preorder Traversal (Root → L → R)

**Syntax**

```java
void preorder(TreeNode root) {
    if (root == null) return;
    System.out.print(root.val);
    preorder(root.left);
    preorder(root.right);
}
```

## Use Case

- Copy tree
    
- Tree serialization
    

### Leetcode

1. [[144. Binary Tree Preorder Traversal]]
    

---

## Postorder Traversal (L → R → Root)

**Syntax**

```java
void postorder(TreeNode root) {
    if (root == null) return;
    postorder(root.left);
    postorder(root.right);
    System.out.print(root.val);
}
```

## Use Case

- Delete tree
    
- Bottom-up computation
    

### Leetcode

1. [[145. Binary Tree Postorder Traversal]]
    

---

# Level Order Traversal (BFS)

**Syntax**

```java
Queue<TreeNode> q = new LinkedList<>();
q.offer(root);

while (!q.isEmpty()) {
    TreeNode node = q.poll();
    if (node.left != null) q.offer(node.left);
    if (node.right != null) q.offer(node.right);
}
```

## Use Case

- Level-wise processing
    
- Shortest path in tree
    

### Leetcode

1. [[102. Binary Tree Level Order Traversal]]
    

---

# Important Binary Tree Techniques

---

## Height / Depth of Tree

**Syntax**

```java
int height(TreeNode root) {
    if (root == null) return 0;
    return 1 + Math.max(height(root.left), height(root.right));
}
```

### Leetcode

- [[104. Maximum Depth of Binary Tree]]
    

---

## Diameter of Tree

**Syntax**

```java
int diameter = 0;

int dfs(TreeNode root) {
    if (root == null) return 0;
    int left = dfs(root.left);
    int right = dfs(root.right);
    diameter = Math.max(diameter, left + right);
    return 1 + Math.max(left, right);
}
```

### Leetcode

- [[543. Diameter of Binary Tree]]
    

---

## Check Balanced Tree

**Syntax**

```java
int check(TreeNode root) {
    if (root == null) return 0;
    int l = check(root.left);
    if (l == -1) return -1;
    int r = check(root.right);
    if (r == -1) return -1;
    if (Math.abs(l - r) > 1) return -1;
    return 1 + Math.max(l, r);
}
```

### Leetcode

- [[110. Balanced Binary Tree]]
    

---

# Path-Based Problems

---

## Root to Leaf Path Sum

**Syntax**

```java
boolean hasPathSum(TreeNode root, int sum) {
    if (root == null) return false;
    if (root.left == null && root.right == null)
        return sum == root.val;
    return hasPathSum(root.left, sum - root.val)
        || hasPathSum(root.right, sum - root.val);
}
```

### Leetcode

- [[112. Path Sum]]
    

---

## All Root to Leaf Paths

**Syntax**

```java
void dfs(TreeNode root, String path) {
    if (root == null) return;
    path += root.val;
    if (root.left == null && root.right == null)
        res.add(path);
    dfs(root.left, path + "->");
    dfs(root.right, path + "->");
}
```

### Leetcode

- [[257. Binary Tree Paths]]
    

---

# Binary Search Tree (BST)

## Definition

A **BST** is a binary tree where:

```text
Left subtree < Root < Right subtree
```

---

## Search in BST

**Syntax**

```java
TreeNode searchBST(TreeNode root, int val) {
    if (root == null || root.val == val) return root;
    if (val < root.val) return searchBST(root.left, val);
    return searchBST(root.right, val);
}
```

### Leetcode

- [[700. Search in a Binary Search Tree]]
    

---

## Insert into BST

**Syntax**

```java
TreeNode insert(TreeNode root, int val) {
    if (root == null) return new TreeNode(val);
    if (val < root.val)
        root.left = insert(root.left, val);
    else
        root.right = insert(root.right, val);
    return root;
}
```

### Leetcode

- [[701. Insert into a Binary Search Tree]]
    

---

## Validate BST

**Syntax**

```java
boolean isValid(TreeNode root, long min, long max) {
    if (root == null) return true;
    if (root.val <= min || root.val >= max) return false;
    return isValid(root.left, min, root.val)
        && isValid(root.right, root.val, max);
}
```

### Leetcode

- [[98. Validate Binary Search Tree]]
    

---

## Lowest Common Ancestor (BST)

**Syntax**

```java
TreeNode lca(TreeNode root, int p, int q) {
    if (root.val > p && root.val > q)
        return lca(root.left, p, q);
    if (root.val < p && root.val < q)
        return lca(root.right, p, q);
    return root;
}
```

### Leetcode

- [[235. Lowest Common Ancestor of a BST]]
    

---

## Delete Node in BST

**Syntax**

```java
TreeNode deleteNode(TreeNode root, int key) {
    if (root == null) return null;
    if (key < root.val)
        root.left = deleteNode(root.left, key);
    else if (key > root.val)
        root.right = deleteNode(root.right, key);
    else {
        if (root.left == null) return root.right;
        if (root.right == null) return root.left;
        TreeNode min = findMin(root.right);
        root.val = min.val;
        root.right = deleteNode(root.right, min.val);
    }
    return root;
}
```

---

# BST Inorder Property

> [!TIP]  
> Inorder traversal of BST → **Sorted array**

---

# Tree Problem Recognition Guide

|Problem asks|Use|
|---|---|
|Level wise|BFS|
|Bottom up|Postorder|
|Path related|DFS|
|Sorted tree|BST|
|Distance|LCA|

---

# Final Advice

> [!TIP]  
> Learn **traversals deeply** — everything else builds on them.

---

## ✅ If you master THIS:

- Trees will stop being scary
    
- Recursion becomes natural
    
- BST logic feels obvious
    

---

If you want next:

- Graphs (complete notes)
    
- DP on Trees
    
- Iterative tree traversals
    
- Tree interview cheat sheet
    

Just tell me 👊
```

```
---


