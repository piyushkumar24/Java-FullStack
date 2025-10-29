# Chapter 2: Java Basics

## Overview

This chapter covers the foundational concepts of Java programming, focusing on how code execution works under the hood. You'll learn about:

- **Classes and Objects**: The blueprint-instance relationship that forms the backbone of Java
- **Memory Management**: Stack vs Heap memory allocation
- **Data Types**: Primitives vs Wrappers
- **Control Flow**: Loops and basic program structure
- **The JVM**: How Java Virtual Machine executes your code

**Why This Matters**: Understanding these concepts isn't just about writing syntactically correct code—it's about knowing what happens in your computer's memory when your program runs. This knowledge is crucial for debugging, optimization, and technical interviews.

---

## Concept Map: Java Program Execution Flow
```
┌─────────────────────────────────────────────────────────────┐
│                    JAVA SOURCE CODE                         │
│                    (Test.java)                              │
└──────────────────────┬──────────────────────────────────────┘
                       │
                       ▼
              ┌────────────────┐
              │ Java Compiler  │
              │   (javac)      │
              └────────┬───────┘
                       │
                       ▼
              ┌────────────────┐
              │   Bytecode     │
              │ (Test.class)   │
              └────────┬───────┘
                       │
                       ▼
    ┌──────────────────────────────────────────┐
    │    Java Virtual Machine (JVM)            │
    │                                          │
    │  ┌─────────────┐    ┌────────────────┐  │
    │  │   STACK     │    │     HEAP       │  │
    │  │             │    │                │  │
    │  │ Function    │    │   Objects      │  │
    │  │ Calls       │    │   (c1, c2)     │  │
    │  │ Variables   │    │                │  │
    │  │ (int x)     │    │   Cleared by   │  │
    │  │             │    │   Garbage      │  │
    │  │ LIFO/FILO   │    │   Collection   │  │
    │  │ Push/Pop    │    │                │  │
    │  └─────────────┘    └────────────────┘  │
    │                                          │
    └──────────────────────────────────────────┘
                       │
                       ▼
              ┌────────────────┐
              │    Output      │
              │ (Hello World)  │
              └────────────────┘
```

---

## 1. The Anatomy of a Java Program

### 1.1 Basic Structure
```java
public class Test {
    public static void main(String[] args) {
        System.out.println("Hello World");
    }
}
```

**Breaking it down:**

- **`public`**: Access modifier - this class can be accessed from anywhere
- **`class`**: Keyword to define a template/blueprint
- **`Test`**: Class name (must match filename: Test.java)
- **`main` method**: Entry point of the program - JVM looks for this specific method to start execution

### 1.2 Why `public static void main(String[] args)`?
```
┌─────────────────────────────────────────────────────┐
│  public  │  static  │  void   │  main  │ String[]  │
├──────────┼──────────┼─────────┼────────┼───────────┤
│ Visible  │ Can call │ Returns │ JVM    │ Command   │
│ to all   │ without  │ nothing │ entry  │ line      │
│ classes  │ object   │         │ point  │ arguments │
└──────────┴──────────┴─────────┴────────┴───────────┘
```

**Why `static`?**  
When the JVM runs your program, it hasn't created any objects yet. It needs a method it can call directly without instantiating the class. That's why `main` must be `static`.

**Example:**
```java
public class Test {
    // JVM calls this without: Test t = new Test();
    public static void main(String[] args) {
        System.out.println(args[0]); // First command-line argument
        System.out.println(args[1]); // Second command-line argument
    }
}
```

**Running:**
```bash
javac Test.java
java Test hello world
# Output:
# hello
# world
```

---

## 2. Classes and Objects: The Blueprint-Instance Relationship

### 2.1 Understanding Classes

A **class** is a template or blueprint. Think of it as a car design document.
```java
class Car {
    int tires;
    int seats;
    
    void drive() {
        // Procedure to drive the car
        System.out.println("Driving...");
    }
}
```

### 2.2 Creating Objects

An **object** is an instance of a class. It's an actual car built from the blueprint.
```java
Car c1 = new Car();  // c1 is an object of Car class
Car c2 = new Car();  // c2 is another object
```

**Real-world analogy:**
- **Class**: Human (blueprint)
- **Objects**: You, me, billions of people (instances)

### 2.3 Visualization: Class vs Object
```
CLASS (Blueprint)                    OBJECTS (Instances)
┌────────────────┐                  ┌─────────────────┐
│     Car        │                  │  c1: Car        │
│ ─────────────  │    creates →     │  tires: 4       │
│ int tires      │                  │  seats: 5       │
│ int seats      │                  └─────────────────┘
│ drive()        │                  ┌─────────────────┐
└────────────────┘    creates →     │  c2: Car        │
                                    │  tires: 4       │
                                    │  seats: 2       │
                                    └─────────────────┘
```

---

## 3. Memory Management: Stack vs Heap

### 3.1 The Two Memory Regions
```
┌───────────────────────────────────────────────────────┐
│                    RAM Memory                         │
├─────────────────────────┬─────────────────────────────┤
│       STACK             │          HEAP               │
├─────────────────────────┼─────────────────────────────┤
│ • Function calls        │ • Objects                   │
│ • Local variables       │ • Class instances           │
│ • Method parameters     │ • Shared across threads     │
│ • LIFO (Last In First)  │ • Garbage collected         │
│ • Thread-specific       │ • Slower access             │
│ • Fast access           │ • Larger size               │
│ • Small size            │                             │
│                         │                             │
│ Example:                │ Example:                    │
│ ┌─────────────┐         │ ┌──────────────┐            │
│ │   f2()      │ ← pop   │ │ c1: Car obj  │            │
│ ├─────────────┤         │ │ tires: 4     │            │
│ │   f1()      │ ← pop   │ │ seats: 5     │            │
│ │ int x = 2   │         │ └──────────────┘            │
│ └─────────────┘         │ ┌──────────────┐            │
│                         │ │ c2: Car obj  │            │
│                         │ └──────────────┘            │
└─────────────────────────┴─────────────────────────────┘
```

### 3.2 Stack Memory in Action
```java
void f1() {
    int x = 2;              // x stored in stack
    System.out.println("Hello");
    f2();                   // f2 pushed onto stack
}

void f2() {
    System.out.println("World");
}  // f2 popped from stack, then f1 popped
```

**Stack Operation:**
1. `f1()` is **pushed** onto stack
2. Variable `x` allocated in stack
3. `f2()` is **pushed** onto stack (on top of f1)
4. `f2()` completes → **popped** from stack
5. `f1()` completes → **popped** from stack

**LIFO (Last In, First Out)**: The last function pushed is the first to be popped.

### 3.3 Heap Memory in Action
```java
Car c1 = new Car();  // c1 goes to HEAP
Car c2 = new Car();  // c2 goes to HEAP
```

- Objects are stored in **heap memory**
- Each object has a **memory address** (hexadecimal value)
- Heap is **shared** across all threads
- Objects remain until **garbage collection** cleans them up

### 3.4 Memory Addresses

When you create an object, it gets stored at a specific memory location with an address like:
```
c1 → 0x7f9a1b2c3d4e (memory address in heap)
```

If you print the object directly:
```java
System.out.println(c1);  // Output: Car@7f9a1b2c3d4e
```

---

## 4. Data Types: Primitives vs Wrappers

### 4.1 Primitive Data Types

These are **built-in** types that come with Java:

| Type      | Size     | Range (approx)        | Example      |
|-----------|----------|-----------------------|--------------|
| `int`     | 4 bytes  | -2³¹ to 2³¹-1         | `int x = 10` |
| `long`    | 8 bytes  | -2⁶³ to 2⁶³-1         | `long y = 100000L` |
| `double`  | 8 bytes  | Decimal numbers       | `double d = 3.14` |
| `float`   | 4 bytes  | Decimal numbers       | `float f = 3.14f` |
| `char`    | 2 bytes  | Single character      | `char c = 'A'` |
| `boolean` | 1 bit    | true/false            | `boolean b = true` |
| `byte`    | 1 byte   | -128 to 127           | `byte b = 127` |
| `short`   | 2 bytes  | -32,768 to 32,767     | `short s = 1000` |

**Memory Representation:**
```
int x = 10;

Stack Memory:
┌─────────────────┐
│ x: 10           │  (4 bytes = 32 bits)
│ [00000000000000000000000000001010]
└─────────────────┘
```

### 4.2 Wrapper Classes

Wrappers are **classes** that wrap primitives and provide additional functionality:

| Primitive | Wrapper Class |
|-----------|---------------|
| `int`     | `Integer`     |
| `long`    | `Long`        |
| `double`  | `Double`      |
| `float`   | `Float`       |
| `char`    | `Character`   |
| `boolean` | `Boolean`     |

**Why use wrappers?**
- They provide **utility methods** (e.g., `Integer.toString()`)
- Required for **Collections** (ArrayList, HashMap, etc.)
- Can be `null` (primitives cannot)

**Example:**
```java
// Primitive
int a = 10;

// Wrapper - provides extra methods
Integer b = Integer.valueOf(10);
String str = Integer.toString(a);  // Convert to String
int max = Integer.MAX_VALUE;       // Get max int value
```

### 4.3 Static Methods in Wrappers
```java
// No object creation needed!
String numStr = Integer.toString(123);  // Static method
```

Why no object? Because `toString()` is declared as `static`:
```java
public class Integer {
    public static String toString(int i) {
        // ...
    }
}
```

---

## 5. The String Class

### 5.1 String Basics

A **String** is a wrapper for character arrays:
```java
String name = "Lovpreet Singh";
```

**String is immutable** - once created, it cannot be changed.

### 5.2 String Memory Allocation
```
Heap Memory:
┌──────────────────────────┐
│ "Lovpreet Singh"         │ ← Stored as object
└──────────────────────────┘
         ↑
         │
Stack Memory:
┌──────────────────────────┐
│ name (reference)         │ ← Points to heap
└──────────────────────────┘
```

---

## 6. Control Flow: Loops

### 6.1 For Loop

**Syntax:**
```java
for (initialization; condition; increment) {
    // code to repeat
}
```

**Example:**
```java
for (int i = 1; i <= 10; i++) {
    System.out.println(i);
}
```

**Breakdown:**
1. `int i = 1` → Initialize counter
2. `i <= 10` → Continue while true
3. `i++` → Increment after each iteration
4. Loop body executes 10 times (1 to 10)

**Variations:**
```java
// Count by 2s
for (int i = 0; i < 10; i += 2) {
    System.out.println(i);  // 0, 2, 4, 6, 8
}

// Count down
for (int i = 10; i > 0; i--) {
    System.out.println(i);  // 10, 9, 8, ..., 1
}
```

### 6.2 While Loop

**Syntax:**
```java
while (condition) {
    // code to repeat
}
```

**Example:**
```java
int i = 1;
while (i <= 10) {
    System.out.println(i);
    i++;
}
```

**Key Difference from For Loop:**
- Variables declared **outside** the loop
- Increment must be **manual**

### 6.3 Do-While Loop

Executes **at least once** even if condition is false:
```java
int i = 1;
do {
    System.out.println(i);
    i++;
} while (i <= 10);
```

---

## 7. Practical Examples

### 7.1 Printing Arguments
```java
public class Test {
    public static void main(String[] args) {
        System.out.println(args[0]);  // First argument
        System.out.println(args[1]);  // Second argument
    }
}
```

**Running:**
```bash
javac Test.java
java Test hello world
# Output:
# hello
# world
```

### 7.2 Data Type Conversion
```java
public class Test {
    public static void main(String[] args) {
        int a = 10;
        String str = Integer.toString(a);  // "10"
        System.out.println(str);
    }
}
```

### 7.3 Nested Loops - Pattern Printing

**Problem:** Print this pattern:
```
*
**
***
****
```

**Solution:**
```java
public class Test {
    public static void main(String[] args) {
        char star = '*';
        
        // Outer loop: controls rows (4 rows)
        for (int i = 0; i < 4; i++) {
            // Inner loop: prints stars in each row
            // First row: j goes from 1 to i+1 (1 time)
            // Second row: j goes from 1 to i+1 (2 times)
            // Third row: j goes from 1 to i+1 (3 times)
            // Fourth row: j goes from 1 to i+1 (4 times)
            for (int j = 1; j <= i + 1; j++) {
                System.out.print(star);
            }
            System.out.println();  // New line after each row
        }
    }
}
```

**How it works:**
```
Iteration 1: i=0, j runs from 1 to 1 → prints * (1 star)
Iteration 2: i=1, j runs from 1 to 2 → prints ** (2 stars)
Iteration 3: i=2, j runs from 1 to 3 → prints *** (3 stars)
Iteration 4: i=3, j runs from 1 to 4 → prints **** (4 stars)
```

---

## 8. Interview Preparation Tips

### 8.1 Common Interview Questions

1. **What is the difference between JDK, JRE, and JVM?**
   - **JDK**: Java Development Kit (compiler + libraries + JRE)
   - **JRE**: Java Runtime Environment (JVM + libraries)
   - **JVM**: Java Virtual Machine (executes bytecode)

2. **What is a process?**
   - A **running program** that uses CPU, memory (RAM), and storage

3. **What is the difference between stack and heap memory?**
   - **Stack**: Stores function calls, local variables; LIFO; thread-specific
   - **Heap**: Stores objects; shared across threads; garbage collected

4. **Why is `main` method `static`?**
   - So JVM can call it **without creating an object** of the class

5. **What is the difference between `==` and `.equals()`?**
   - `==`: Compares memory addresses (reference equality)
   - `.equals()`: Compares actual content (value equality)

6. **What is garbage collection?**
   - Automatic memory management that removes unused objects from heap

7. **What is the difference between `int` and `Integer`?**
   - `int`: Primitive type (4 bytes)
   - `Integer`: Wrapper class with utility methods

8. **What does `static` mean?**
   - Belongs to the **class**, not instances; can be accessed without creating objects

### 8.2 Key Concepts to Emphasize

- **Memory efficiency**: Understanding stack vs heap shows you care about performance
- **Object lifecycle**: Know when objects are created and destroyed
- **Static vs instance**: Critical for design decisions
- **Immutability**: Strings are immutable - explain why this matters

---

## 9. Common Mistakes or Misunderstandings

### 9.1 Mistake: Confusing `i++` and `++i`
```java
int i = 0;
System.out.println(i++);  // Prints 0, then increments to 1
System.out.println(++i);  // Increments to 2, then prints 2
```

**Rule:**
- **Post-increment (`i++`)**: Use current value, then increment
- **Pre-increment (`++i`)**: Increment first, then use new value

### 9.2 Mistake: Thinking Strings are Primitives
```java
String s1 = "hello";
String s2 = "hello";
System.out.println(s1 == s2);  // true (same reference in string pool)

String s3 = new String("hello");
System.out.println(s1 == s3);  // false (different objects)
System.out.println(s1.equals(s3));  // true (same content)
```

### 9.3 Mistake: Not Understanding `static`
```java
class Test {
    int x = 10;  // Instance variable
    
    public static void main(String[] args) {
        System.out.println(x);  // ERROR! Cannot access non-static from static
    }
}
```

**Fix:**
```java
class Test {
    static int x = 10;  // Now it's static
    
    public static void main(String[] args) {
        System.out.println(x);  // Works!
    }
}
```

### 9.4 Mistake: Forgetting Semicolons
```java
int x = 10  // ERROR! Missing semicolon
```

Java requires semicolons at the end of statements.

### 9.5 Mistake: Using Single Quotes for Strings
```java
char c = 'A';      // Correct (single character)
String s = "ABC";  // Correct (multiple characters)
char c2 = "A";     // ERROR! Use single quotes
String s2 = 'ABC'; // ERROR! Use double quotes
```

---

## 10. Tooling & IDE Integration

### 10.1 Visual Studio Code Setup

**Required Extensions:**
- **Extension Pack for Java** (Microsoft)
- **Debugger for Java**

**Compiling and Running:**
```bash
# Compile
javac Test.java

# Run
java Test

# With arguments
java Test arg1 arg2 arg3
```

### 10.2 IntelliJ IDEA Features

- **Auto-import**: Automatically imports classes
- **Live templates**: Type `psvm` + Tab → generates `public static void main`
- **Debugging**: Set breakpoints, inspect variables

### 10.3 Eclipse Features

- **Quick Fix**: Ctrl+1 for suggestions
- **Code formatting**: Ctrl+Shift+F
- **Run configurations**: Save argument configurations

---

## 11. Advanced Notes / Behind the Scenes

### 11.1 How Bytecode Works
```
Java Source (.java) → Bytecode (.class) → JVM → Machine Code
```

**Why bytecode?**
- **Platform independence**: Same bytecode runs on Windows, Mac, Linux
- **Security**: JVM can verify bytecode before execution
- **Optimization**: JIT compiler optimizes at runtime

### 11.2 Method Overloading

You can have multiple methods with the same name but different parameters:
```java
class Calculator {
    int add(int a, int b) {
        return a + b;
    }
    
    double add(double a, double b) {
        return a + b;
    }
    
    int add(int a, int b, int c) {
        return a + b + c;
    }
}
```

### 11.3 Access Modifiers

| Modifier    | Class | Package | Subclass | World |
|-------------|-------|---------|----------|-------|
| `public`    | ✓     | ✓       | ✓        | ✓     |
| `protected` | ✓     | ✓       | ✓        | ✗     |
| `default`   | ✓     | ✓       | ✗        | ✗     |
| `private`   | ✓     | ✗       | ✗        | ✗     |

### 11.4 The `this` Keyword

Refers to the current object:
```java
class Car {
    int seats;
    
    Car(int seats) {
        this.seats = seats;  // Disambiguate parameter from field
    }
}
```

---

## 12. Homework Problem

**Problem:** Print this pattern:
```
    *
   ***
  *****
 *******
```

**Hints:**
- You need **spaces** before stars (use `' '` character)
- Row 1: 3 spaces, 1 star
- Row 2: 2 spaces, 3 stars
- Row 3: 1 space, 5 stars
- Row 4: 0 spaces, 7 stars

**Approach:**
1. Outer loop for rows (4 iterations)
2. Inner loop 1: Print spaces (decreasing each row)
3. Inner loop 2: Print stars (increasing odd numbers: 1, 3, 5, 7)

---

## Glossary

- **Bytecode**: Intermediate code that JVM executes
- **Class**: Blueprint or template for creating objects
- **Garbage Collection**: Automatic memory management that removes unused objects
- **Heap**: Memory region for storing objects
- **JVM (Java Virtual Machine)**: Executes Java bytecode
- **Object**: Instance of a class
- **Primitive**: Basic data type built into the language
- **Process**: A running program
- **Stack**: Memory region for function calls and local variables (LIFO)
- **Static**: Belongs to the class, not instances
- **Wrapper**: Class that wraps a primitive and adds functionality

---

## Footnotes

1. **Thread Safety**: The heap is shared, but each thread has its own stack
2. **String Pool**: Java optimizes string storage by reusing identical string literals
3. **Autoboxing**: Java automatically converts between primitives and wrappers:
```java
   Integer i = 10;  // Autoboxing (int → Integer)
   int j = i;       // Unboxing (Integer → int)
```
4. **Platform-Specific**: Memory addresses may vary between operating systems and JVM implementations

---

## Quick Reference Commands
```bash
# Compile Java file
javac Filename.java

# Run compiled class
java Filename

# Run with arguments
java Filename arg1 arg2

# Check Java version
java -version

# Check compiler version
javac -version
```

---
