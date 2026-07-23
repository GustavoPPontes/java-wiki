# Why does programming logic exist?

## What is an algorithm?

An algorithm is a finite, ordered and unambiguous sequence of well-defined instructions that, starting from an initial state, is designed to solve a specific problem or reaches a defined result. But what does that mean?

| Property                     | Meaning                                                       | What happens if violated                                                             |
| ---------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| Finite                       | Has a beginning and an end                                    | Infinite loop: the program crashes or consumes resources indefinitely                |
| Ordered                      | Each step depends on the previous one in the correct sequence | Logic errors: wrong results or inconsistent system                                   |
| Unambiguous                  | Each instruction has exactly one interpretation               | Unpredictable behavior — the machine chooses an interpretation that may not be yours |
| Starts from an initial state | Defines the input conditions                                  | The algorithm may work for some inputs and fail for others                           |
| Reaches a defined result     | Has a completion criterion                                    | You don't know when the execution has finished                                       |

For example, when we want to make a cup of coffee, we follow a series of steps: we get the coffee maker, fill it with a certain amount of water, put the coffee grounds in the filter, grab a mug, turn on the machine, and wait for it to finish. When we do this, we are following a sequence of instructions to achieve a desired result (in this case, the coffee).

And this is exactly what an algorithm is. Everything we see on a computer is driven by vast sequences of instructions that work together to perform the tasks we use every day, like creating a folder, opening Google Chrome, and even running Java code. Complex software systems rely on multiple algorithms working together to function.

### What is NOT an algorithm — a common beginner mistake

Many people confuse algorithms with code. They are distinct things:
 - Algorithm: The logic behind the solution, regardless of the programming language or machine. It can be written in English, pseudocode, or drawn as a flowchart.
 - Code: The implementation of the algorithm in a specific programming language (Java, Python, C, etc.).

So, an algorithm is the step-by-step process we design to achieve a specific result, while code is the "translation" of that algorithm using a programming language's syntax.

## Programming logic: Why it's a must have?

If an algorithm is the "logic path" you want the computer to follow, and coding is the implementation of that algorithm, then `programming logic` is the ability to structure reasoning (through algorithms) to solve problems in a way that a machine can follow and execute it efficiently/correctly.

It encompasses:
 - Sequencing: How to order instructions correctly.
 - Selection (Decision-making): How to make decisions (if X, do Y; else, do Z).
 - Iteration (Repetition): How to repeat actions (do this while a condition is true).
 - Data organization: How to organize data and perform operations on it.

### Why is it independent of the programming language?

Here lies one of the biggest misconceptions in programming education: people learn Java, Python, or JavaScript **without** ever developing programming logic. The result: they know the syntax, but freeze when faced with even a slightly new problem.

Knowing the `language syntax` is like knowing how to use a hammer; **understanding** `programming logic` is knowing what to build with it.

When you master programming logic:
- Learning a new language takes weeks, not months/years (you only learn the new syntax, not the reasoning)
- You solve problems you’ve never seen before because you know how to decompose and structure any challenge
- You read other people's code and understand the intent, even if it's in a different language

**Why beginners confuse logic with syntax? And how to avoid it**

Syntax is the set of grammatical rules of a programming language. In Java, you write `System.out.println("text")`. In Python, you write `print("text")`. In both, the logic is identical: to display text on the screen.

The classic mistake: studying `for`, `while`, and `if/else` in Java and thinking you are learning logic. You are are just learning **how** Java expresses logic. Logic itself (the reasoning about iteration, decision, and sequence) predates the language.

## Computational Thinking: the 4-pillar framework

The term Computational Thinking was popularized by the computer scientist Jeannette Wing in 2006. It describes how programmers (and those who solve complex problems in general) structure their reasoning.

It's not thinking *like* a computer. It's thinking *for* a computer — in a precise, structured, and scalable way.

| Pillar                  | What it is                                                                | Concrete Example                                                                                               |
| ----------------------- | ------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| **Decomposition**       | Breaking a large problem into smaller, manageable sub-problems            | "Creating a login system" → "validate email format" + "verify password in database" + "generate session token" |
| **Pattern Recognition** | Identifying similarities between problems to reuse solutions              | "Sorting a list of names" uses the same pattern as "sorting a list of prices"                                  |
| **Abstraction**         | Ignoring irrelevant details and focusing on what matters for the solution | To calculate a grade average, you don't need to know the student's name, only the numbers                      |
| **Algorithms**          | Creating the sequence of steps that solves the decomposed problem         | The concrete steps, in the correct order, to execute the solution                                              |

You can note that these 4 pillars operate in a natural sequence: you **decompose** the problem → **recognize** patterns among the parts → **abstract** the essential → **define the algorithm**. In practice, this cycle repeats iteratively.

## Problem Decomposition: the most underrated skill in programming

As noted before, the first pillar of *Computational Thinking* is **Decomposition**. It is safe to say that it is one of, if not the most important pillar, because it is what truly defines a great programmer.

### What decomposition really is

Decomposition is the ability to take a problem that seems large and intimidating and **break it down into smaller parts, each solvable independently or sequentially**.

The stopping criterion for decomposition is: *each resulting part must be simple enough to be solved directly or decomposed again*. You keep breaking it down until you reach atomic steps—units so small that they cannot be further subdivided usefully.

**Why it's the most important skill and why it's underrated**

Most bugs (code errors) aren't syntax errors. They're logic errors: the programmer didn't fully understand the problem before starting. And most logic errors come from trying to solve the whole problem at once, without decomposing it.

When faced with a complex problem, senior developers (the really good ones) resist the urge to open their editor immediately. They map out the problem first. This may sound counterintuitive to beginners, who feel that 'thinking' isn't progress. It is exactly the opposite: thinking things through saves hours of rework later.

Here is an example problem: Push code to GitHub
1. Have an existing local repository (or create one with git init)
2. Have a remote repository on GitHub (create via the website)
3. Connect the two (git remote add origin )
4. Add files to the stage (git add .)
5. Create the commit (git commit -m "message")
6. Push to the remote (git push -u origin main)

Each item on this list is solvable independently. If step 2 fails, you don't need to redo step 1. If step 3 has an authentication issue, steps 1 and 2 are still correct. Decomposition allows you to **locate and fix faults without starting from scratch**.

This is the same as what a programmer does when solving a coding problem: break it down into parts, solve each part, and integrate.

### How to decompose well — practical criteria
1. **Ask:** "What needs to happen before this?" → This reveals dependencies and a natural order.
2. **Ask:** "Can this be broken down into independent parts?" → If yes, break it down.
3. **Ask:** "Can I solve this subproblem without having to solve another one first?" → If yes, it's atomic enough
4. **Don't try to get it perfectly decomposed on the first try** → Decomposition is iterative. You decompose, try, realize that one part is still too big, and decompose again.

In real-world systems, decomposition is the foundation of all software architecture. When a system is poorly decomposed, problems manifest as excessive coupling: changing one thing breaks ten others. When it is well decomposed, each part can evolve independently.

### How to Interpret and Solve Coding Challenges

Problem decomposition is the **key** to solving coding challenges. Not only the ones we see on [LeetCode](https://leetcode.com/) or [CodeWars](https://www.codewars.com/), but also in a programmer's everyday life.

That's why it has a great step-by-step guide we should follow to help build this decomposition skill:

**Problem-solving framework for any challenge (a sequence that works):**

**Step 1 — Read the entire problem before doing anything.**
It sounds obvious. Almost no one does it. Most start writing code on the second line of the prompt. Result: you solve the wrong problem.

**Step 2 — Identify: Inputs, Processing, Outputs (IPO)**
Every computational problem has this structure:
- Input: What does the problem provide? What data comes in?
- Processing: What needs to be done with this data?
- Output: What is the expected result?

Example: "Given a student's name and grade, display whether they passed (grade >= 7) or failed."

- Input: name (text), grade (number)
- Processing: compare grade with 7
- Output: text 'passed' or 'failed'

**Step 3 — Solve it in English first.**
Write the algorithm in plain language, without thinking about code. This eliminates the cognitive load of syntax while you are still building the logic.

**Step 4 — Test the algorithm with examples**
Take concrete cases and "run" your algorithm manually. Verify if the result makes sense.
- Common case: grade = 8 → pass ✓
- Boundary case: grade = 7 → pass ✓ (because it is >= 7)
- Failure case: grade = 6.9 → fail ✓

Boundary cases (values at the limits of conditions) are where most bugs live. Testing them manually before coding saves hours.

**Step 5 — Convert to code**
Only now do you open the editor! The code is the translation of the algorithm you have already validated.

---

You can see that this framework (especially in step 2) connects with what we already covered in '*How to decompose well — practical criteria*'. With this, you can continuously decompose and evolve the algorithm with a clear structure, ready to be translated into code!