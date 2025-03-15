# Cron Expressions in spring boot

In Spring Boot, **cron expressions** are used to schedule tasks to run at specific intervals or times.


## 🔥 **Where Do Cron Expressions Come From?**

* Cron expressions originate from **Unix/Linux cron jobs**, where they're used to schedule scripts.
* In Spring Boot, these expressions follow a **specific format** to control task execution.


## ✅ **Cron Expression Format in Spring Boot**

A cron expression in Spring Boot consists of **6 fields** (or **7** if seconds are included):

```

second minute hour day-of-month month day-of-week [year]

```

### **Field Breakdown**:


| **Field**        | **Allowed Values** | **Special Characters** |
| ---------------- | ------------------ | ---------------------- |
| **Seconds**      | 0–59              | `* / , -`              |
| **Minutes**      | 0–59              | `* / , -`              |
| **Hours**        | 0–23              | `* / , -`              |
| **Day of Month** | 1–31              | `* / , - ? L W`        |
| **Month**        | 1–12 or JAN–DEC  | `* / , -`              |
| **Day of Week**  | 0–6 or SUN–SAT   | `* / , - ? L #`        |

---

### **Special Characters Explained**:

* → Every possible value (e.g., every minute, every hour).
* `?` → No specific value (used for **either** day-of-month or day-of-week).
* → Defines ranges (e.g., `1-5` means Monday to Friday).
* `,` → Lists multiple values (e.g., `MON,WED,FRI`).
* `/` → Specifies increments (e.g., `/5` means every 5 units).
* `L` → Last day of the month or week.
* `W` → Nearest weekday to a given day.
* `#` → Specific occurrence (e.g., `2#1` means **first Monday** of the month).

---

## 🚀 **Usage of Cron Expressions in Spring Boot**

---

### **1️⃣ Enabling Scheduling**

First, enable scheduling in the main Spring Boot application class:

```java

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.scheduling.annotation.EnableScheduling;

@SpringBootApplication
@EnableScheduling
public class SchedulerApplication {
    public static void main(String[] args) {
        SpringApplication.run(SchedulerApplication.class, args);
    }
}

```

---

### **2️⃣ Creating a Scheduled Task**

Use the `@Scheduled` annotation with a cron expression:

```java
import org.springframework.scheduling.annotation.Scheduled;
import org.springframework.stereotype.Component;

@Component
public class ScheduledTasks {

    @Scheduled(cron = "0 0 0 * * ?")
    public void runDailyTask() {
        System.out.println("Running daily task at midnight");
    }
}

```

---

### **Explanation**:

* **Problem**: How to run the task every day at **midnight**?
* **Solution**: The cron `"0 0 0 * * ?"` means:
  * `0` seconds
  * `0` minutes
  * `0` hours
  * every day
  * every month
  * `?` no specific day of the week.

---

## 🕒 **Common Cron Expression Examples**


| **Cron Expression**   | **Meaning**                              |
| --------------------- | ---------------------------------------- |
| `"0 0 * * * *"`       | Every hour.                              |
| `"0 0 12 * * ?"`      | Every day at**12 PM**.                   |
| `"0 0 12 * * MON"`    | Every**Monday at 12 PM**.                |
| `"0 0/5 * * * ?"`     | Every**5 minutes**.                      |
| `"0 15 10 * * ?"`     | Every day at**10:15 AM**.                |
| `"0 0 0 1 * ?"`       | **First day**of every month at midnight. |
| `"0 0 0 * * SUN"`     | Every**Sunday at midnight**.             |
| `"0 0 0 * * MON-FRI"` | Every**weekday at midnight**.            |

---

### **3️⃣ Using External Cron Expressions**

You can externalize cron expressions to make them configurable:

```

myapp.cron.daily=0 0 0 * * ?

```

Then use it in the code:

```java

@Scheduled(cron = "${myapp.cron.daily}")
public void dailyTask() {
    System.out.println("Daily task from externalized cron");
}

```

---

### **Explanation**

* **Problem**: Hardcoding cron expressions makes future changes difficult.
* **Solution**: Externalizing cron expressions in `application.properties` allows for easier modifications.

---

### **4️⃣ Handling Time Zones**

Spring Boot uses the system’s default timezone. To specify a custom timezone:

```java

@Scheduled(cron = "0 0 0 * * ?", zone = "Asia/Kolkata")
public void taskWithTimeZone() {
    System.out.println("Scheduled in IST timezone");
}

```

---

### **Explanation**

* **Problem**: In global applications, tasks may need to run according to specific local times.
* **Solution**: The `zone` attribute ensures the task runs in the correct timezone.
