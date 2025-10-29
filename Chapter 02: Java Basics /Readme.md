# ☕ Chapter 2: Introduction to Java Basics

---

## 📘 Overview
This chapter introduces the foundational concepts of **Object-Oriented Programming (OOP)** in **Java**, including classes, objects, memory management, wrapper types, and method behavior. You’ll understand how Java handles data and code internally, and how memory (stack and heap) plays a vital role in object creation and execution.

---

## 🧭 Concept Map
Java Class → Blueprint for Object  
↓  
Object → Instance of Class (stored in Heap)  
↓  
Memory Management:  
• Stack → Primitive variables, references, method calls  
• Heap → Objects and their data  
↓  
Static Members → Shared by all objects  
↓  
Wrapper Classes → Convert primitives to objects  

---

## 🧩 Detailed Sections

### 🔹 What is a Class?
A **class** in Java is a **blueprint** or **template** that defines properties (data) and behaviors (functions or methods).

```
```java
class Student {
    String name;
    int roll;
    int marks;
}
```
```

This defines a structure, but **no memory is allocated** yet.

---

### 🔹 What is an Object?
An **object** is an **instance** of a class — a real entity created using the `new` keyword.

```
```java
Student s1 = new Student();
s1.name = "Piyush";
s1.roll = 1;
s1.marks = 95;
```
```

Each object has its own copy of the data members.

---

### 🔹 Memory Allocation — Stack vs Heap
| Type | Stores | Lifetime | Example |
|------|---------|-----------|----------|
| **Stack** | Method calls, primitive variables, object references | Temporary (cleared after function ends) | `int x = 10` |
| **Heap** | Actual objects created using `new` | Persistent until Garbage Collected | `new Student()` |

---

### 🔹 Primitive vs Reference Types
- **Primitive types:** `int`, `float`, `char`, `boolean`, etc. — stored directly in **stack memory**.  
- **Reference types:** store **addresses** (references) that point to objects in **heap memory**.

---

### 🔹 Garbage Collection
Java automatically deletes unreferenced objects using its **Garbage Collector (GC)**. You don’t need to manually free memory.

---

### 🔹 Wrapper Classes
Wrapper classes convert primitives into objects (used in Collections, generics, etc.).

| Primitive | Wrapper Class |
|------------|---------------|
| `int` | `Integer` |
| `float` | `Float` |
| `char` | `Character` |
| `boolean` | `Boolean` |

Example:
```
```java
int a = 5;
Integer obj = a; // Auto-boxing
int b = obj;     // Unboxing
```
```

---

## 💻 Practical Example

```
```java
class Car {
    String brand;
    int speed;

    void accelerate() {
        speed += 10;
        System.out.println(brand + " speed: " + speed);
    }
}

public class Main {
    public static void main(String[] args) {
        Car c1 = new Car();
        c1.brand = "Tesla";
        c1.speed = 100;
        c1.accelerate();

        Car c2 = new Car();
        c2.brand = "BMW";
        c2.speed = 120;
        c2.accelerate();
    }
}
```
```

Output:
```
Tesla speed: 110
BMW speed: 130
```

---

## 🎯 Interview Preparation Tips

✅ Explain difference between **class** and **object**.  
✅ Draw **stack vs heap** diagram when explaining memory.  
✅ Know **autoboxing/unboxing**.  
✅ Mention that **static members** belong to the class, not object.  
✅ Be clear on **Garbage Collection** concept.  

---

## ⚠️ Common Mistakes

❌ Thinking that class occupies memory before object creation.  
❌ Confusing primitive copy vs reference copy.  
❌ Forgetting that wrapper objects are immutable.  
❌ Assuming `==` compares values (it compares references for objects).  

---

## 🛠️ Tooling & IDE Integration

- Use **IntelliJ IDEA** or **VS Code** for Java with debugger support.  
- Use **Memory View / Heap Dump** tools to visualize object allocation.  
- **JVisualVM** (bundled with JDK) helps monitor heap memory and GC activity.

---

## 🧠 Advanced Notes

- **Objects** are stored in **heap**, but their **references** are in **stack**.  
- **Static methods** can’t access non-static members directly.  
- **finalize()** is deprecated; GC is automatic.  
- Wrapper classes are part of `java.lang` and immutable.

---

## 🧾 Glossary

| Term | Definition |
|------|-------------|
| **Class** | Blueprint for creating objects |
| **Object** | Instance of a class with state and behavior |
| **Stack Memory** | Stores method calls and references |
| **Heap Memory** | Stores dynamically created objects |
| **Garbage Collector** | Frees unreferenced objects automatically |
| **Wrapper Class** | Object representation of primitive type |

---
