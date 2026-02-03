Love this request 🔥
Here’s a **📘 Complete Java Collections Cheat Sheet** in **clean Markdown**, styled **exactly like your notes** but **more polished, colorful, and exam/LeetCode friendly**.

You can **directly paste this into Obsidian / GitHub**.

---

# <font color="red">Java Collections Framework – Complete Cheat Sheet</font>

---

## <font color="blue">Collection Hierarchy</font>

```
Iterable
 └── Collection
     ├── List
     │    ├── ArrayList
     │    ├── LinkedList
     │    └── Vector
     ├── Set
     │    ├── HashSet
     │    ├── LinkedHashSet
     │    └── TreeSet
     └── Queue
          ├── PriorityQueue
          ├── ArrayDeque
          └── LinkedList

Map (separate hierarchy)
 ├── HashMap
 ├── LinkedHashMap
 ├── TreeMap
 └── Hashtable
```

---

# <font color="red">List</font>

**Syntax**

```java
List<Type> list = new ArrayList<>();
```

### Important Methods

* `add(e)`
* `add(index,e)`
* `get(index)`
* `set(index,e)`
* `remove(index)`
* `size()`
* `contains(e)`
* `subList(start,end)`
* `listIterator()`

### Use Case

* Ordered collection
* Allows duplicates
* Index-based access

---

# <font color="red">ArrayList</font>

**Syntax**

```java
ArrayList<Type> list = new ArrayList<>();
```

### Important Methods

* `add(e)`
* `get(i)`
* `set(i,e)`
* `remove(i)`
* `clear()`

### Use Case

* Fast read operations
* Dynamic array
* Sliding window problems

> [!TIP]
> Best when **read > write**

---

# <font color="red">LinkedList</font>

**Syntax**

```java
LinkedList<Type> list = new LinkedList<>();
```

### Important Methods

* `addFirst(e)`
* `addLast(e)`
* `removeFirst()`
* `removeLast()`
* `getFirst()`
* `getLast()`

### Use Case

* Frequent insert/delete
* Stack & Queue implementation

---

# <font color="red">Set</font>

**Syntax**

```java
Set<Type> set = new HashSet<>();
```

### Important Methods

* `add(e)`
* `remove(e)`
* `contains(e)`
* `size()`
* `isEmpty()`

### Use Case

* Unique elements
* Remove duplicates

---

# <font color="red">HashSet</font>

**Syntax**

```java
HashSet<Type> set = new HashSet<>();
```

### Use Case

* Fast lookup
* No order maintained

---

# <font color="red">LinkedHashSet</font>

**Syntax**

```java
LinkedHashSet<Type> set = new LinkedHashSet<>();
```

### Use Case

* Maintains insertion order
* Unique elements

---

# <font color="red">TreeSet</font>

**Syntax**

```java
TreeSet<Type> set = new TreeSet<>();
```

### Important Methods

* `first()`
* `last()`
* `higher(e)`
* `lower(e)`

### Use Case

* Sorted set
* Range queries

> [!WARNING]
> Slower than HashSet (O(log n))

---

# <font color="red">Queue</font>

**Syntax**

```java
Queue<Type> q = new LinkedList<>();
```

### Important Methods

* `offer(e)`
* `poll()`
* `peek()`

### Use Case

* FIFO operations
* BFS

---

# <font color="red">PriorityQueue</font>

**Syntax**

```java
PriorityQueue<Type> pq = new PriorityQueue<>();
```

### Important Methods

* `offer(e)`
* `poll()`
* `peek()`

### Use Case

* Heap implementation
* Top K problems

---

# <font color="red">Deque</font>

**Syntax**

```java
Deque<Type> dq = new ArrayDeque<>();
```

### Important Methods

* `addFirst(e)`
* `addLast(e)`
* `removeFirst()`
* `removeLast()`

### Use Case

* Sliding window
* Stack & Queue both

---

# <font color="red">Map</font>

**Syntax**

```java
Map<K,V> map = new HashMap<>();
```

### Important Methods

* `put(k,v)`
* `get(k)`
* `getOrDefault(k,0)`
* `containsKey(k)`
* `keySet()`
* `values()`
* `entrySet()`

### Use Case

* Key-value storage
* Frequency counting

---

# <font color="red">HashMap</font>

**Use Case**

* Fast lookup
* No order

---

# <font color="red">LinkedHashMap</font>

**Use Case**

* Maintains insertion order
* LRU Cache

---

# <font color="red">TreeMap</font>

**Use Case**

* Sorted keys
* Range-based queries

---

# <font color="red">Iterator</font>

**Syntax**

```java
Iterator<Type> it = collection.iterator();
```

### Methods

* `hasNext()`
* `next()`
* `remove()`

---

# <font color="red">ListIterator</font>

**Syntax**

```java
ListIterator<Type> it = list.listIterator();
```

### Methods

* `hasNext()`
* `hasPrevious()`
* `next()`
* `previous()`
* `add(e)`
* `set(e)`

> [!NOTE]
> Can traverse **both directions**

---

# <font color="red">Arrays (Utility Class)</font>

### Important Methods

* `Arrays.sort(arr)`
* `Arrays.binarySearch(arr,key)`
* `Arrays.fill(arr,val)`
* `Arrays.toString(arr)`
* `Arrays.copyOf(arr,len)`
* `Arrays.asList(arr)`

---

# <font color="green">When to Use What?</font>

| Requirement    | Use           |
| -------------- | ------------- |
| Fast access    | ArrayList     |
| Insert/Delete  | LinkedList    |
| Unique values  | HashSet       |
| Ordered unique | LinkedHashSet |
| Sorted         | TreeSet       |
| Key-Value      | HashMap       |
| Sorted Map     | TreeMap       |
| Heap           | PriorityQueue |

---


