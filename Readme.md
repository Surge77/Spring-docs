![Spring Logo](https://miro.medium.com/v2/resize:fit:100/1*uK7MtWXftyVVmbfa0NW3Nw.jpeg)

Welcome to the **Spring Documentation** repository! This repository contains comprehensive and up-to-date documentation for the **Spring Framework** and related projects, including Spring Boot, Spring Security, Spring Data, Spring Cloud, and more.

Whether you're a beginner or an experienced developer, this documentation aims to provide everything you need to understand, configure, and effectively use the Spring ecosystem for building enterprise-level Java applications.

#### Key Features:

* **Comprehensive Guides**: Detailed step-by-step guides for various Spring projects (e.g., Spring Boot, Spring Data JPA, Spring Security).
* **API References**: In-depth explanations of Spring Framework’s APIs and their usage.
* **Tutorials**: Practical examples and tutorials on implementing common use cases with Spring.
* **Best Practices**: Recommendations on how to build scalable, maintainable, and secure Spring applications.
* **Community Contributions**: Contributions from the Spring community to ensure the documentation stays relevant and up-to-date.

#### Topics Covered:

* **Spring Boot**: Auto-configuration, Spring Boot Starter Projects, Creating REST APIs, and more.
* **Spring Security**: Authentication, Authorization, OAuth2, JWT, and other security features.
* **Spring Data**: Integrating with databases using JPA, MongoDB, Cassandra, and more.
* **Spring Cloud**: Distributed systems, microservices, service discovery, and cloud-native development.
* **Spring Integration**: Building messaging-based applications with Spring Integration.
* **Spring Batch**: Handling batch processing in Spring.

* [X]  4 Different ways of creating a springboot project

- create a maven project and add starter dependencies
- Using spring initializr
- Using IDE like sts (Spring tool suite)
- Springboot command line interface

Application Context => This is an interface so we cant create object of it so we use the subclasses of the application context

- ClasspathXMLApplicationContex
- AnnotationConfigApplicationContext
- FileSystemXMLApplicationContext

* [X]  Data Access Framework (DAF)
* [X]  Spring MVC Framework
* [X]  Spring bean?
* [X]  @Component @Autowired
* [X]  Dependency injection types : Field injection,constructor injection,setter injection,Configuration methods
* [X]  Difference between dependencies and dependency injection (DI)
* [X]  Console Project vs Web project
* [X]  Lombok => **Lombok** is a Java library that helps **reduce boilerplate code** in Java applications, such as **getters, setters, constructors, `toString()`, and `equals()` methods**
* [X]  Why do we create a interface in repository package => Interfaces in repositories promote **abstraction, flexibility, and maintainability**, aligning with the core principle of writing clean, scalable, and testable code.
* [X]  In Model package define the schema
* [X]  THe job of the repository is to connect to the database and perform CRUD operations
* [X]  JDBC -> 7 steps process
* [X]  ORM -> A mapping/connecting of objects in java to the relational tables in sql/ any other rdbms
* [X]  Relational database mapping

* Classname becomes -> table name
* Each variable inside class becomes -> column
* Each object becomes -> row in the table
* ORM does all these things for you
* EX : hibernate(Mostly used), EclipseLink, Mybatis

* [X]  Spring Data JPA (Java persistence API) -> These are just standards and the ORMs like hibernate implement them
* [X]  Inversion of control Container (IOC) => requires two things , Beans/POJO's and xml configurations
* [X]  Why do we use @getMapping,@postMapping instead of just @RequestMapping
* [X]  Enums
* [ ]  UI Layer => ProductController => We use tools like Strut/JSF or Spring MVC
* [ ]  Bussiness/Services Layer => ProductService => modules Spring security, Transaction management
* [ ]  Data Access Layer => ProductDao => We use tools like Spring JDBC,spring ORM
* [ ]  Spring Core Modules =>  Core , beans , Context , spEL
* [ ]  other modules => AOP , Aspect , Instrumentation , Messaging
* [ ]  Data Access/Integration modules => JDBC , ORM , JMS , OXM
* [ ]  Web modules => Web , Portlet , Servlet , WebSocket
* [ ]  Testing modules => Test
* [X]  Pom => Project Object model
* [X]  RestTemplate, Rest client, Rest Template, webflux
* [X]  Custom finder methods/derived query methods
* [X]  mvn clean install => Build the project using Maven
* [X]  mvn spring-boot:run => Run the application
* [X]  Spring boot starter mail
* [X]  Validation annotations
* [X]  Exception annotations
* [X]  Aspect oriented programming (AOP)
* [X]  ResponseEntity<>
* [X]  Logger in springboot
* [X]  cron expressions using @Scheduled annotation

## **Project Structure**

```
spring-boot-concepts/
├── src/
│   ├── main/
│   │   ├── java/com/TEJAS/springbootweb/
│   │   │   ├── controllers/   # Handles API requests
│   │   │   ├── services/      # Business logic layer
│   │   │   ├── repositories/  # Data access layer (JPA Repositories)
│   │   │   ├── models/        # Data models/entities
│   │   │   ├── advices/       # Exception handling
│   │   │   ├── SpringbootwebApplication.java  # Main application entry point
│   ├── test/                  # Test cases for components
├── pom.xml                    # Maven dependencies
├── README.md                   # Documentation
```

* **Spring Boot Web**: Build RESTful web applications with ease.
* **Validation**: Data validation using `javax.validation` and Spring Boot Starter Validation.
* **Database Management**: Use of JPA with H2 in-memory database.
* **Model Mapping**: Efficient object mapping with ModelMapper.
* **Lombok**: Simplifies Java code by reducing boilerplate.
* **Testing**: Unit and integration testing with Spring Boot Starter Test.

### **1. Spring Boot Starter Web**

- **What is it?**
  A starter dependency to build web applications and REST APIs.
- **Why used?**
  Provides auto-configuration for Spring MVC and embedded Tomcat server.
- **Key Features:**
  - RESTful controllers (`@RestController`)
  - Request handling with `@GetMapping`, `@PostMapping`, etc.
  - Exception handling with `@ControllerAdvice`.

---

### **2. Spring Boot Validation**

- **What is it?**
  Validates request data using annotations like `@NotNull`, `@Size`, etc.
- **Why used?**
  Ensures data integrity before processing requests.
- **Key Features:**
  - `@Valid` annotation to trigger validation.
  - Custom error messages via `@ExceptionHandler`.

**Example:**

```java
@Valid
public ResponseEntity<User> createUser(@RequestBody @Valid User user) {
   return ResponseEntity.ok(userService.save(user));
}
```

---

### **3. Spring Data JPA**

- **What is it?**
  An abstraction layer for database interactions.
- **Why used?**
  Simplifies database access with repository interfaces.
- **Key Features:**
  - `CrudRepository` and `JpaRepository` for CRUD operations.
  - Query methods like `findById`, `findAll`, etc.

**Example:**

```java
public interface UserRepository extends JpaRepository<User, Long> {
   Optional<User> findByEmail(String email);
}
```

---

### **4. H2 Database**

- **What is it?**
  A lightweight in-memory database for testing and development.
- **Why used?**
  Allows testing without the need for an external database.
- **Key Features:**
  - Auto-configuration in `application.properties`
  - Web console for inspecting data (`http://localhost:8080/h2-console`).

**Example Configuration:**

```properties
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=
```

---

### **5. Lombok**

- **What is it?**
  A library to reduce boilerplate code in Java (e.g., getters, setters).
- **Why used?**
  Makes code cleaner and easier to maintain.
- **Key Annotations:**
  - `@Data` - Generates getters, setters, toString, and equals methods.
  - `@NoArgsConstructor` and `@AllArgsConstructor` - Generates constructors.

**Example:**

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class User {
   private Long id;
   private String name;
   private String email;
}
```

---

### **6. ModelMapper**

- **What is it?**
  A library for object-to-object mapping.
- **Why used?**
  Converts DTOs to entities and vice versa without manual mapping.
- **Example:**

```java
ModelMapper modelMapper = new ModelMapper();
UserDTO userDTO = modelMapper.map(user, UserDTO.class);
```

---

### **7. Exception Handling**

- **What is it?**
  A mechanism to handle application errors gracefully.
- **Why used?**
  Provides user-friendly error messages and logs.
- **Key Components:**
  - `@ControllerAdvice` for centralized error handling.
  - `@ExceptionHandler` for specific exception handling.

**Example:**

```java
@ControllerAdvice
public class GlobalExceptionHandler {
   @ExceptionHandler(ResourceNotFoundException.class)
   public ResponseEntity<String> handleNotFound(ResourceNotFoundException ex) {
      return ResponseEntity.status(HttpStatus.NOT_FOUND).body(ex.getMessage());
   }
}
```

---

## **Running Tests**

To run unit tests, use the following command:

```bash
mvn test
```

Test cases are written to validate controllers and services.
