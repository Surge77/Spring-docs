# Validation Annotations

Spring Boot provides **validation annotations** to enforce rules on data inputs in applications. These annotations come from **Jakarta Validation API (Javax Validation API)** and are used to ensure data integrity before processing.

1. **Fundamental Problem**:
   * Users might send incorrect or invalid data in HTTP requests.
   * Storing bad data can lead to system crashes, security risks, or incorrect results.
2. **Core Principles for a Solution**:
   * We need **automated validation** before data reaches the service layer.
   * Validation should be **easy to apply** and should not require extra boilerplate code.
   * Errors should be reported **clearly** to the user.
3. **Derived Solutions**:
   * Spring Boot leverages **Jakarta Validation API** with annotations to check data automatically.
   * These annotations work with **DTOs (Data Transfer Objects)** to ensure incoming data is valid.
