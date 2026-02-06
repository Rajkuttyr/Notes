```java
import java.util.*;

  

class Tree {

  

static class Node {

int data;

Node left, right;

  

Node(int data) {

this.data = data;

left = right = null;

}

}

  

// INSERT INTO BST

public static Node insertBST(Node root, int data) {

if (root == null) {

return new Node(data);

}

  

if (data < root.data) {

root.left = insertBST(root.left, data);

} else if (data > root.data) {

root.right = insertBST(root.right, data);

}

  

return root;

}

  

// PREORDER (Root Left Right)

public static void preOrder(Node root) {

if (root == null) return;

  

System.out.print(root.data + " ");

preOrder(root.left);

preOrder(root.right);

}

  

// INORDER (Left Root Right)

public static void inOrder(Node root) {

if (root == null) return;

  

inOrder(root.left);

System.out.print(root.data + " ");

inOrder(root.right);

}

  

// POSTORDER (Left Right Root)

public static void postOrder(Node root) {

if (root == null) return;

  

postOrder(root.left);

postOrder(root.right);

System.out.print(root.data + " ");

}

  

// LEVEL ORDER (BFS)

public static void levelOrder(Node root) {

if (root == null) return;

  

Queue<Node> q = new LinkedList<>();

q.add(root);

  

while (!q.isEmpty()) {

Node curr = q.poll();

System.out.print(curr.data + " ");

  

if (curr.left != null) q.add(curr.left);

if (curr.right != null) q.add(curr.right);

}

}

  

public static void main(String[] args) {

Scanner sc = new Scanner(System.in);

  

int n = sc.nextInt();

Node root = null;

  

for (int i = 0; i < n; i++) {

root = insertBST(root, sc.nextInt()); // IMPORTANT

}

  

System.out.println("PreOrder:");

preOrder(root);

  

System.out.println("\nInOrder:");

inOrder(root);

  

System.out.println("\nPostOrder:");

postOrder(root);

  

System.out.println("\nLevelOrder:");

levelOrder(root);

}

}
```