# Encapsulation

## The Problem: Why Encapsulation Exists

Consider a Java class that represents a bank account.

```java
public class BankAccount {
    public String owner;
    public double balance;
}
```

Both fields are `public`. That means any code in your entire project can read them or overwrite them at any time. Somewhere else in the codebase, another class can do this:

```java
BankAccount account = new BankAccount();
account.owner = "Alice";
account.balance = -9000.00;
```

That code compiles. It runs without an error. The JVM accepts it because `balance` is declared as `double`, and `-9000.00` is a valid `double`. The JVM does not know that a negative bank balance violates every rule your business has. It only checks the type. Domain rules (a balance cannot be negative, a withdrawal cannot exceed the available funds) are entirely invisible to it.

Now imagine your application has forty classes. Any one of them can write any value into `balance`. To prevent corrupt data, you would need to add a validation check in every single place that touches the field. If you miss one, or if a new developer on the team does not know the rule, the account can end up in an invalid state with no warning.

This is the real problem. Not bad programmers. Not careless code reviews. The design itself has no enforcement mechanism. The class holds data but has no control over what gets written into it.

## What Encapsulation Is

Encapsulation is the practice of keeping a class's fields private and exposing all reads and writes through methods that the class itself defines and controls.

The word "private" here is a formal Java keyword, not a metaphor. A `private` field can only be accessed by code written inside the same class. No other class, regardless of which package it lives in or who wrote it, can read or write that field directly. The moment you declare a field `private`, the compiler enforces this rule at build time, before the program ever runs.

The methods that provide controlled access are called **getters** and **setters** (covered in detail in the next section). The key insight is that a method can contain logic. A raw field cannot. When you route all access through methods, you place your domain rules inside those methods, and the class enforces them automatically, every time.

To fix the `BankAccount` example, the field becomes private:

```java
public class BankAccount {
    private String owner;
    private double balance;
}
```

Now try the same assignment from the other class:

```java
BankAccount account = new BankAccount();
account.balance = -9000.00; // Compile error: balance has private access in BankAccount
```

The compiler rejects this. The program cannot even be built. The invalid assignment is stopped before execution, not after.

The field still exists in memory. It still holds a `double`. Nothing about the internal structure changed. What changed is who is allowed to touch it.

## Access Modifiers: The Four Levels

Before the getter/setter pattern makes full sense, you need to understand the mechanism that makes it work. Every field, method, and class in Java has an **access modifier**: a keyword that tells the compiler which parts of the program are allowed to see and use that element.

There are four levels.

| Modifier | Visible to... | Typical use |
| --- | --- | --- |
| `public` | Every class in the entire project | Methods and constructors you intentionally expose as an API |
| `private` | Only code inside the same class | Fields that must be protected from external modification |
| `protected` | The same class, the same package, AND any subclass in any package | Fields or methods intended for inheritance hierarchies |
| (none) / package-private | Only code inside the same package | Internal utilities shared within a module, not intended for outside use |

**What "package" means here:** A package is a folder structure in Java (`com.myapp.accounts`, for example). The compiler uses the package declaration at the top of each file to determine which classes are "neighbors." Two classes in the same package are neighbors. Two classes in different packages are not.

A common mistake is assuming that `protected` is more restrictive than package-private, because the word "protected" sounds stricter. It is the opposite. Package-private limits access to the same package only. `Protected` extends access to all subclasses, even those in completely different packages. `Protected` is broader.

To make this concrete, consider two classes in different packages:

```java
// File: com/myapp/accounts/BankAccount.java
package com.myapp.accounts;

public class BankAccount {
    private double balance;      // accessible only inside BankAccount
    double interestRate;         // package-private: accessible to any class in com.myapp.accounts
    protected String branch;     // accessible to BankAccount, its package, and all subclasses
    public String owner;         // accessible everywhere
}
```

```java
// File: com/myapp/reports/ReportGenerator.java
package com.myapp.reports;

import com.myapp.accounts.BankAccount;

public class ReportGenerator {
    public void generate(BankAccount account) {
        System.out.println(account.owner);       // OK: public
        System.out.println(account.branch);      // Compile error: protected, and ReportGenerator is not a subclass
        System.out.println(account.interestRate);// Compile error: package-private, wrong package
        System.out.println(account.balance);     // Compile error: private
    }
}
```

The compiler blocks every access that the modifier does not permit, at build time. This means the enforcement cost is zero at runtime. The rule is checked once, before the program runs, and never again.

For the rest of this text, the focus is on `private` fields and `public` methods, because that combination is the foundation of encapsulation.

## Getters and Setters: The JavaBean Pattern

A **getter** is a public method that reads and returns the value of a private field. A **setter** is a public method that receives a new value as a parameter and writes it into a private field. There is no language-level magic. They are ordinary methods that follow a naming convention.

That naming convention is called the **JavaBean specification**, and the rules are straightforward:

- A getter for a field named `balance` is called `getBalance()`. It takes no parameters and returns the field's type.
- A getter for a `boolean` field named `active` is called `isActive()`, not `getActive()`.
- A setter for a field named `balance` is called `setBalance()`. It takes one parameter of the field's type and returns `void`.

```java
public class BankAccount {
    private String owner;
    private double balance;

    // Getter: returns the current value of the private field
    public double getBalance() {
        return balance;
    }

    // Setter: receives a new value and assigns it to the private field
    public void setBalance(double amount) {
        balance = amount;
    }

    public String getOwner() {
        return owner;
    }

    public void setOwner(String name) {
        owner = name;
    }
}
```

### How a Getter and Setter Work Under the Hood

When external code calls `account.getBalance()`, the JVM executes the method body of `getBalance()`. The method reads the value currently stored in the `balance` field of that specific object and returns it to the caller. The caller gets the value. It never touches the field directly.

When external code calls `account.setBalance(500.00)`, the JVM executes the method body of `setBalance()`. The parameter `amount` receives the value `500.00`. The method then assigns `500.00` to the `balance` field. Again, the caller never touches the field. The method is the only path in.

This indirection is the entire point. The method is a door with a lock. You can decide what the lock checks before it opens.

### When NOT to Create a Getter or Setter

Many IDEs offer a command like "Generate Getters and Setters" that creates both methods for every field in a class. This is one of the most common practices that quietly breaks encapsulation.

If a field should never change after the object is created, do not write a setter for it. A bank account's unique ID is a clear example. It is assigned once at creation and must never change. Adding a `setId()` method means any code anywhere can change it, which defeats the purpose of having an ID.

If a field is always computed from other fields, do not expose it as a separate gettable field at all. Consider a `User` class with `firstName` and `lastName` fields. A method `getFullName()` that returns `firstName + " " + lastName` is correct. Adding a separate `fullName` field and a `getFullName()` that returns it introduces a field that can fall out of sync with the other two.

The rule: every getter and setter you create is a deliberate decision to expose a specific operation. It is not a default that you fill in automatically.

## Protecting Business Rules: Validation in Setters and Constructors

Because a setter is a method, it can contain any Java logic before it assigns a value. This is where you place your business rules.

Returning to the `BankAccount` example, the rule is: a balance cannot be negative. The setter enforces it:

```java
public void setBalance(double amount) {
    if (amount < 0) {
        throw new IllegalArgumentException(
            "Balance cannot be negative. Received: " + amount
        );
    }
    balance = amount;
}
```

Now try the invalid assignment:

```java
BankAccount account = new BankAccount();
account.setBalance(-9000.00); // Throws IllegalArgumentException at runtime
```

The program throws an exception immediately, with a clear message that names the invalid value. The field `balance` is never modified. The account's state stays valid.

This is the difference between the public-field design and the encapsulated design. With a public field, the invalid value enters the object silently and causes a bug somewhere else, much later, and much harder to trace. With an encapsulated setter, the violation is caught at the point of the bad write, with the actual bad value visible in the error message.

### Validation in the Constructor

A setter protects every write that happens after the object exists. But the object also needs to be born in a valid state.

Consider this constructor:

```java
public class BankAccount {
    private String owner;
    private double balance;

    public BankAccount(String owner, double initialBalance) {
        this.owner = owner;
        this.balance = initialBalance; // No validation here
    }

    public void setBalance(double amount) {
        if (amount < 0) {
            throw new IllegalArgumentException(
                "Balance cannot be negative. Received: " + amount
            );
        }
        balance = amount;
    }
}
```

The setter validates. The constructor does not. So this is possible:

```java
BankAccount account = new BankAccount("Alice", -9000.00);
// The object is created. balance is -9000.00. No exception.
```

The object exists in an invalid state from birth. You validated the setter and forgot the constructor. This is the most common encapsulation mistake.

The fix: apply the same rule in both places.

```java
public BankAccount(String owner, double initialBalance) {
    if (initialBalance < 0) {
        throw new IllegalArgumentException(
            "Initial balance cannot be negative. Received: " + initialBalance
        );
    }
    this.owner = owner;
    this.balance = initialBalance;
}
```

A better approach in larger classes is to call the setter from the constructor, so the validation logic lives in exactly one place:

```java
public BankAccount(String owner, double initialBalance) {
    this.owner = owner;
    setBalance(initialBalance); // Reuses the setter's validation
}
```

Now the rule is written once. The constructor and every subsequent write go through the same check. If the rule changes (say, the minimum balance becomes 10.00 instead of 0), you update one method, not two.

## Records (Java 16+): Immutable Data Classes with Less Code

The pattern of private fields plus a constructor plus getters is entirely valid. It is also verbose. For a class that simply carries a fixed set of values from one place to another, and where those values never need to change after the object is created, the boilerplate can dwarf the actual content.

### The Problem That Records Solve

Look at what a proper immutable data class requires (a slightly more complex example to help us for a while):

```java
public final class InvoiceItem {
    private final String productName;
    private final int quantity;
    private final double unitPrice;

    public InvoiceItem(String productName, int quantity, double unitPrice) {
        this.productName = productName;
        this.quantity = quantity;
        this.unitPrice = unitPrice;
    }

    public String getProductName() { return productName; }
    public int getQuantity()       { return quantity; }
    public double getUnitPrice()   { return unitPrice; }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (!(o instanceof InvoiceItem)) return false;
        InvoiceItem other = (InvoiceItem) o;
        return quantity == other.quantity
            && Double.compare(unitPrice, other.unitPrice) == 0
            && productName.equals(other.productName);
    }

    @Override
    public int hashCode() {
        return Objects.hash(productName, quantity, unitPrice);
    }

    @Override
    public String toString() {
        return "InvoiceItem[productName=" + productName
            + ", quantity=" + quantity
            + ", unitPrice=" + unitPrice + "]";
    }
}
```

That is roughly 35 lines. The actual information content is three fields and their types. Everything else is structural ceremony that Java requires but that adds nothing to your understanding of what an `InvoiceItem` is.

### The Syntax of a Record

A `record` is a special class form that the Java compiler expands automatically. You write the structure. The compiler generates the constructor, the accessors, `equals()`, `hashCode()`, and `toString()`.

```java
public record InvoiceItem(String productName, int quantity, double unitPrice) { }
```

One line. The parenthesized list is called the **record header**. Each element in the header is a **record component**: a name and a type. The compiler reads the header and generates the full class for you at build time.

You use it exactly like the 35-line version:

```java
InvoiceItem item = new InvoiceItem("Wireless Keyboard", 3, 79.99);

System.out.println(item.productName()); // Wireless Keyboard
System.out.println(item.quantity());    // 3
System.out.println(item.unitPrice());   // 79.99
System.out.println(item);
// Output: InvoiceItem[productName=Wireless Keyboard, quantity=3, unitPrice=79.99]

InvoiceItem sameItem = new InvoiceItem("Wireless Keyboard", 3, 79.99);
System.out.println(item.equals(sameItem)); // true
```

### Guaranteed Immutability

Every record component is implicitly `private` and `final`. "Final" means the field can be assigned exactly once, in the constructor, and never changed afterwards. There is no way to add a setter to a record component. The compiler does not allow it. Once an `InvoiceItem` exists, its `productName`, `quantity`, and `unitPrice` are fixed for the life of that object.

This is a stronger guarantee than encapsulating a field in a traditional class with no setter. In a traditional class, you can always add a setter later, or accidentally expose the field. In a record, the immutability is structural. The language prevents mutation by design, not by convention.

### Getters Without the `get` Prefix

Notice that the accessors in the record example are `item.productName()`, `item.quantity()`, and `item.unitPrice()`. Not `item.getProductName()`. Not `item.getQuantity()`.

Records use **accessor methods** instead of JavaBean getters. The accessor for a component named `productName` is simply `productName()`. This is a deliberate departure from the JavaBean naming convention.

The reason: records are data types, not beans. The JavaBean convention (with `get` and `set`) was designed for mutable objects in frameworks that use reflection to discover and call those methods. Records are immutable. The `get` prefix signals a mutable object where a corresponding `set` might exist. On a record, that signal is misleading.

If you need to use a record in a framework that specifically requires JavaBean-style getters, you can add them manually as regular methods in the record body. But this is a framework-compatibility workaround, not a normal pattern.

### The Compact Constructor: Validation in Records

The compiler-generated constructor for a record assigns each parameter to the corresponding field. If you need to validate the data (as you saw with the setter and constructor sections above), you can intercept this process using a **compact constructor**.

A compact constructor has no parameter list in parentheses. The parameters from the record header are available implicitly. Critically, you do not write the field assignments. The compiler adds them automatically after your validation code runs.

```java
public record InvoiceItem(String productName, int quantity, double unitPrice) {

    // Compact constructor: no parameter list, no field assignments
    public InvoiceItem {
        if (productName == null || productName.isBlank()) {
            throw new IllegalArgumentException("Product name cannot be blank.");
        }
        if (quantity <= 0) {
            throw new IllegalArgumentException(
                "Quantity must be greater than zero. Received: " + quantity
            );
        }
        if (unitPrice < 0) {
            throw new IllegalArgumentException(
                "Unit price cannot be negative. Received: " + unitPrice
            );
        }
        // The compiler inserts: this.productName = productName;
        //                        this.quantity = quantity;
        //                        this.unitPrice = unitPrice;
        // You do not write these lines. They are generated automatically.
    }
}
```

Now this is rejected at object creation:

```java
InvoiceItem badItem = new InvoiceItem("", 3, 79.99);
// Throws IllegalArgumentException: Product name cannot be blank.
```

And this is also rejected:

```java
InvoiceItem badItem = new InvoiceItem("Wireless Keyboard", -1, 79.99);
// Throws IllegalArgumentException: Quantity must be greater than zero. Received: -1
```

The compact constructor gives you the same protection you built manually in the traditional class, without writing the field assignments yourself.

### Records vs. Traditional Classes: When to Use Each

The decision comes down to one question: does the object's state need to change after it is created?

| Scenario | Use |
| --- | --- |
| The object carries a fixed set of data and never changes (a coordinate, an API response payload, an event logged in a system, an invoice line item) | Record |
| The object has mutable state (a shopping cart where items are added and removed, a user profile that the account holder can update) | Traditional class with private fields and controlled setters |
| The object extends another class (records cannot extend classes other than `java.lang.Record`) | Traditional class |
| The object needs complex behavior in addition to holding data (methods that modify internal state, lazy initialization, different internal representations) | Traditional class |
| The object is used as a data transfer object (DTO) between layers of an application, and you want to guarantee no layer can mutate it unexpectedly | Record |

To make this concrete: imagine an order-processing system. An `Order` that a customer builds over time, adding products and applying discount codes, is a traditional class. Its state changes many times before the order is placed. An `OrderSummary` that the system creates once an order is confirmed, containing the final totals, the items, and the timestamp, never changes. It travels from the service layer to the controller to the response JSON. Nothing should mutate it in transit. That is a record.

```java
// Mutable: traditional class
public class Order {
    private final String orderId;
    private final List<InvoiceItem> items = new ArrayList<>();
    private double discountRate = 0.0;

    public Order(String orderId) {
        this.orderId = orderId;
    }

    public void addItem(InvoiceItem item) {
        items.add(item);
    }

    public void applyDiscount(double rate) {
        if (rate < 0 || rate > 1) {
            throw new IllegalArgumentException(
                "Discount rate must be between 0.0 and 1.0. Received: " + rate
            );
        }
        discountRate = rate;
    }

    public double getTotal() {
        double subtotal = items.stream()
            .mapToDouble(i -> i.quantity() * i.unitPrice())
            .sum();
        return subtotal * (1 - discountRate);
    }
}

// Immutable: record
public record OrderSummary(
    String orderId,
    List<InvoiceItem> confirmedItems,
    double finalTotal,
    String confirmedAt
) { }
```

The `Order` accumulates state. It needs setters and validation on every mutation. The `OrderSummary` is a snapshot. It is created once, in a valid state, and never touched again. The record enforces that guarantee structurally, so no developer on the team can accidentally add a setter to it.

This is the encapsulation principle in its two forms: a traditional class that guards mutable state through private fields and validated methods, and a record that eliminates mutation entirely by making state permanent from birth.