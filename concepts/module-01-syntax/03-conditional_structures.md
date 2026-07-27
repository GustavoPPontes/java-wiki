# Condicional Structures in Java

## The `if / else if / else` — Simple and Chained Decision-Making

Every program you will ever write needs to react differently depending on what happens at runtime. A grade calculator must distinguish between passing and failing. A login screen must separate valid credentials from invalid ones. The mechanism that enables this is the **conditional structure**, and `if` is where it all starts.

The basic syntax in Java:

```java
if (condition) {
    // executes if condition is true
} else if (otherCondition) {
    // executes if the first is false and this is true
} else {
    // executes if all conditions above are false
}
```

The machine evaluates each condition top to bottom and stops at the **first one that is true**. The remaining branches are skipped entirely. This has a practical consequence: the order of your conditions matters. Put the most specific conditions first.

### The `{}` Rule — When You Can Omit Braces (and When You Shouldn't)

Java allows you to omit the curly braces `{}` when the branch contains exactly one statement:

```java
if (grade >= 7)
    System.out.println("Passed");
```

This compiles. It runs correctly. And it is a trap waiting to happen. The moment you add a second line under that `if`, thinking it belongs to the branch, it doesn't:

```java
if (grade >= 7)
    System.out.println("Passed");
    System.out.println("Congratulations"); // This ALWAYS runs. Not part of the if.
```

The indentation is for humans. The compiler ignores it. **Always use braces.** This single habit eliminates an entire category of silent bugs.

### Is `else` Mandatory?

No. An `if` without an `else` is valid and common. The `else` branch only exists when your program needs to do something specifically when the condition fails. If there is nothing to do in the failure case, omit it.

```java
if (isAdmin) {
    enableAdminPanel();
}
// No else needed — regular users just don't get the admin panel.
```

### Nesting `if` Inside `if`

You can place an `if` inside another `if`'s block. This is called **nested conditionals** and it is legitimate when the inner condition only makes sense after the outer one is confirmed:

```java
if (userIsLoggedIn) {
    if (userIsAdmin) {
        showAdminDashboard();
    } else {
        showUserDashboard();
    }
}
```

The inner `if` on `userIsAdmin` only runs when `userIsLoggedIn` is already true. Checking admin status for a user who isn't logged in would be meaningless.

The problem with nesting is depth. Two levels are readable. Three levels are a warning sign. Four levels mean the problem is asking to be decomposed into smaller methods.

---

## `switch case` — When to Use It Instead of `if/else`

The `if/else` chain handles any condition — comparisons, ranges, complex boolean expressions. The `switch` statement handles a narrower but common situation: **one variable compared against multiple discrete values**.

```java
int day = 3;

switch (day) {
    case 1:
        System.out.println("Monday");
        break;
    case 2:
        System.out.println("Tuesday");
        break;
    case 3:
        System.out.println("Wednesday");
        break;
    default:
        System.out.println("Another day");
}
```

The `switch` evaluates `day` once, jumps directly to the matching `case`, runs it, and stops when it hits `break`.

### The Fall-Through Trap

Remove a `break` and the execution doesn't stop at the end of that case. It *falls through* into the next case and runs it too, regardless of whether it matches:

```java
switch (day) {
    case 1:
        System.out.println("Monday");
        // Missing break!
    case 2:
        System.out.println("Tuesday"); // Also prints when day = 1
        break;
}
```

This is the single most common `switch` bug. Fall-through is intentional behavior in Java (it has valid uses, covered below), but when it happens by accident, the result is two case blocks executing when you expected one. **Always add `break` at the end of each case unless you explicitly intend to fall through.**

### What `switch` Accepts — and What It Doesn't

The `switch` expression doesn't accept every type. It works with:

- `byte`, `short`, `int`, `char`
- Their wrapper classes: `Byte`, `Short`, `Integer`, `Character`
- `String` (since Java 7)
- `enum` types

It does **not** work with `long`, `float`, `double`, `boolean`, or arbitrary objects. If your condition involves ranges (`grade >= 7`), inequality comparisons, or complex logic, `switch` cannot express it. Use `if/else`.

### `if/else if` vs. `switch` — Comparative Table

| Criterion | `if / else if` | `switch / case` |
|---|---|---|
| Condition type | Any boolean expression | Equality to discrete values only |
| Supported types | All | `int`, `char`, `String`, `enum` and their wrappers |
| Ranges (`x > 10`) | ✓ | ✗ |
| Multiple values per case | Only with `&&` / `\|\|` | ✓ (via fall-through or Switch Expression) |
| Readability with many values | Degrades fast | Stays clean |
| Risk of silent bugs | Lower | Fall-through if `break` forgotten |

The practical rule: if you are comparing one variable against more than three or four fixed values, `switch` reads better. If you are dealing with ranges, conditions, or types it doesn't support, `if/else` is the only option.

---

## The Ternary Operator: `condition ? value_if_true : value_if_false`

The ternary operator is a compact way to express a two-branch condition that **produces a value**. The syntax is:

```java
String result = (grade >= 7) ? "Passed" : "Failed";
```

This is not a control-flow statement that executes blocks of code. It is an **expression that evaluates to one of two values** and that value gets assigned, returned, or printed. The equivalent `if/else` for the example above:

```java
String result;
if (grade >= 7) {
    result = "Passed";
} else {
    result = "Failed";
}
```

Both produce the same outcome. The ternary version is shorter and perfectly readable in this form.

### When to Use — and When Not To

Use the ternary operator when:
- The condition is simple and fits on one line without wrapping.
- Each branch produces a single value, not a sequence of statements.
- The intent is assignment, return, or print — not complex logic.

Do not use it when:
- Each branch requires multiple operations. The ternary only holds one expression per side.
- You are nesting ternaries inside ternaries. This is legal Java and unreadable to every human being, including the person who wrote it six months later.

```java
// Readable
String label = (score > 0) ? "positive" : "non-positive";

// Do not do this
String category = (score > 90) ? "A" : (score > 80) ? "B" : (score > 70) ? "C" : "F";
```

That last line is a chained ternary. It works. An `if/else if` chain with four branches is incomparably clearer. The ternary's value is compactness for simple cases, and that value disappears the moment you chain it.

---

## Switch Expression (Java 14+): The Modern `switch`

Java 14 introduced the **Switch Expression**, a redesigned version of the classic `switch` that fixes its two biggest problems: mandatory `break` statements and fall-through by default.

The syntax uses an arrow `->` instead of a colon:

```java
int day = 3;

String dayName = switch (day) {
    case 1 -> "Monday";
    case 2 -> "Tuesday";
    case 3 -> "Wednesday";
    case 4 -> "Thursday";
    case 5 -> "Friday";
    default -> "Weekend";
};
```

Several things changed:

- **No `break` needed.** Each arrow case executes exactly one expression and stops. Fall-through does not exist in this syntax.
- **It produces a value.** The entire `switch` block is an expression that resolves to a value, which can be assigned to a variable, returned from a method, or passed as an argument.
- **`default` is required** when the compiler cannot prove all cases are covered (e.g., non-enum types).

### Multi-Line Cases and `yield`

When a case requires more than a single expression — a block of statements — you use curly braces and the `yield` keyword to specify the value the block produces:

```java
String classification = switch (score) {
    case 10 -> "Perfect";
    case 9, 8 -> "Excellent";
    default -> {
        String base = "Score: " + score;
        yield base + " — needs review";
    }
};
```

`yield` is to Switch Expressions what `return` is to methods: it exits the block and delivers the value. It has no meaning outside a Switch Expression block.

### Multiple Values per Case

In both classic and modern `switch`, you can group multiple values under one case. In the classic syntax this required intentional fall-through (and was a source of the exact bugs described earlier). In Switch Expressions, it's explicit and clean:

```java
String type = switch (day) {
    case 1, 2, 3, 4, 5 -> "Weekday";
    case 6, 7 -> "Weekend";
    default -> "Invalid";
};
```

No fall-through, no risk. The comma-separated values are handled as a single case.

### Classic `switch` vs. Switch Expression — Full Comparison

| Feature | Classic `switch` | Switch Expression (Java 14+) |
|---|---|---|
| Syntax | `case X:` with `:` | `case X ->` with `->` |
| `break` required | Yes — missing it causes fall-through | No — each case is self-contained |
| Fall-through behavior | Default; requires `break` to prevent | Does not exist |
| Produces a value | No | Yes — assignable, returnable |
| Multiple values per case | Via fall-through (risky) | Via comma-separated values (explicit) |
| Multi-statement case | Natural (no special syntax) | Requires `{}` and `yield` |
| Java version | All versions | Java 14+ (preview in 12–13) |

The Switch Expression doesn't deprecate the classic `switch`. But for new code targeting Java 14 or later, it is the better default: it eliminates the fall-through trap structurally, not by discipline, and produces cleaner code when you need a value.

---

## Bonus: Java I/O — Reading and Writing Data

### Output: `System.out`

`System.out` is a static object of type `PrintStream` available in every Java program. It exposes three commonly used methods:

```java
System.out.print("No line break at the end");
System.out.println("With line break at the end");
System.out.printf("Formatted: %s scored %.2f%n", name, grade);
```

`printf` follows C-style formatting. The format string contains **format specifiers** — placeholders that get replaced by the arguments you pass:

| Specifier | Type | Example | Output |
|---|---|---|---|
| `%d` | Integer (`int`, `long`) | `printf("%d", 42)` | `42` |
| `%f` | Floating-point (`float`, `double`) | `printf("%f", 3.14)` | `3.140000` |
| `%.2f` | Float, 2 decimal places | `printf("%.2f", 3.14159)` | `3.14` |
| `%s` | String | `printf("%s", "Ana")` | `Ana` |
| `%c` | Character (`char`) | `printf("%c", 'A')` | `A` |
| `%b` | Boolean | `printf("%b", true)` | `true` |
| `%n` | Platform line break | `printf("line%n")` | `line` + newline |

`%n` is preferred over `\n` inside `printf` because it uses the correct line separator for the operating system the code runs on.

### Input: `Scanner`

`Scanner` is the standard class for reading user input from the terminal. It lives in `java.util` and must be imported:

```java
import java.util.Scanner;

Scanner sc = new Scanner(System.in);

System.out.print("Enter your name: ");
String name = sc.nextLine();

System.out.print("Enter your grade: ");
double grade = sc.nextDouble();
```

The `Scanner` reads data from an input stream. `System.in` connects it to the keyboard. The key methods:

| Method | Reads | Returns |
|---|---|---|
| `nextLine()` | An entire line until `\n` | `String` |
| `next()` | A single token (until whitespace) | `String` |
| `nextInt()` | An integer | `int` |
| `nextDouble()` | A floating-point number | `double` |
| `nextBoolean()` | `true` or `false` | `boolean` |

### The Buffer Trap

This is the most common `Scanner` bug and it catches almost every beginner. The cause: `nextInt()`, `nextDouble()`, and similar methods read the value but **leave the newline character `\n` in the buffer** (the input stream's memory). The next `nextLine()` call reads that leftover `\n` instead of waiting for the user to type.

```java
System.out.print("Enter your age: ");
int age = sc.nextInt();         // Reads "25", leaves "\n" in buffer

System.out.print("Enter your name: ");
String name = sc.nextLine();    // Reads the leftover "\n" — name = ""
```

The fix is to consume the leftover newline with a `nextLine()` call immediately after any `nextInt()`, `nextDouble()`, or similar method, before reading a `String`:

```java
int age = sc.nextInt();
sc.nextLine(); // Consumes the leftover "\n"

String name = sc.nextLine(); // Now reads the actual input
```

This single line prevents an entire class of input bugs. Add it as a habit whenever you mix `nextInt()` / `nextDouble()` with `nextLine()` in the same program.