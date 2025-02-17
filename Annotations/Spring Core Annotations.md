# Core Spring Annotations

### **🔹 `@Component` (Core Bean)**

* **What it does:** Marks a class as a Spring-managed **Bean** (an object that Spring creates and manages).
* **Why?** Instead of manually creating objects (`new MyClass()`), Spring handles it.

```java
@Component
public class MyService {
    public void serve() {
        System.out.println("Service running...");
    }
}

```

### **🔹 `@Autowired` (Dependency Injection)**

* **What it does:** Injects a required **Bean** automatically.
* **Why?** Instead of manually creating dependencies, Spring provides them.

```java
@Component
public class MyController {
    @Autowired  // Injects MyService Bean
    private MyService myService;
  
    public void execute() {
        myService.serve();
    }
}
```

### **🔹 `@Service` (Business Logic Bean)**

* **What it does:** Specialized version of `@Component` used for **business logic** classes.
* **Why?** Helps organize code and improve readability.

```java
@Service
public class OrderService {
    public void processOrder() {
        System.out.println("Order processed.");
    }
}
```

### **🔹 `@Repository` (Data Access Bean)**

* **What it does:** Specialized `@Component` for **data access (DAO) classes**.
* **Why?** It helps catch database-related exceptions and provides a clean separation.

```java
@Repository
public class UserRepository {
    public void saveUser() {
        System.out.println("User saved to DB.");
    }
}
```

### **🔹 `@Controller` (Handles Web Requests)**

* **What it does:** Specialized `@Component` for **handling HTTP requests** in MVC.
* **Why?** Tells Spring that this class contains **web endpoints**.

```java
@Controller
public class HomeController {
    @GetMapping("/")
    public String home() {
        return "home";
    }
}
```
