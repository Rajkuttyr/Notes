Alright, let’s lock in **`Queue` in `java.util`** cleanly and exam-ready 👇  
(No fluff, but I’ll add practical notes where it helps.)

---

## 📦 `Queue` in `java.util`

### What is `Queue`?

> A **FIFO (First In, First Out)** data structure interface in Java.

- Elements are **inserted at the rear**
    
- Elements are **removed from the front**
    

```java
import java.util.Queue;
```

⚠️ `Queue` is an **interface**, not a class.

---

## 🧬 Class hierarchy (important)

```text
Iterable
  ↓
Collection
  ↓
Queue
     ↓
     Deque
```

---

## ✅ Common Implementations

|Class|Use case|
|---|---|
|`LinkedList`|Normal queue|
|`ArrayDeque`|Fast, recommended|
|`PriorityQueue`|Priority-based|
|`ConcurrentLinkedQueue`|Thread-safe|

---

## 🧠 Core Queue Methods (VERY IMPORTANT)

### 1️⃣ Insert element

|Method|Behavior|
|---|---|
|`add(e)`|Throws exception if fails|
|`offer(e)`|Returns `false` if fails|

```java
queue.add(10);
queue.offer(20);
```

---

### 2️⃣ Remove element

|Method|Behavior|
|---|---|
|`remove()`|Throws exception if empty|
|`poll()`|Returns `null` if empty|

```java
queue.remove();
queue.poll();
```

---

### 3️⃣ View front element

|Method|Behavior|
|---|---|
|`element()`|Exception if empty|
|`peek()`|`null` if empty|

```java
queue.peek();
queue.element();
```

---

## 🔄 Method Comparison Table (EXAM FAVORITE)

|Operation|Exception|Safe|
|---|---|---|
|Insert|`add()`|`offer()`|
|Remove|`remove()`|`poll()`|
|Peek|`element()`|`peek()`|

---

## 🧪 Example: Simple Queue

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Queue<Integer> q = new ArrayDeque<>();

        q.offer(10);
        q.offer(20);
        q.offer(30);

        System.out.println(q.poll()); // 10
        System.out.println(q.peek()); // 20
    }
}
```

---

## ⭐ `ArrayDeque` vs `LinkedList`

|Feature|ArrayDeque|LinkedList|
|---|---|---|
|Performance|Faster|Slower|
|Memory|Less|More|
|Thread-safe|❌|❌|
|Recommended|✅|❌|

👉 **Use `ArrayDeque` unless you need list operations.**

---

## 🎯 `PriorityQueue` (IMPORTANT VARIANT)

```java
Queue<Integer> pq = new PriorityQueue<>();
pq.offer(30);
pq.offer(10);
pq.offer(20);

System.out.println(pq.poll()); // 10
```

- Not FIFO
    
- Ordered by **natural order** or **Comparator**
    

---

## ⏱️ Time Complexity

|Operation|Complexity|
|---|---|
|Insert|O(1)|
|Remove|O(1)|
|Peek|O(1)|

⚠️ `PriorityQueue`: Insert & remove → **O(log n)**

---

## ❌ What Queue does NOT allow

- ❌ Random access (`get(i)`)
    
- ❌ `null` elements (in most implementations)
    

---

## 🎤 Interview one-liner

> **`Queue` is a FIFO data structure interface in `java.util`, commonly implemented using `ArrayDeque` or `LinkedList`, with safe and exception-based method pairs.**

---

=Nice, this is a **core Java + interview favorite** topic.  
Below is **EVERY Queue method from `java.util.Queue`**, with **syntax + short example + behavior**.

---

# 📋 `java.util.Queue` — ALL METHODS

```java
import java.util.Queue;
import java.util.ArrayDeque;
```

```java
Queue<Integer> q = new ArrayDeque<>();
```

---

## 🟢 INSERT METHODS

### 1️⃣ `boolean add(E e)`

👉 Inserts element  
❌ Throws exception if fails

```java
q.add(10);
```

---

### 2️⃣ `boolean offer(E e)`

👉 Inserts element safely  
✅ Returns `false` if fails

```java
q.offer(20);
```

---

## 🔴 REMOVE METHODS

### 3️⃣ `E remove()`

👉 Removes front element  
❌ Throws `NoSuchElementException` if empty

```java
int x = q.remove();
```

---

### 4️⃣ `E poll()`

👉 Removes front element safely  
✅ Returns `null` if empty

```java
Integer x = q.poll();
```

---

## 👀 PEEK / ACCESS METHODS

### 5️⃣ `E element()`

👉 Returns front element  
❌ Throws exception if empty

```java
int x = q.element();
```

---

### 6️⃣ `E peek()`

👉 Returns front element safely  
✅ Returns `null` if empty

```java
Integer x = q.peek();
```

---

## 🔵 METHODS FROM `Collection` (Queue inherits these)

### 7️⃣ `int size()`

```java
int n = q.size();
```

---

### 8️⃣ `boolean isEmpty()`

```java
if (q.isEmpty()) {
    System.out.println("Queue empty");
}
```

---

### 9️⃣ `boolean contains(Object o)`

```java
q.contains(10);
```

---

### 🔟 `boolean remove(Object o)`

👉 Removes specific element (NOT front)

```java
q.remove(20);
```

---

### 1️⃣1️⃣ `void clear()`

```java
q.clear();
```

---

### 1️⃣2️⃣ `Iterator<E> iterator()`

```java
for (int x : q) {
    System.out.println(x);
}
```

---

### 1️⃣3️⃣ `Object[] toArray()`

```java
Object[] arr = q.toArray();
```

---

### 1️⃣4️⃣ `<T> T[] toArray(T[] a)`

```java
Integer[] arr = q.toArray(new Integer[0]);
```

---

### 1️⃣5️⃣ `boolean addAll(Collection<? extends E> c)`

```java
q.addAll(List.of(1, 2, 3));
```

---

### 1️⃣6️⃣ `boolean containsAll(Collection<?> c)`

```java
q.containsAll(List.of(1, 2));
```

---

### 1️⃣7️⃣ `boolean removeAll(Collection<?> c)`

```java
q.removeAll(List.of(1, 2));
```

---

### 1️⃣8️⃣ `boolean retainAll(Collection<?> c)`

```java
q.retainAll(List.of(3, 4));
```

---

## ⚠️ IMPORTANT RULES (EXAM GOLD)

|Situation|Use|
|---|---|
|Avoid exception|`offer()`, `poll()`, `peek()`|
|Strict FIFO|`ArrayDeque`|
|Priority needed|`PriorityQueue`|
|Thread-safe|`ConcurrentLinkedQueue`|

---

## 🧠 MOST ASKED INTERVIEW TABLE

|Operation|Exception|Safe|
|---|---|---|
|Insert|`add()`|`offer()`|
|Remove|`remove()`|`poll()`|
|Peek|`element()`|`peek()`|

---

## 🧪 COMPLETE MINI PROGRAM

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Queue<Integer> q = new ArrayDeque<>();

        q.offer(10);
        q.offer(20);
        q.offer(30);

        System.out.println(q.peek());   // 10
        System.out.println(q.poll());   // 10
        System.out.println(q.size());   // 2
        System.out.println(q.isEmpty()); // false
    }
}
```

---

## 🎤 One-line interview answer

> **Queue in `java.util` provides FIFO operations using paired exception-based and safe methods like `add/offer`, `remove/poll`, and `element/peek`.**

---

If you want next:

- 🔥 **Deque (ALL methods like this)**
    
- 🧠 **PriorityQueue deep dive**
    
- 💡 **BFS / Sliding Window using Queue**
    
- 📄 **Downloadable PDF notes**
    

=Ju

