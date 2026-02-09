Perfect — this is exactly the right ask **one day before the test** 👍
Below is a **COMPLETE JAVA CODING PACK** with:

* ✅ **Clean templates**
* ✅ **Driver code**
* ✅ **Interview-safe**
* ✅ **Easy to recall under pressure**

You can **memorize structure**, not logic.

---

# 🟢 LEVEL 1 — CORE TEMPLATES (WITH DRIVER)

---

## 🔁 Two Pointers (Pair Sum)

```java
import java.util.*;

public class TwoPointersPairSum {
    public static boolean pairSum(int[] arr, int target) {
        Arrays.sort(arr);
        int l = 0, r = arr.length - 1;

        while (l < r) {
            int sum = arr[l] + arr[r];
            if (sum == target) return true;
            if (sum < target) l++;
            else r--;
        }
        return false;
    }

    public static void main(String[] args) {
        int[] arr = {2, 7, 11, 15};
        int target = 9;
        System.out.println(pairSum(arr, target));
    }
}
```

---

## 🪟 Sliding Window (Max Sum Subarray of Size K)

```java
public class SlidingWindow {
    public static int maxSum(int[] arr, int k) {
        int sum = 0, max = 0;

        for (int i = 0; i < k; i++)
            sum += arr[i];

        max = sum;

        for (int i = k; i < arr.length; i++) {
            sum += arr[i] - arr[i - k];
            max = Math.max(max, sum);
        }
        return max;
    }

    public static void main(String[] args) {
        int[] arr = {2, 1, 5, 1, 3, 2};
        System.out.println(maxSum(arr, 3));
    }
}
```

---

## 📚 Stack (Valid Parentheses)

```java
import java.util.*;

public class ValidParentheses {
    public static boolean isValid(String s) {
        Stack<Character> st = new Stack<>();

        for (char c : s.toCharArray()) {
            if (c == '(' || c == '{' || c == '[')
                st.push(c);
            else {
                if (st.isEmpty()) return false;
                char top = st.pop();
                if ((c == ')' && top != '(') ||
                    (c == '}' && top != '{') ||
                    (c == ']' && top != '['))
                    return false;
            }
        }
        return st.isEmpty();
    }

    public static void main(String[] args) {
        System.out.println(isValid("(){}[]"));
    }
}
```

---

## 🗂 HashMap (Subarray Sum = K)

```java
import java.util.*;

public class SubarraySumK {
    public static int subarraySum(int[] nums, int k) {
        Map<Integer, Integer> map = new HashMap<>();
        map.put(0, 1);

        int sum = 0, count = 0;

        for (int n : nums) {
            sum += n;
            if (map.containsKey(sum - k))
                count += map.get(sum - k);
            map.put(sum, map.getOrDefault(sum, 0) + 1);
        }
        return count;
    }

    public static void main(String[] args) {
        int[] nums = {1, 2, 3};
        System.out.println(subarraySum(nums, 3));
    }
}
```

---

# 🟡 LEVEL 2 — TREES / TRIE / SEGMENT TREE

---

## 🌳 Binary Tree (DFS + BFS)

```java
import java.util.*;

class TreeNode {
    int val;
    TreeNode left, right;
    TreeNode(int v) { val = v; }
}

public class BinaryTreeTemplate {

    static int maxDepth(TreeNode root) {
        if (root == null) return 0;
        return 1 + Math.max(maxDepth(root.left), maxDepth(root.right));
    }

    static void levelOrder(TreeNode root) {
        if (root == null) return;
        Queue<TreeNode> q = new LinkedList<>();
        q.add(root);

        while (!q.isEmpty()) {
            TreeNode node = q.poll();
            System.out.print(node.val + " ");
            if (node.left != null) q.add(node.left);
            if (node.right != null) q.add(node.right);
        }
    }

    public static void main(String[] args) {
        TreeNode root = new TreeNode(1);
        root.left = new TreeNode(2);
        root.right = new TreeNode(3);

        System.out.println("Depth: " + maxDepth(root));
        levelOrder(root);
    }
}
```

---

## 🔤 Trie (Complete)

```java
class TrieNode {
    TrieNode[] children = new TrieNode[26];
    boolean isEnd;
}

public class TrieTemplate {
    static TrieNode root = new TrieNode();

    static void insert(String word) {
        TrieNode cur = root;
        for (char c : word.toCharArray()) {
            int idx = c - 'a';
            if (cur.children[idx] == null)
                cur.children[idx] = new TrieNode();
            cur = cur.children[idx];
        }
        cur.isEnd = true;
    }

    static boolean search(String word) {
        TrieNode cur = root;
        for (char c : word.toCharArray()) {
            int idx = c - 'a';
            if (cur.children[idx] == null) return false;
            cur = cur.children[idx];
        }
        return cur.isEnd;
    }

    public static void main(String[] args) {
        insert("apple");
        System.out.println(search("apple"));
        System.out.println(search("app"));
    }
}
```

---

## 📏 Segment Tree (Range Sum)

```java
public class SegmentTree {
    int[] tree;
    int n;

    SegmentTree(int[] arr) {
        n = arr.length;
        tree = new int[4 * n];
        build(0, 0, n - 1, arr);
    }

    void build(int node, int l, int r, int[] arr) {
        if (l == r) {
            tree[node] = arr[l];
            return;
        }
        int mid = (l + r) / 2;
        build(2 * node + 1, l, mid, arr);
        build(2 * node + 2, mid + 1, r, arr);
        tree[node] = tree[2 * node + 1] + tree[2 * node + 2];
    }

    int query(int node, int l, int r, int ql, int qr) {
        if (qr < l || ql > r) return 0;
        if (ql <= l && r <= qr) return tree[node];
        int mid = (l + r) / 2;
        return query(2 * node + 1, l, mid, ql, qr)
             + query(2 * node + 2, mid + 1, r, ql, qr);
    }

    public static void main(String[] args) {
        int[] arr = {1, 3, 5, 7, 9};
        SegmentTree st = new SegmentTree(arr);
        System.out.println(st.query(0, 0, arr.length - 1, 1, 3));
    }
}
```

---

# 🔴 LEVEL 3 — GRAPHS (FULL TEMPLATE)

---

## 🌐 Graph (BFS + DFS + Cycle + Topo)

```java
import java.util.*;

public class GraphTemplate {
    static List<List<Integer>> graph;
    static boolean[] visited;

    static void dfs(int node) {
        visited[node] = true;
        System.out.print(node + " ");
        for (int nei : graph.get(node))
            if (!visited[nei])
                dfs(nei);
    }

    static void bfs(int start) {
        Queue<Integer> q = new LinkedList<>();
        q.add(start);
        visited[start] = true;

        while (!q.isEmpty()) {
            int node = q.poll();
            System.out.print(node + " ");
            for (int nei : graph.get(node))
                if (!visited[nei]) {
                    visited[nei] = true;
                    q.add(nei);
                }
        }
    }

    static boolean hasCycle(int node, int parent) {
        visited[node] = true;
        for (int nei : graph.get(node)) {
            if (!visited[nei]) {
                if (hasCycle(nei, node)) return true;
            } else if (nei != parent) return true;
        }
        return false;
    }

    static void topoSort(int n) {
        int[] indeg = new int[n];
        for (int i = 0; i < n; i++)
            for (int nei : graph.get(i))
                indeg[nei]++;

        Queue<Integer> q = new LinkedList<>();
        for (int i = 0; i < n; i++)
            if (indeg[i] == 0) q.add(i);

        while (!q.isEmpty()) {
            int node = q.poll();
            System.out.print(node + " ");
            for (int nei : graph.get(node)) {
                if (--indeg[nei] == 0)
                    q.add(nei);
            }
        }
    }

    public static void main(String[] args) {
        int n = 5;
        graph = new ArrayList<>();
        for (int i = 0; i < n; i++)
            graph.add(new ArrayList<>());

        graph.get(0).add(1);
        graph.get(1).add(2);
        graph.get(2).add(3);

        visited = new boolean[n];
        bfs(0);

        System.out.println("\nTopo:");
        topoSort(n);
    }
}
```

---

# 🧠 WHAT TO MEMORIZE (IMPORTANT)

* **Graph skeleton**
* **Tree recursion**
* **Sliding window loop**
* **HashMap prefix logic**

If you want next:

* 📄 **Single-file “EXAM TEMPLATE”**
* ⏱ **4-question mock test**
* 🔥 **Most common bugs checklist**

Just say the word 💪
