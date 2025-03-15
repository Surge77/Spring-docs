# Why do we need a model class

### ✅ **1. Represent Real-World Entities**

* **Problem:** Every application manages data, which represents **real-world entities** (like `User`, `Product`, or `Order`).
* **Solution:** A **model class** is used to define these entities in the application as **plain Java objects (POJOs)**.


### ✅ **2. Define Data Structure**

* **Problem:** The application needs a **structured format** to store and manipulate data consistently.
* **Solution:** A model class defines the **structure of data** with its attributes (fields).

```java
public class User {
    private Long id;
    private String name;
    private String email;
}

```


### ✅ **3. Facilitate Database Mapping**

* **Problem:** The object-oriented nature of Java needs to be mapped to relational database tables.
* **Solution:** ORM tools (like Hibernate) use **annotations** in model classes to automatically map them to **database tables**.

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

Here, ORM maps: * Class → Table (`users`)

* Fields → Columns (`id`, `name`, `email`)
* Objects → Rows


### ✅ **4. Ensure Data Integrity**

* **Problem:** Not all data should be accepted into the system (like empty names or invalid emails).
* **Solution:** Use **validation annotations** in the model class.

```java
@NotNull
@Size(min = 2, message = "Name should have at least 2 characters")
private String name;

```

This ensures the data is **valid** before being saved.

### ✅ **5. Simplify Data Transfer**

* **Problem:** Data needs to be transferred between layers (like Controller → Service → Repository).
* **Solution:** The model class acts as a **Data Transfer Object (DTO)**, carrying data across the application.

### ✅ **6. Encapsulation (Object-Oriented Principle)**

* **Problem:** Direct access to data can lead to inconsistency or security risks.
* **Solution:** Use **private fields** with public **getters and setters** to control data access.

```java
public String getName() {
    return name;
}

public void setName(String name) {
    this.name = name;
}

```



| **Core Problem**                                    | **First Principle Solution (Model Class Role)**        |
| --------------------------------------------------- | ------------------------------------------------------ |
| Need to represent real-world entities               | Define classes that mirror real-world data structures. |
| Require structured and consistent data              | Use fields to define the structure of each entity.     |
| Database needs mapping to Java objects              | Use ORM annotations for automatic mapping.             |
| Ensure only valid data enters the system            | Use validation annotations to enforce data integrity.  |
| Data must be transferred between layers             | Model classes act as**Data Transfer Objects (DTOs)**.  |
| Maintain encapsulation and control over data access | Use private fields with public getters and setters.    |
