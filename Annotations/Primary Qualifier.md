# `@Primary` vs `@Qualifier` in Spring Boot

When there are **multiple beans of the same type**, Spring **doesn’t know which one to use**.
That's where `@Primary` and `@Qualifier` come in—they **resolve conflicts** by deciding which bean to inject.

Spring Boot **automatically injects beans**, but what if there are **multiple beans of the same type**?

```java
@Component
class Dog implements Animal {
    public String speak() { return "Woof!"; }
}

@Component
class Cat implements Animal {
    public String speak() { return "Meow!"; }
}

@Component
class PetService {
    private final Animal animal;

    @Autowired
    public PetService(Animal animal) {
        this.animal = animal;
    }

    public String getSound() {
        return animal.speak();
    }
}
```

💥 **Spring will throw an error** because it doesn’t know whether to inject **Dog** or **Cat** into `PetService`.

## Use `@Qualifier` (Explicit Choice)

If we **don’t** want to use `@Primary`, we can use `@Qualifier` to **specify exactly which bean** we want.

```java
@Component
class Dog implements Animal {
    public String speak() { return "Woof!"; }
}

@Component
class Cat implements Animal {
    public String speak() { return "Meow!"; }
}

@Component
class PetService {
    private final Animal animal;

    @Autowired
    public PetService(@Qualifier("cat") Animal animal) { // 👈 Choose "cat"
        this.animal = animal;
    }

    public String getSound() {
        return animal.speak();
    }
}
```

## Use `@Primary` (Default Bean)

* `@Primary` tells Spring **which bean to use by default** when there’s no `@Qualifier`.
* If multiple beans exist, **Spring picks the `@Primary` one** automatically.

```java
@Component
@Primary  // This will be the default bean
class Dog implements Animal {
    public String speak() { return "Woof!"; }
}

@Component
class Cat implements Animal {
    public String speak() { return "Meow!"; }
}
```

### ✅ Use `@Primary` when:

* One bean should be the **default** choice.
* You **don’t want to manually specify** which bean to inject every time.

### ✅ Use `@Qualifier` when:

* You **need fine-grained control** over which bean is injected.
* There are **multiple beans**, and `@Primary` isn’t suitable.
* You **want different beans for different scenarios**.
