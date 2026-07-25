# Operators in Java

## Why do operators exist?

In the previous sections, we established that *programming logic* is the ability to structure reasoning through algorithms, and that every computational problem follows the **IPO** structure: **Input → Processing → Output**. Operators are the core tools of the "Processing" step. They are the symbols that tell the machine *what to do* with the data it receives.

Without operators, you could store data but never transform it. You could have variables holding numbers, but no way to add them, compare them, or decide anything based on their values. Operators are what make data *useful*.

Java groups its operators into categories based on what kind of transformation they perform.

## 1. Arithmetic Operators (`+`, `-`, `*`, `/`, `%`)

These perform mathematical operations. If you have ever used a calculator, you already know most of them.

| Operator | Name           | Example | Result |
| -------- | -------------- | ------- | ------ |
| `+`      | Addition       | `5 + 3` | `8`    |
| `-`      | Subtraction    | `5 - 3` | `2`    |
| `*`      | Multiplication | `5 * 3` | `15`   |
| `/`      | Division       | `5 / 3` | `1`    |
| `%`      | Modulo         | `5 % 3` | `2`    |

Addition, subtraction, and multiplication behave exactly as you expect. Division and modulo do not.

### The big gotcha: integer division

Look at the table above. `5 / 3` results in `1`, not `1.666...`. This is the single most common source of confusion for beginners doing math in Java.

The rule is straightforward: **when both operands are integers (`int`), Java performs integer division — it truncates the decimal part entirely.** It does not round. It chops.

```java
int a = 5;
int b = 3;
System.out.println(a / b); // prints 1, not 1.666...
```

To get the decimal result, at least one of the operands must be a floating-point type (`double` or `float`):

```java
double a = 5.0;
int b = 3;
System.out.println(a / b); // prints 1.6666666666666667

double c = 7.0 / 2;       // 3.5
```

You can also cast one of them inline:

```java
int a = 5;
int b = 3;
System.out.println((double) a / b); // prints 1.6666666666666667
// The (double) before `a` (which is 5) converts the value of `a` to a double for this operation.
// This promotes the division: double / int → double.
```

> "Ahead-of-time question: 'What is this `(double)` in front?' It is a type cast: you are explicitly telling Java, 'treat this value as a double now.' Think of it as a 'temporary conversion."
>
> "What if I do `(double)(7 / 2)`? — The result would be `3.0`, not `3.5`. Why? Because the parentheses force integer division first (`7 / 2 = 3`), and only then is the result converted to a double (`(double) 3 = 3.0`). The type cast must happen before the division to take effect."

The classic mistake: writing `int result = 10 / 3;` and expecting `3.333...`. Java sees two `int` values, performs integer division, and stores `3`. No warning, no error. Just a silent, wrong result. These are the hardest bugs to find because the code compiles and runs without complaint.

### The modulo operator (%)

The modulo operator returns the **remainder** of a division. `5 % 3` equals `2` because 5 divided by 3 is 1 with a remainder of 2.

This operator appears constantly in real programming:

- **Checking if a number is even or odd:** `number % 2 == 0` → even. `number % 2 != 0` → odd.
- **Cycling through a fixed range:** if you need an index to "wrap around" after reaching a limit (like cycling through days of the week), modulo handles it: `index % 7` always gives a value between 0 and 6.
- **Check divisibility:** (`year % 4 == 0 and year % 100 != 0`) or (`year % 400 == 0`) → leap year
- **Extracting digits:** `1234 % 10` gives `4` (the last digit).

**Behavior with negative numbers in Java:** The sign of the result follows the sign of the dividend (the left-hand number).

```java
System.out.println(-7 % 2);  // -1 (not 1)
System.out.println(7 % -2);  //  1 (not -1)
```

### Bonus: `+` with Strings (concatenation)

The `+` operator has a dual identity in Java. When used between numbers, it adds them. When at least one side is a `String`, it **concatenates** (joins the texts together).

```java
System.out.println("Hello" + " " + "World"); // Hello World
System.out.println("Age: " + 25);             // Age: 25
```

Watch the evaluation order carefully:

```java
System.out.println(1 + 2 + " cats");  // "3 cats" — 1+2 is math, then concat
System.out.println("cats " + 1 + 2);  // "cats 12" — both are concat left to right
```

In the second line, once Java encounters the `String` on the left, every subsequent `+` becomes concatenation. `1` and `2` are glued as text, not added as numbers. This is another silent trap that produces no errors, just unexpected output.

## 2. Assignment Operators (`=`, `+=`, `-=`, `*=`, `/=`, `%=`)

The `=` sign in Java does **not** mean "equals" in the mathematical sense. It means "assign the value on the right to the variable on the left."

```java
int x = 10; // store the value 10 inside the variable x
```

Java provides compound assignment operators that combine an arithmetic operation with assignment. They exist to reduce repetition:

| Long form   | Shorthand | Meaning                              |
| ----------- | --------- | ------------------------------------ |
| `x = x + 5` | `x += 5`  | Add 5 to x and store the result in x |
| `x = x - 3` | `x -= 3`  | Subtract 3 from x                    |
| `x = x * 2` | `x *= 2`  | Multiply x by 2                      |
| `x = x / 4` | `x /= 4`  | Divide x by 4                        |
| `x = x % 2` | `x %= 2`  | Store the remainder of x / 2 in x    |

These are not new operations. `x += 5` is strictly equivalent to `x = x + 5`. The compound forms exist for conciseness and readability, nothing more. Use them when the intent is clear; avoid chaining them in ways that make the code harder to read than the long form.

## 3. Relational Operators (`==`, `!=`, `>`, `<`, `>=`, `<=`)

Relational operators **compare** two values and return a `boolean`: either `true` or `false`. They are the backbone of every `if`, `while`, and `for` statement you will ever write, because those structures need a condition to evaluate.

| Operator | Meaning                  | Example  | Result  |
| -------- | ------------------------ | -------- | ------- |
| `==`     | Equal to                 | `5 == 5` | `true`  |
| `!=`     | Not equal to             | `5 != 3` | `true`  |
| `>`      | Greater than             | `5 > 3`  | `true`  |
| `<`      | Less than                | `5 < 3`  | `false` |
| `>=`     | Greater than or equal to | `5 >= 5` | `true`  |
| `<=`     | Less than or equal to    | `3 <= 5` | `true`  |

With primitive types (`int`, `double`, `char`, etc.), these operators work exactly as you expect.

### ⚠️ Critical warning: `==` with objects

With objects (including `String`), `==` does **not** compare the content. It compares the **memory reference** — it asks "are these two variables pointing to the exact same object in memory?", not "do these two objects contain the same data?"

```java
String a = new String("hello");
String b = new String("hello");

System.out.println(a == b);      // false — different objects in memory
System.out.println(a.equals(b)); // true  — same content
```

Both `a` and `b` contain `"hello"`, but they are two separate objects stored at different memory addresses. `==` checks the address, not the text. To compare the actual content of objects, use the `.equals()` method.

This is one of the most frequent bugs in Java, especially because `String` literals (without `new`) sometimes behave differently due to Java's String Pool optimization:

```java
String a = "hello";
String b = "hello";

System.out.println(a == b); // true — Java reuses the same object from the pool
```

This `true` result is a side effect of an optimization, not a guarantee of correct behavior. **Always use `.equals()` for `String` comparison.** Relying on `==` for `String` is a bug waiting to happen.

## 4. Logical Operators (`&&`, `||`, `!`)

Logical operators combine or invert `boolean` expressions. They are how you express conditions like "if the user is logged in **and** has permission" or "if the input is empty **or** null."

| Operator | Name | What it does                                          |
| -------- | ---- | ----------------------------------------------------- |
| `&&`     | AND  | `true` only if **both** sides are `true`              |
| `\|\|`   | OR   | `true` if **at least one** side is `true`             |
| `!`      | NOT  | Inverts the value: `true` → `false`, `false` → `true` |

```java
boolean hasAccess = isLoggedIn && hasPermission;   // both must be true
boolean canRetry = attemptsLeft > 0 || isAdmin;    // at least one must be true
boolean isInvalid = !isValid;                      // flips the boolean
```

Truth tables define the exact behavior:

**AND (`&&`)**

| A       | B       | A && B  |
| ------- | ------- | ------- |
| `true`  | `true`  | `true`  |
| `true`  | `false` | `false` |
| `false` | `true`  | `false` |
| `false` | `false` | `false` |

**OR (`||`)**

| A       | B       | A \|\| B |
| ------- | ------- | -------- |
| `true`  | `true`  | `true`   |
| `true`  | `false` | `true`   |
| `false` | `true`  | `true`   |
| `false` | `false` | `false`  |

**NOT (`!`)**

| A       | !A      |
| ------- | ------- |
| `true`  | `false` |
| `false` | `true`  |

### Short-circuit evaluation

Java does **not** always evaluate both sides of a logical expression. It takes a shortcut whenever the result is already determined by the left side alone.

- `&&`: if the left side is `false`, the right side is **never evaluated**. `false && (anything)` is always `false`, so Java skips the second part.
- `||`: if the left side is `true`, the right side is **never evaluated**. `true || (anything)` is always `true`.

This is not just a performance detail. It has real consequences for how you write code:

```java
if (name != null && name.length() > 0) {
    // safe: if name is null, the second check never runs
}
```

If Java did not short-circuit, `name.length()` would execute on a `null` reference, and the program would crash with a `NullPointerException`. The order of the conditions matters: **put the safety check first**.

A common pattern you will see in professional code is using `&&` to guard a second condition that would fail if the first condition is `false`. This is not a trick or a hack. It is the intended use.

## 5. Bitwise Operators (`&`, `|`, `^`, `~`, `<<`, `>>`)

Bitwise operators work directly on the **binary (bit-level) representation** of integer values. They are less common in everyday application code, but they appear in specific domains: flags, permissions systems, low-level protocols, and performance-sensitive algorithms.

### What are bits?

Every value in a computer is stored as a sequence of bits (binary digits: `0` or `1`). The decimal number `5`, for instance, is represented in binary as `101`. The number `3` is `011`.

Java's `int` type uses 32 bits, but for clarity, we will use simplified representations in the examples below.

### Each operator explained

**AND (`&`)** — returns `1` only where **both** bits are `1`.

```
  5 → 1 0 1
  3 → 0 1 1
& ─────────
  1 → 0 0 1
```

**OR (`|`)** — returns `1` where **at least one** bit is `1`.

```
  5 → 1 0 1
  3 → 0 1 1
| ─────────
  7 → 1 1 1
```

**XOR (`^`)** — returns `1` where the bits are **different**.

```
  5 → 1 0 1
  3 → 0 1 1
^ ─────────
  6 → 1 1 0
```

**NOT (`~`)** — inverts every bit. In Java, `~5` is not simply `010` because Java uses 32-bit signed integers with two's complement representation. `~5` results in `-6`. The rule is: `~n` equals `-(n + 1)`.

```
~ 0000 0101  (5)
-----------
  1111 1010  → In Java (two's complement): -6
```

**Left Shift (`<<`)** — shifts all bits to the left by `n` positions, filling with `0` on the right. Each shift left **multiplies the value by 2**.

```
5      → 0 0 1 0 1
5 << 1 → 0 1 0 1 0 = 10  
5 << 2 → 1 0 1 0 0 = 20
```

```java
int result = 5 << 1; // 10
int result2 = 5 << 2; // 20
```

**Right Shift (`>>`)** — shifts all bits to the right by `n` positions. Each shift right **divides the value by 2** (integer division).

```
20      → 1 0 1 0 0
20 >> 1 → 0 1 0 1 0 = 10
20 >> 2 → 0 0 1 0 1 = 5
```

The **unsigned right shift operator (>>>)** in Java shifts all bits of a number to the right by a specified amount, filling the leftmost bits with 0 (zero) regardless of whether the number is positive or negative, unlike the signed right shift (>>), which preserves the sign bit.

**Visual example for easy understanding:**

```
Number:  -8  →  11111111 11111111 11111111 11111000  (32 bits)

-8 >> 1  (signed)   →  11111111 11111111 11111111 11111100  =  -4
                       ↑ preserves the sign bit (1)

-8 >>> 1 (unsigned)  →  01111111 11111111 11111111 11111100  =  2147483644
                        ↑ pad with zeros (ignore sign)
```

### When bitwise operators appear in practice

You will likely not use bitwise operators daily. But you will encounter them in:

- **Permission/flag systems:** a single `int` can store multiple boolean flags. Each bit represents one flag. `&` checks if a flag is set, `|` sets a flag, `^` toggles a flag.
- **Hash functions and cryptography:** algorithms like SHA and MD5 rely heavily on XOR and shifts.
- **Low-level performance tricks:** multiplying by 2 using `<< 1` instead of `* 2` is a classic optimization in embedded systems and game engines, though modern compilers usually handle this automatically.

You don't need to master bitwise operators right now. Understand what they do at a conceptual level and recognize them when you see them. The depth will come when a real problem demands it.

## 6. Operator Precedence

When an expression contains multiple operators, Java does not simply evaluate them left to right. It follows a **precedence hierarchy**, just like math: multiplication happens before addition unless you use parentheses to override the order.

```java
int result = 2 + 3 * 4; // result is 14, not 20
```

Java evaluated `3 * 4` first (because `*` has higher precedence than `+`), then added `2`.

Here is the precedence table for the operators we covered, from **highest** (evaluated first) to **lowest** (evaluated last):

| Precedence  | Operators                         | Category       |
| ----------- | --------------------------------- | -------------- |
| 1 (highest) | `( )`                             | Grouping       |
| 2           | `!`, `~`, `cast (type)`           | Unary          |
| 3           | `*`, `/`, `%`                     | Multiplicative |
| 4           | `+`, `-`                          | Additive       |
| 5           | `<<`, `>>`                        | Shift          |
| 6           | `<`, `<=`, `>`, `>=`              | Relational     |
| 7           | `==`, `!=`                        | Equality       |
| 8           | `&`                               | Bitwise AND    |
| 9           | `^`                               | Bitwise XOR    |
| 10          | `\|`                              | Bitwise OR     |
| 11          | `&&`                              | Logical AND    |
| 12          | `\|\|`                            | Logical OR     |
| 13 (lowest) | `=`, `+=`, `-=`, `*=`, `/=`, `%=` | Assignment     |

Memorizing this entire table is unnecessary. What matters in practice is knowing three things:

1. **Arithmetic before comparison, comparison before logic.** `a + b > c && d == e` is read as `((a + b) > c) && (d == e)`. This matches natural reading order in most cases.
2. **`&&` binds tighter than `||`.** `a || b && c` means `a || (b && c)`, not `(a || b) && c`. If this feels ambiguous when reading the code, add parentheses.
3. **When in doubt, use parentheses.** They cost nothing at runtime and make your intent explicit. Code that requires someone to recall the precedence table to understand it is poorly written code, regardless of whether it is technically correct.

The goal is not to write the most compact expression possible. The goal is to write code that another person (or you, six months later) can read and immediately understand.