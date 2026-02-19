# <font color="red">List (Interface)</font>

**Syntax**

`List<Type> list = new ArrayList<>(); List<Type> list = new LinkedList<>();`

# Important Methods

1. `list.add(element)`
    
2. `list.addAll(collection)`
    
3. `list.get(index)`
    
4. `list.remove(index)`
    
5. `list.indexOf(element)`
    
6. `list.lastIndexOf(element)`
    
7. `list.subList(start, end)`
    
8. `list.iterator()`
    
9. `list.listIterator()`
    

## Use Case

- Parent interface for `ArrayList`, `LinkedList`
    
- Enables **polymorphism**
    
- Switching implementations easily
    
- Cleaner code design
    

> [!NOTE]  
> Prefer `List` reference over implementation for flexibility

### Leetcode problem number and name to check

1. [[1431. Kids With the Greatest Number of Candies]]
    
2. [[1470. Shuffle the Array]]
    

---

# <font color="red">Arrays</font>

**Syntax**

`int[] arr = new int[n]; String[] str = new String[n];`

# Important Methods (java.util.Arrays)

1. `Arrays.sort(arr)`
    
2. `Arrays.binarySearch(arr, key)`
    
3. `Arrays.equals(arr1, arr2)`
    
4. `Arrays.fill(arr, value)`
    
5. `Arrays.copyOf(arr, newLength)`
    
6. `Arrays.toString(arr)`
    
7. `Arrays.asList(arr)`
    

## Use Case

- Fixed-size data
    
- Faster than collections
    
- Low memory overhead
    
- Used in competitive programming
    

> [!WARNING]  
> `Arrays.asList()` returns **fixed-size list** – cannot add/remove elements

### Leetcode problem number and name to check

1. [[1. Two Sum]]
    
2. [[977. Squares of a Sorted Array]]
    
3. [[169. Majority Element]]
    

---

If you want, next I can do:

- `LinkedList`
    
- `Stack / Queue / Deque`
    
- `HashSet / TreeSet`
    
- `Map + Iterator + ListIterator`
    
-