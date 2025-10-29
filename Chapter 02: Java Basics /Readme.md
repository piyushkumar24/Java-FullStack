# 🧩 Chapter 2: Introduction to Java Basics & OOPs Concepts ☕

---

## 📘 Overview
Java is a **pure object-oriented programming language** designed around the concept of **classes and objects**. Every piece of code in Java resides inside a class, and every action is performed through an **object**.

In this chapter, we’ll explore how memory works in Java (**Stack vs Heap**), the role of `main()` and static methods, and how Java handles **primitive** and **reference** types.

---

## 🧭 Concept Map
```
           ┌──────────────────────────┐
           │        Class             │
           └────────────┬─────────────┘
                        │ creates
                        ▼
           ┌──────────────────────────┐
           │        Object            │
           └────────────┬─────────────┘
                        │ stored in
           ┌─────────────┴─────────────┐
           │         Memory            │
           │  (Stack & Heap Areas)     │
           └─────────────┬─────────────┘
                        │ uses
           ┌─────────────┴─────────────┐
           │   Variables & Methods     │
           │ (Primitive, Reference)    │
           └─────────────┬─────────────┘
                        │ manages
                        ▼
           ┌──────────────────────┐
           │  Static & Wrapper    │
           │   Concepts in Java   │
           └──────────────────────┘
```

---

## 🧩 Detailed Sections

### ☕ 1. What is a Class?
A **class** is a blueprint or template that defines the **structure** and **behavior** (data and methods) of objects.  
It is a **user-defined data type** that tells the compiler **what** the object will contain and **how** it will behave.

**Example:**
```
java
class Dog {
    String breed;
    int age;

    void bark() {
        System.out.println("Woof!");
    }
}
```

Here, `Dog` is a class containing:  
- Data members → `breed`, `age`  
- Method → `bark()`

---

### 🐶 2. What is an Object?
An **object** is a **real-world entity** created from a class.  
It occupies **memory** and represents a specific instance of that class.

**Example:**
```
java
Dog d1 = new Dog();  // Object creation
```

Here:  
- `Dog` → Class  
- `d1` → Reference variable (points to the object)  
- `new Dog()` → Allocates memory for the object  

---

### 🧠 3. Stack vs Heap Memory
In Java, memory is divided mainly into **Stack** and **Heap**.

| Memory Type | Stores | Lifetime | Access |
|--------------|---------|-----------|---------|
| **Stack** | Local variables, method calls | Temporary (until method ends) | Fast |
| **Heap** | Objects and instance variables | Until garbage collected | Slower |

**Example:**
```
java
int x = 10;      // stored in Stack
Dog d = new Dog(); // reference (d) in Stack, object in Heap
```

💡 When a method is called, its local variables go on the **stack**. When it ends, the **stack frame** is destroyed.

---

### 🔢 4. Primitive vs Reference Types

| Type | Stored Where | Example | Description |
|------|---------------|----------|--------------|
| **Primitive** | Stack | `int`, `char`, `boolean`, etc. | Stores actual value |
| **Reference** | Heap | Objects, Arrays, Strings | Stores address (memory reference) |

**Example:**
```
java
int a = 5;          // primitive (value stored directly)
Dog d1 = new Dog(); // reference (address to heap object)
```

---

### 🧱 5. Wrapper Classes & Autoboxing
Java provides **wrapper classes** for every primitive type.

| Primitive | Wrapper |
|------------|----------|
| `int` | `Integer` |
| `char` | `Character` |
| `double` | `Double` |
| `boolean` | `Boolean` |

**Autoboxing:** Automatically converting a primitive type to its wrapper class.  
```
java
int num = 10;
Integer obj = num;  // Autoboxing
```

**Unboxing:** Automatically converting a wrapper to primitive.  
```
java
Integer val = 5;
int n = val;  // Unboxing
```

---

### ⚙️ 6. Static Methods and Memory Sharing
`static` methods and variables belong to the **class** rather than individual objects.  
Only **one copy** exists in memory.

**Example:**
```
java
class MathUtils {
    static int square(int x) {
        return x * x;
    }
}

System.out.println(MathUtils.square(5)); // called without object
```

💡 Static variables are stored in a special memory area called the **Method Area**.

---

### 🧩 7. How Methods Are Called Internally
When a method is called:
1. A **stack frame** is created.  
2. Local variables and return addresses are pushed to the **stack**.  
3. If the method uses objects, references point to **heap memory**.  
4. When the method completes, the stack frame is removed.

**Example:**
```
java
class Demo {
    static void printMessage() {
        System.out.println("Hello Java");
    }

    public static void main(String[] args) {
        printMessage(); // Stack frame created for printMessage
    }
}
```

---

### 💡 8. The `new` Keyword & Object Creation Flow
When you write:
```
java
Student s1 = new Student();
```

It performs:
1. Allocates memory in **heap** for `Student`  
2. Initializes fields to **default values**  
3. Calls **constructor**  
4. Returns reference stored in variable `s1`

---

### 🧮 9. The `main()` Method Explained
```
java
public static void main(String[] args)
```

| Keyword | Meaning |
|----------|----------|
| **public** | Accessible from JVM |
| **static** | Called without creating an object |
| **void** | Does not return any value |
| **String[] args** | Command-line arguments |

💬 JVM starts execution from `main()` method.

---

## 💻 Practical Example
```
java
class Student {
    String name;
    int age;

    void showDetails() {
        System.out.println("Name: " + name + ", Age: " + age);
    }
}

public class Main {
    public static void main(String[] args) {
        Student s1 = new Student();
        s1.name = "Piyush";
        s1.age = 21;
        s1.showDetails();
    }
}
```

**Output:**
```
Name: Piyush, Age: 21
```

🧠 Here, `s1` is stored in **stack**, while its data (`name`, `age`) live in **heap**.

---

## 🎯 Interview Preparation Tips
- Difference between **class** and **object**  
- Difference between **stack** and **heap memory**  
- What are **wrapper classes** and **autoboxing**?  
- Why is **main()** method **static**?  
- Can static methods access instance variables? (**No, they require an object**)  
- Explain **object creation process** in Java  

---

## ⚠️ Common Mistakes
🚫 Forgetting `new` keyword when creating objects.  
🚫 Trying to access non-static members from static methods.  
🚫 Confusing primitive vs reference variable behavior.  
🚫 Assuming all data is stored on the stack.  

---

## 🧰 Tooling & IDE Integration
🧩 In **IntelliJ IDEA / Eclipse**:
- Use “Show Memory View” or **Debugger** to visualize Stack & Heap.  
- “Static Analysis” helps identify unused static variables.  
- “Auto-complete” shows method suggestions from wrapper classes.  

---

## 🧠 Advanced Notes
- All classes in Java **inherit from `Object` class** by default.  
- Java’s **Garbage Collector** automatically frees memory from unused heap objects.  
- Java uses **Pass-by-Value** for all method arguments (even for objects, where the value is the reference).  
- **Static blocks** can initialize static data before `main()` executes.  

---

## 📖 Glossary

| Term | Description |
|------|--------------|
| **Class** | Blueprint defining variables and methods |
| **Object** | Instance of a class stored in heap memory |
| **Stack Memory** | Temporary memory for local variables and method calls |
| **Heap Memory** | Long-term storage for objects |
| **Wrapper Class** | Object representation of primitive types |
| **Autoboxing** | Automatic conversion from primitive → object |
| **Static** | Belongs to class, shared among all objects |
| **main()** | Entry point for program execution |
| **Garbage Collector** | Automatic memory management system |

---
