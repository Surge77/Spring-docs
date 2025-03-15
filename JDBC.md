# JDBC => Java Database Connectivity


## 🔄 **7 Step process**


| **Core Problem**                                       | **JDBC Step (FPT Solution)**                            |
| ------------------------------------------------------ | ------------------------------------------------------- |
| Java doesn't know how to interact with databases       | **Import JDBC packages**to provide necessary classes.   |
| Java doesn’t know which driver to use                 | **Register the JDBC driver**to establish compatibility. |
| No communication channel exists by default             | **Establish a connection**using database credentials.   |
| SQL queries need to be defined and executed            | **Create a statement**to specify and send queries.      |
| Queries must be executed to interact with the database | **Execute the query**to retrieve or modify data.        |
| Data must be processed for application use             | **Process the result**by iterating over the`ResultSet`. |
| Open resources can lead to memory leaks                | **Close the connection**to free up system resources.    |
