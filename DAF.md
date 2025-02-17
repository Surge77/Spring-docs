# Data Access Framework (DAF)

#### **🔍 Step 1: What Are We Trying to Solve?**

When working with databases in Java, we need to:

* Connect to a database
* Execute queries (SELECT, INSERT, UPDATE, DELETE)
* Map results to Java objects
* Handle transactions efficiently

**Traditional Approach (Without a Framework):**
We use **JDBC (Java Database Connectivity)** to interact with databases manually:

```java
Connection conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/mydb", "user", "password");
Statement stmt = conn.createStatement();
ResultSet rs = stmt.executeQuery("SELECT * FROM users");

while (rs.next()) {
    System.out.println(rs.getString("username"));
}

```

🚨 **Problems:**

* **Too much boilerplate code** (connection handling, query execution, result mapping).
* **Error-prone** (managing connections manually can lead to memory leaks).
* **Difficult to scale** (hard to switch between databases like MySQL, PostgreSQL).

---

#### **🔍 Step 2: What Are the Core Principles Behind the Solution?**

✅ **Abstraction** → Hide low-level database interactions.
✅ **Reusability** → Avoid writing repetitive SQL code.
✅ **Efficiency** → Automatically manage database connections & transactions.

---

#### **🔍 Step 3: What If We Remove Assumptions and Rebuild from Scratch?**

* **Assumption:** "Developers must handle database connections manually."
* **Reframe:** "What if we had a tool that handles connections and SQL queries for us?"
* **New Idea:** A framework that provides a **simplified, high-level API** for database operations.

---

#### **🔍 Step 4: The Birth of Spring Data Access Framework**

Spring Boot provides **Spring Data JPA**, which simplifies database interactions.

Instead of writing **JDBC code manually**, we use **Spring JPA Repositories**:

```java
@Repository
public interface UserRepository extends JpaRepository<User, Long> {
    List<User> findByUsername(String username);
}
```

🔥 **No need to write SQL!** Spring automatically generates queries for us.
