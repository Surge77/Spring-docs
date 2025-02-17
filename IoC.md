# Inversion of Control (IOC)


**IoC (Inversion of Control) means letting Spring Boot manage object creation instead of doing it manually.**

🚀 **Think of a restaurant:**

* **Before IoC:** You cook your own food (manual object creation).
* **With IoC:** You order food, and the kitchen (Spring) prepares it for you (automatic dependency injection).


1️⃣ **Before IoC (Manual Object Creation – Tight Coupling)**

* If `OrderService` depends on `PaymentService`, you manually create an instance.

```JAVA
class OrderService {

     private PaymentService paymentService = new PaymentService();

}
```

🚨 **Problems:**

* Tightly coupled (if `PaymentService` changes, `OrderService` must be updated).
* Hard to test and replace dependencies.


2️⃣ **With IoC (Spring Manages Object Creation – Loose Coupling)**

* Instead of creating objects manually, Spring injects them automatically

```JAVA
@Component
class PaymentService {}

@Component
class OrderService {
    private final PaymentService paymentService;

    @Autowired  // Spring automatically provides the dependency
    public OrderService(PaymentService paymentService) {
        this.paymentService = paymentService;
    }
}

```


✅ **Benefits of IoC:**

* **Loose coupling** → Classes don’t need to know how dependencies are created.
* **Scalability** → Easy to add more services without modifying existing ones.
* **Testability** → Can replace `PaymentService` with `MockPaymentService` for unit testing.
