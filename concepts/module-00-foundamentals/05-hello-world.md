# Your First Program: Hello World

Every language begins here. Not because it's useful, but because it proves everything works: the JDK is installed, the environment is configured, the compiler compiles, and the runtime runs.

## 1. Write the code

Open any text editor (Notepad, VS Code, or whatever you prefer) and type:

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

Save it as `HelloWorld.java`. The file name **must** match the public class name exactly — including capitalization.

### 2. Understand what you wrote

| Element                                  | What it means                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| ---------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `public class HelloWorld`                | Declares a public class named `HelloWorld`. In Java, all code lives inside classes.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `public static void main(String[] args)` | The **entry point** of the program. The JVM looks for this exact method (action) signature to start execution. `public` means accessible from anywhere (allowing other classes and the JVM itself to access and execute it), `static` means it belongs to the class itself (usually, methods require an object/instance to be created and used; static methods belong to the class, so they can run without any object.), `void` means it returns nothing (The `main` method executes everything and terminates, without returning any data to the JVM or to any other method or class that might use that data.), and `String[] args` accepts command-line arguments (When running `java MyProgram hello 42`, these extra words arrive as a list of strings: `args[0] = "hello"`, `args[1] = "42"`.). |
| `System.out.println(...)`                | Prints text to the console. `System` is a built-in class (a class built into Java that contains system tools; such as access to the keyboard, screen, and errors), `out` is its output stream (an object within System that acts as a communication channel for sending data from your program to the external environment: the console.), and `println()` is the method that prints a line and moves the cursor to the next one (sends the text to `out`, which displays it on the console, and automatically moves to the next line).                                                                                                                                                                                                                                                                |

## 3. Compile it

Open a terminal, navigate to the folder where you saved the file, and run:

```bash
javac HelloWorld.java
```

This invokes the **Java compiler**. It reads your `.java` file (human-readable source code) and translates it into a `.class` file (bytecode that the JVM can execute). If the code has no errors, the command produces no output (silence means success). You'll see a new file called `HelloWorld.class` in the same directory.

## 4. Run it

```bash
java HelloWorld
```

Note: no `.class` extension, no `.java` extension: just the class name. This command starts the JVM, which loads your compiled bytecode, finds the `main` method, and executes it.

The output:
```
Hello, World!
```

That's it. You wrote source code, compiled it into bytecode, and the JVM executed it. Three steps: **write, compile, run**. That reflect the fundamental cycle of Java development.

## 5. The shortcut (Java 11+)

Since JDK 11, you can skip the explicit compilation step for single-file programs:

```bash
java HelloWorld.java
```

This compiles the file in memory and runs it immediately. It's convenient for quick tests, learning, and small scripts. Since JDK 22, this even works across multiple `.java` files (JEP 458). But for real projects, the traditional `javac` → `java` workflow (or a build tool like Maven/Gradle) is the standard.