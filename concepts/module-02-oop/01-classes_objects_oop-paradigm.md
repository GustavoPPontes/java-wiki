# Classes, Objects and OOP Paradigm in Java

## What is a Programming Paradigm?

Before understanding Object-Oriented Programming, you need to understand what a **programming paradigm** is, because OOP is one specific paradigm among several.

A programming paradigm is a structural contract. It is a set of rules, abstractions, and mental models that governs how you organize code at a fundamental level. It does not just describe a style preference. It defines what the basic building block of a program is: an instruction, an object, a function, or a declaration. Different paradigms produce different ways of decomposing a problem and different ways of connecting the parts of a solution.

The four most common paradigms are:

| Paradigm | Fundamental building block | How logic is organized | Example languages |
|---|---|---|---|
| **Procedural** | Instruction | A sequence of commands executed top to bottom, grouped into functions | C, Pascal |
| **Object-Oriented (OOP)** | Object | Data and behavior bundled together into self-contained units | Java, C++, Python |
| **Functional** | Function | Data transformation through the application of pure functions, with no side effects | Haskell, Erlang, Clojure |
| **Declarative** | Declaration | You describe WHAT you want; the system decides HOW to get it | SQL, HTML |

Java is primarily an object-oriented language. That does not mean Java is incapable of other styles: a Java file can hold a `main` method with a sequence of instructions, which is procedural. Starting from Java 8, lambda expressions introduce functional patterns. But the core architecture of Java, its class system, its memory model, its standard library, was designed around OOP. To write Java well, you must understand why OOP exists and what structural problem it solves.

### A common beginner mistake about paradigms

Many beginners treat paradigms as rigid, mutually exclusive categories that define a language forever. They are not. A paradigm is the primary lens a language is designed around. Most modern languages support more than one, to different degrees. What matters is knowing which paradigm you are working in at any given moment, because it shapes every structural decision you make.

---

## Why Does OOP Exist? The Problem It Was Designed to Solve

To understand why OOP exists, you need to see the problem it solves in concrete terms. The problem lives in procedural code at scale.

Look at the following procedural-style code. It manages three support tickets using plain variables and static methods:

```java
public class TicketSystem {

    // Ticket 1 data
    static String ticket1Title = "Login page crashes on mobile";
    static String ticket1Status = "open";
    static int ticket1Priority = 2;

    // Ticket 2 data
    static String ticket2Title = "Profile picture not uploading";
    static String ticket2Status = "open";
    static int ticket2Priority = 1;

    // Ticket 3 data
    static String ticket3Title = "Password reset email not sending";
    static String ticket3Status = "open";
    static int ticket3Priority = 3;

    static void escalateTicket1() {
        ticket1Priority = ticket1Priority + 1;
    }

    static void closeTicket(int ticketNumber) {
        // Which variable do we update?
        // We have to write a separate branch for each ticket.
        if (ticketNumber == 1) {
            ticket1Status = "closed";
        } else if (ticketNumber == 2) {
            ticket2Status = "closed";
        } else if (ticketNumber == 3) {
            ticket3Status = "closed";
        }
    }

    public static void main(String[] args) {
        escalateTicket1();
        closeTicket(2);
    }
}
```

This code works for three tickets. Now imagine it works for three hundred. You need 300 groups of variables. Every method that operates on a ticket must either target a specific ticket by number (as `closeTicket` does) or be duplicated for each ticket. Adding a new ticket attribute, say `assignedAgent`, means editing every method that touches ticket data. There is no enforced connection between the data (the variables) and the behavior (the methods). Any method anywhere in the file can read or overwrite `ticket1Priority` without restriction. One typo in one method corrupts the wrong ticket, and the compiler does not warn you.

This is the core problem: **data and behavior are structurally disconnected.**

OOP solves this by making the connection between data and behavior a first-class rule of the language. Instead of having loose variables and separate functions, you create a single unit that holds both. That unit is an **object**. The template that defines what an object looks like is a **class**.

With OOP, you define the concept of a ticket once. Then you create as many independent ticket objects as you need, each holding its own data and each carrying its own behavior. The behavior travels with the data. Adding a new attribute means editing one place. Adding a new operation means adding one method to one class. The rest of the codebase does not break.

---

## Class: The Blueprint

A **class** is a source-code definition. It describes, in one place, two things: the data every object of this type will hold and the operations every object of this type can perform. The class itself is not a running thing. No memory is allocated for the data it describes when you write the class definition. The class is a compile-time artifact, a template that Java reads and uses later when you ask it to create an actual object.

Here is the `SupportTicket` class in its most basic form:

```java
public class SupportTicket {
    // We will fill this in across the next sections.
}
```

When the Java compiler processes this file, it registers that a type called `SupportTicket` exists. It notes what attributes and methods it will have. But no `SupportTicket` object exists in memory yet. Nothing is running. Nothing is allocated. The class definition is like an architectural blueprint: the blueprint describes a building, but no building exists until someone builds one from it.

### A critical distinction: class is not object

This is the most common confusion at this stage. A class is the definition. An object is the thing that exists in memory at runtime, built from that definition. You write a class once. You can create dozens of objects from it, each independent. Writing `public class SupportTicket` does not create a ticket. It tells Java what a ticket looks like.

If you try to access the data of a class as if the class itself were an object, the compiler will refuse:

```java
// This does not compile. SupportTicket is a class, not an object.
// There is no actual ticket in memory to access data from.
System.out.println(SupportTicket.title); // ERROR
```

You cannot read `title` from the class. You can only read `title` from a specific object created from that class. How you create objects is covered in the section on `new`.

---

## Attributes: The State of an Object

An **attribute** is a variable declared directly inside the class body, outside of any method. This is its defining location. Attributes describe what data each object will store. When Java creates an object from a class, it allocates a block of memory on the heap. Inside that block, it reserves a slot for each attribute. Each object gets its own independent copy of every attribute.

The term "attribute" is also called a "field" or "instance variable" in Java literature. All three names refer to the same thing. This text uses "attribute" throughout.

Add three attributes to `SupportTicket`:

```java
public class SupportTicket {
    String title;
    String status;
    int priority;
}
```

`title` holds the text that describes the problem. `status` holds whether the ticket is open, in progress, or closed. `priority` holds an integer where a higher number means a more urgent ticket.

These three attributes do not exist yet as real data in memory. They are declarations. They describe what data each future `SupportTicket` object will hold. The moment you create a `SupportTicket` object, Java allocates memory for that specific object and that specific object gets its own `title`, `status`, and `priority` slot. A second `SupportTicket` object gets a completely separate set of those three slots.

### Attributes vs. local variables: the difference that matters

A local variable is a variable declared inside a method. It exists only while that method is running. When the method returns, the local variable is gone. An attribute is different: it exists for the entire lifetime of the object. As long as the object exists in memory, its attributes exist.

```java
public class SupportTicket {
    String title;      // Attribute: lives as long as the object lives.
    String status;
    int priority;

    void processTicket() {
        int stepCount = 0;  // Local variable: exists only inside this method.
        stepCount = stepCount + 1;
        // When processTicket() returns, stepCount is gone.
        // title, status, and priority are unaffected and still exist.
    }
}
```

---

## Objects: The Instance

An **object** is a running, memory-resident copy of a class blueprint. The word "instance" means the same thing: one specific, concrete realization of the class in memory. When you create two objects from the same class, each occupies its own space in the heap. Each holds its own copy of every attribute. They do not share attribute values.

As noted in the section on `new` (coming shortly), the full mechanism of how an object is created in memory is covered there. For now, focus on what an object IS, not yet on all the steps that create it.

After creating two ticket objects:

```java
SupportTicket ticket1 = new SupportTicket("Login page crashes on mobile", 2);
SupportTicket ticket2 = new SupportTicket("Profile picture not uploading", 1);
```

`ticket1` and `ticket2` are two independent objects. Each has its own `title`, `status`, and `priority`. Changing `ticket1.priority` does not touch `ticket2.priority`:

```java
ticket1.priority = 5;

System.out.println(ticket1.priority); // Prints: 5
System.out.println(ticket2.priority); // Prints: 1 (unchanged)
```

This is the structural guarantee OOP provides. Each object owns its data. No other object can accidentally overwrite it by targeting the wrong variable name.

---

## Methods: The Behavior of an Object

A **method** is a block of code declared inside the class body. It defines an operation that any object of that class can perform. When you call a method on a specific object, the Java Virtual Machine (JVM) executes that block in the context of that object's attribute values. The method has direct access to the attributes of the object it was called on.

Add two methods to `SupportTicket`:

```java
public class SupportTicket {
    String title;
    String status;
    int priority;

    void escalate() {
        priority = priority + 1;
    }

    String getSummary() {
        return "Ticket: " + title + " | Priority: " + priority + " | Status: " + status;
    }
}
```

`escalate()` increases the priority of the ticket by 1. `getSummary()` reads the three attributes and returns them as a single formatted string.

Trace what happens when you call `ticket1.escalate()`:

1. The JVM receives the instruction `ticket1.escalate()`.
2. It locates the memory block for `ticket1`.
3. It executes the `escalate()` code in the context of `ticket1`'s data.
4. Inside `escalate()`, `priority = priority + 1` reads `ticket1.priority` (which is 2) and writes the result (3) back to `ticket1.priority`.
5. The method returns.

```java
System.out.println(ticket1.getSummary());
// Prints: Ticket: Login page crashes on mobile | Priority: 2 | Status: null

ticket1.escalate();

System.out.println(ticket1.getSummary());
// Prints: Ticket: Login page crashes on mobile | Priority: 3 | Status: null
```

Notice `Status: null`. The `status` attribute was never initialized. That problem is exactly what the constructor solves.

### A method is not a standalone function

A method always belongs to a class and always runs against a specific object's data. The question "which ticket's priority do I increase?" is answered by the object you call the method on. In the procedural code shown earlier, `escalateTicket1()` was hardcoded to one ticket. The method approach replaces the repetition with a single definition that works for any ticket object.

---

## Constructor: The Initialization Method

When Java creates a new object, it allocates memory and sets each attribute to a default value: `null` for String attributes, `0` for int attributes, `false` for boolean attributes. Those defaults are technically valid Java, but they are almost never meaningful for your application. A `SupportTicket` with a `null` title and a status of `null` is not a useful starting state.

The **constructor** solves this. A constructor is a special method that Java calls automatically, immediately after allocating memory for a new object. Its job is to set the initial values of the object's attributes. It has two structural rules that distinguish it from every other method:

1. Its name must be identical to the class name.
2. It has no return type (not even `void`).

Add a constructor to `SupportTicket`:

```java
public class SupportTicket {
    String title;
    String status;
    int priority;

    SupportTicket(String title, int priority) {
        this.title = title;
        this.priority = priority;
        this.status = "open";
    }

    void escalate() {
        priority = priority + 1;
    }

    String getSummary() {
        return "Ticket: " + title + " | Priority: " + priority + " | Status: " + status;
    }
}
```

Now trace what happens when you write `new SupportTicket("Login page crashes on mobile", 2)`:

1. Java allocates a memory block for the new object. At this moment, `title` is `null`, `status` is `null`, and `priority` is `0`.
2. Java calls the constructor, passing `"Login page crashes on mobile"` as the `title` parameter and `2` as the `priority` parameter.
3. Inside the constructor, `this.title = title` sets the attribute `title` to the value `"Login page crashes on mobile"`.
4. `this.priority = priority` sets the attribute `priority` to `2`.
5. `this.status = "open"` sets the attribute `status` to `"open"` unconditionally, because every new ticket starts open.
6. The constructor ends. The object is now fully initialized.

```java
SupportTicket ticket1 = new SupportTicket("Login page crashes on mobile", 2);
System.out.println(ticket1.getSummary());
// Prints: Ticket: Login page crashes on mobile | Priority: 2 | Status: open
```

Compare this to the output from the previous section (`Status: null`). The constructor is the difference between an object in a valid, usable state and an object full of meaningless defaults.

---

## The `this` Keyword: Referencing the Object Itself

The `this` keyword is a reference that every object holds pointing to itself. When a method or constructor runs, it runs in the context of a specific object. `this` is the way to explicitly name that object from inside the running code.

The most important use of `this` appears in the constructor you just read. Look at the constructor signature:

```java
SupportTicket(String title, int priority) {
```

The constructor has a parameter named `title` and an attribute also named `title`. Inside the constructor body, both exist at the same time. If you write just `title`, Java resolves it to the parameter (the closest scope wins). The attribute `title` is shadowed. Without `this`, the assignment `title = title` assigns the parameter to itself and does nothing to the attribute.

Here is that exact failure, with no `this`:

```java
SupportTicket(String title, int priority) {
    title = title;       // Assigns the parameter to itself. Attribute is untouched.
    priority = priority; // Same problem.
    status = "open";
}
```

This code compiles without any error or warning. Java does not tell you that something is wrong. But when you create a ticket and call `getSummary()`, the output reveals the problem:

```java
SupportTicket ticket1 = new SupportTicket("Login page crashes on mobile", 2);
System.out.println(ticket1.getSummary());
// Prints: Ticket: null | Priority: 0 | Status: open
```

`title` is `null` and `priority` is `0`. The values you passed in were silently ignored.

The fix is `this`:

```java
SupportTicket(String title, int priority) {
    this.title = title;       // "this.title" = the attribute; "title" = the parameter.
    this.priority = priority; // "this.priority" = the attribute; "priority" = the parameter.
    this.status = "open";
}
```

Now `this.title` unambiguously refers to the attribute on the current object, and `title` on the right side refers to the parameter. The assignment works correctly.

`this` also appears inside methods when you want to be explicit that you are accessing the current object's attribute rather than a local variable:

```java
void escalate() {
    this.priority = this.priority + 1; // Explicit. Equivalent to: priority = priority + 1;
}
```

In a simple method like `escalate()`, where there is no parameter with the same name as the attribute, `this` is optional. The behavior is identical. But in constructors with matching parameter names, `this` is not optional. It is the only way to distinguish the attribute from the parameter.

---

## `new`: Creating Instances in Memory

The `new` keyword is an operator that triggers a three-step process every time you use it:

1. **Allocation.** Java asks the heap (the region of memory reserved for objects at runtime) to allocate a block large enough to hold all the object's attributes. At this point, the attributes hold their defaults (`null`, `0`, `false`).
2. **Initialization.** Java calls the constructor on that allocated block. The constructor sets the attributes to their intended starting values, as described in the previous section.
3. **Reference return.** Java returns the memory address of the newly created object. This address is stored in the variable on the left side of the assignment.

Trace the full line `SupportTicket ticket1 = new SupportTicket("Login page crashes on mobile", 2)`:

```
Step 1: new SupportTicket(...)
        → Java allocates a memory block at, say, address 0x4A2F.
        → That block contains: title=null, status=null, priority=0.

Step 2: SupportTicket("Login page crashes on mobile", 2)
        → Java calls the constructor.
        → Constructor sets: this.title = "Login page crashes on mobile",
                            this.priority = 2,
                            this.status = "open".
        → The block at 0x4A2F now contains real data.

Step 3: ticket1 = (result of new)
        → The variable ticket1 receives the address 0x4A2F.
        → ticket1 does NOT contain the object. It contains the address where the object lives.
```

This distinction between a variable and an object is not academic. It has a concrete consequence. If you write:

```java
SupportTicket ticket1 = new SupportTicket("Login page crashes on mobile", 2);
SupportTicket ticket2 = ticket1;
```

You do not have two independent tickets. You have two variables pointing to the same memory address (0x4A2F). Both `ticket1` and `ticket2` refer to the same object. Modifying the object through one variable is visible through the other:

```java
ticket2.priority = 99;

System.out.println(ticket1.priority); // Prints: 99
```

You changed `ticket2.priority`, and `ticket1.priority` changed too. They are the same object. You only get a second independent ticket by calling `new` a second time:

```java
SupportTicket ticket1 = new SupportTicket("Login page crashes on mobile", 2);
SupportTicket ticket2 = new SupportTicket("Profile picture not uploading", 1);
```

Each `new` allocates a separate block of memory. Each returns a different address. Now `ticket1` and `ticket2` truly point to independent objects, and modifying one does not affect the other.

### Putting the full picture together

The six concepts you just covered, class, object, attribute, method, constructor, and `new`, are not independent features. They are one mechanism:

1. You write a **class** that declares **attributes** and **methods**.
2. You write a **constructor** inside that class to set the initial state of the attributes.
3. You use the **`new`** operator to allocate memory, call the constructor, and receive a reference.
4. You store that reference in a variable. That variable points to an **object** living on the heap.
5. You call **methods** on that object. Each method runs in the context of that object's attribute values.
6. Inside every method and constructor, **`this`** refers to the specific object the code is currently running on.

Here is the complete `SupportTicket` class with all of these parts in place:

```java
public class SupportTicket {

    String title;
    String status;
    int priority;

    SupportTicket(String title, int priority) {
        this.title = title;
        this.priority = priority;
        this.status = "open";
    }

    void escalate() {
        this.priority = this.priority + 1;
    }

    void close() {
        this.status = "closed";
    }

    String getSummary() {
        return "Ticket: " + this.title + " | Priority: " + this.priority + " | Status: " + this.status;
    }

    public static void main(String[] args) {
        SupportTicket ticket1 = new SupportTicket("Login page crashes on mobile", 2);
        SupportTicket ticket2 = new SupportTicket("Profile picture not uploading", 1);

        System.out.println(ticket1.getSummary());
        // Prints: Ticket: Login page crashes on mobile | Priority: 2 | Status: open

        ticket1.escalate();
        System.out.println(ticket1.getSummary());
        // Prints: Ticket: Login page crashes on mobile | Priority: 3 | Status: open

        ticket2.close();
        System.out.println(ticket2.getSummary());
        // Prints: Ticket: Profile picture not uploading | Priority: 1 | Status: closed

        System.out.println(ticket1.getSummary());
        // Prints: Ticket: Login page crashes on mobile | Priority: 3 | Status: open
        // ticket1 was not affected by what you did to ticket2.
    }
}
```

Each object manages its own state. Methods travel with the data. No method needs to be told which ticket to act on: the answer is always the object the method was called on. This is the structural guarantee OOP provides, and it is why every Java program you will write from here is organized around classes and objects.