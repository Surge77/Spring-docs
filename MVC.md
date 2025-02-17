# Spring MVC Framework

🚀 **Think of it like a restaurant:**

* **Model (M)** → The ingredients (data) you use to make a dish.
* **Controller (C)** → The chef who takes an order, prepares the dish, and serves it.
* **View (V)** → The presentation of the dish on the table (HTML, JSON, etc.).

When a customer (user) places an order (HTTP request), the **chef (Controller) prepares it using ingredients (Model) and serves it (View).**

---

### **⚡ 20% of the Details (How It Works & Why It Matters)**

1️⃣ **Spring MVC Uses Annotations to Define Controllers**

* `@Controller`: Marks a class as a controller.
* `@GetMapping("/url")`: Handles GET requests for a specific URL.
* `@PostMapping("/url")`: Handles POST requests.

2️⃣ **Spring MVC Automatically Maps Data to Views**

* Instead of writing response-handling logic manually, use **Thymeleaf, JSP, or JSON**.
* Example:

  ```html
  <h1 th:text="${message}"></h1>

  ```

  🔥 Spring **automatically replaces `${message}`** with the value from the controller!

3️⃣ **Spring MVC Supports REST APIs**

* If you don’t need HTML views, Spring can return **JSON responses**:

```java
@RestController
public class APIController {
    @GetMapping("/user")
    public User getUser() {
        return new User("John", "Doe");
    }
}

```

No need for manual JSON conversion!
