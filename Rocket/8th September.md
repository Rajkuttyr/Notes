
# **Object-Oriented Programming (OOP)**

**Speaker:** Yogaraj

## **1. Introduction to OOP**

**OOP — Object-Oriented Programming** is a programming paradigm based on the concept of **objects**, which contain:

- **Data** → Properties / Attributes
- **Behavior** → Methods / Functions

OOP helps us design software that is:

- Modular
- Reusable
- Maintainable
- Secure
- Easier to extend

### **Important History**

- **Smalltalk** is one of the earliest languages designed around the object-oriented programming paradigm.
- Java is an object-oriented programming language that follows OOP principles.

---

# **2. Java Platform Independence**

One of the major features of Java is:

**Write Once, Run Anywhere (WORA)**

Java achieves platform independence through the **JVM (Java Virtual Machine)**.

### **How Java Works**

```text
Java Source Code
       ↓
    javac
       ↓
   Bytecode (.class)
       ↓
      JVM
       ↓
Machine Code
       ↓
Processor
```

Java source code is compiled into **bytecode**, rather than directly into processor-specific machine code.

The JVM on each operating system converts/executes the bytecode for that particular platform.

```text
             Java Bytecode
                  ↓
        ┌─────────┼─────────┐
        ↓         ↓         ↓
      JVM       JVM       JVM
     Windows    Linux     macOS
        ↓         ↓         ↓
      CPU       CPU       CPU
```

### **JDK vs JRE vs JVM**

| **Component** | **Purpose**                                       |
| ------------- | ------------------------------------------------- |
| **JVM**       | Executes Java bytecode                            |
| **JRE**       | JVM + libraries required to run Java applications |
| **JDK**       | JRE + development tools such as `javac`           |

**Key point:** Java is platform-independent because the **bytecode is platform-independent**, while the JVM is platform-dependent.

---

# **3. Four Pillars of OOP**

The four fundamental pillars of OOP are:

1. 🔒 **Encapsulation**
2. 🧬 **Inheritance**
3. 🎭 **Polymorphism**
4. 🎯 **Abstraction**

---

# **3.1 Encapsulation**

### **Definition**

**Encapsulation is the process of bundling data and the methods that operate on that data inside a class, while restricting direct access to the data.**

In simple terms:

**Encapsulation = Data hiding + Controlled access**

### **Example**

Consider a bank account.

We should not allow anyone to directly modify the account balance.

❌ Bad:

```java
account.balance = -50000;
```

Instead, we make `balance` private and provide controlled methods.

```java
class BankAccount {

    private double balance;

    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
        }
    }

    public double getBalance() {
        return balance;
    }
}
```

Usage:

```java
BankAccount account = new BankAccount();

account.deposit(5000);

System.out.println(account.getBalance());
```

The user cannot directly access:

```java
account.balance;
```

because `balance` is declared as:

```java
private double balance;
```

### **Access Modifiers**

Java provides access modifiers to control visibility.

|**Modifier**|**Same Class**|**Same Package**|**Subclass**|**Everywhere**|
|---|---|---|---|---|
|`private`|✅|❌|❌|❌|
|default|✅|✅|❌*|❌|
|`protected`|✅|✅|✅|❌|
|`public`|✅|✅|✅|✅|

### **Key Points**

- Use `private` to hide internal state.
- Provide controlled access through methods.
- Encapsulation improves security and maintainability.
- It prevents unwanted modification of object state.
- Getters and setters are commonly used for encapsulation.

---

# **3.2 Inheritance**

### **Definition**

**Inheritance allows one class to acquire the properties and behavior of another class.**

It represents an **IS-A relationship**.

For example:

```text
        Animal
          ↑
      ┌───┴───┐
      ↓       ↓
     Dog     Cat
```

A `Dog` **is an** `Animal`.

### **Java Example**

```java
class Animal {

    void eat() {
        System.out.println("Animal is eating");
    }
}

class Dog extends Animal {

    void bark() {
        System.out.println("Dog is barking");
    }
}
```

Usage:

```java
Dog dog = new Dog();

dog.eat();
dog.bark();
```

Output:

```text
Animal is eating
Dog is barking
```

The `Dog` class inherits the `eat()` method from `Animal`.

### **Important Keyword**

```java
extends
```

is used for class inheritance.

```java
class Dog extends Animal {
}
```

### **Types of Inheritance in Java**

```text
Single Inheritance

Animal
  ↓
 Dog
```

```text
Multilevel Inheritance

Animal
  ↓
Mammal
  ↓
 Dog
```

```text
Hierarchical Inheritance

       Animal
       /    \
      Dog   Cat
```

Java **does not support multiple inheritance using classes**:

```text
   A       B
    \     /
      C
```

because it can create ambiguity.

However, Java supports multiple inheritance through **interfaces**.

### **Key Points**

- Promotes code reuse.
- Creates a parent-child relationship.
- Uses `extends` for classes.
- Represents an **IS-A** relationship.
- Java doesn’t support multiple inheritance with classes.
- Interfaces can be used to achieve multiple inheritance of type.

---

# **3.3 Polymorphism**

### **Definition**

**Polymorphism means “many forms”.**

An object or method can behave differently depending on the situation.

There are two major types of polymorphism in Java:

1. **Compile-time polymorphism**
2. **Runtime polymorphism**

---

## **Compile-Time Polymorphism**

Achieved using **method overloading**.

Same method name but different parameters.

```java
class Calculator {

    int add(int a, int b) {
        return a + b;
    }

    int add(int a, int b, int c) {
        return a + b + c;
    }

    double add(double a, double b) {
        return a + b;
    }
}
```

Usage:

```java
Calculator calculator = new Calculator();

System.out.println(calculator.add(10, 20));
System.out.println(calculator.add(10, 20, 30));
System.out.println(calculator.add(10.5, 20.5));
```

The compiler determines which method should be called.

### **Method Overloading**

```text
add(int, int)
add(int, int, int)
add(double, double)
```

Same method name, different parameter lists.

---

# **Runtime Polymorphism**

Achieved using **method overriding**.

```java
class Animal {

    void sound() {
        System.out.println("Animal makes sound");
    }
}

class Dog extends Animal {

    @Override
    void sound() {
        System.out.println("Dog barks");
    }
}

class Cat extends Animal {

    @Override
    void sound() {
        System.out.println("Cat meows");
    }
}
```

Now:

```java
Animal animal;

animal = new Dog();
animal.sound();

animal = new Cat();
animal.sound();
```

Output:

```text
Dog barks
Cat meows
```

The reference is of type `Animal`, but the actual object determines which `sound()` method executes.

This is called **runtime polymorphism** or **dynamic method dispatch**.

### **Key Points**

- Polymorphism = **many forms**.
- Overloading → compile-time polymorphism.
- Overriding → runtime polymorphism.
- Runtime polymorphism is strongly associated with inheritance.
- `@Override` helps indicate that a method is being overridden.

---

# **3.4 Abstraction**

### **Definition**

**Abstraction means hiding implementation details and exposing only the essential functionality.**

A simple real-world example:

When driving a car, you use:

```text
Accelerator
Brake
Steering
```

You don’t need to know the internal implementation of the engine to drive the car.

Similarly, in programming, we expose **what an object does** while hiding **how it does it**.

---

## **Abstraction using Abstract Classes**

```java
abstract class Vehicle {

    abstract void start();

    void stop() {
        System.out.println("Vehicle stopped");
    }
}
```

Child class:

```java
class Car extends Vehicle {

    @Override
    void start() {
        System.out.println("Car starts using engine");
    }
}
```

Usage:

```java
Vehicle vehicle = new Car();

vehicle.start();
vehicle.stop();
```

Output:

```text
Car starts using engine
Vehicle stopped
```

An abstract class can contain:

- Abstract methods
- Concrete methods
- Variables
- Constructors

---

# **Abstraction using Interfaces**

Interfaces are another major mechanism for abstraction in Java.

```java
interface Payment {

    void pay(double amount);
}
```

Implementation:

```java
class CreditCardPayment implements Payment {

    @Override
    public void pay(double amount) {
        System.out.println("Paid using credit card: " + amount);
    }
}
```

Another implementation:

```java
class UPIPayment implements Payment {

    @Override
    public void pay(double amount) {
        System.out.println("Paid using UPI: " + amount);
    }
}
```

Usage:

```java
Payment payment = new UPIPayment();

payment.pay(1000);
```

The caller only needs to know:

```java
payment.pay(1000);
```

They don’t need to know the internal implementation of UPI payment.

### **Key Points**

- Abstraction hides implementation details.
- Focuses on **what** rather than **how**.
- Achieved using:
    - Abstract classes
    - Interfaces
- Helps reduce complexity.
- Makes systems easier to extend and maintain.

---

# **4. Constructor**

A **constructor** is a special member of a class used to initialize an object.

```java
class Student {

    String name;

    Student(String name) {
        this.name = name;
    }
}
```

Creating an object:

```java
Student student = new Student("Raj");
```

The constructor is called when the object is created.

### **Important Characteristics**

- Constructor name must be the same as the class name.
- It has **no return type**, not even `void`.
- It can be overloaded.
- It is automatically invoked during object creation.

### **Constructor and Memory**

When we write:

```java
Student student = new Student("Raj");
```

the `new` operator is responsible for allocating memory for the object, and the constructor initializes that object.

So, more accurately:

**`new`** **allocates memory and the constructor initializes the object.**

---

# **5. Class vs Object**

### **Class**

A class is a **blueprint/template** for creating objects.

```java
class Car {

    String color;

    void drive() {
        System.out.println("Car is driving");
    }
}
```

### **Object**

An object is an **instance of a class**.

```java
Car car = new Car();
```

Here:

```text
Car
 ↓
Class / Blueprint

car
 ↓
Object / Instance
```

Multiple objects can be created from the same class:

```java
Car car1 = new Car();
Car car2 = new Car();
Car car3 = new Car();
```

Each object can have its own state.

---

# **6. Complete Example — All Four Pillars**

Here’s a small example combining the concepts:

```java
abstract class Animal {

    // Encapsulation
    private String name;

    Animal(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

    // Abstraction
    abstract void sound();
}


// Inheritance
class Dog extends Animal {

    Dog(String name) {
        super(name);
    }

    // Polymorphism - method overriding
    @Override
    void sound() {
        System.out.println(getName() + " says Woof!");
    }
}


class Cat extends Animal {

    Cat(String name) {
        super(name);
    }

    // Polymorphism - method overriding
    @Override
    void sound() {
        System.out.println(getName() + " says Meow!");
    }
}


public class Main {

    public static void main(String[] args) {

        Animal animal1 = new Dog("Bruno");
        Animal animal2 = new Cat("Kitty");

        animal1.sound();
        animal2.sound();
    }
}
```

### **What is happening?**

|**OOP Concept**|**Example**|
|---|---|
|**Encapsulation**|`private String name`|
|**Inheritance**|`Dog extends Animal`|
|**Polymorphism**|`animal1.sound()` / `animal2.sound()`|
|**Abstraction**|`abstract class Animal` and `abstract void sound()`|
|**Constructor**|`Dog(String name)`|
|**Object creation**|`new Dog("Bruno")`|

---

# **7. Quick Revision**

```text
                 OOP
                  │
       ┌──────────┼──────────┐
       │          │          │
 Encapsulation Inheritance Polymorphism
       │          │          │
  Data hiding   Reuse      Many forms
       │          │          │
    private      extends    Overloading
                           Overriding
                  │
              Abstraction
                  │
          Hide implementation
                  │
          Interface / Abstract
               class
```

### **One-line Definitions**

🔒 **Encapsulation** → Protect and control access to data.

🧬 **Inheritance** → Reuse properties and behavior from another class.

🎭 **Polymorphism** → One interface/method can have multiple forms.

🎯 **Abstraction** → Hide implementation details and expose essential functionality.

---

## **⭐ Important Interview Points**

- **OOP has four pillars:** Encapsulation, Inheritance, Polymorphism, Abstraction.
- **Smalltalk** is an early object-oriented language.
- Java follows the **Write Once, Run Anywhere** principle through bytecode and JVMs.
- **JVM is platform-dependent; Java bytecode is platform-independent.**
- `private` is the most restrictive access modifier.
- `extends` is used for class inheritance.
- **Overloading** → compile time.
- **Overriding** → runtime.
- Java doesn’t support multiple inheritance through classes.
- Java supports multiple inheritance through interfaces.
- `new` allocates memory for an object; the constructor initializes it.
- A **class** is a blueprint; an **object** is an instance of that class.
- Encapsulation is not simply “making variables private”; it is about **bundling data with behavior and controlling access to the object’s state**.