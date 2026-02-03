🔥 **THIS is a solid move for DSA mastery.**
You’re basically building a **pattern-based DSA playbook** — exactly how top coders think.

Below is a **📘 DSA Techniques Cheat Sheet** written **strictly in YOUR format**:

* 🔴 Colored title
* ✅ **Syntax**
* ⭐ **Important steps / methods**
* 🧠 **Use cases**
* 🧪 **LeetCode problems**
* Clean **Markdown (.md)**, Obsidian-friendly

---

# <font color="red">Two Pointer Technique</font>

**Syntax**

```java
int left = 0;
int right = arr.length - 1;

while (left < right) {
    // logic
    left++;
    right--;
}
```

# Important Ideas

1. Move pointers based on condition
2. Works on sorted arrays or strings
3. Reduces O(n²) → O(n)

## Use Case

* Pair sum
* Reverse array/string
* Palindrome check
* Remove duplicates

### Leetcode problem number and name to check

1. [[167. Two Sum II - Input Array Is Sorted]]
2. [[125. Valid Palindrome]]
3. [[344. Reverse String]]

---

# <font color="red">Sliding Window (Fixed Size)</font>

**Syntax**

```java
int windowSum = 0;
int k = 3;

for (int i = 0; i < arr.length; i++) {
    windowSum += arr[i];

    if (i >= k - 1) {
        // use windowSum
        windowSum -= arr[i - (k - 1)];
    }
}
```

# Important Ideas

1. Window size is constant
2. Avoid recomputing sum
3. O(n) time

## Use Case

* Max/Min sum subarray of size k
* Average of subarrays
* Fixed window problems

### Leetcode problem number and name to check

1. [[643. Maximum Average Subarray I]]
2. [[2461. Maximum Sum of Distinct Subarrays With Length K]]

---

# <font color="red">Sliding Window (Variable Size)</font>

**Syntax**

```java
int left = 0;

for (int right = 0; right < n; right++) {
    // expand window

    while (condition) {
        // shrink window
        left++;
    }
}
```

# Important Ideas

1. Window size changes
2. Shrink when condition breaks
3. Two pointers inside loop

## Use Case

* Longest substring
* Smallest subarray
* Frequency-based problems

### Leetcode problem number and name to check

1. [[3. Longest Substring Without Repeating Characters]]
2. [[76. Minimum Window Substring]]

---

# <font color="red">Fast & Slow Pointer (Linked List)</font>

**Syntax**

```java
ListNode slow = head;
ListNode fast = head;

while (fast != null && fast.next != null) {
    slow = slow.next;
    fast = fast.next.next;
}
```

# Important Ideas

1. Fast moves 2x speed
2. Detect cycles
3. Find middle node

## Use Case

* Cycle detection
* Middle of linked list
* Palindrome linked list

### Leetcode problem number and name to check

1. [[141. Linked List Cycle]]
2. [[876. Middle of the Linked List]]
3. [[234. Palindrome Linked List]]

---

# <font color="red">Monotonic Stack</font>

**Syntax (Increasing Stack)**

```java
Stack<Integer> st = new Stack<>();

for (int i = 0; i < n; i++) {
    while (!st.isEmpty() && st.peek() > arr[i]) {
        st.pop();
    }
    st.push(arr[i]);
}
```

# Important Ideas

1. Stack maintains order
2. Each element pushed & popped once
3. O(n) time

## Use Case

* Next Greater Element
* Histogram problems
* Stock span

### Leetcode problem number and name to check

1. [[496. Next Greater Element I]]
2. [[84. Largest Rectangle in Histogram]]
3. [[739. Daily Temperatures]]

---

# <font color="red">Tree Traversal Techniques</font>

---

## <font color="blue">Inorder Traversal</font>

**Syntax**

```java
void inorder(TreeNode root) {
    if (root == null) return;
    inorder(root.left);
    visit(root);
    inorder(root.right);
}
```

## Use Case

* BST sorted order

### Leetcode

1. [[94. Binary Tree Inorder Traversal]]

---

## <font color="blue">Preorder Traversal</font>

**Syntax**

```java
void preorder(TreeNode root) {
    if (root == null) return;
    visit(root);
    preorder(root.left);
    preorder(root.right);
}
```

## Use Case

* Tree copying
* Serialization

### Leetcode

1. [[144. Binary Tree Preorder Traversal]]

---

## <font color="blue">Postorder Traversal</font>

**Syntax**

```java
void postorder(TreeNode root) {
    if (root == null) return;
    postorder(root.left);
    postorder(root.right);
    visit(root);
}
```

## Use Case

* Tree deletion
* Bottom-up problems

### Leetcode

1. [[145. Binary Tree Postorder Traversal]]

---

# <font color="red">Level Order Traversal (BFS)</font>

**Syntax**

```java
Queue<TreeNode> q = new LinkedList<>();
q.offer(root);

while (!q.isEmpty()) {
    TreeNode node = q.poll();
    // visit node
    if (node.left != null) q.offer(node.left);
    if (node.right != null) q.offer(node.right);
}
```

## Use Case

* Shortest path
* Level-based problems

### Leetcode

1. [[102. Binary Tree Level Order Traversal]]

---

# <font color="green">DSA Pattern Tip</font>

> [!TIP]
> If you can **recognize the pattern**, the solution is already 50% done.

---

🔥 This is a **next-level DSA move**.  
You already covered core patterns — now these are the **“supporting techniques”** that actually decide whether you _solve_ the problem or get stuck.

Below are **ESSENTIAL DSA TECHNIQUES** that are **NOT the usual two-pointer / sliding window**, but are **required for almost EVERY DSA problem**.

Written **strictly in your format** ✅  
Markdown-ready, Obsidian-friendly 📘

---

# Frequency Counting

**Syntax**

```java
Map<Character, Integer> freq = new HashMap<>();

for (char c : s.toCharArray()) {
    freq.put(c, freq.getOrDefault(c, 0) + 1);
}
```

# Important Ideas

1. Convert problem to count-based logic
    
2. Avoid nested loops
    
3. Works with arrays, strings, windows
    

## Use Case

- Anagrams
    
- Majority element
    
- Character counting
    
- Window problems
    

### Leetcode problem number and name to check

1. [[242. Valid Anagram]]
    
2. [[169. Majority Element]]
    
3. [[438. Find All Anagrams in a String]]
    

---

# Prefix Sum

**Syntax**

```java
int[] prefix = new int[n];
prefix[0] = arr[0];

for (int i = 1; i < n; i++) {
    prefix[i] = prefix[i - 1] + arr[i];
}
```

# Important Ideas

1. Precompute cumulative data
    
2. Range queries in O(1)
    
3. Avoid repeated summation
    

## Use Case

- Subarray sum
    
- Range queries
    
- Sliding window optimization
    

### Leetcode problem number and name to check

1. [[560. Subarray Sum Equals K]]
    
2. [[724. Find Pivot Index]]
    

---

# Difference Array

**Syntax**

```java
int[] diff = new int[n + 1];

diff[l] += val;
diff[r + 1] -= val;
```

# Important Ideas

1. Lazy range updates
    
2. Convert back using prefix sum
    
3. O(1) range update
    

## Use Case

- Range update problems
    
- Flight bookings
    
- Array manipulation
    

### Leetcode problem number and name to check

1. [[1109. Corporate Flight Bookings]]
    

---

# Sorting as a Preprocessing Step

**Syntax**

```java
Arrays.sort(arr);
```

# Important Ideas

1. Enables two pointer
    
2. Groups duplicates
    
3. Simplifies logic
    

## Use Case

- Pair problems
    
- Greedy solutions
    
- Remove duplicates
    

### Leetcode problem number and name to check

1. [[15. 3Sum]]
    
2. [[56. Merge Intervals]]
    

---

# Greedy Choice Strategy

**Syntax (Pattern)**

```java
// Choose locally optimal decision
if (better(option1, option2)) {
    choose option1;
}
```

# Important Ideas

1. Local optimal → global optimal
    
2. Requires proof
    
3. Often combined with sorting
    

## Use Case

- Interval scheduling
    
- Resource allocation
    

### Leetcode problem number and name to check

1. [[435. Non-overlapping Intervals]]
    
2. [[55. Jump Game]]
    

---

# Binary Search on Answer

**Syntax**

```java
int low = min, high = max;

while (low <= high) {
    int mid = low + (high - low) / 2;
    if (isPossible(mid)) high = mid - 1;
    else low = mid + 1;
}
```

# Important Ideas

1. Search on result, not array
    
2. Monotonic condition
    
3. Reduces O(n²) → O(n log n)
    

## Use Case

- Optimization problems
    
- Capacity / minimum / maximum
    

### Leetcode problem number and name to check

1. [[875. Koko Eating Bananas]]
    
2. [[1011. Capacity To Ship Packages Within D Days]]
    

---

# Recursion Template

**Syntax**

```java
void solve(params) {
    if (baseCase) return;

    solve(nextState);
}
```

# Important Ideas

1. Base case is mandatory
    
2. Stack space matters
    
3. Think in terms of subproblem
    

## Use Case

- Tree problems
    
- Backtracking
    
- DFS
    

---

# Backtracking Template

**Syntax**

```java
void backtrack(path, options) {
    if (goalReached) {
        result.add(path);
        return;
    }

    for (choice : options) {
        makeChoice(choice);
        backtrack(path, options);
        undoChoice(choice);
    }
}
```

## Use Case

- Permutations
    
- Combinations
    
- Sudoku
    

### Leetcode problem number and name to check

1. [[46. Permutations]]
    
2. [[77. Combinations]]
    

---

# State Representation

**Syntax Idea**

```java
class State {
    int node;
    int mask;
    int cost;
}
```

# Important Ideas

1. Encode problem state
    
2. Used in BFS / DP
    
3. Prevent revisiting
    

## Use Case

- Graph problems
    
- Bitmask DP
    
- BFS shortest path
    

---

# Universal DSA Thinking Checklist

> [!TIP]  
> Before coding, ask:
> 
> 1. Can I sort?
>     
> 2. Can I use prefix / map?
>     
> 3. Can I reduce brute force?
>     
> 4. Is condition monotonic?
>     
> 5. Is this recursion / DP?
>     

---

If you want next 🔥:

- **Problem → Pattern mapping table**
    
- **DSA decision flowchart**
    
- **Mistakes checklist (why WA/TLE happens)**
    
- **Interview-only techniques**
    

Just tell me — we’ll build a **DSA master notebook** 📘🚀
