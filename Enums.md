# Enumerations or enums

## 🎯 **1. What is the Core Problem?**

* In any application, we often need to represent a **fixed set of constant values**.
* For example, defining statuses like `PENDING`, `APPROVED`, `REJECTED` or user roles like `ADMIN`, `USER`.

### 🚩 **Problems Without Enums**:

1. **Magic Strings or Integers**
   * Using hardcoded strings or numbers leads to **errors and inconsistency**.

```java

String status = "approved"; // Easy to make typos like "apprved"

```

1. **Lack of Type Safety**
   * The compiler can’t detect invalid values, causing **runtime errors**.
2. **Difficult Maintenance**
   * Changing constant values in multiple places is **error-prone**.



## ⚙️ 3. What is an Enum?

* An **enum** is a **special data type** in Java used to represent a **fixed set of constants**.
* It enforces **type safety**, reduces errors, and improves readability.


### ✅ **Example of Enum in Spring Boot**

```java

public enum Status {
    PENDING,
    APPROVED,
    REJECTED
}

```

* Now, when you use `Status`, you're **restricted to these values**.

```java

Status status = Status.APPROVED;

```


## 🔄 **4. How to Use Enums in Spring Boot? (FPT Approach)**

### ✅ **a. Using Enum in Entity Classes**

```java

@Entity
public class Order {
    @Id
    private Long id;

    @Enumerated(EnumType.STRING)
    private Status status;
}

```

> Why use @Enumerated(EnumType.STRING)?

* It tells Hibernate to store the enum as a **string** (e.g., `"PENDING"`) in the database, ensuring **readability and maintainability**.
* Without specifying, it defaults to `EnumType.ORDINAL` (0, 1, 2), which is less readable and harder to maintain.


### ✅ **b. Using Enum in Repositories**

```java

public interface OrderRepository extends JpaRepository<Order, Long> {
    List<Order> findByStatus(Status status);
}

```

* ORM tools (like Hibernate) automatically map the **enum values** during query execution.

---

### ✅ **c. Using Enum in REST APIs (Request & Response)**

```java

@PostMapping("/order")
public ResponseEntity<Order> createOrder(@RequestBody Order order) {
    return ResponseEntity.ok(orderRepository.save(order));
}

```

> How Spring Boot Handles Enums Automatically:

* When a request is sent with:

```json

{
    "status": "PENDING"
}

```

* Spring Boot automatically **converts the string to the corresponding enum**.


## 🔥 5. How Does Spring Boot Handle Enums Internally?

1. **Deserialization (JSON → Enum)**
   * Spring Boot uses **Jackson** to automatically map JSON string values to the corresponding enum constants.
2. **Database Mapping**
   * Using `@Enumerated(EnumType.STRING)`, Spring Boot maps the enum to the corresponding **string** in the database.
3. **Validation**
   * Spring Boot validates whether the provided value is a **valid enum constant**. If not, it throws an error.

---

---

## ⚡ 6. Enum with Custom Methods

* Enums can also have **custom fields and methods** for advanced logic.

```java

public enum Status {
    PENDING("Pending Approval"),
    APPROVED("Approved Successfully"),
    REJECTED("Rejected by Admin");

    private final String message;

    Status(String message) {
        this.message = message;
    }

    public String getMessage() {
        return message;
    }
}

```

* Usage:

```java
Status status = Status.APPROVED;
System.out.println(status.getMessage()); // "Approved Successfully"

```

> ✅ Justification:

* Simplifies complex status handling by **encapsulating logic** within the enum.
* Reduces the need for **if-else chains**.


## ⚙️ **8. Common Mistakes to Avoid with Enums in Spring Boot**

1. **Not Using `EnumType.STRING`**
   * Using the default `EnumType.ORDINAL` stores enums as integers (0, 1, 2), which is less readable.
2. **Case Sensitivity in REST APIs**
   * Enums are **case-sensitive** by default. `"pending"` will cause an error; it must be `"PENDING"`.
3. **Not Handling Invalid Enums in APIs**
   * Spring Boot will throw a `400 Bad Request` if an invalid enum is passed.
