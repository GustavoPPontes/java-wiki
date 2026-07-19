## Anatomy of a Java Project

A Java project can be as simple as a single `.java` file in a folder. But as soon as the project grows — more classes, tests, libraries, configuration files — structure becomes essential. Not for aesthetic reasons, but for survival. A well-organized project is easy to navigate, easy to build, and easy to hand off to another developer.

The **standard project structure** used by both Maven and Gradle (the two dominant build tools in the Java ecosystem) looks like this:

```
my-project/
├── src/
│   ├── main/
│   │   ├── java/              ← Your application source code (.java files)
│   │   │   └── com/
│   │   │       └── example/
│   │   │           └── App.java
│   │   └── resources/         ← Configuration files, static assets, etc.
│   └── test/
│       ├── java/              ← Your test source code
│       │   └── com/
│       │       └── example/
│       │           └── AppTest.java
│       └── resources/         ← Test-specific resources
├── target/ (or build/)        ← Compiled output (generated, not manually created)
├── pom.xml (Maven) or build.gradle (Gradle)
└── README.md
```

Here's what each part does:

| Directory / File           | Purpose                                                                                                                                           |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `src/main/java/`           | Contains all the Java source files of the application, organized by package (e.g., `com.example`).                                                |
| `src/main/resources/`      | Holds non-code files used at runtime: configuration files (like `application.properties`), templates, static assets, etc.                         |
| `src/test/java/`           | Mirrors the structure of `src/main/java/`, but contains test classes. Keeps tests separate from production code.                                  |
| `src/test/resources/`      | Test-specific resources (mock data, test configs).                                                                                                |
| `target/` or `build/`      | Where compiled `.class` files, packaged `.jar` files, and other build artifacts end up. This is generated automatically — never edit it manually. |
| `pom.xml` / `build.gradle` | The build configuration file. Declares dependencies, plugins, Java version, and how to compile, test, and package the project.                    |

The folder convention exists so that **any developer can open any Maven or Gradle project and immediately know where everything is**. Source code is here, tests are there, resources go in that folder. No guessing, no README required to find the entry point.

> **Note:** For beginners just starting out, you don't need Maven or Gradle yet. A single folder with a single `.java` file is a perfectly valid Java project. The structure above is what you'll adopt once your projects grow beyond simple exercises — and understanding it early means you won't be confused when you encounter it in real-world codebases or tutorials.