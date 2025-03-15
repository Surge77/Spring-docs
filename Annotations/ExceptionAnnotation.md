# Exception Annotations

In any application, **exceptions** are inevitable. In Spring Boot, handling exceptions effectively is crucial to avoid crashes, provide meaningful error responses, and enhance user experience.

### ✅ **1. `@ExceptionHandler`**

> 📖 Purpose: Handles specific exceptions in a controller or globally.

---

### 🔥 **Example Usage**

```java

@RestController
@RequestMapping("/users")
public class UserController {

    @GetMapping("/{id}")
    public User getUser(@PathVariable Long id) {
        return userService.findById(id)
                .orElseThrow(() -> new UserNotFoundException("User not found with id: " + id));
    }

    @ExceptionHandler(UserNotFoundException.class)
    public ResponseEntity<String> handleUserNotFoundException(UserNotFoundException ex) {
        return ResponseEntity.status(HttpStatus.NOT_FOUND).body(ex.getMessage());
    }
}

```

---

### ✅ **What Happens Here?**

* When a `UserNotFoundException` is thrown, Spring automatically invokes the method annotated with `@ExceptionHandler`.
* The method returns a **`404 Not Found`** response with a custom error message.

> ✅ Justification:
>
> * Centralizes error handling for **specific exceptions**.
> * Reduces repetitive try-catch blocks in controllers.
> * Provides **custom error messages** to clients.

---

---

### ✅ **2. `@ControllerAdvice`**

> 📖 Purpose: Defines a global exception handler for multiple controllers.

---

### 🔥 **Example Usage**

```java

@ControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(UserNotFoundException.class)
    public ResponseEntity<String> handleUserNotFoundException(UserNotFoundException ex) {
        return ResponseEntity.status(HttpStatus.NOT_FOUND).body(ex.getMessage());
    }

    @ExceptionHandler(Exception.class)
    public ResponseEntity<String> handleGeneralException(Exception ex) {
        return ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR)
                             .body("An unexpected error occurred");
    }
}

```

---

### ✅ **What Happens Here?**

* Any exception from **any controller** is intercepted by `@ControllerAdvice`.
* Provides **consistent, centralized error handling** for the entire application.

> ✅ Justification:
>
> * Avoids **repetitive exception handling** across multiple controllers.
> * Centralizes logic for **maintainability and consistency**.
> * Ensures **standardized responses** for clients.

---

---

### ✅ **3. `@ResponseStatus`**

> 📖 Purpose: Automatically sets the HTTP status code for a specific exception.

---

### 🔥 **Example Usage**

```java

@ResponseStatus(value = HttpStatus.NOT_FOUND, reason = "User Not Found")
public class UserNotFoundException extends RuntimeException {
    public UserNotFoundException(String message) {
        super(message);
    }
}

```

---

### ✅ **What Happens Here?**

* When `UserNotFoundException` is thrown, Spring automatically sets the **HTTP status to `404 Not Found`** with the specified reason.
* No need for a separate exception handler.

> ✅ Justification:
>
> * Simplifies exception handling for **simple use cases**.
> * Automatically provides the **correct status code** without extra code.

---

---

### ✅ **4. `@ResponseBody`**

> 📖 Purpose: Ensures that the response is automatically serialized to JSON and returned in the response body.

---

### 🔥 **Example Usage in Exception Handling**

```java

@ExceptionHandler(UserNotFoundException.class)
@ResponseBody
public String handleUserNotFoundException(UserNotFoundException ex) {
    return ex.getMessage();
}

```

---

### ✅ **What Happens Here?**

* The response is **directly sent as JSON** to the client.
* Ensures no need for manually converting the object to JSON.

> ✅  Justification:
>
> * Ensures **automatic JSON serialization**.
> * Simplifies the response handling for **REST APIs**.

---

---

### ✅ **5. `@RestControllerAdvice`**

> 📖 Purpose: Combines the functionality of @ControllerAdvice and @ResponseBody for global exception handling in REST APIs.

---

### 🔥 **Example Usage**

```java

@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(UserNotFoundException.class)
    public ResponseEntity<Map<String, String>> handleUserNotFound(UserNotFoundException ex) {
        Map<String, String> response = new HashMap<>();
        response.put("error", ex.getMessage());
        response.put("status", "404");
        return ResponseEntity.status(HttpStatus.NOT_FOUND).body(response);
    }
}

```

---

### ✅ **What Happens Here?**

* Automatically ensures that the response is **in JSON format**.
* Provides centralized exception handling for **RESTful APIs**.

> ✅ Justification:
>
> * Simplifies and centralizes exception handling for REST APIs.
> * Reduces **boilerplate code**.

---

---

## ✅ **6. When to Use Each Exception Annotation?**


| **Scenario**                                           | **Best Annotation**     | **Why? (FPT Justification)**                                       |
| ------------------------------------------------------ | ----------------------- | ------------------------------------------------------------------ |
| Handling exceptions**in a specific controller**        | `@ExceptionHandler`     | Simple, localized exception handling.                              |
| Handling exceptions**globally across controllers**     | `@ControllerAdvice`     | Centralized handling for consistent responses.                     |
| Automatically setting**status code for simple errors** | `@ResponseStatus`       | Reduces boilerplate for simple exception scenarios.                |
| Ensuring response is**in JSON format**                 | `@ResponseBody`         | Automatically converts response to JSON.                           |
| Handling REST API exceptions globally                  | `@RestControllerAdvice` | Combines`@ControllerAdvice`and`@ResponseBody`for RESTful services. |
