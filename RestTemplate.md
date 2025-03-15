# Rest Template

## 🎯 **1. What is the Core Problem?**

In modern applications, services often need to **communicate with other services over HTTP**. This is especially common in **microservices architectures** where services are distributed.

### 🚩 **Challenges Faced Without a REST Client**:

1. **Manual HTTP Communication is Tedious**

Sending and receiving HTTP requests using low-level APIs (like Java's `HttpURLConnection`) requires a **lot of repetitive, boilerplate code**.

1. **Error-Prone Code**
   * Manually handling HTTP status codes, error responses, and data serialization/deserialization increases the **risk of bugs**.
2. **Manual Serialization**
   * Converting Java objects to JSON and vice versa needs **custom code**.
3. **Difficult Maintenance**
   * Custom HTTP client code is **harder to maintain and debug**.

---

---

## 🚀 **2. What is the First Principles Solution?**

> Principle: Automate and simplify HTTP communication by reducing boilerplate, handling serialization, and managing errors, thereby enhancing developer productivity and code maintainability.

---

---

## ⚙️ **3. What is `RestTemplate`?**

* `RestTemplate` is a **synchronous HTTP client** provided by Spring Boot.
* It simplifies interaction with **REST APIs** by providing built-in methods for common operations like **GET, POST, PUT, and DELETE**.

---

### ✅ Why Use `RestTemplate`? 


| **Core Problem**                                       | **How`RestTemplate`Solves It (FPT Justification)**                             |
| ------------------------------------------------------ | ------------------------------------------------------------------------------ |
| Writing manual HTTP code is repetitive and error-prone | `RestTemplate`provides**simple methods**like`getForObject()`,`postForObject()` |
| Manual serialization/deserialization is tedious        | `RestTemplate` **automatically handles JSON conversion**.                      |
| Managing error handling manually is complex            | It provides**built-in error handling**.                                        |
| Managing HTTP connections manually is inefficient      | `RestTemplate` **automatically manages connections**.                          |

---

---

## 🔥4. Example of Using `RestTemplate`

### ✅ **Making a GET Request**

```java

RestTemplate restTemplate = new RestTemplate();
User user = restTemplate.getForObject("<http://api.example.com/users/1>", User.class);
System.out.println(user.getName());

```

* **What Happens Internally?**
  * Sends an HTTP `GET` request.
  * Receives the response.
  * **Automatically deserializes** JSON into a `User` object.
  * Handles any errors internally.

---

### ✅ **Making a POST Request**

```java

User newUser = new User("Alice", "alice@example.com");
User savedUser = restTemplate.postForObject("<http://api.example.com/users>", newUser, User.class);
System.out.println(savedUser.getId());

```

* **What Happens Internally?**
  * Converts `User` object to JSON.
  * Sends it as a `POST` request.
  * Receives the response and **automatically deserializes** it back into a `User` object.

---

---

## 🔄 5. Common `RestTemplate` Methods


| **Method**        | **Purpose (FPT Justification)**                                      |
| ----------------- | -------------------------------------------------------------------- |
| `getForObject()`  | Fetches an object from the API and**automatically deserializes it**. |
| `postForObject()` | Sends a new object and**handles JSON conversion automatically**.     |
| `put()`           | Updates an existing resource.                                        |
| `delete()`        | Deletes a resource.                                                  |
| `exchange()`      | Offers more control over HTTP requests and responses.                |

---

---

## ⚡ 6. How Does `RestTemplate` Work Internally?

1. **Serialization and Deserialization**
   * Uses **Jackson** (or any other configured library) to automatically **convert objects to JSON** and vice versa.
2. **Connection Handling**
   * Manages **HTTP connections and sessions** under the hood.
3. **Error Handling**
   * Automatically throws exceptions for **HTTP error codes**.
4. **Thread Blocking**
   * It's **synchronous**, meaning the thread **waits** for the response.


## 🔥 10. Why is `RestTemplate` Deprecated?

1. **Blocking Nature** → Consumes threads and reduces scalability.
2. **Inefficient for High Concurrency** → Each request blocks a thread until completion.
3. **Modern Web Requires Asynchronous Processing** → `WebClient` (from Spring WebFlux) provides better async and reactive support.

---

---

## ✅ 11. Why Use `WebClient` Instead?

* **Non-Blocking and Asynchronous** → More scalable and efficient.
* **Better Resource Utilization** → Consumes fewer threads.
* **Modern Web Applications** → Fits perfectly with reactive and microservice architectures.
