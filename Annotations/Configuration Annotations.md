# Configuration & Lifecycle Annotations

These annotations **control Spring’s behavior** at runtime.

### **🔹 `@Configuration` (Defines Beans Manually)**

* **What it does:** Marks a class as a Spring **configuration** class.
* **Why?** Useful when manually defining Beans.

```java
@Configuration
public class AppConfig {
    @Bean
    public MyService myService() {
        return new MyService();
    }
}
```

### **🔹 `@Bean` (Manually Define a Bean)**

* **What it does:** Registers a method's return value as a **Spring Bean**.
* **Why?** Needed when we can't use `@Component`.

```java
@Bean
public RestTemplate restTemplate() {
    return new RestTemplate();
}
```

### **🔹 `@Scope` (Bean Scope Control)**

* **What it does:** Defines how a Bean should be created.
* **Common Scopes:**
  * `@Scope("singleton")` → One Bean for the whole app.
  * `@Scope("prototype")` → New Bean every time.

```java
@Component
@Scope("prototype")
public class MyBean {
}
```

### **🔹 `@PostConstruct` (Initialize a Bean)**

* **What it does:** Runs a method **after the Bean is created**.
* **Why?** Useful for **initializing resources**.

```java
@Component
public class MyBean {
    @PostConstruct
    public void init() {
        System.out.println("Bean initialized!");
    }
}
```

### **🔹 `@PreDestroy` (Clean Up Before Shutdown)**

* **What it does:** Runs a method **before the Bean is destroyed**.
* **Why?** Useful for **releasing resources**.

```java
@Component
public class MyBean {
    @PreDestroy
    public void destroy() {
        System.out.println("Bean destroyed!");
    }
}
```
