# Validation Annotations

Spring Boot provides **validation annotations** to enforce rules on data inputs in applications. These annotations come from **Jakarta Validation API (Javax Validation API)** and are used to ensure data integrity before processing.

1. **Fundamental Problem**:
   * Users might send incorrect or invalid data in HTTP requests.
   * Storing bad data can lead to system crashes, security risks, or incorrect results.
2. **Core Principles for a Solution**:
   * We need **automated validation** before data reaches the service layer.
   * Validation should be **easy to apply** and should not require extra boilerplate code.
   * Errors should be reported **clearly** to the user.
3. **Derived Solutions**:
   * Spring Boot leverages **Jakarta Validation API** with annotations to check data automatically.
   * These annotations work with **DTOs (Data Transfer Objects)** to ensure incoming data is valid.


## **🔹 Validation Annotations in Spring Boot**

Here’s how they work, along with their **First Principles Explanation**:

### **1️⃣ @NotNull**

* **Principle**: A field must not be `null`, but it **can** be empty (`""`).
* **Use Case**: Ensures critical fields (e.g., username, email) are not null.
* **Example**:
  ```java

  public class UserDTO {
      @NotNull(message = "Username cannot be null")
      private String username;
  }

  ```
* **Explanation**:
  * Problem: If `username` is null, the app might break when trying to process it.
  * Solution: This ensures a value is always present before processing.

---

### **2️⃣ @NotEmpty**

* **Principle**: A field must **not be empty**, but it can contain spaces.
* **Use Case**: Strings should have some content.
* **Example**:
  ```java

  public class UserDTO {
      @NotEmpty(message = "Password cannot be empty")
      private String password;
  }

  ```
* **Explanation**:
  * Problem: If a user submits `""` as a password, they might gain unintended access.
  * Solution: Ensures passwords and other required fields are not empty.

---

### **3️⃣ @NotBlank**

* **Principle**: A field must contain **non-whitespace characters**.
* **Use Case**: Prevents users from entering just spaces.
* **Example**:
  ```java

  public class UserDTO {
      @NotBlank(message = "First name cannot be blank")
      private String firstName;
  }

  ```
* **Explanation**:
  * Problem: Users might enter just `" "` (spaces), which is not useful.
  * Solution: Forces users to enter at least one visible character.

---

### **4️⃣ @Size(min, max)**

* **Principle**: Limits the length of a string or collection.
* **Use Case**: Ensures inputs are not too short or too long.
* **Example**:
  ```java

  public class UserDTO {
      @Size(min = 3, max = 15, message = "Username must be between 3 and 15 characters")
      private String username;
  }

  ```
* **Explanation**:
  * Problem: If a username is too short, it’s not meaningful; too long, it’s impractical.
  * Solution: Controls input length for better UX and data consistency.

---

### **5️⃣ @Min & @Max**

* **Principle**: Sets numerical limits.
* **Use Case**: Ensures age, price, quantity, etc., are within a valid range.
* **Example**:
  ```java

  public class ProductDTO {
      @Min(value = 1, message = "Price must be at least 1")
      @Max(value = 10000, message = "Price must not exceed 10000")
      private int price;
  }

  ```
* **FPT Explanation**:
  * Problem: Users could enter negative prices, breaking the logic.
  * Solution: Forces numbers to stay within reasonable limits.

---

### **6️⃣ @Pattern**

* **Principle**: Ensures a field matches a **regular expression (regex)**.
* **Use Case**: Enforcing email, phone number, or specific formatting rules.
* **Example**:
  ```java

  public class UserDTO {
      @Pattern(regexp = "^[A-Za-z0-9]{5,15}$", message = "Username must be alphanumeric and 5-15 characters long")
      private String username;
  }

  ```
* **Explanation**:
  * Problem: Users might enter special characters or incorrect formats.
  * Solution: Forces input to match specific rules.

---

### **7️⃣ @Email**

* **Principle**: Ensures a field follows **email format**.
* **Use Case**: Validating user email addresses.
* **Example**:
  ```java

  public class UserDTO {
      @Email(message = "Invalid email format")
      private String email;
  }

  ```
* **Explanation**:
  * Problem: Users could enter `"notanemail"`, breaking communication features.
  * Solution: Ensures emails are correctly formatted.

---

### **8️⃣ @Positive & @Negative**

* **Principle**: Ensures a number is **greater than zero** or **less than zero**.
* **Use Case**: Validating IDs, prices, bank balances, etc.
* **Example**:
  ```java

  public class AccountDTO {
      @Positive(message = "Balance must be positive")
      private double balance;
  }

  ```
* **Explanation**:
  * Problem: Negative balances might cause incorrect calculations.
  * Solution: Forces positive values where needed.

---

### **9️⃣ @Future & @Past**

* **Principle**: Ensures a **date is in the future or past**.
* **Use Case**: Birthdates, appointment dates, etc.
* **Example**:
  ```java

  public class BookingDTO {
      @Future(message = "Appointment date must be in the future")
      private LocalDate appointmentDate;
  }

  ```
* **Explanation**:
  * Problem: Users might enter invalid dates.
  * Solution: Ensures dates are logically valid.

---

### **🔹 Implementing Validation in Spring Boot**

To enable validation, use `@Valid` inside a controller:

```java

import org.springframework.http.ResponseEntity;
import org.springframework.validation.annotation.Validated;
import org.springframework.web.bind.annotation.*;

import javax.validation.Valid;

@RestController
@RequestMapping("/users")
@Validated
public class UserController {

    @PostMapping("/register")
    public ResponseEntity<String> registerUser(@Valid @RequestBody UserDTO userDTO) {
        return ResponseEntity.ok("User registered successfully!");
    }
}

```
