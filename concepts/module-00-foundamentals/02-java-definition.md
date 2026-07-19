# Java

## What's Java?
Java is a high-level, object-oriented programming language created in 1995 by James Gosling and his team at Sun Microsystems. Its original promise was radical and simple: **"Write Once, Run Anywhere" (WORA)** — write your code once, and it runs on any device that has a Java Virtual Machine (JVM), regardless of the underlying hardware or operating system.

Sun Microsystems was later acquired by Oracle Corporation in 2010, which has maintained and evolved the language ever since. In the early days, release cycles were slow — new versions took 3 to 5 years to arrive. That changed in 2017 when Oracle shifted to a **six-month release cadence** (one new version every March and September), with a **Long-Term Support (LTS)** version every two years for enterprises that need stability over novelty.

As of mid-2026, **Java 26** is the latest release (March 2026), a short-term version, while **Java 25** (September 2025) is the current LTS. The language has come a long way from its early versions: virtual threads, pattern matching, records, structured concurrency — modern Java is faster, leaner, and more expressive than the Java of ten years ago. It is not the same language people complain about from the Java 8 era. It evolved, it adapted, and it stayed.

## Where is Java Used?
Java is everywhere — not in a vague, marketing sense, but in a very concrete, infrastructure sense.

It ranks consistently among the **top 3 programming languages in the world** (TIOBE Index, 2026), and roughly **30% of professional developers** use it regularly. Over **460,000 companies** worldwide run Java in production, and around **90% of Fortune 500 companies** rely on it for their core systems. It is not trendy. It is foundational.

Here are the main areas where Java dominates:
- **Enterprise Backend Systems:** Large-scale business applications — ERPs, CRMs, internal platforms — are built on Java and frameworks like Spring Boot. Its strong typing, mature ecosystem, and backward compatibility make it a safe bet for systems that must run for years without breaking.
- **Banking and Fintech:** Java is the **#1 language in finance interviews** (HackerRank) and powers most of Wall Street's trading platforms, payment gateways, and core banking software. When a mistake means losing someone's money (not their comment or photo), reliability is not optional — it is the requirement.
- **Cloud and Microservices:** Modern Java, with virtual threads and frameworks like Quarkus, Micronaut, and Helidon, is now a strong fit for cloud-native, containerized architectures running on AWS, Azure, and GCP.
- **Android Development:** Java was the original language for Android apps. Although Kotlin (which also runs on the JVM) is now Google's preferred language for Android, Java remains widely used across legacy and enterprise mobile applications.
- **Big Data and AI:** Tools like Apache Hadoop, Apache Spark, and Apache Kafka are built in Java or run on the JVM. As enterprises integrate AI into their stacks, Java serves as the backbone — 62% of enterprises use Java to support AI functionality as of 2026.

**In Brazil specifically**, Java has a massive presence. The country has **over 759,000 software developers** (the 6th largest developer population in the world), and Java/Kotlin is among the **most in-demand skill sets**, alongside Python and React/TypeScript. Major cities like São Paulo, Belo Horizonte, and Curitiba are key talent hubs, with hundreds of open Java positions across banking, fintech, and enterprise software — from companies like Inter, PagBank, Nubank, CI&T, and many others. Brazil's growing tech sector, combined with a **530,000-person talent shortage**, means Java developers are not just employable — they are actively competed for.

## JVM, JRE and JDK

These three acronyms appear everywhere in Java, and they are often confused. They shouldn't be — each one has a clear role, and each one contains the previous:

**JVM (Java Virtual Machine)** is the engine. It takes the compiled Java code (called **bytecode**) and translates it into machine instructions that your specific operating system and hardware can understand. This is what makes Java platform-independent: your code doesn't talk to the machine directly — the JVM does. Different operating systems have different JVM implementations, but the bytecode stays the same. Write once, run anywhere.

**JRE (Java Runtime Environment)** is the JVM **plus** everything needed to *run* a Java application: core libraries, configuration files, and other resources. If you are an end user who just needs to run a Java program (not write one), the JRE is what you need. It provides the environment; the JVM provides the execution.

**JDK (Java Development Kit)** is the JRE **plus** everything needed to *develop* Java applications: the compiler (`javac`), the debugger, documentation tools, and other development utilities. If you are a developer, this is what you install. It contains the JRE, which contains the JVM.

Think of it as layers:

| Layer   | What it is                      | Who needs it                 |
| ------- | ------------------------------- | ---------------------------- |
| **JVM** | The engine that runs bytecode   | Embedded inside the JRE      |
| **JRE** | JVM + libraries to run programs | End users running Java apps  |
| **JDK** | JRE + tools to develop programs | Developers writing Java code |

In short: the **JDK** is for building, the **JRE** is for running, and the **JVM** is for executing. One contains the other — the JDK wraps the JRE, and the JRE wraps the JVM.

> **Note:** Since Java 11, Oracle no longer offers the JRE as a separate download. If you download a modern JDK, it already includes everything. The distinction is still conceptually important, but in practice, developers just install the JDK and move on.