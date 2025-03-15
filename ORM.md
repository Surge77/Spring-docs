# ORM (Object Relational Mapping)

## 🎯 **1. What is the Core Problem?**

* Applications are typically built using **Object-Oriented Programming (OOP)** languages like Java, Python, or C#.
* Data in applications is represented as **objects** (with attributes and methods).
* However, most databases store data in **relational tables** with rows and columns.

> 🚩 **Key Problem:**

* There's a **fundamental mismatch** between how objects are represented in code (OOP) and how data is stored in relational databases (tables).
* This is known as the **Object-Relational Impedance Mismatch**.


## ⚡ **2. What Challenges Arise Without ORM?**

1. **Manual Mapping Complexity**
   * Developers need to manually convert objects to database tables and vice versa.
   * This involves **writing a lot of boilerplate SQL code**.
2. **Error-Prone Data Handling**
   * Manually mapping data can lead to **inconsistencies and mistakes** (like missing fields or incorrect data types).
3. **Difficult Relationship Management**
   * Complex relationships (like **one-to-many** or **many-to-many**) are hard to manage manually.
4. **Transaction Management is Tedious**
   * Developers must manually manage **transactions**, ensuring consistency and rollback in case of errors.
5. **Time-Consuming Development**
   * Writing and maintaining SQL queries slows down development.


## ⚙️ **4. How Does ORM Solve the Core Problems?**

### ✅ **a. Automatic Mapping (Class ↔️ Table)**

* ORM frameworks like **Hibernate, JPA, and MyBatis** automatically map:


| **Object-Oriented Concept** | **Relational Database Concept** |
| --------------------------- | ------------------------------- |
| Class                       | Table                           |
| Object                      | Row                             |
| Fields                      | Columns                         |
| Object Relationships        | Foreign Keys                    |


```java
@Entity
@Table(name = "users")
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;
    private String email;
}

```


> **What does ORM do?**

* Automatically creates a **`users` table** with `id`, `name`, and `email` columns.
* Automatically maps each **`User` object** to a row in the table.
* ORM allows performing database operations without writing SQL.

> Without ORM (Manual SQL):

```sql

INSERT INTO users (name, email) VALUES ('Alice', 'alice@example.com');

```

> With ORM:

```sql
User user = new User("Alice", "alice@example.com");
userRepository.save(user);

```

> ✅ How Does This Solve the Core Problem?

* **Reduces repetitive code**.
* **Prevents mistakes** in query syntax.
* Simplifies development.


### ✅ **c. Automatic Relationship Management**

* ORM handles **complex relationships** using simple annotations.

```java

@Entity
public class User {
    @OneToMany(mappedBy = "user")
    private List<Order> orders;
}

@Entity
public class Order {
    @ManyToOne
    @JoinColumn(name = "user_id")
    private User user;
}

```

* ORM automatically manages the foreign key (`user_id`) and relational integrity.


### ✅ **d. Transaction Management**

* ORM frameworks **automatically handle transactions**.

```java

@Transactional
public void saveUser(User user) {
    userRepository.save(user);
}

```

* If an error occurs, the transaction **automatically rolls back**, ensuring data consistency.


### ✅ **e. Query Simplification**

* ORM simplifies complex queries using method naming conventions or JPQL (Java Persistence Query Language).

```java

User user = userRepository.findByEmail("alice@example.com");

```

* Spring Data JPA automatically generates the SQL query.
