# Arrays and Loops

## Arrays: storing more than one value

Suppose you need to store the grades of 30 students. Without arrays, you would need 30 separate variables: `grade1`, `grade2`, `grade3`… and so on until `grade30`. Every operation (finding the highest grade, calculating the average, printing all values) would have to be written 30 times. This is not just inconvenient; it makes the program impossible to maintain.

An **array** is a fixed-size, ordered collection of elements of the same type, stored in contiguous positions in memory and accessed by a numeric index.

Three properties define what an array fundamentally is:

| Property | Meaning | Consequence if ignored |
|---|---|---|
| **Fixed size** | The number of slots is defined at creation and cannot change | Attempting to access a slot beyond the declared size crashes the program |
| **Same type** | All elements must be of the same data type | You cannot mix `int` and `String` in the same array |
| **Zero-indexed** | The first element is at position `0`, not `1` | The last valid index of an array of size `n` is `n-1`, not `n` |

### Declaration, initialization, and assignment

Working with an array happens in three distinct stages — and confusing them is one of the most common beginner mistakes.

**Declaration** tells Java that a variable will hold a reference to an array of a specific type. It does not create the array yet; it just reserves the variable name.

```java
int[] grades;
```

**Initialization** is when the array itself is created in memory, with a defined number of slots. At this point, all slots are filled with a default value: `0` for numeric types, `false` for `boolean`, and `null` for objects.

```java
grades = new int[5]; // Creates an array of 5 integers, all defaulting to 0
```

Declaration and initialization are often combined into a single line:

```java
int[] grades = new int[5];
```

Alternatively, when you already know the values at the time of creation, you can use an **array literal**, which declares, initializes, and assigns all values simultaneously:

```java
int[] grades = {8, 7, 9, 6, 10};
```

**Assignment** means placing a value into a specific slot. Each slot is identified by its index, which starts at `0`.

```java
grades[0] = 8;  // First slot
grades[1] = 7;  // Second slot
grades[4] = 10; // Fifth (and last) slot of a size-5 array
```

### Accessing, modifying, and reading the size

Accessing and modifying an element use the same index syntax. Reading a value:

```java
System.out.println(grades[2]); // Prints the value at index 2
```

Modifying a value:

```java
grades[2] = 99; // Replaces whatever was at index 2 with 99
```

The number of slots in an array is accessible through the `.length` property. Note: `.length` is a property, not a method — there are no parentheses.

```java
System.out.println(grades.length); // Prints 5
```

### The ArrayIndexOutOfBoundsException

If you try to access an index that does not exist — either negative, or greater than or equal to `.length` — Java throws an `ArrayIndexOutOfBoundsException` and halts the program. This is not a warning; it is a runtime crash.

```java
int[] grades = new int[5]; // Valid indices: 0, 1, 2, 3, 4
System.out.println(grades[5]); // CRASH: index 5 does not exist
```

The off-by-one error (using `grades.length` instead of `grades.length - 1` as the last index) is by far the most common cause of this exception.

---

## Why loops exist

With an array of 5 elements, you could access each one manually:

```java
System.out.println(grades[0]);
System.out.println(grades[1]);
System.out.println(grades[2]);
System.out.println(grades[3]);
System.out.println(grades[4]);
```

With 1,000 elements, this is obviously not an option. But the issue is not just volume. The real problem is that the same instruction "access element at position X and do something with it" is being repeated with only one thing changing each time: the index. Repetition with a controlled variation is exactly what a **loop** is designed to do.

A loop is a control structure that repeats a block of instructions for as long as a condition is true, or for a defined number of iterations. Without loops, every program that processes collections, reads files, scans user input, or retries failed operations would be impossible to write.

Java provides four loop structures: `for`, `while`, `do-while`, and `for-each`. They are not interchangeable. Each has a specific use case, and choosing the wrong one is a logic decision, not just a style preference.

---

## The classic `for` loop

The `for` loop is the right choice when you know, at the moment the loop starts, exactly how many times it needs to run. Iterating through an array is the canonical case.

### Complete anatomy

```java
for (int i = 0; i < grades.length; i++) {
    System.out.println(grades[i]);
}
```

The `for` header has three parts, separated by semicolons:

| Part | In the example | Role |
|---|---|---|
| **Initialization** | `int i = 0` | Declares and initializes the counter. Runs exactly once, before the loop starts. |
| **Condition** | `i < grades.length` | Evaluated before each iteration. If `true`, the body runs. If `false`, the loop ends. |
| **Update** | `i++` | Runs after each iteration, before the condition is checked again. |

The execution order is: Initialization → Condition → Body → Update → Condition → Body → Update → ... → Condition fails → loop ends.

### Variations

The three parts of the `for` header are flexible. The counter does not have to start at `0`, increment by `1`, or go forward.

**Counting down:**
```java
for (int i = grades.length - 1; i >= 0; i--) {
    System.out.println(grades[i]);
}
```

**Stepping by more than 1** (every other element):
```java
for (int i = 0; i < grades.length; i += 2) {
    System.out.println(grades[i]);
}
```

**Multiple variables in the header** (less common, but valid):
```java
for (int i = 0, j = grades.length - 1; i < j; i++, j--) {
    // i moves forward, j moves backward simultaneously
}
```

### Common pitfalls

**Using `<=` instead of `<` with `.length`:** `i <= grades.length` causes the loop to reach index `grades.length`, which does not exist → `ArrayIndexOutOfBoundsException`.

**Modifying the counter inside the body:** Changing `i` inside the loop body (e.g., `i = i + 2` inside a loop that also does `i++` in the header) produces logic errors that are hard to trace.

**An empty `for` loop:** The body is optional in Java syntax, which means a misplaced semicolon creates an infinite no-op loop and the actual body runs only once after:

```java
for (int i = 0; i < 10; i++); // The semicolon is the entire body — the loop does nothing
System.out.println("This runs once, after the loop"); // Not part of the loop
```

---

## The `while` loop

The `while` loop is the right choice when you do not know in advance how many iterations are needed. The loop continues for as long as a condition remains true, and the number of iterations is determined at runtime.

### Anatomy

```java
while (condition) {
    // body
}
```

The condition is evaluated before every iteration. If it is false from the start, the body never runs (not even once).

```java
int attempts = 0;
while (attempts < 3) {
    System.out.println("Attempt " + (attempts + 1));
    attempts++;
}
```

### Choosing `for` vs. `while`

The practical rule: if the number of iterations is controlled by a counter you can define upfront, use `for`. If the loop depends on a condition that changes based on events or data you cannot predict, use `while`.

Validating user input is the classic `while` case:

```java
Scanner scanner = new Scanner(System.in);
int input = scanner.nextInt();

while (input < 0 || input > 100) {
    System.out.println("Invalid. Enter a value between 0 and 100.");
    input = scanner.nextInt();
}
```

You do not know how many times the user will enter invalid data. A `for` loop would force you to guess.

### Common pitfalls

**Infinite loop:** If the condition never becomes false, the program hangs. The two causes are: the condition is logically always true, or the variable being tested is never updated inside the body.

```java
int i = 0;
while (i < 10) {
    System.out.println(i);
    // Missing i++ → i stays 0 forever → infinite loop
}
```

**Forgetting that the body may never execute:** When the condition is false on the first check, the body is skipped entirely. If your program depends on the body running at least once, `while` is the wrong tool; `do-while` is.

---

## The `do-while` loop

The `do-while` loop has one defining characteristic that separates it from every other loop in Java: the body executes first, and the condition is checked afterward. This guarantees that the body runs at least once, unconditionally.

### Anatomy

```java
do {
    // body
} while (condition);
```

Note the semicolon after the closing parenthesis. It is mandatory and often forgotten.

### The crucial difference

In a `while` loop, the condition acts as a gate: if it's false from the start, the body is never entered. In a `do-while`, the body is always entered first; the condition only determines whether to repeat.

```java
// while: may execute 0 times
while (false) {
    System.out.println("This never prints");
}

// do-while: always executes at least once
do {
    System.out.println("This always prints once");
} while (false);
```

### Its real niche

`do-while` is the correct tool when an action must always be performed first, and then you check whether to repeat it. Menu-driven programs are the canonical example: you always display the menu at least once before asking whether the user wants to continue.

```java
int choice;
do {
    System.out.println("1 - New game");
    System.out.println("2 - Load game");
    System.out.println("0 - Exit");
    choice = scanner.nextInt();
} while (choice != 0);
```

Implementing this with a `while` would require either duplicating the menu display code (before the loop and inside it) or using an artificial flag variable. `do-while` eliminates that duplication.

### Common pitfalls

**Missing semicolon:** `} while (condition)` without the final `;` is a compile error.

**Assuming it works like `while`:** Placing a condition that should prevent the body from running at all into a `do-while` produces a bug that is hard to detect, because the body always runs once regardless.

---

## The `for-each` loop

The `for-each` loop (formally called the **enhanced for loop**) exists to simplify one specific task: iterating through all elements of an array or collection from start to finish, in order, without needing the index.

### Anatomy

```java
for (int grade : grades) {
    System.out.println(grade);
}
```

Read as: "for each `int` named `grade` in the array `grades`, execute the body." The variable `grade` holds a copy of each element sequentially; it is declared specifically for the loop and does not exist outside it.

### Critical limitations

`for-each` trades flexibility for readability. That trade-off has hard limits:

| Operation | `for-each` capable? | Reason |
|---|---|---|
| Read each element | ✓ Yes | Direct access to value |
| Modify each element (primitives) | ✗ No | The loop variable is a copy; modifying it does not affect the array |
| Access the current index | ✗ No | No counter variable is exposed |
| Iterate in reverse | ✗ No | Direction is fixed: first to last |
| Iterate over two arrays simultaneously | ✗ No | Only one iterable per loop |

The modification limitation deserves emphasis because it is consistently misunderstood:

```java
int[] numbers = {1, 2, 3};
for (int n : numbers) {
    n = n * 2; // Modifies the local copy, NOT the array
}
System.out.println(numbers[0]); // Still prints 1
```

To actually modify array elements, use a classic `for` with index-based assignment (`numbers[i] = numbers[i] * 2`).

### When to use it — and when not to

Use `for-each` when you need to read every element of an array or collection in order and you have no need for the index. It is cleaner and eliminates the off-by-one risk entirely.

Do not use `for-each` when you need the index, when you are modifying elements, when you need to iterate partially, or when you need to iterate in reverse.

---

## `break` and `continue`: controlling the flow mid-loop

Both `break` and `continue` alter the normal execution of a loop from inside its body. They are not interchangeable.

**`break`** terminates the loop entirely. Execution jumps to the first statement after the loop's closing brace. The remaining iterations are abandoned.

**`continue`** skips the rest of the current iteration and jumps directly to the next one. The loop itself does not end.

```java
// break: stop as soon as we find the first negative grade
for (int i = 0; i < grades.length; i++) {
    if (grades[i] < 0) {
        System.out.println("Invalid grade found at index " + i);
        break; // No further elements are checked
    }
}

// continue: skip grades of zero and process only the rest
for (int grade : grades) {
    if (grade == 0) {
        continue; // Jump to the next iteration
    }
    System.out.println("Processing grade: " + grade);
}
```

### Labeled `break`

A regular `break` only exits the innermost loop. When you have nested loops and need to exit an outer one from inside an inner one, Java provides **labeled `break`**.

A label is an identifier placed directly before a loop, followed by a colon.

```java
outerLoop:
for (int i = 0; i < 5; i++) {
    for (int j = 0; j < 5; j++) {
        if (i == 2 && j == 3) {
            break outerLoop; // Exits both loops, not just the inner one
        }
        System.out.println("i=" + i + ", j=" + j);
    }
}
System.out.println("Execution continues here after labeled break");
```

Without the label, `break` on that line would only exit the inner loop, and the outer loop would continue. The label makes the target of the `break` explicit.

Labeled `break` is not a common pattern, but it is the correct tool when the alternative is a boolean flag variable used purely to propagate the exit condition from the inner loop outward (which is more complex and harder to read).

### The abuse to avoid

Using `break` as a substitute for a well-designed loop condition is a code smell. If your loop's exit condition can be expressed directly in the `while` or `for` header, express it there. Reserve `break` for genuinely exceptional exits: finding a specific element, hitting an error condition, or responding to external input mid-iteration.

---

You can see how each of these structures connects back to the core problem that introduced them: a collection of data that needs to be processed systematically. Arrays make mass data storage possible. Loops make processing that data tractable. The four loop types are not variations of the same thing! They are answers to four distinct questions: *how many times?* (`for`), *while what is true?* (`while`), *do it once, then check?* (`do-while`), and *just give me every element, cleanly?* (`for-each`). `break` and `continue` exist for the cases where the answer changes mid-execution.