Alright, Trie time 🌲  
This is **high-yield, interview-ready Trie notes**—exactly what you need for **LeetCode + GFG + contests**.

---

# 🌲 Trie (Prefix Tree) — Complete Notes

## 🔹 What is a Trie?

A **Trie** (pronounced _try_) is a **tree-based data structure** used to store **strings**, where:

- Each node represents a **character**
    
- Paths from root form **words**
    
- Common prefixes are stored **once**
    

📌 Also called **Prefix Tree**

---

## 🔹 Why Trie? (Why not HashSet?)

|Operation|HashSet|Trie|
|---|---|---|
|Search word|O(L)|O(L)|
|Prefix search|❌|✅|
|Auto-complete|❌|✅|
|Memory|Low|Higher|
|Lexicographic order|❌|✅|

👉 Trie shines when **prefix queries** are needed.

---

## 🔹 Trie Node Structure

### Typical Node

```java
class TrieNode {
    TrieNode[] children = new TrieNode[26];
    boolean isEnd;
}
```

### Root Node

- Empty character
    
- Acts as starting point
    

---

## 🔹 Core Operations (Must Know)

### 1️⃣ Insert Word — O(L)

```java
public void insert(String word) {
    TrieNode node = root;
    for (char c : word.toCharArray()) {
        int idx = c - 'a';
        if (node.children[idx] == null) {
            node.children[idx] = new TrieNode();
        }
        node = node.children[idx];
    }
    node.isEnd = true;
}
```

📌 Mark `isEnd = true` only at **last character**

---

### 2️⃣ Search Word — O(L)

```java
public boolean search(String word) {
    TrieNode node = root;
    for (char c : word.toCharArray()) {
        int idx = c - 'a';
        if (node.children[idx] == null) return false;
        node = node.children[idx];
    }
    return node.isEnd;
}
```

✔ Ensures **exact word exists**

---

### 3️⃣ Prefix Search (`startsWith`) — O(L)

```java
public boolean startsWith(String prefix) {
    TrieNode node = root;
    for (char c : prefix.toCharArray()) {
        int idx = c - 'a';
        if (node.children[idx] == null) return false;
        node = node.children[idx];
    }
    return true;
}
```

✔ Does NOT check `isEnd`

---

## 🔹 Complete Trie Implementation (LeetCode Ready)

```java
class Trie {

    class TrieNode {
        TrieNode[] children = new TrieNode[26];
        boolean isEnd;
    }

    TrieNode root;

    public Trie() {
        root = new TrieNode();
    }

    public void insert(String word) {
        TrieNode node = root;
        for (char c : word.toCharArray()) {
            int idx = c - 'a';
            if (node.children[idx] == null)
                node.children[idx] = new TrieNode();
            node = node.children[idx];
        }
        node.isEnd = true;
    }

    public boolean search(String word) {
        TrieNode node = root;
        for (char c : word.toCharArray()) {
            int idx = c - 'a';
            if (node.children[idx] == null) return false;
            node = node.children[idx];
        }
        return node.isEnd;
    }

    public boolean startsWith(String prefix) {
        TrieNode node = root;
        for (char c : prefix.toCharArray()) {
            int idx = c - 'a';
            if (node.children[idx] == null) return false;
            node = node.children[idx];
        }
        return true;
    }
}
```

---

## 🔹 Time & Space Complexity

|Operation|Complexity|
|---|---|
|Insert|O(L)|
|Search|O(L)|
|Prefix|O(L)|
|Space|O(Σ characters)|

L = length of word

---

## 🔹 Advanced Trie Variants (High Priority)

### 🔥 1. Trie with Frequency Count

Used in:

- Longest Common Prefix
    
- Prefix frequency problems
    

```java
int count;
```

---

### 🔥 2. Trie for XOR (Bitwise Trie)

Used in:

- Maximum XOR of two numbers
    
- Subarray XOR problems
    

```java
TrieNode[] children = new TrieNode[2]; // bits 0,1
```

---

### 🔥 3. Delete Word from Trie (Tricky!)

Requires **backtracking**

Idea:

- Unmark `isEnd`
    
- Remove node only if:
    
    - No children
        
    - Not end of another word
        

---

### 🔥 4. Auto Complete / Suggestions

DFS from prefix node

---

## 🔹 Common LeetCode Problems (Must Do)

|Problem|Concept|
|---|---|
|Implement Trie|Basics|
|Longest Common Prefix|Prefix traversal|
|Replace Words|Prefix match|
|Word Search II|Trie + DFS|
|Maximum XOR|Bit Trie|
|Map Sum Pairs|Prefix sum|

---

## 🔹 Common Mistakes ❌

🚫 Forgetting `isEnd` check  
🚫 Not initializing children  
🚫 Using HashMap instead of array (slower)  
🚫 Deleting nodes wrongly  
🚫 Confusing prefix vs full word

---

## 🧠 Interview Cheat Sheet

✔ Trie = Prefix problems  
✔ Fixed alphabet → Array[26]  
✔ Dynamic charset → HashMap  
✔ Words only → `isEnd`  
✔ Prefix only → no `isEnd` check

---

If you want next:

- 🔥 **Trie + DFS (Word Search II)**
    
- 🔥 **Bitwise Trie (XOR problems)**
    
- 🧠 **Trie deletion (step-by-step)**
    
- 🧾 **Obsidian-ready markdown notes**
    

Just say which one 🚀




