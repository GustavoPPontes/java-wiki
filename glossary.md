# Glossary - Technical Terms in Simple Language

## A

**Abstraction**
The process of ignoring irrelevant details and focusing only on what matters for the solution.
One of the four pillars of Computational Thinking.

**Access Modifier**
A keyword that controls where a class, method, or variable can be accessed from.
Examples: `public`, `private`, `protected`.

**Algorithm**
A finite, ordered, and unambiguous sequence of instructions designed to solve a specific problem.
It is the logic behind the solution, independent of any programming language.

**Allocation (Memory Allocation)**
The process of reserving a block of memory on the heap to hold an object's data.
Triggered by the `new` keyword before the constructor runs.

**AND (`&&`)**
A logical operator that returns `true` only if both sides are `true`.
Uses short-circuit evaluation: if the left side is `false`, the right side is never checked.

**AND (`&`) — Bitwise**
A bitwise operator that compares two numbers bit by bit.
Returns `1` only where both corresponding bits are `1`.

**Android**
A mobile operating system based on Linux.
Uses Java and Kotlin as its primary development languages.

**Array**
A fixed-size, ordered collection of elements of the same type stored in contiguous memory positions.
Each element is accessed by a numeric index starting at `0`.

**Array Literal**
A shorthand syntax that declares, initializes, and assigns all values of an array at once.
Example: `int[] grades = {8, 7, 9, 6, 10};`

**ArrayIndexOutOfBoundsException**
A runtime crash that occurs when you try to access an index that does not exist in an array.
The most common cause is using `.length` instead of `.length - 1` as the last index.

**Apache Hadoop / Spark / Kafka**
Open-source frameworks used for Big Data processing.
They run on the JVM and handle massive amounts of data across clusters.

**Arithmetic Operators**
Symbols that perform mathematical operations on numeric values.
Examples: `+`, `-`, `*`, `/`, `%`.

**Arguments (args)**
Extra information passed to a program when it starts.
In the terminal, these are the words you type after the program name.

**Assignment**
The operation of replacing the current value of a variable with a new one.
Done with the `=` operator after the variable already has a value.

**Assignment Operator (`=`)**
The symbol that stores the value on the right into the variable on the left.
Does not mean "equals" in the mathematical sense.

**Atomic Step**
A sub-problem small enough that it cannot be broken down further usefully.
The stopping point of decomposition.

**Attribute (Field / Instance Variable)**
A variable declared directly inside a class body, outside any method.
Each object created from the class gets its own independent copy of every attribute.

**Autoboxing**
Java's automatic conversion between a primitive type and its corresponding wrapper class.
Example: converting `int` to `Integer` without explicit code.

## B

**Backend**
The "behind-the-scenes" part of an application.
Handles data, logic, and servers. Users don't see it directly.

**Backward Compatibility**
The ability of newer software to run code or files created in older versions.
Java is famous for ensuring old code still works on new versions.

**bin (Folder)**
Short for "binary". It is the subfolder inside the JDK that contains the actual executable files.
This is where `java` and `javac` live.

**Binary**
The base-2 number system used by computers.
Represents all values using only `0` and `1`.

**BigDecimal**
A Java class used for precise decimal arithmetic.
The correct choice when working with money or financial calculations, where floating-point errors are unacceptable.

**Bit**
The smallest unit of data in a computer.
Has only two possible values: `0` or `1`.

**Bitbucket**
A web-based Git hosting platform.
Provides repository hosting, code review tools, and CI/CD features.

**Bitwise Operators**
Operators that work directly on the binary representation of integer values.
Examples: `&`, `|`, `^`, `~`, `<<`, `>>`.

**Blueprint**
A metaphor for what a class is: a definition that describes what an object will look like.
The blueprint itself is not the building — the class itself is not the object.

**`boolean`**
A primitive type that stores only `true` or `false`.
Used for conditions and decision-making.

**Boundary Case**
A test input that sits exactly at the limit of a condition (e.g., grade = 7 when the threshold is >= 7).
Where most bugs are found.

**Braces (`{}`)**
Curly brackets used to define a block of code that belongs to a structure like `if`, `for`, or a method.
Always using them — even for single-line blocks — prevents silent bugs.

**Branch**
An independent line of development in a Git repository.
Allows you to work on changes without affecting the main codebase.

**Branching**
The act of creating and working on branches.
Makes parallel development possible.

**`break`**
A keyword that immediately terminates the current loop or `switch` block.
Execution jumps to the first statement after the closing brace of the structure.

**Boolean Flag**
A `boolean` variable used to track a condition across multiple iterations or scopes.
Often a sign that the code structure could be simplified with `break` or better loop design.

**Buffer**
A temporary memory area that holds data while it is being transferred or processed.
In `Scanner`, unread characters (like `\n`) stay in the buffer until consumed.

**Buffer Trap**
A common `Scanner` bug where a leftover newline character in the buffer causes the next `nextLine()` to read an empty string.
Fixed by calling `sc.nextLine()` immediately after `nextInt()` or `nextDouble()`.

**Bug**
An error or flaw in a program that causes incorrect behavior. Can be a syntax error or a logic error.
Usually fixed in a separate branch and committed as a patch.

**Build Artifact**
The final output of the build process (like a `.jar` file).
It is the "product" ready to be executed or distributed.

**Build Tool**
A program that automates the process of compiling, testing, and packaging code.
In Java, the most common are Maven and Gradle.

**`byte`**
The smallest integer primitive type in Java.
Uses 8 bits and stores values from -128 to 127.

**Bytecode**
The intermediate code generated by the Java compiler.
It's not readable by humans or machines directly; only the JVM can run it.

## C

**camelCase**
A naming convention where the first word is lowercase and each subsequent word starts with an uppercase letter.
Used for variable and method names in Java (e.g., `studentGrade`).

**Case Sensitivity**
A rule where the computer distinguishes between uppercase and lowercase letters.
In Java, `HelloWorld` and `helloworld` are considered completely different things.

**Cast (Type Cast)**
An explicit instruction to convert a value from one type to another.
Example: `(double) a` temporarily treats `a` as a `double` for one operation.

**`char`**
A primitive type that stores a single Unicode character.
Uses single quotes: `'A'`.

**Chained Ternary**
A ternary operator nested inside another ternary.
Legal in Java but extremely hard to read. Use `if/else if` instead.

**CI/CD (Continuous Integration / Continuous Deployment)**
A set of automated practices that build, test, and deploy code.
Ensures changes are integrated and released quickly and safely.

**Class**
The basic building block of a Java application. It describes the attributes and methods every object of that type will have.
It acts as a template for creating objects. Each `.java` file usually contains one class. No memory is allocated for a class when it is defined — only when an object is created from it.

**Class Field (Instance Variable)**
A variable declared directly inside a class, outside any method.
Automatically initialized to a default value by Java.

**Class Name**
The identifier given to a class.
In Java, the file name must match the name of the `public class` exactly.

**Clone**
The act of copying a remote repository to your local machine.
Done with `git clone`.

**CMD (Command Prompt)**
The classic, basic command-line interpreter for Windows.
It is older and simpler than PowerShell, mainly used for executing basic legacy commands.

**Code Review (Git)**
The process of examining someone else's code before merging it.
Usually done through pull requests on platforms like GitHub.

**Codebase**
The entire collection of source code for a project.
Includes all files tracked in the repository.

**CodeWars**
An online platform with coding challenges of varying difficulty.
Used to practice programming logic and problem-solving.

**Cognitive Load**
The mental effort required to process information.
Solving logic and syntax at the same time increases cognitive load unnecessarily.

**Collection**
A data structure that groups multiple elements together.
Arrays are the simplest form; Java also provides more flexible collection types like `ArrayList`.

**Command-Line Interface (CLI)**
A way of interacting with a program by typing specific lines of text.
Instead of clicking buttons, you type commands to get things done. Git is a classic example of a CLI.

**Compile-time Error**
An error detected by the compiler before the program runs.
Examples: using an uninitialized variable or assigning the wrong type.

**Compiler (javac)**
A tool that translates human-readable code into machine-readable bytecode.
It checks for errors before the program even runs.

**Compound Assignment Operators**
Operators that combine an arithmetic operation with assignment in one step.
Examples: `+=`, `-=`, `*=`, `/=`, `%=`.

**Computational Thinking**
A structured framework for solving problems in a precise and scalable way.
Composed of four pillars: Decomposition, Pattern Recognition, Abstraction, and Algorithms.

**Commit**
A snapshot of the project at a specific moment.
Includes the changes made, the author, a timestamp, and a message.

**Commit Message**
A short description written when creating a commit.
Explains what was changed and why.

**Concatenation**
The operation of joining two or more strings together.
In Java, the `+` operator performs concatenation when at least one operand is a `String`.

**Conditional Structure**
A programming construct that executes different blocks of code depending on whether a condition is true or false.
The foundation of decision-making in any program. Examples: `if`, `switch`.

**Conflict Resolution (Git)**
The process of manually fixing differences when two branches modify the same lines of code.
Required when a merge conflict occurs.

**Constant**
A variable whose value cannot change after it is initialized.
Declared with the `final` keyword and named in `SCREAMING_SNAKE_CASE`.

**Constructor**
A special method called automatically by Java immediately after a new object is allocated.
It has the same name as the class and no return type. Its job is to set the initial state of the object's attributes.

**`continue`**
A keyword that skips the rest of the current loop iteration and jumps to the next one.
The loop itself does not end — only the current pass is interrupted.

**Contiguous Memory**
Memory positions that are physically adjacent to each other.
Arrays store all their elements in contiguous positions, making index-based access fast.

**Convention**
A set of agreed-upon rules or standards for doing things (like folder naming).
Following conventions makes it easier for different developers to work on the same project.

**Counter Variable**
A variable used to track the number of iterations in a loop.
Commonly named `i`, `j`, or `k` by convention.

**Coupling**
The degree to which one part of a system depends on another.
Excessive coupling means changing one thing breaks many others.

## D

**Data Organization**
The way data is structured and stored for efficient access and manipulation.
One of the core concepts of programming logic.

**Declaration**
The operation of telling the compiler that a variable of a certain type exists.
Example: `int age`;

**Declarative Programming**
A paradigm where you describe *what* you want, and the system decides *how* to produce it.
Examples: SQL, HTML.

**Decomposition**
Breaking a large problem into smaller, manageable sub-problems.
The first and most fundamental pillar of Computational Thinking.

**Decision-making (Selection)**
The ability to choose between different paths based on a condition.
Expressed in code as `if/else` statements.

**Default Value**
The value Java automatically assigns to class fields when no explicit value is given.
Examples: `0` for integers, `false` for booleans, `null` for objects.

**`default` (switch)**
The fallback case in a `switch` statement or expression that runs when no other case matches.
Required in Switch Expressions when the compiler cannot guarantee all cases are covered.

**Dependency**
An external library or piece of code that your project needs to function.
Instead of writing everything from scratch, you "depend" on these existing tools.

**De Facto Standard**
A tool or practice that becomes the accepted standard through widespread use.
Git is the de facto standard for version control.

**Deployable (Git)**
In a stable state ready to be released or used in production.
The `main` branch is typically kept deployable.

**Diff (Git)**
A comparison between two versions of a file.
Shows what lines were added, removed, or changed.

**Discrete Values**
Specific, individual values as opposed to ranges or continuous values.
`switch` can only compare against discrete values, not ranges like `x > 10`.

**Distributed Version Control System (DVCS)**
A version control system where every user has a complete copy of the repository and its history.
Git is a distributed system.

**Dividend**
The number being divided in a division operation.
In `7 % 2`, the dividend is `7`.

**`double`**
A primitive type that stores decimal numbers with about 15-16 digits of precision.
Uses 64 bits. The default choice for decimal arithmetic in Java.

**`do-while` Loop**
A loop that executes its body first and checks the condition afterward.
Guarantees the body runs at least once, regardless of the condition.

## E

**Enhanced `for` Loop (`for-each`)**
A simplified loop syntax for iterating through all elements of an array or collection in order.
Does not expose the index and cannot modify primitive array elements directly.

**Entry Point**
The specific place where a program starts its execution.
In Java, the entry point is always the `main` method.

**`enum`**
A special Java type that defines a fixed set of named constants.
Fully supported by `switch` statements and expressions.

**Environment Variables**
Settings in your operating system that store information about the environment.
They act like "global variables" that any program can read.

**Equality Operator (`==`)**
An operator that checks if two values are equal.
For primitives, compares values. For objects, compares memory references — not content.

**Executable**
A file that contains a program or a sequence of instructions for the computer to run.
In the terminal, you run these by typing their name.

**Exponent (Floating-point)**
The part of a floating-point number that controls its magnitude or scale.
Determines how far the decimal point shifts.

## F

**Fall-through**
The behavior in a classic `switch` where execution continues into the next case when `break` is missing.
Intentional in some patterns, but a common source of silent bugs when accidental.

**Feature**
A new functionality added to a software project.
Often developed in its own branch (Git).

**Field**
See *Attribute*.

**`final`**
A keyword that prevents a variable from being reassigned after initialization.
Also prevents methods from being overridden and classes from being extended.

**Finite**
Having a clear beginning and end.
A required property of any valid algorithm.

**Flag**
A boolean value used to represent the on/off state of a feature or condition.
In bitwise systems, individual bits serve as flags within a single integer.

**`float`**
A primitive type that stores decimal numbers with about 7 digits of precision.
Uses 32 bits and requires an `f` suffix on literals (e.g., `3.14f`).

**Floating-point**
A way of representing decimal numbers in binary.
Cannot represent all decimal values exactly, which leads to small precision errors.

**Floating-point Division**
Division where at least one operand is a `double` or `float`.
Returns a decimal result instead of truncating.

**Flowchart**
A visual diagram that represents the steps of an algorithm using shapes and arrows.
An alternative to pseudocode for expressing logic without code.

**`for` Loop**
A loop designed for situations where the number of iterations is known before the loop starts.
Its header contains three parts: initialization, condition, and update.

**`for-each` Loop**
See *Enhanced `for` Loop*.

**Fork (Git)**
A personal copy of someone else's repository on a hosting platform.
Common in open-source collaboration.

**Format Specifier**
A placeholder in a `printf` format string that gets replaced by an argument value.
Examples: `%d` for integers, `%s` for strings, `%.2f` for floats with 2 decimal places.

**Format String**
A string passed to `printf` that contains text mixed with format specifiers.
Controls exactly how the output is displayed.

**Framework**
A pre-built set of tools and libraries that provide a foundation for developing applications.
Examples include Spring Boot, Quarkus, and Micronaut.

**Framework (Problem-solving)**
A structured step-by-step approach to solving a problem consistently.
Helps organize thinking before writing any code.

**Functional Programming**
A paradigm where logic is organized through the application of pure functions with no side effects.
Examples: Haskell, Erlang, Clojure.

## G

**Garbage Collector**
A JVM mechanism that automatically frees memory occupied by objects no longer in use.
Removes the need for manual memory management in Java.

**Git**
A distributed version control system.
Tracks changes to files and manages collaboration between developers.

**GitHub**
A web platform built on top of Git.
Provides hosting, collaboration tools, and automation features.

**GitHub Actions**
GitHub’s built-in CI/CD automation tool.
Runs workflows like testing or deployment automatically.

**GitLab**
A web-based Git hosting platform similar to GitHub.
Includes integrated CI/CD and project management features.

**Gradle**
A modern tool used to build and automate software projects.
Similar to Maven, but uses a different language (Groovy or Kotlin) for its configuration.

## H

**Hash Function**
An algorithm that converts data into a fixed-size numeric value.
Used in cryptography and data structures. Relies heavily on XOR and shift operations.

**Heap**
A large, dynamic memory area managed by the JVM where objects are stored at runtime.
Managed by the Garbage Collector. Every object created with `new` lives here.

**History (Git)**
The complete timeline of commits in a repository.
Records what changed, when, and by whom.

## I

**IDE (Integrated Development Environment)**
A powerful text editor specialized for coding (like IntelliJ IDEA or VS Code).
It combines a code editor, debugger, and build tools in one place.

**Identifier**
A name given to a variable, class, method, or package by the programmer.
Must follow compiler rules and cannot be a reserved keyword.

**`import`**
A keyword that brings a class or package into scope so it can be used without its full name.
Example: `import java.util.Scanner`

**Infinite Loop**
A loop whose condition never becomes false, causing the program to run forever.
Usually caused by forgetting to update the variable being tested in the condition.

**Init (git init)**
The command that creates a new Git repository in a folder.
Turns a normal directory into a tracked project.

**Initialization**
The operation of assigning a value to a variable for the first time.
Example: `age = 20`;

**Instance**
One specific, concrete object created from a class and living in memory.
Two instances of the same class are independent — they do not share attribute values.

**Instance Variable**
See *Attribute*.

**`int`**
The standard integer primitive type in Java.
Uses 32 bits and stores values from roughly -2.1 billion to 2.1 billion.

**Integer Division**
Division between two integer values where the decimal part is discarded entirely.
`5 / 3` returns `1`, not `1.666...`.

**Integer Literal**
A number written directly in source code representing a whole number value.
`long` literals require an `L` suffix; bare numbers are treated as `int` by default.

**Infinite Loop**
A sequence of instructions that repeats forever because it never reaches a stopping condition.
Causes the program to crash or consume resources indefinitely.

**Input**
The data provided to a program or algorithm to be processed.
The starting material for any computation.

**Input Stream**
A channel through which data flows into a program.
`System.in` is the standard input stream connected to the keyboard.

**Instance**
A specific "copy" of a class created in memory (an object).
While a class is a blueprint, an instance is the actual house built from it.

**IPO (Input, Processing, Output)**
A framework for breaking down any computational problem into three parts.
Helps identify what data comes in, what happens to it, and what comes out.

**Issue**
A task, bug report, or feature request tracked on platforms like GitHub.
Used to organize and discuss work.

**Iterable**
Any object that can be traversed element by element by a loop.
Arrays and Java collections are iterable.

**Iteration (Repetition)**
The ability to repeat a set of instructions while a condition is true. (One complete execution of a loop body.)
Expressed in code as `for` or `while` loops. A loop with 5 repetitions performs 5 iterations.

## J

**Java**
A high-level, object-oriented programming language designed to be platform-independent.
Its motto is "Write Once, Run Anywhere" (WORA).

**JAVA_HOME**
A specific environment variable that points to the main folder where Java is installed.
Used by other software to find where the Java compiler and libraries are located.

**java (Command)**
The command used in the terminal to run a compiled Java program.
It starts the JVM.

**javac (Command)**
The Java Compiler command.
It converts your .java source code files into .class bytecode files.

**JDK**
Java Development Kit. The complete toolkit for developing in Java.
Includes the compiler, debugger, and the JRE (JVM + standard libraries).

**JRE**
Java Runtime Environment. The package needed to run Java applications.
Contains the JVM and standard libraries, but no development tools.

**JVM**
Java Virtual Machine. The engine that executes Java bytecode.
Acts as a bridge between the code and the specific hardware/OS.

**`.jar` (Java ARchive)**
A file format that packages many Java classes and associated metadata into a single file.
It is the standard way to distribute Java applications or libraries.

**`.java` (File)**
A plain text file containing Java source code.
This is what developers write before it gets compiled into bytecode.

## K

**Kernel (Linux Kernel)**
The core part of the Linux operating system.
Git was originally created to manage its development.

**Keyword (Reserved Word)**
A word that Java has claimed for its own grammar and cannot be used as an identifier.
Examples: `class`, `static`, `void`, `return`, `new`.

**Kotlin**
A modern programming language that also runs on the JVM.
Fully compatible with Java and preferred by Google for Android development.

## L

**Label (Labeled `break`)**
An identifier placed before a loop, followed by a colon, used as a target for `break` or `continue`.
Allows exiting an outer loop from inside a nested inner loop.

**Lambda Expression**
A concise way to represent a function as a value, introduced in Java 8.
Brings functional programming patterns into Java.

**LeetCode**
An online platform with coding challenges focused on algorithms and data structures.
Widely used for technical interview preparation.

**Left Shift (`<<`)**
A bitwise operator that moves all bits to the left by a given number of positions.
Each shift left is equivalent to multiplying the value by 2.

**Local Repository**
A Git repository stored on your own machine.
Contains the full project history.

**Local Variable**
A variable declared inside a method.
Has no default value; Java refuses to compile if it is used before being initialized.

**Logic Error**
A mistake in the reasoning of a program that produces wrong results without crashing.
More subtle and harder to detect than syntax errors.

**Logical Operators**
Operators that combine or invert boolean expressions.
Examples: `&&` (AND), `||` (OR), `!` (NOT).

**`long`**
A primitive type for very large integers.
Uses 64 bits and requires an `L` suffix on literals (e.g., `10_000_000_000L`).

**Long-Term Support (LTS)**
A version of software that is guaranteed to receive updates and security patches for several years.
Focuses on stability for corporate environments.

**Loop**
A control structure that repeats a block of instructions for as long as a condition is true or for a fixed number of iterations.
Java provides four: `for`, `while`, `do-while`, and `for-each`.

**`.length` (Array Property)**
A property that returns the total number of slots in an array.
It is a property, not a method — no parentheses are used.

## M

**Main (Branch)**
The default primary branch in a Git repository.
Represents the stable version of the project.

**`malloc()`**
A function in C used to manually request memory allocation at runtime.
Not used in Java, where memory management is handled automatically by the JVM.

**Mantissa (Significand)**
The part of a floating-point number that stores its significant digits.
More bits in the mantissa means higher precision.

**Memory Address**
A specific location in RAM where data is stored.
In Java, developers never deal with addresses directly — the JVM handles them.

**Memory Alignment**
The practice of storing data at memory addresses that match certain size boundaries.
Can cause the JVM to allocate more space than logically needed (e.g., for `boolean`).

**Memory Leak**
A bug where a program fails to release memory it no longer needs.
Common in languages like C; prevented in Java by the Garbage Collector.

**Memory-Resident**
Describes data that currently exists and is accessible in RAM.
An object is memory-resident from the moment `new` allocates it until the Garbage Collector removes it.

**Merge**
The act of combining changes from one branch into another.
Integrates parallel work back into a single line of development.

**Merge Conflict**
A situation where Git cannot automatically combine changes.
Requires manual correction.

**Method**
A block of code declared inside a class that defines an operation any object of that class can perform.
It is like a "verb" in the programming language (e.g., `println` performs the action of printing). When called on a specific object, it runs in the context of that object's attribute values.

**Microservices**
An architectural style where an application is built as a collection of small, independent services.
Each service runs a specific function and communicates via the network.

**Mirroring**
The practice of recreating the exact same folder structure in two different places.
In Java, the test folder mirrors the main folder to keep tests organized by the same packages.

**Modulo (`%`)**
An operator that returns the remainder of a division.
`5 % 3` returns `2`. Commonly used to check divisibility or cycle through ranges.

## N

**Naming Convention**
A community-agreed standard for naming variables, classes, and methods.
Improves readability and consistency across codebases.

**Nested Conditionals**
An `if` statement placed inside another `if` block.
Valid when the inner condition only makes sense after the outer one is confirmed. Avoid going deeper than two levels.

**Nested Loop**
A loop placed inside the body of another loop.
The inner loop completes all its iterations for each single iteration of the outer loop.

**`new` (Keyword / Operator)**
An operator that triggers three steps: allocates memory on the heap, calls the constructor, and returns a reference to the new object.
Every object must be created with `new`.

**Newline Character (`\n`)**
A special character that represents the end of a line of text.
Left behind in the buffer by `nextInt()` and `nextDouble()`, causing the buffer trap.

**NOT (`!`)**
A logical operator that inverts a boolean value.
`!true` becomes `false`, and `!false` becomes `true`.

**NOT (`~`) — Bitwise**
A bitwise operator that inverts every bit of a number.
In Java, `~n` always equals `-(n + 1)` due to two's complement representation.

**`null`**
A keyword representing the explicit absence of an object reference.
Primitives cannot be `null`; objects can.

**`NullPointerException`**
A runtime error that occurs when a program tries to use a method or field on a `null` reference.
One of the most common errors in Java.

## O

**Object**
A running, memory-resident instance of a class.
It holds its own copy of all attributes defined by the class and can perform all methods defined by the class.

**Object-Oriented Programming (OOP)**
A programming paradigm where code is organized around objects that bundle data and behavior together.
Organizes software design around data rather than functions. The primary paradigm of Java.

**Object Reference**
A variable that stores the memory address of an object, not the object itself.
When two object variables share a reference, changes through one affect the other.

**Off-by-one Error**
A logic mistake where a loop runs one iteration too many or too few.
The most common cause in arrays is using `<= .length` instead of `< .length`.

**Operand**
A value or variable on which an operator acts.
In `5 + 3`, both `5` and `3` are operands.

**Operator Precedence**
The set of rules that determines which operations are evaluated first in an expression.
Similar to the mathematical rule that multiplication happens before addition.

**OR (`||`)**
A logical operator that returns `true` if at least one side is `true`.
Uses short-circuit evaluation: if the left side is `true`, the right side is never checked.

**OR (`|`) — Bitwise**
A bitwise operator that compares two numbers bit by bit.
Returns `1` where at least one corresponding bit is `1`.

**Output**
The result produced by a program or algorithm after processing the input.
What the computation delivers at the end.

**Output Stream**
A communication channel used by a program to send data to an external destination (e.g, a file, console screen).
`System.out` is the standard channel to send data to the screen.

**Overflow**
What happens when a value exceeds the maximum size a type can hold.
Example: assigning a number too large for `int` without using `long`.

## P

**Package**
A way of organizing Java classes into namespaces (like `com.example`; named in all lowercase).
In the file system, a package corresponds to a folder structure.

**Paradigm**
A structural contract that defines the fundamental building block of a program and how logic is organized.
Examples: procedural, object-oriented, functional, declarative.

**PascalCase**
A naming convention where every word starts with an uppercase letter.
Used for class names in Java (e.g., `StudentRecord`).

**PATH**
An environment variable that lists folders where the operating system looks for commands.
If a folder is in the PATH, you can run its programs from any terminal location.

**Pattern Recognition**
The ability to identify similarities between problems to reuse known solutions.
The second pillar of Computational Thinking.

**Pointer**
A variable in languages like C that stores and manipulates memory addresses directly.
Java does not expose pointers to developers.

**Primitive Type**
A basic data type built directly into Java.
Stores values directly in memory with no methods or overhead. Java has 8: `byte`, `short`, `int`, `long`, `float`, `double`, `char`, `boolean`.

**`printf`**
A method on `System.out` that prints formatted output using a format string and arguments.
Follows C-style formatting with specifiers like `%d`, `%s`, and `%.2f`.

**`PrintStream`**
The Java class type of `System.out`.
Provides methods like `print()`, `println()`, and `printf()` for sending output to the console.

**`private`**
An access modifier that restricts visibility to within the same class only.
Hides internal details from the outside.

**Procedural Programming**
A paradigm where logic is organized as a sequence of instructions grouped into functions.
Examples: C, Pascal.

**Processing**
The set of operations performed on input data to produce the output.
The "middle step" in the IPO framework.

**Programming Logic**
The ability to structure reasoning through algorithms to solve problems in a way a machine can execute.
Independent of any specific programming language.

**`protected`**
An access modifier that allows visibility within the same package and in subclasses.
Used in inheritance hierarchies.

**Pseudocode**
An informal, human-readable description of an algorithm.
Written in plain language, not in any specific programming language syntax.

**`public`**
An access modifier that makes a class, method or variable accessible from anywhere in the project.
If it’s public, the JVM and other classes can see and use it. Required for the `main` method so the JVM can call it.

**Pure Function**
A function that always produces the same output for the same input and has no side effects.
A central concept in functional programming.

**`pom.xml`**
The configuration file for Maven.
It contains all the information about the project, including its dependencies and build instructions.

**PowerShell**
A modern and powerful shell developed by Microsoft.
It uses more complex commands than CMD and is used for advanced automation and system tasks in Windows.

**Platform (Web Platform)**
An online service that provides tools and infrastructure for development.
GitHub, GitLab, and Bitbucket are Git hosting platforms.

**Pull**
The act of downloading and integrating changes from a remote repository.
Done with `git pull`.

**Pull Request (PR)**
A request to merge changes from one branch into another via a hosting platform.
Allows discussion, review, and approval before merging.

**Push**
The act of sending local commits to a remote repository.
Done with `git push`.

## R

**RAM (Random Access Memory)**
The fast, temporary memory where the JVM stores data while a program runs.
Variables and objects live here during execution.

**Refactor**
The process of restructuring existing code without changing its behavior.
Improves readability or maintainability.

**Reference**
A variable that stores the memory address of an object, not the object itself.
Assigning one reference variable to another makes both point to the same object, not two independent copies.

**Relational Operators**
Operators that compare two values and return a boolean.
Examples: `==`, `!=`, `>`, `<`, `>=`, `<=`.

**Remainder**
The amount left over after integer division.
Returned by the modulo operator `%`.

**Remote Repository**
A version of the repository hosted on a server.
Shared among collaborators.

**Repository (Repo)**
A project folder managed by Git.
Contains files and their full version history (.git/).

**Resources**
Non-code files that the application needs at runtime.
Examples include configuration files, images, or database settings.

**`return`**
A keyword that exits a method and optionally sends a value back to the caller.
A method declared `void` uses `return` with no value, or omits it entirely. Constructors have no return type — not even `void`.

**Rework**
The time spent fixing or redoing work that was done incorrectly the first time.
Good decomposition and planning reduce rework significantly.

**Right Shift (`>>`)**
A bitwise operator that moves all bits to the right by a given number of positions.
Each shift right is equivalent to dividing the value by `2` (integer division). Preserves the sign bit.

**Root Directory**
The main "top-level" folder of a project or installation.
For the JDK, it is the folder that contains bin, lib, and other subfolders (e.g., C:\Program Files\Java\jdk-21).

**Runtime**
The period when a compiled program is actually executing.
Objects are created and destroyed at runtime, not at compile time.

**Runtime Error/Crash**
An error that occurs while the program is running, not during compilation.
`ArrayIndexOutOfBoundsException` and `NullPointerException` are common runtime crashes.

## S

**Scanner**
A built-in Java class used to read input from the user or other sources.
Commonly used to read keyboard input via `System.in`. Must be imported from `java.util` and connected to `System.in` for keyboard input.

SCREAMING_SNAKE_CASE (UPPER_SNAKE_CASE)
A naming convention where all letters are uppercase and words are separated by underscores.
Used for constants in Java (e.g., `MAX_SCORE`).

**Scope**
The region of code where a variable is visible and accessible.
Local variables are scoped to their method; attributes are scoped to the entire object's lifetime.

**Self-documenting Code**
Code written so clearly that its intent is obvious from the names and structure alone.
Good variable and method names eliminate the need for explanatory comments.

**Sequencing**
The correct ordering of instructions so that each step logically follows the previous one.
A fundamental concept of programming logic.

**Shadow (Variable Shadowing)**
When a local variable or parameter has the same name as an attribute, hiding the attribute from direct access.
Resolved by using `this.attributeName` to explicitly refer to the attribute.

**Shell**
The program that interprets your text commands and tells the operating system what to do.
It is the "brain" inside the terminal. Common examples are Bash (Linux/Mac) and PowerShell (Windows).

**`short`**
An integer primitive type smaller than `int`.
Uses 16 bits and stores values from -32,768 to 32,767.

**Short-circuit Evaluation**
A behavior where Java stops evaluating a logical expression as soon as the result is determined.
Prevents unnecessary or dangerous operations on the right side of `&&` and `||`.

**Side Effect**
Any change a function or method makes to state outside its own scope.
Modifying an attribute inside a method is a side effect.

**Sign Bit**
The leftmost bit in a signed integer that indicates whether the number is positive or negative.
`0` means positive, `1` means negative.

**Signed Integer**
An integer type that can represent both positive and negative numbers.
Java's `int` is a 32-bit signed integer.

**Signature (Method Signature)**
The unique combination of a method's name and its parameters.
The JVM uses the signature to identify exactly which method to run.

**State**
The current values of all attributes of an object at a given moment.
The constructor sets the initial state; methods can change it over time.

**Static Method**
A method that belongs to the class itself, not to any specific instance.
Cannot access instance attributes directly because it has no associated object.

**String Pool**
An area in Java's memory where string literals are stored and reused.
Two string literals with the same content may share the same object, making `==` return `true` — but this is an optimization, not a rule.

**Snapshot**
A saved state of the project at a specific moment.
Each commit represents a snapshot.

**Software Architecture**
The high-level structure of a software system, defining how its parts are organized and interact.
Good decomposition is the foundation of good software architecture.

**Source Code**
The human-readable instructions written by a programmer.
In Java, these are the files ending in `.java`.

**Spring Boot**
The most popular Java framework for building web and enterprise applications.
Simplifies the setup and configuration of complex systems.

**Staging Area (Git)**
An intermediate space where selected changes are prepared before committing.
Allows precise control over what goes into a commit.

**`static`**
A keyword indicating that a member (method or variable) belongs to the class itself, not to a specific instance.
You can run and acess a **static** method/member without creating an object first.

**Static Assets**
Files that do not change while the program is running.
Commonly refers to images, CSS files, or plain text documents included in the project.

**`String`**
A class (not a primitive) that represents a sequence of characters (text).
In Java, Strings are always wrapped in double quotes (e.g., `"Hello"`). Has built-in compiler support for literals (`"text"`) and comes with methods like `.equals()` and `.length()`.

**`String Literal`**
A sequence of characters written directly in code between double quotes.
Example: `"Hello, World!"`

**Strong Typing**
A feature where the programming language strictly enforces rules about data types.
Prevents errors by ensuring you don't treat text like a number by mistake.

**Switch Expression (Java 14+)**
A modern redesign of the classic `switch` that produces a value and eliminates fall-through.
Uses arrow syntax (`->`) instead of colons, and requires `yield` for multi-line cases.

**Switch Statement (Classic `switch`)**
A control-flow structure that jumps to a matching case based on a variable's value.
Requires `break` at the end of each case to prevent fall-through.

**Sync (Git)**
To update two repositories (remote and local) so they contain the same commits.
Happens when pushing or pulling.

**Syntax**
The set of grammatical rules that define how code must be written in a specific language.
Different from logic — syntax varies by language, logic does not.

**Syntax Error**
A mistake in the written structure of code that violates the language's rules.
Usually caught by the compiler before the program runs.

**`System.in`**
A static object representing the standard input stream (the keyboard).
Passed to `Scanner` to enable reading user input.

**`System.out`**
A static `PrintStream` object available in every Java program.
Used to send output to the console via `print()`, `println()`, and `printf()`.

**System.out.println**
The standard command to display text on the console.
It prints the content and then automatically moves to a new line.

## T

**Target / Build (Folder)**
The directory where the build tool places all generated files.
It is usually ignored by version control (like Git) because it can be recreated at any time.

**Terminal**
A text-based interface used to type commands to the computer.
It allows you to talk directly to the operating system without using a mouse or menus.

**Ternary Operator (`? :`)**
A compact operator that evaluates a condition and returns one of two values.
Syntax: `condition ? value_if_true : value_if_false`. Best used for simple, single-line assignments.

**`this`**
A reference inside a method or constructor that points to the specific object the code is currently running on.
Used to distinguish between class fields (attribute) and method parameters with the same name.

**Threads**
A small unit of a process that executes tasks.
Think of it as a "worker" inside a program. A single program can have multiple threads working at the same time to speed things up.

**Truth Table**
A table that shows every possible combination of boolean inputs and their resulting output.
Used to define the exact behavior of logical operators like `&&`, `||`, and `!`.

**Timestamp (Git)**
The recorded date and time when a commit was created.
Helps track the sequence of changes.

**Truncation**
The silent removal of the decimal part of a number when storing it in an integer type.
Example: in Java, storing `3.9` in an `int` results in `3`, not `4`.

**Token**
A single unit of input separated by whitespace (space, tab, or newline).
`Scanner.next()` reads one token at a time.

**Type**
A classification that defines what values a variable can hold and what operations are valid on it.
In OOP, a class defines a new custom type.

**Type Inference**
The ability of the compiler to automatically determine a variable's type from its assigned value.
Enabled in Java with the `var` keyword (Java 10+).

**Two's Complement**
The standard binary method Java uses to represent negative integers.
It allows the same hardware to handle both addition and subtraction.

## U

**Unambiguous**
Having exactly one possible interpretation.
A required property of algorithm instructions so the machine behaves predictably.

**Unary Operator**
An operator that acts on a single operand.
Examples: `!` (logical NOT) and `~` (bitwise NOT).

**Unicode**
An international standard that assigns a unique number to every character across all languages and symbols.
Java's `char` type is based on Unicode.

**Unit (Self-contained)**
In OOP, an object that bundles its own data and behavior together.
No external code needs to manage its internal state directly.

**Uninitialized Variable**
A variable that has been declared but not yet assigned a value.
Java refuses to compile code that tries to use a local uninitialized variable.

**Unsigned Right Shift (`>>>`)**
A bitwise operator that shifts bits to the right and always fills the left with `0`.
Unlike `>>`, it ignores the sign bit, treating the number as unsigned.

**Update (Loop)**
The third part of a `for` loop header that runs after each iteration.
Typically increments or decrements the counter variable (e.g., `i++` or `i--`).

## V

**`var`**
A keyword introduced in Java 10 that allows the compiler to infer a variable's type automatically.
The type is still fixed after inference — `var` only removes the need to write it explicitly.

**Variable**
A named location in memory that holds a value of a specific type.
Composed of three elements: type, name, and value.

**Version Control**
A system that tracks changes to files over time.
Allows reverting, comparing, and collaborating safely.

**Version**
A specific state of a project at a given time.
Can be restored or compared with others.

**Virtual Threads**
A lightweight type of thread introduced in modern Java.
Allows applications to handle thousands of simultaneous tasks with very low memory cost.

**`void`**
A keyword used in a method declaration to indicate that the method does not return any value.
It performs an action but doesn't give back a result (e.g, printing output).

## W

**Wrapper Class**
A class that wraps a primitive type into an object.
Examples: `Integer` for `int`, `Double` for `double`, `Boolean` for `boolean`.

**"Write Once, Run Anywhere" (WORA)**
Java's motto.
Philosophy that allows developers to write a program once and have it run on multiple operating systems and hardware platforms.

**`while` Loop**
A loop designed for situations where the number of iterations is not known in advance.
The condition is evaluated before every iteration; if false from the start, the body never runs.

## X

**XOR (`^`) — Bitwise**
A bitwise operator that returns `1` where the two corresponding bits are different.
Used in cryptography, hashing, and toggling flags.

## Y

**`yield`**
A keyword used inside a multi-line Switch Expression case block to specify the value the block produces.
Plays the same role that `return` plays in a method — but only inside Switch Expression blocks.

## Z

**Zero-indexed**
A convention where the first element of a collection is at position `0`, not `1`.
In a Java array of size `n`, valid indices range from `0` to `n - 1`.