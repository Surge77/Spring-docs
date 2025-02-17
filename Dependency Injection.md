# Dependency & Dependency Injection in Spring

#### **Step 1: What is the core problem?**

When building applications, classes and objects often depend on each other. If these dependencies are created manually inside a class, it leads to **tight coupling**, making the system hard to maintain, test, and scale.

#### **Step 2: Breaking it Down**

1. **Dependency**: Any object that another object needs to function.
   * Example: A car (class) needs an engine (dependency) to run.
2. **Traditional Approach**:
   * If the car class **creates** the engine inside itself (`new Engine()`), the car is tightly coupled to the engine.
   * Problem? If we need a **diesel engine instead of a petrol engine**, we have to modify the car class.
3. **Better Approach?** Let someone else provide the engine.

#### **Step 3: Rebuilding the Concept**

This is where **Dependency Injection (DI)** comes in. Instead of a class **creating** its dependencies, they are **injected from the outside** (like giving the car an engine instead of it building one).

### **Dependency Injection (DI) Meaning**

* **"Give me what I need instead of making me create it."**
* A class **does not create** its dependencies; they are **injected by the Spring framework**.

### **Why DI?**

✅ **Loosely Coupled Code** – Easily switch implementations (e.g., change MySQL to PostgreSQL without modifying logic).
✅ **Easier Testing** – Mocks can be injected during testing.
✅ **Better Maintainability** – Dependencies are managed separately.

### **3 Types of Dependency Injection in Spring**

* **Constructor Injection** (Best for required dependencies)
* **Setter Injection** (Best for optional dependencies)
* **Field Injection** (Direct injection but harder to test)
