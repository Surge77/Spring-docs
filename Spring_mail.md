# Spring Boot Starter Mail

## **🔹 What is the Core Problem?**

📌 Problem Statement:How can a Java application send emails reliably without manually handling SMTP, authentication, and connection management?

### **Breaking It Down**

1️⃣ **What does it mean to send an email?**

* Email is a system for sending messages between computers using **SMTP (Simple Mail Transfer Protocol)**.
* It requires:
  * A **mail server** (e.g., Gmail, Yahoo, Outlook).
  * A **message** (subject, body, attachments).
  * Authentication (username/password or App Passwords).

2️⃣ **What is Spring Boot Starter Mail?**

* Instead of writing SMTP logic manually, **Spring Boot provides a pre-built library** called **Spring Boot Starter Mail** (`spring-boot-starter-mail`).
* It abstracts:
  * **SMTP Configuration**
  * **Email Formatting**
  * **Connection Handling**
  * **Error Management**

3️⃣ **Why Not Just Use JavaMail API Directly?**

* **JavaMail API** requires a lot of **boilerplate code**:
  * Manually configuring SMTP properties.
  * Handling transport sessions.
  * Setting up messages and authentication.
* **Spring Boot simplifies this** by offering a **pre-configured and easy-to-use** solution.


1️⃣ **Install Spring Boot Mail Dependency**

```java
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-mail</artifactId>
</dependency>

```

* This pulls in the **JavaMail API** and Spring’s mail integration.

2️⃣ **Configure SMTP Server in `application.properties`**

* The application needs an **SMTP server** to send emails.

```
spring.mail.host=smtp.gmail.com                  # This is the Gmail SMTP server's address.
spring.mail.port=587                             # Port 587 is used for sending emails securely via STARTTLS.
spring.mail.username=your-email@gmail.com        # Your Gmail address is used for authentication.
spring.mail.password=your-email-password        # Your Gmail password (or App Password if 2FA is enabled).
spring.mail.protocol=smtp                        # The protocol for communication is SMTP.
spring.mail.smtp.auth=true                       # Enable authentication using the username and password.
spring.mail.smtp.starttls.enable=true            # Use STARTTLS to upgrade the connection to a secure one.

```

These properties tell Spring Boot **how to connect to the mail server**.

3️⃣ **Send an Email Using `JavaMailSender`**

* **Spring Boot internally creates a `JavaMailSender` bean** that simplifies sending emails:

```java
@Service
public class EmailService {
    @Autowired
    private JavaMailSender mailSender;

    public void sendEmail(String to, String subject, String text) {
        SimpleMailMessage message = new SimpleMailMessage();
        message.setTo(to);
        message.setSubject(subject);
        message.setText(text);
        message.setFrom("your-email@gmail.com");

        mailSender.send(message);
    }
}

```


* **Internally, this does the following:**
  1. Creates an **SMTP session** with Gmail/Yahoo/Outlook.
  2. **Authenticates** using `spring.mail.username` and `spring.mail.password`.
  3. **Sends the email** to the recipient.
  4. Closes the SMTP session to free resources.

4️⃣ **What Happens If There’s an Error?**

* Spring **handles errors** internally, like:

  * Wrong SMTP credentials → `AuthenticationFailedException`
  * Server issues → `MailSendException`
* You can add a **try-catch block** to handle failures:

  ```java

  try {
      mailSender.send(message);
  } catch (MailException e) {
      System.out.println("Failed to send email: " + e.getMessage());
  }

  ```
