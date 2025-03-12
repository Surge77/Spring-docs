# Comparison JPQL vs Native Query


## **Comparison: JPQL vs Native Query**


| Feature           | JPQL (`@Query`)                       | Native SQL (`@Query(nativeQuery = true)`)  |
| ----------------- | ------------------------------------- | ------------------------------------------ |
| Works on          | Entity Objects                        | Database Tables                            |
| Portability       | **Database-independent**              | **Database-specific**                      |
| Syntax            | **Similar to SQL, but uses entities** | **Pure SQL**                               |
| Named Queries     | ✅ Supported                          | ✅ Supported                               |
| Positional Params | ✅ Supported (`?1`,`?2`)              | ✅ Supported (`?1`,`?2`)                   |
| Modifying Queries | ✅ Supported (`@Modifying`)           | ✅ Supported (`@Modifying`)                |
| Best Use Case     | **General Queries**                   | **Complex, performance-optimized queries** |
