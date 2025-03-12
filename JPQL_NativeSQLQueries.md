# Executing JPQL and Native Queries with Spring Data JPA (`@Query` & `@Param` Annotations)

Spring Data JPA provides the `@Query` annotation to define **JPQL (Java Persistence Query Language)** or **Native SQL** queries within repository interfaces. These annotations allow complex queries beyond standard JPA methods.

## **1. JPQL (`@Query`) – Object-Oriented Queries**

JPQL is similar to SQL but operates on **entity objects** instead of database tables.

### **Example: JPQL Query using `@Query`**

```java
@Repository
public interface EmployeeRepository extends JpaRepository<Employee, Long> {
  
    // JPQL Query: Fetch employees by department
    @Query("SELECT e FROM Employee e WHERE e.department = :dept")
    List<Employee> findEmployeesByDepartment(@Param("dept") String department);
}

```

### **Explanation:**

* `@Query("SELECT e FROM Employee e WHERE e.department = :dept")`
  * Uses **JPQL** (operates on entities, not tables).
  * `Employee e` refers to the **Employee entity**, not the table.
* `:dept` is a named parameter (placeholder for the method argument).
* `@Param("dept")` binds the method parameter `department` to `:dept`.

### **Usage in Service Layer:**

```java
@Service
public class EmployeeService {
    @Autowired
    private EmployeeRepository employeeRepository;

    public List<Employee> getEmployeesByDepartment(String department) {
        return employeeRepository.findEmployeesByDepartment(department);
    }
}

```

## **2. Native SQL Queries (`@Query` with `nativeQuery = true`)**

Native queries allow writing **pure SQL** instead of JPQL.

### **Example: Native SQL Query**

```java
@Repository
public interface EmployeeRepository extends JpaRepository<Employee, Long> {

    // Native SQL Query
    @Query(value = "SELECT * FROM employees WHERE department = :dept", nativeQuery = true)
    List<Employee> findEmployeesByDepartmentNative(@Param("dept") String department);
}

```

### **Key Differences from JPQL:**

* `@Query(value = "SELECT * FROM employees WHERE department = :dept", nativeQuery = true)`
  * Uses **SQL** (works directly on tables).
  * `"employees"` is the actual **table name** in the database.
* `nativeQuery = true` tells Spring Data JPA to treat it as a **native SQL query**.

## **3. Query with Multiple Parameters**

You can pass multiple parameters to the query.

### **Example: Find Employees by Department and Salary**

```java
@Repository
public interface EmployeeRepository extends JpaRepository<Employee, Long> {
  
    // JPQL Query with multiple parameters
    @Query("SELECT e FROM Employee e WHERE e.department = :dept AND e.salary > :sal")
    List<Employee> findEmployeesByDepartmentAndSalary(
        @Param("dept") String department,
        @Param("sal") double salary
    );
}

```

### Native SQL Version

```java
@Query(value = "SELECT * FROM employees WHERE department = :dept AND salary > :sal", nativeQuery = true)
List<Employee> findEmployeesByDepartmentAndSalaryNative(@Param("dept") String department, @Param("sal") double salary);

```

## **4. Using Indexed Parameters (Positional Parameters)**

Instead of named parameters (`:paramName`), you can use **positional parameters (`?1`, `?2`, etc.)**.

### **Example: Find Employee by Name (Using Positional Parameters)**

````java
@Query("SELECT e FROM Employee e WHERE e.name = ?1 AND e.salary > ?2")
List<Employee> findByNameAndSalary(String name, double salary);

```
````

* `?1` refers to the **first parameter** (`name`).
* `?2` refers to the **second parameter** (`salary`).

## **5. Modifying Queries (`@Modifying`)**

For **update and delete** operations, you must use `@Modifying`.

### **Example: Update Employee Salary**

```java
@Modifying
@Query("UPDATE Employee e SET e.salary = :sal WHERE e.id = :id")
@Transactional
int updateEmployeeSalary(@Param("id") Long id, @Param("sal") double salary);

```

### **Explanation:**

* `@Modifying` is required for **update or delete** operations.
* `@Transactional` ensures the query executes within a **transaction**.

### **Usage in Service Layer:**

```java
@Transactional
public void changeSalary(Long id, double newSalary) {
    employeeRepository.updateEmployeeSalary(id, newSalary);
}

```

## **6. Delete Query Example**

```java
@Modifying
@Query("DELETE FROM Employee e WHERE e.id = :id")
@Transactional
void deleteEmployeeById(@Param("id") Long id);

```

## **7. Pagination and Sorting with JPQL**

Spring Data JPA supports **pagination** with `Pageable`.

### **Example: Paginated Query**

```java
@Query("SELECT e FROM Employee e WHERE e.department = :dept")
Page<Employee> findByDepartment(@Param("dept") String department, Pageable pageable);

```

### Usage in Service Layer

```java
public Page<Employee> getEmployeesByDepartment(String department, int page, int size) {
    Pageable pageable = PageRequest.of(page, size, Sort.by("salary").descending());
    return employeeRepository.findByDepartment(department, pageable);
}

```

## **8. Dynamic Queries using `SpEL (Spring Expression Language)`**

Spring Data allows **dynamic sorting** using SpEL.

### **Example: Dynamic Sorting**

```java
@Query("SELECT e FROM Employee e WHERE e.department = :#{#dept}")
List<Employee> findByDynamicDepartment(@Param("dept") String department);

```
