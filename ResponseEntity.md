# Response Entity

`ResponseEntity` is a class in **Spring Framework** (part of Spring Boot) that represents an HTTP response, including status code, headers, and body. It is not a built-in Java feature but comes from the **Spring Web dependency** (`spring-web`).

## **What is `ResponseEntity<>`?**

* `ResponseEntity<>` is a **wrapper around an HTTP response** that allows you to:
  1. Set the **HTTP status code**.
  2. Include **headers**.
  3. Attach a **response body (data object)**.

### **How to Use ResponseEntity**

`ResponseEntity` is commonly used in **RESTful APIs** to customize responses.

### **1. Returning a ResponseEntity in a REST Controller**

```java

import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping("/api")
public class MyController {

    @GetMapping("/hello")
    public ResponseEntity<String> sayHello() {
        return new ResponseEntity<>("Hello, World!", HttpStatus.OK);
    }
}

```

* `ResponseEntity<>("Hello, World!", HttpStatus.OK)` returns an HTTP 200 (OK) response with a message.
* You can use `HttpStatus.BAD_REQUEST`, `HttpStatus.NOT_FOUND`, etc., as needed.

---

### **2. Returning JSON Data with ResponseEntity**

```java

import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;
import java.util.HashMap;
import java.util.Map;

@RestController
@RequestMapping("/api")
public class UserController {

    @GetMapping("/user")
    public ResponseEntity<Map<String, String>> getUser() {
        Map<String, String> user = new HashMap<>();
        user.put("name", "John Doe");
        user.put("email", "john.doe@example.com");

        return ResponseEntity.ok(user);
    }
}

```

* `ResponseEntity.ok(user)` is a shortcut for `new ResponseEntity<>(user, HttpStatus.OK)`, returning a JSON response.

---

### **3. Handling Errors with ResponseEntity**

```java

import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/api")
public class ErrorController {

    @GetMapping("/error")
    public ResponseEntity<String> handleError() {
        return ResponseEntity.status(HttpStatus.BAD_REQUEST).body("Invalid request");
    }
}

```

* `ResponseEntity.status(HttpStatus.BAD_REQUEST).body("Invalid request")` sets both status and body.

---

### **4. ResponseEntity with Custom Headers**

```java

import org.springframework.http.HttpHeaders;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping("/api")
public class HeaderController {

    @GetMapping("/custom-header")
    public ResponseEntity<String> withHeaders() {
        HttpHeaders headers = new HttpHeaders();
        headers.add("Custom-Header", "MyValue");

        return new ResponseEntity<>("Response with headers", headers, HttpStatus.OK);
    }
}

```
