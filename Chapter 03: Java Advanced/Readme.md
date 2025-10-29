# 📘 Chapter 3: Java Advanced: Collections Framework — Arrays, List, Set, Map, Generics & Optionals

---

## 🌟 Overview
In this chapter, we will learn the most important data structures and concepts from **Java’s Collections Framework**, including:

- **Arrays vs Lists**
- **List** and **ArrayList**
- **Set** and **HashSet**
- **Immutable Lists**
- **Map** and **HashMap**
- **Generics**
- **Optionals**
- **Interface vs Class**

Understanding these topics gives us the power to handle data efficiently in Java — making our code cleaner, safer, and enterprise-ready.

---

## 🧭 Concept Map

```text
📦 Collection (Interface)
│
├── 🗂️ List (Interface)
│   ├── 📋 ArrayList
│   └── 🔗 LinkedList
│
├── 🧱 Set (Interface)
│   ├── 🧩 HashSet
│   └── 🌲 TreeSet
│
└── 🗺️ Map (Interface)
    ├── 🧭 HashMap
    └── 🌳 TreeMap

```

---

## 📘 1. Arrays vs Lists

### 🔹 Arrays
- Fixed size once declared  
- Can store both primitive and object data  
- Access elements using index  
- Faster, but less flexible  

Example:
int[] arr = {1, 2, 3};
System.out.println(arr[1]); // 2

### 🔹 Lists
- Dynamic size — grows and shrinks automatically  
- Can only store objects (not primitives directly)  
- Provides rich methods like add(), remove(), contains()  

Example:
import java.util.*;

List<Integer> list = new ArrayList<>();
list.add(10);
list.add(20);
System.out.println(list.get(1)); // 20

### ✅ Key Differences

| Feature | Array | List |
|----------|--------|------|
| Size | Fixed | Dynamic |
| Type | Can store primitives | Only objects |
| Performance | Slightly faster | More flexible |
| Belongs to | Core Java | Collections Framework |

---

## 📗 2. List and ArrayList

### 🔹 What is a List?
A **List** is an ordered collection that allows **duplicate elements** and provides **index-based access**.

### 🔹 ArrayList
`ArrayList` is a **resizable array** that automatically grows as elements are added.

Example:
import java.util.*;

public class Main {
    public static void main(String[] args) {
        List<String> names = new ArrayList<>();
        names.add("Piyush");
        names.add("Riya");
        names.add("Piyush"); // duplicates allowed
        System.out.println(names); // [Piyush, Riya, Piyush]
    }
}

Key Points:
✅ Maintains insertion order  
✅ Allows duplicates  
✅ Provides random access using index  
⚠️ Not synchronized (use Vector or Collections.synchronizedList() for thread safety)

---

## 📙 3. Set and HashSet

### 🔹 What is a Set?
A **Set** is an **unordered collection** that does **not allow duplicates**.

### 🔹 HashSet
`HashSet` uses a **hash table** internally to store unique elements.

Example:
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Set<String> names = new HashSet<>();
        names.add("Piyush");
        names.add("Riya");
        names.add("Piyush"); // ignored (duplicate)
        System.out.println(names); // [Riya, Piyush] (order not guaranteed)
    }
}

Key Points:
✅ Does not allow duplicates  
⚡ Faster lookups due to hashing  
⚠️ No guaranteed order of elements  

---

## 📒 4. Immutable List

### 🔹 What is an Immutable List?
An **Immutable List** cannot be modified after creation — useful for read-only or constant data.

Example:
import java.util.*;

public class Main {
    public static void main(String[] args) {
        List<String> names = List.of("Piyush", "Riya", "Aman");
        // names.add("Neha"); // UnsupportedOperationException
        System.out.println(names);
    }
}

Key Points:
✅ Fixed and read-only data  
✅ Thread-safe by design  
⚠️ Cannot add/remove elements after creation  

---

## 🧩 5. Map and HashMap

### 🔹 What is a Map?
A **Map** stores data in **key–value pairs**. Each key is unique, and each maps to exactly one value.

### 🔹 HashMap
`HashMap` is an implementation of `Map` that uses **hashing** for fast access.

Example:
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Map<Integer, String> map = new HashMap<>();
        map.put(1, "Piyush");
        map.put(2, "Riya");
        map.put(1, "Aman"); // key 1 overwritten
        System.out.println(map); // {1=Aman, 2=Riya}
    }
}

Key Points:
✅ Stores data in key-value pairs  
✅ Keys are unique  
✅ Allows null keys and values  
⚠️ Order not guaranteed  

---

## 🧮 6. Generics

### 🔹 What are Generics?
Generics ensure **type safety** by enforcing that collections only hold specific types.

Example:
import java.util.*;

public class Main {
    public static void main(String[] args) {
        List<Integer> numbers = new ArrayList<>();
        numbers.add(10);
        // numbers.add("Hello"); // Compile-time error
        System.out.println(numbers);
    }
}

Key Points:
✅ Ensures compile-time type safety  
✅ Removes need for type casting  
✅ Increases code reliability  

---

## 💡 7. Optionals

### 🔹 What is Optional?
`Optional` is a container that may or may not hold a non-null value — used to avoid `NullPointerException`.

Example:
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Optional<String> name = Optional.of("Piyush");
        System.out.println(name.isPresent()); // true
        System.out.println(name.get()); // Piyush

        Optional<String> empty = Optional.empty();
        System.out.println(empty.orElse("Default")); // Default
    }
}

Key Points:
✅ Prevents NullPointerExceptions  
✅ Encourages safe null handling  
✅ Provides methods like isPresent(), orElse(), ifPresent()  

---

## 🧱 8. Interface vs Class

### 🔹 Interface
- Defines a **contract** of methods that must be implemented by classes.  
- Cannot have method implementations (except default/static).  
- Used to achieve **abstraction** and **multiple inheritance**.

Example:
interface Animal {
    void sound();
}

class Dog implements Animal {
    public void sound() {
        System.out.println("Woof!");
    }
}

### 🔹 Class
- Defines **data members and methods** together.  
- Can have both implemented and non-implemented methods.  
- Used to create **objects**.

Example:
class Cat {
    void sound() {
        System.out.println("Meow!");
    }
}

### ✅ Key Differences

| Feature | Interface | Class |
|----------|------------|-------|
| Purpose | Defines behavior | Defines implementation |
| Variables | public static final | instance or static |
| Methods | abstract (by default) | fully implemented |
| Object Creation | Not possible | Possible |
| Inheritance | Multiple | Single |

---

## 🎯 Summary
- **Arrays** → Fixed size  
- **List** → Ordered, duplicates allowed  
- **Set** → Unordered, unique elements  
- **Map** → Key-value pairs  
- **Immutable List** → Read-only collection  
- **Generics** → Type-safe collections  
- **Optional** → Safe null handling  
- **Interface vs Class** → Abstraction vs Implementation  

---

## 🧠 Interview Tips
💬 Common Questions:
1. Difference between Array and List?  
2. How does HashMap handle key collisions?  
3. Difference between List, Set, and Map?  
4. What are Generics and why use them?  
5. What is Optional and when to use it?  
6. Interface vs Abstract Class?  

---

## ⚙️ Tooling & IDE Tips
- Use **Ctrl + P** in IntelliJ to view generic types.  
- Use **Debugger** to see HashMap entries in memory.  
- Try **List.of()** and **Set.of()** for immutable collections.  
- Hover over code in IDE to see inferred types with Generics.  

---

## 🚀 Advanced Notes
- Prefer `LinkedHashSet` for maintaining order without duplicates.  
- Use `ConcurrentHashMap` for thread-safe operations.  
- `Optional` improves functional programming with `ifPresent()`.  
- Immutable collections were added in **Java 9+** (`List.of()` etc.).  

---

## 📘 Glossary
| Term | Description |
|------|--------------|
| Array | Fixed-size sequential data storage |
| Collection | Root interface for data structures |
| List | Ordered collection allowing duplicates |
| Set | Unordered, unique element collection |
| Map | Key–value pair structure |
| Generics | Type-safe mechanism for collections |
| Optional | Wrapper to handle null safely |
| Interface | Blueprint defining behavior |
| Class | Structure implementing logic and data |

---
