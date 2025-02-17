# Spring Beans

In a Java application, we often create objects like this:

```java
UserService userService = new UserService();

```

🚨 **Problems:**

* **Manual object creation:** We have to manually instantiate and manage dependencies.
* **Tightly coupled code:** If `UserService` needs `DatabaseService`, we must pass it manually.
* **Hard to test & maintain:** Changing one class means modifying many parts of the code.

🚀 **Think of it like a Coffee Shop:**

* Instead of making coffee at home (manual object creation),
* You order it from a barista (Spring Container).
* The barista prepares it and serves it when needed (Bean Management).

Spring **acts as the barista**, preparing and serving objects (Beans) when required.

1️⃣ **Spring Beans Are Created Automatically**

We define a Bean, and Spring **creates it automatically**:

```java
@Component
public class DatabaseService {
    public void connect() {
        System.out.println("Connected to database!");
    }
}

```

2️⃣ **Spring Injects Dependencies Automatically (Dependency Injection)**
If `UserService` needs `DatabaseService`, we **just annotate it**:

```java
@Service
public class UserService {
    private final DatabaseService dbService;

    @Autowired  // Spring injects DatabaseService automatically
    public UserService(DatabaseService dbService) {
        this.dbService = dbService;
    }
}

```

🔥 **No need to manually create objects!**

3️⃣ **Types of Spring Beans**

* `@Component` → Generic bean
* `@Service` → Used for business logic classes
* `@Repository` → Used for database interactions
* `@Controller` → Used for web controllers
