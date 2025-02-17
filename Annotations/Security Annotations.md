# Security & Validation Annotations

Used for **authentication, validation, and security** in Spring Boot.

### **🔹 `@Secured` & `@PreAuthorize` (Security)**

* **What they do:** Restrict access based on roles.

```java
@Secured("ROLE_ADMIN")
public void adminOnly() {
    System.out.println("Admin access granted!");
}
```

### **🔹 `@Valid` (Validates Input)**

* **What it does:** Validates request body data.

```java
public ResponseEntity<String> createUser(@Valid @RequestBody User user) {
    return ResponseEntity.ok("User is valid!");
}
```
