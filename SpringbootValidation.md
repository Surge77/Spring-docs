# Spring Boot Validation

The **Spring Starter Validation** dependency (from `spring-boot-starter-validation`) provides various annotations to validate user input in Spring Boot applications. It is based on **Jakarta Bean Validation (formerly Javax Validation)**.


### **1. Basic Constraints**


| Annotation            | Description                                                                                         |
| --------------------- | --------------------------------------------------------------------------------------------------- |
| `@NotNull`            | Field must not be`null`, but can be empty (for strings).                                            |
| `@NotEmpty`           | Field must not be`null`and must have at least one character (for strings, collections, maps, etc.). |
| `@NotBlank`           | Field must contain at least one non-whitespace character (for strings).                             |
| `@Size(min=, max=)`   | Ensures a string, collection, or array is within a specific size range.                             |
| `@Pattern(regexp="")` | Ensures a string matches the given**regular expression**.                                           |

### **2. Numeric Constraints**


| Annotation                     | Description                                                |
| ------------------------------ | ---------------------------------------------------------- |
| `@Min(value)`                  | Ensures a number is at least a certain value.              |
| `@Max(value)`                  | Ensures a number does not exceed a certain value.          |
| `@Positive`                    | Ensures a number is**greater than zero**.                  |
| `@PositiveOrZero`              | Ensures a number is**zero or greater**.                    |
| `@Negative`                    | Ensures a number is**less than zero**.                     |
| `@NegativeOrZero`              | Ensures a number is**zero or less**.                       |
| `@Digits(integer=, fraction=)` | Limits the number of**integer and decimal places**allowed. |

### **3. Date & Time Constraints**


| Annotation         | Description                                    |
| ------------------ | ---------------------------------------------- |
| `@Past`            | Ensures a date is in the**past**.              |
| `@PastOrPresent`   | Ensures a date is in the**past or present**.   |
| `@Future`          | Ensures a date is in the**future**.            |
| `@FutureOrPresent` | Ensures a date is in the**future or present**. |

### **4. Advanced Constraints**


| Annotation     | Description                   |
| -------------- | ----------------------------- |
| `@Email`       | Ensures a valid email format. |
| `@AssertTrue`  | Field must be`true`.          |
| `@AssertFalse` | Field must be`false`.         |

### **5. Custom Validation**

* **`@Valid`**: Used for **nested objects** (e.g., if a field is another object, Spring will validate it recursively).
* **`@Validated`**: Used at the **class or method level** to enable validation on method parameters.
* After adding the validation inside the model class update the corresponding controller class using @Valid

### **Where to Add `@Valid`?**


| Scenario                          | Annotation Placement                              | Example                      |
| --------------------------------- | ------------------------------------------------- | ---------------------------- |
| **JSON Body (POST, PUT)**         | `@Valid @RequestBody`                             | ✅ Common                    |
| **Query Params (`?key=value`)**   | `@Validated`at class level + constraint in method | 🔹 Rare                      |
| **Path Variables (`/user/{id}`)** | `@Validated`at class level + constraint in method | 🔹 Rare                      |
| **Form Data (MVC Apps)**          | `@Valid @ModelAttribute`                          | 🔹 Only for traditional apps |
