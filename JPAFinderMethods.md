# Derived Query methods or Custom finder methods

**Spring Boot** using **Spring Data JPA**, the `JpaRepository` provides several default **finder methods** (also called **CRUD methods**) out of the box. These methods help in basic CRUD operations without needing to write explicit queries.


### **Default Finder Methods in `JpaRepository`**

When you extend `JpaRepository<T, ID>`, you automatically get the following methods:

#### **1. Basic CRUD Operations**


| Method                                      | Description                                           |
| ------------------------------------------- | ----------------------------------------------------- |
| `save(S entity)`                            | Saves the given entity (insert or update).            |
| `saveAll(Iterable<S> entities)`             | Saves multiple entities at once.                      |
| `findById(ID id)`                           | Retrieves an entity by its ID (returns`Optional<T>`). |
| `findAll()`                                 | Retrieves all entities.                               |
| `findAllById(Iterable<ID> ids)`             | Retrieves multiple entities by their IDs.             |
| `existsById(ID id)`                         | Checks if an entity exists by ID.                     |
| `count()`                                   | Returns the total count of entities.                  |
| `deleteById(ID id)`                         | Deletes an entity by ID.                              |
| `delete(T entity)`                          | Deletes a specific entity.                            |
| `deleteAllById(Iterable<ID> ids)`           | Deletes multiple entities by their IDs.               |
| `deleteAll(Iterable<? extends T> entities)` | Deletes multiple entities.                            |
| `deleteAll()`                               | Deletes all entities from the table.                  |


#### **2. Sorting & Pagination**


| Method                       | Description                                       |
| ---------------------------- | ------------------------------------------------- |
| `findAll(Sort sort)`         | Retrieves all entities sorted in the given order. |
| `findAll(Pageable pageable)` | Retrieves entities in a paginated way.            |

#### **3. Custom Finder Methods (Derived Query Methods)**

Spring Data JPA allows you to define custom finder methods based on **naming conventions**.


| Method Pattern                                           | Example                                      |
| -------------------------------------------------------- | -------------------------------------------- |
| `findByFieldName(Type fieldValue)`                       | `findByName(String name)`                    |
| `findByFieldNameAndOtherField(Type value1, Type value2)` | `findByNameAndAge(String name, int age)`     |
| `findByFieldNameOrOtherField(Type value1, Type value2)`  | `findByNameOrAge(String name, int age)`      |
| `findByFieldNameBetween(Type value1, Type value2)`       | `findByAgeBetween(int startAge, int endAge)` |
| `findByFieldNameLessThan(Type value)`                    | `findByAgeLessThan(int age)`                 |
| `findByFieldNameGreaterThan(Type value)`                 | `findByAgeGreaterThan(int age)`              |
| `findByFieldNameLike(String pattern)`                    | `findByNameLike(String pattern)`             |
| `findByFieldNameStartingWith(String prefix)`             | `findByNameStartingWith(String prefix)`      |
| `findByFieldNameEndingWith(String suffix)`               | `findByNameEndingWith(String suffix)`        |
| `findByFieldNameContaining(String text)`                 | `findByNameContaining(String text)`          |
| `findByFieldNameIn(Collection<Type> values)`             | `findByAgeIn(List<Integer> ages)`            |
| `findByFieldNameNot(Type value)`                         | `findByStatusNot(String status)`             |
| `findTopByFieldName(Type value)`                         | `findTopByAge(int age)`                      |
| `findFirstByFieldName(Type value)`                       | `findFirstByAge(int age)`                    |
| `findTop3ByFieldNameOrderByOtherFieldAsc(Type value)`    | `findTop3ByAgeOrderBySalaryAsc(int age)`     |

#### **4. Query Methods with Sorting & Pagination**


| Method Pattern                                    | Example                                      |
| ------------------------------------------------- | -------------------------------------------- |
| `findByFieldNameOrderByOtherFieldAsc(Type value)` | `findByNameOrderByAgeAsc(String name)`       |
| `findByFieldName(Pageable pageable)`              | `findByName(String name, Pageable pageable)` |
