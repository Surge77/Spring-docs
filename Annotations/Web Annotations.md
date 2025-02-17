# Web Annotations (For REST APIs)

These annotations are used **when building REST APIs** in Spring Boot.

### **🔹 `@RestController` (API Controller)**

* **What it does:** Combines `@Controller` + `@ResponseBody` to return JSON responses.
* **Why?** Used for building REST APIs instead of HTML pages.

```java
@RestController
public class UserController {
    @GetMapping("/user")
    public String getUser() {
        return "John Doe";
    }
}
```

### **🔹 `@RequestMapping` (Define URL Paths)**

* **What it does:** Maps **HTTP requests to methods**.
* **Why?** Controls how URLs are handled.

```java
@RequestMapping("/api")
public class ApiController {
    @GetMapping("/hello")
    public String sayHello() {
        return "Hello, World!";
    }
}
```

### **🔹 `@GetMapping`, `@PostMapping`, `@PutMapping`, `@DeleteMapping`**

* **What they do:** Shortcuts for `@RequestMapping` for specific HTTP methods.
* **Why?** Makes API code cleaner.

```java
@RestController
@RequestMapping("/users")
public class UserController {
  
    @GetMapping("/{id}")
    public String getUser(@PathVariable int id) {
        return "User " + id;
    }

    @PostMapping("/")
    public String createUser(@RequestBody String user) {
        return "User created: " + user;
    }
}
```
