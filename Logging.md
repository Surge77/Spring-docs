# Logging

In any application, especially large-scale ones, **logging** is critical for debugging, tracking errors, and monitoring system behavior. Spring Boot simplifies logging by integrating with popular logging frameworks.

### **2️⃣ Create a Logger**

Use SLF4J's Logger interface in any class.

```java

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.stereotype.Service;

@Service
public class UserService {

    private static final Logger logger = LoggerFactory.getLogger(UserService.class);

    public void createUser(String username) {
        logger.info("Creating user with username: {}", username);

        try {
            // Simulate a process
            if (username == null) {
                throw new IllegalArgumentException("Username cannot be null");
            }
        } catch (Exception e) {
            logger.error("An error occurred: {}", e.getMessage());
        }
    }
}

```

---

### **Explanation**

* **Problem**: Without logs, it's hard to track when the user creation happens or why it fails.
* **Solution**:
  * `logger.info` → Logs normal, informational events.
  * `logger.error` → Captures critical errors.
  * `{}` → Placeholders for dynamic content, avoiding string concatenation.

---

### **3️⃣ Log Levels in Spring Boot**

Each log level serves a **specific purpose**, ensuring clarity and avoiding log noise.


| **Level** | **Use Case**                                         |
| --------- | ---------------------------------------------------- |
| `TRACE`   | Most detailed information (used during development). |
| `DEBUG`   | Detailed debugging information.                      |
| `INFO`    | Informational messages (standard events).            |
| `WARN`    | Potential issues or important warnings.              |
| `ERROR`   | Errors that need immediate attention.                |

---

**Example of Each Level:**

```java

logger.trace("Trace level - Very detailed message");
logger.debug("Debug level - Detailed debugging message");
logger.info("Info level - Informational message about routine operations");
logger.warn("Warn level - Something might be wrong");
logger.error("Error level - Something failed");

```

---

### **4️⃣ Configure Logging in `application.properties`**

You can control the logging behavior using Spring Boot's configuration files.

```

# Set the root logging level
logging.level.root=INFO

# Set logging level for a specific package
logging.level.com.example=DEBUG

# Specify log file location
logging.file.name=app-log.log

# Set log pattern for better readability
logging.pattern.console=%d{yyyy-MM-dd HH:mm:ss} [%thread] %-5level %logger{36} - %msg%n

```

---

### **Explanation**

* **Problem**: Too many logs or irrelevant data can clutter log files.
* **Solution**:
  * Set appropriate **log levels** to filter noise.
  * Direct logs to files for persistence (`logging.file.name`).
  * Customize log formats for readability.

---

### **5️⃣ Custom Log Configuration with `logback-spring.xml`**

For advanced customization, use an XML file:

```xml

<?xml version="1.0" encoding="UTF-8"?>
<configuration>

    <appender name="FILE" class="ch.qos.logback.core.FileAppender">
        <file>logs/myapp.log</file>
        <encoder>
            <pattern>%d{yyyy-MM-dd HH:mm:ss} [%thread] %-5level %logger{36} - %msg%n</pattern>
        </encoder>
    </appender>

    <logger name="com.example" level="DEBUG"/>

    <root level="INFO">
        <appender-ref ref="FILE"/>
    </root>

</configuration>

```

---

**Explanation**

* **Problem**: Default logging isn’t flexible enough for advanced needs (like sending logs to external systems).
* **Solution**: Custom configurations using Logback's XML file for better control over file location, log rotation, and more.

---

### **6️⃣ Exception Logging Best Practices**

Instead of:

```java

logger.error("An error occurred: " + e);

```

Do this for better performance and readability:

```java

logger.error("An error occurred: {}", e.getMessage(), e);

```

* This ensures **efficient string construction** and provides a **full stack trace**.
