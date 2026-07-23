# Data Types, Variables, and Keywords

## Variables: Storing Information to Use It Later

Variables exist because programs need to remember things. Without them, every value computed or received would vanish the instant it appeared (e.g, you couldn't compare a user's grade to a passing threshold if you had nowhere to store that grade).

In Java, it is composed of three inseparable elements:

| Element   | What it is                                                                | Example                   |
| --------- | ------------------------------------------------------------------------- | ------------------------- |
| **Type**  | Defines what the variable can store and how much memory space it occupies | `int`, `double`, `String` |
| **Name**  | Unique identifier you use to access the value                             | `age`, `testGrade`        |
| **Value** | The data itself, stored in the reserved space                             | `25`, `9.5`, `"Maria"`    |

A variable is a named location in memory that holds a value. Think of it as a labeled box: the label is the name, the box is the reserved memory, and whatever sits inside is the value.

**Where is it in memory?** When you declare a variable in Java, the JVM (Java Virtual Machine — the runtime environment we saw in Module 0) reserves a specific space in RAM with a physical address. The variable name is like a nickname for that address. When you type `age`, the JVM knows exactly which memory address to look up. You never have to deal with addresses directly, because Java does that for you, unlike languages like C.

> In C, developers use variables called **pointers** to store and manipulate exact memory addresses. This allows direct access to the computer's hardware and allows "pointer arithmetic" (e.g., adding numbers to a memory address to jump to the next byte).
> However, this demands manual memory management using functions like `malloc()`. Forgetting to release memory or accessing the wrong address leads to severe bugs like memory leaks, program crashes, or security vulnerabilities.

### Declaration, Initialization, and Assignment: the three moments in a variable's lifecycle

Three distinct operations govern how variables work:

| Operation          | What it does                                                | Example     |
| ------------------ | ----------------------------------------------------------- | ----------- |
| **Declaration**    | Tells the compiler that a variable of a certain type exists | `int age;`  |
| **Initialization** | Assigns a value for the first time                          | `age = 20;` |
| **Assignment**     | Replaces the current value with a new one                   | `age = 21;` |

These can be collapsed into one line:

```java
int age = 20; // declaration + initialization
age = 21;     // assignment — 20 is gone, 21 takes its place
```

The question you should be asking is: *"If '`int age;`' has no value, what's stored in that space?"*

It depends on where the variable is declared:
- **Inside a method (local variable):** Space is reserved, but no default value is assigned. **Java will refuse to compile** if you try to use an uninitialized local variable, throwing the error: `variable 'x' might not have been initialized`.
- **As a class field (instance variable):** Java automatically assigns default values (`0` for integers, `0` for decimals, `false` for booleans, `null` for objects). However, don't rely on this! Explicit initialization is always a best practice.

```java
int score;
System.out.println(score); // ERROR: variable score might not have been initialized
```

The type always comes first. It tells the compiler how much memory to reserve and what operations are legal on that variable. You cannot store a decimal number in an `int` and expect it to behave like one; Java will either reject it outright or silently truncate it, depending on the context. Either way, the result is not what you wanted.

**An important nuance — `final` variables:**

If you want a variable to be immutable (remain constant) after it's initialized, use the `final` keyword:

```java
final double APPROVAL_RATE = 0.6; // Cannot be reassigned
APPROVAL_RATE = 0.7;              // Compile-time ERROR
```

`final` variables are treated as **constants**. By convention, their names are written in `SCREAMING_SNAKE_CASE`: all uppercase, words separated by underscores. This is a Java community standard, not a compiler rule, but it is universally followed.

---

## Primitive Types — and the String That Isn't One

Java has eight primitive types. Each one is a fixed-size, direct value stored in memory. No objects, no overhead — just raw data.

**Why does Java have 8 different types for something as seemingly simple as a "number"?**

Because memory matters. A number between 0 and 100 doesn't need the same amount of space as a number with 18 decimal places. Having different types allows the programmer to use *exactly the space needed* (nothing more, nothing less). In systems that process millions of data points, this makes a real difference in performance.

### 8 Primitive Data Types Table

| Type      | What it stores            | Size           | Range (possible values)                                                             | Example                     |
| --------- | ------------------------- | -------------- | ----------------------------------------------------------------------------------- | --------------------------- |
| `byte`    | Integer, narrow range     | 8 bits         | -128 a 127                                                                          | `byte b = 100;`             |
| `short`   | Integer, medium range     | 16 bits        | -32.768 a 32.767                                                                    | `short s = 30000;`          |
| `int`     | Integer, standard range   | 32 bits        | -2.147.483.648 a 2.147.483.647                                                      | `int x = 1_000_000;`        |
| `long`    | Integer, large range      | 64 bits        | -9,2 × 10^18 (-9,223,372,036,854,775,808) a 9,2 × 10^18 (9,223,372,036,854,775,807) | `long l = 10_000_000_000L;` |
| `float`   | Decimal, single precision | 32 bits        | ~7 digits of precision                                                              | `float f = 3.14f;`          |
| `double`  | Decimal, double precision | 64 bits        | ~15-16 digits of precision                                                          | `double d = 3.14159;`       |
| `char`    | Single Unicode character  | 16 bits        | '\u0000' a '\uffff' (0 a 65.535)                                                    | `char c = 'A';`             |
| `boolean` | True or false only        | JVM-dependent* | true ou false                                                                       | `boolean active = true;`    |

> *`boolean`: the Java specification does not define an exact size. In practice, the JVM generally uses 1 logical bit, but it may allocate more for memory alignment reasons. This rarely affects the code, but it is good to know that the specification is deliberately vague here.

#### A clearer explanation about float and double values

Floating-point variables `float` and `double` both share the same structural components: 1 sign bit that defines whether the number is positive or negative, a set of bits for the exponent (which controls the magnitude/scale of the number; in simple terms: how big the number is, determining how many decimal places the decimal point must shift to the right based on computer base-2 math), and bits to store the mantissa (also known as the significand, which contains the significant digits; meaning the digits visible before the 'E', starting from the first digit after the decimal point).
- `float`: Uses 8 bits for the exponent and 23 bits for the mantissa. Because of an implied leading bit, it achieves about 7 decimal digits of precision.
- `double`: Uses 11 bits for the exponent and 52 bits for the mantissa. It achieves about 15 to 16 decimal digits of precision.

**For example:**

Assigning *123456789123456789* to both variables instantly illustrates their precision differences. The `float` will round the number (relying on its shorter mantissa) to `1.2345679E8`, while the `double` will capture much higher precision and correctly store `1.2345678912345679E8`.

---

A few things that routinely trip beginners:

- `long` literals require an `L` suffix: `10_000_000_000L`. Without it, Java reads the literal as an `int` and overflows *before* the assignment happens.
- `float` literals require an `f` suffix: `3.14f`. A bare `3.14` is a `double` by default.
- `char` uses single quotes. `'A'` is a character; `"A"` is a `String`. They are not the same type and cannot be used interchangeably.
- For most decimal arithmetic, use `double`. `float` trades precision for memory — a trade that is rarely worth making.

#### The fundamental limitation of both floating-point types

Floating-point numbers cannot represent all decimal numbers with exact precision in binary. This isn't a Java bug, it's a fundamental mathematical limitation of how binary works.

```java
System.out.println(0.1 + 0.2);  // Result: 0.30000000000000004
```

`0.1` doesn't have an exact binary representation (just as `1/3` doesn't have an exact decimal representation — it becomes `0.333...`). The error is extremely small, but it exists. For most cases (grades, temperatures, coordinates), this is irrelevant. For **money and finance**, never use `double` — use `BigDecimal`.

### String — The Special Case

`String` is not a primitive type. It is a class, and every `String` value is an object. But Java gives it syntax that looks primitive:

```java
String name = "Alice"; // looks primitive — it is not
```

This works because the Java compiler has built-in support for `String` literals. Under the hood, `"Alice"` is an instance of `java.lang.String`, which means it carries methods:

```java
name.length();      // 5
name.toUpperCase(); // "ALICE"
name.charAt(0);     // 'A'
```

A String can be `null` (having no value). Primitives cannot be (`int x = null`; doesn't compile). Primitives also have no methods. `int` cannot call `.compareTo()` on itself. `String` can, because it is an object. This distinction becomes critical when comparing strings — never use `==` to compare two `String` values. That comparison checks memory addresses, not content. Use `.equals()` instead. This will make full sense once objects are covered; for now, treat it as a firm rule.

---

## Primitives vs. Objects — A First Look

This distinction will be covered in depth when classes and objects are introduced. But knowing the boundary now prevents a class of bugs that quietly confuses beginners for months.

**Primitives (`int`, `double` ...)** store the value directly in the variable. When you write `int a = 5; int b = a;`, `b` gets its own independent copy of `5`. Changing `b` does nothing to `a`.

**Objects (`String`, `Scanner` ...)** store a reference — an address pointing to where the actual data lives in memory. When you assign one object variable to another, both variables point to the *same* data. Modifying through one affects the other:

```java
// Primitives: independent copies
int a = 5;
int b = a;
b = 10;
System.out.println(a); // 5 — unchanged

// Objects: shared reference
int[] arr1 = {1, 2, 3};
int[] arr2 = arr1;     // both point to the same array
arr2[0] = 99;
System.out.println(arr1[0]); // 99 — arr1 was affected
```

The `==` operator reflects this split. For primitives, it compares values. For objects, it compares references (whether two variables point to the same location in memory), not whether their contents are equal. That is exactly why `"hello" == "hello"` can return `false` depending on how the strings were created, and why `.equals()` exists.

One more distinction worth knowing now: primitives cannot be `null`. An `int` always holds a number. An object variable can hold `null` (the explicit absence of a reference); Accessing methods on a `null` reference throws a `NullPointerException`, one of the most common runtime errors in Java.

| Characteristic  | Primitives (`int`, `double`...)  | Objects (`String`, `Scanner`...)                  |
| --------------- | -------------------------------- | ------------------------------------------------- |
| Memory location | Directly in the variable (stack) | Variable stores address; object stays in the heap |
| Can be `null`?  | No                               | Yes                                               |
| Has methods?    | No                               | Yes                                               |
| Name            | Lowercase (int, char)            | Uppercase (String, Scanner)                       |
| Fixed size?     | Yes — always the same            | No — depends on the content                       |

> **Stack** and **Heap** are memory areas managed by the JVM. The **Stack** is a fast, fixed-size memory area where local variables and object references are stored during method execution, while the **Heap** is a larger, dynamic area where Java physically allocates objects and which is managed by the Garbage Collector (a JVM automatic memory management mechanism).

**Wrapper classes** (a note for future reference): each primitive has a corresponding class: `int` has `Integer`, `double` has `Double`, `boolean` has `Boolean`, etc. They exist for situations where Java requires an object but you have a primitive. Java does the conversion automatically in many cases (this is called *autoboxing*).

---

## Java Reserved Words

Reserved words — also called keywords — are identifiers Java has claimed for its own grammar. You cannot use them as variable names, class names, or method names. The compiler rejects the code before it runs.

| Keyword                          | What it signals                                                                | Example                    |
| -------------------------------- | ------------------------------------------------------------------------------ | -------------------------- |
| `class`                          | Defines a class                                                                | `class Candidate { }`      |
| `public`                         | Access modifier — visible from anywhere                                        | `public class MyClass`     |
| `private`                        | Access modifier — visible only within the class                                | `private int sale`         |
| `protected`                      | Access modifier — visible within the package and subclasses                    | `protected String model`   |
| `static`                         | Belongs to the class, not to any instance                                      | `public static void main`  |
| `void`                           | Method returns no value                                                        | `void printName()`         |
| `return`                         | Exits a method and optionally sends a value back                               | `return grade * 2`         |
| `new`                            | Creates a new object instance                                                  | `new Scanner(System.in)`   |
| `if` / `else`                    | Conditional branching                                                          | `if (approved) { }`        |
| `for` / `while` / `do`           | Iteration                                                                      | `for (i = 0; ...)`         |
| `int`, `double`, `boolean`, etc. | Type declarations                                                              | `int stock = 100`          |
| `true` / `false`                 | The only valid boolean literals                                                | `boolean happy = true`     |
| `null`                           | Absence of an object reference                                                 | `String name = null`       |
| `this`                           | Reference to the current object                                                | `this.name = name`         |
| `final`                          | Prevents reassignment on variables; prevents overriding on methods and classes | `final double pi = 3.14`   |
| `import`                         | Brings a class or package into scope                                           | `import java.util.Scanner` |
| `extends` / `implements`         | Inheritance and interface contracts                                            | `class Dog extends Animal` |

`int class = 5;` is illegal. `String new = "hello";` is illegal. `boolean return = true;` is illegal. The compiler will tell you immediately in every case.

A practical observation: if your IDE highlights a name you chose in a color different from ordinary identifiers, it is almost certainly a keyword. Rename it.

### `var` — the "modern" keyword (Java 10+)

```java
var name = "Maria";     // Java infers: String
var age = 25;         // Java infers: int
var grade = 9.5;         // Java infers: double
```

The `var` keyword allows Java to infer (deduce) the type automatically from the value you assign. This is called local-variable type inference. The type still exists and is fixed: you cannot do `var x = 10` and then x` = "text"`. Only writing it in the code is optional. It is useful for reducing verbosity, especially with long types. However, for beginners: writing the type explicitly is a better practice while you are learning, because you internalize the types much faster.

---

## Naming Conventions

Naming in Java has two layers: rules the compiler enforces and conventions the community follows. Violating the first breaks your code. Violating the second breaks the readability of every file you touch — which, in any collaborative environment, is a different kind of problem.

### Compiler Rules — Non-Negotiable

- Names can only contain letters, digits, `_`, and `$` (Avoid `$`, it's reserved for generated code).
- Names cannot start with a digit. `1score` is illegal; `score1` is legal.
- Names cannot contain spaces (`test score` → invalid).
- Names cannot be a Java keyword.
- Names are case-sensitive. `score`, `Score`, and `SCORE` are three distinct identifiers as far as the compiler is concerned.

### Community Conventions — Always Follow

| What you are naming        | Convention                                                     | Example                              |
| -------------------------- | -------------------------------------------------------------- | ------------------------------------ |
| Variables and methods      | `camelCase` — starts lowercase, subsequent words are uppercase | `studentGrade`, `calculateAverage()` |
| Classes                    | `PascalCase` — each word starts uppercase                      | `StudentRecord`, `BankAccount`       |
| Constants (`static final`) | `UPPER_SNAKE_CASE`/`SCREAMING_SNAKE_CASE`                      | `MAX_SCORE`, `DEFAULT_TIMEOUT`       |
| Packages                   | all lowercase, no underscores                                  | `com.example.project`                |

These are not stylistic preferences. Java projects involve teams, code reviews, and maintenance that spans years. A class named `myclass` or a variable named `X` forces the next developer — often yourself, three weeks later — to read the entire implementation to understand the intent. A variable named `studentGrade` is self-documenting.

**On meaningful names:** `int x = 90;` is syntactically legal. `int studentGrade = 90;` is correct. The difference is not cosmetic — it determines whether the code explains itself or demands an explanation. Name things for what they *are*, not for what they happen to *contain* at this particular moment.

One concrete sub-rule for `boolean` variables: they should read as a yes/no question when used in a condition. `isActive`, `hasPermission`, `isEmpty` — these read naturally inside an `if` statement. `flag`, `check`, and `b` do not. If a reader has to stop and think about what a variable name means, the name is wrong.