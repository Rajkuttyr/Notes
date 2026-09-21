
# **Design Principles & Design Patterns**

**Speaker:** Bharath Kumar  
**Topic:** Design Principles & Five Design Patterns

## **Abstract**

Design patterns are **reusable solutions to common software design problems**. They help us structure an application so that the code is easier to **maintain, extend, test, and understand**.

In an e-commerce application, different patterns can solve different responsibilities:

|**Pattern**|**Main Idea**|**E-commerce Example**|
|---|---|---|
|**Singleton**|One shared instance|Application configuration / shared service|
|**Factory**|Decides **what** object to create|Payment method|
|**Strategy**|Decides **how** an operation works|Payment algorithm / discount calculation|
|**Observer**|Event-driven notification|Order placed → notify services|
|**Repository**|Separates data access from business logic|Product/Order database access|

---

# **1. Singleton Pattern**

### **Core Idea**

**Singleton = Only one instance of a class is created and shared throughout the application.**

Instead of creating multiple objects of the same class, the application maintains **one shared object**.

### **E-commerce Example**

Suppose we have an application configuration or a service that should have a single shared instance.

```text
E-Commerce Application
        │
        ▼
   Singleton Object
        │
   ┌────┼────┐
   ▼    ▼    ▼
Service A  Service B  Service C
```

### **Important Correction**

Singleton does **not** mean:

“Put all application services in a single file.”

Instead, it means:

**A particular class has only one instance, and that instance is shared where required.**

### **Example**

```java
public class AppConfig {

    private static AppConfig instance;

    private AppConfig() {}

    public static AppConfig getInstance() {
        if (instance == null) {
            instance = new AppConfig();
        }
        return instance;
    }
}
```

### **When to use**

- Shared configuration
- Certain resource managers
- Application-wide components

⚠️ **Note:** Singleton can introduce global state and make testing harder, so it shouldn’t be used everywhere.

---

# **2. Factory Pattern**

### **Core Idea**

**Factory = Decides WHAT object should be created.**

The client doesn’t need to know the exact class that needs to be instantiated.

### **E-commerce Example — Payment**

Suppose an e-commerce application supports:

```text
Payment
 ├── CreditCard
 ├── UPI
 ├── PayPal
 └── NetBanking
```

Instead of writing:

```java
if (paymentType.equals("UPI")) {
    new UPI();
}
else if (paymentType.equals("CARD")) {
    new CreditCard();
}
```

we can use a factory.

```java
Payment payment = PaymentFactory.create("UPI");
```

The factory decides:

```text
"UPI"
   │
   ▼
PaymentFactory
   │
   ▼
UPIPayment object
```

### **Key Question**

**Factory answers:**

“What object should I create?”

---

# **3. Strategy Pattern**

### **Core Idea**

**Strategy = Decides HOW a particular operation should be performed.**

It allows us to define multiple algorithms and select one at runtime.

### **E-commerce Example — Payment Processing**

Different payment methods can have different payment-processing strategies.

```text
Payment Processing
       │
 ┌─────┼──────┐
 ▼     ▼      ▼
UPI   Card   PayPal
 │      │      │
 ▼      ▼      ▼
UPI    Card   PayPal
Logic  Logic  Logic
```

For example:

```java
interface PaymentStrategy {
    void pay(double amount);
}
```

Implementations:

```java
class UPIPayment implements PaymentStrategy {
    public void pay(double amount) {
        // UPI payment logic
    }
}

class CardPayment implements PaymentStrategy {
    public void pay(double amount) {
        // Card payment logic
    }
}
```

### **Key Question**

**Strategy answers:**

“How should this operation work?”

---

# **Factory + Strategy**

This is an important combination.

**Factory and Strategy can work together.**

They solve **different problems**:

```text
Factory
   │
   │ What?
   ▼
Select Strategy
   │
   ▼
Strategy
   │
   │ How?
   ▼
Execute Algorithm
```

### **Example**

Customer selects:

```text
Payment = UPI
```

The **Factory** decides:

```text
"UPI" → UPIPaymentStrategy
```

Then the **Strategy** performs:

```text
UPIPaymentStrategy
        │
        ▼
Execute UPI payment logic
```

So remember:

🏭 **Factory → WHAT to create**🧠 **Strategy → HOW to perform the operation**

---

# **4. Observer Pattern**

### **Core Idea**

**Observer = Event-driven communication between objects.**

When something happens, interested components are automatically notified.

### **E-commerce Example**

Imagine a customer places an order.

```text
Customer
   │
   ▼
Place Order
   │
   ▼
Order Created Event
   │
   ├───────────────┐
   ▼               ▼
Email Service   Notification Service
   │               │
   ▼               ▼
Send Email      Send Notification
```

The order service doesn’t need to directly control every notification system.

Instead:

```text
Order Service
      │
      ▼
 Order Event
      │
 ┌────┼──────────┐
 ▼    ▼          ▼
Email SMS    Inventory
```

Each observer reacts to the event.

### **Example**

```java
interface Observer {
    void update(Order order);
}
```

Observers could be:

```text
EmailObserver
SMSObserver
InventoryObserver
AnalyticsObserver
```

### **Key Question**

**Observer answers:**

“Who needs to know that something happened?”

---

# **5. Repository Pattern**

### **Core Idea**

**Repository = Separates data access logic from business logic.**

Instead of putting SQL/database operations directly inside business services, we create a repository layer.

### **E-commerce Example**

```text
Controller
    │
    ▼
Service
    │
    ▼
Repository
    │
    ▼
Database
```

For example:

```java
interface ProductRepository {
    Product findById(Long id);
    List<Product> findAll();
    void save(Product product);
}
```

The service doesn’t need to know exactly how the data is stored.

```java
productRepository.findById(id);
```

The repository handles the database interaction.

### **Key Question**

**Repository answers:**

“How do I access my data?”

---

# **Putting Everything Together**

A simple e-commerce architecture can use all five patterns:

```text
                    E-Commerce Application
                             │
                     ┌───────▼────────┐
                     │   Controller   │
                     └───────┬────────┘
                             │
                     ┌───────▼────────┐
                     │    Service     │
                     └───┬────────┬───┘
                         │        │
                ┌────────▼─┐   ┌──▼──────────┐
                │ Factory  │   │ Repository  │
                └────┬─────┘   └─────┬───────┘
                     │               │
                 What?              Data
                     │               │
                     ▼               ▼
                ┌─────────┐      Database
                │Strategy │
                └────┬────┘
                     │
                   How?
                     │
                     ▼
              Payment / Discount
                     │
                     ▼
                  Order Event
                     │
              ┌──────┼──────┐
              ▼      ▼      ▼
            Email   SMS   Inventory
              ▲      ▲      ▲
              └──── Observer ────┘
```

---

# **🧠 Easy Way to Remember**

Think about building an e-commerce application:

### **Singleton**

**“How many?”**

One shared instance.

### **Factory**

**“What?”**

What object should I create?

### **Strategy**

**“How?”**

How should this operation be performed?

### **Observer**

**“Who should know?”**

Who needs to be notified when something happens?

### **Repository**

**“Where is the data?”**

How do I access and manage the data?

---

## **One-Line Summary**

**Singleton manages one shared instance, Factory creates the appropriate object, Strategy selects how an operation is performed, Observer enables event-driven notifications, and Repository separates data access from business logic.**

### **E-commerce mental model**

```text
Singleton  → One
Factory    → What?
Strategy   → How?
Observer   → Who needs to know?
Repository → Where is the data?
```

This is a nice set of notes to keep because these five patterns cover **object creation, behavior, communication, and data access**—four big areas you’ll repeatedly encounter when designing Spring Boot applications.