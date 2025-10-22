## ✅ Top 100 Spring Boot Interview Questions

---

### 🔹 1–20: Spring Boot Basics

## 1. What is Spring Boot and why is it used?

### ✅ What is Spring Boot?

**Spring Boot** is an **open-source Java-based framework** used to create **standalone, production-grade Spring-based applications** with minimal configuration.

It is built on top of the **Spring Framework** and was developed by **Pivotal Team** (now part of VMware).

---

### ✅ Why is Spring Boot used?

Spring Boot is designed to **simplify the setup, development, and deployment** of Spring applications. Here's **why** it's used:

| Feature                     | Why it Matters                                                                                                |
| --------------------------- | ------------------------------------------------------------------------------------------------------------- |
| **Auto Configuration**      | Automatically configures Spring and third-party libraries based on the dependencies present in the classpath. |
| **Standalone Applications** | Runs as a Java application without needing an external web server (like Tomcat or Jetty).                     |
| **Embedded Servers**        | Comes with embedded servers (Tomcat, Jetty, Undertow), so no need to deploy WAR files to a separate server.   |
| **Production Ready**        | Comes with features like health checks, metrics, and externalized configuration for easy monitoring.          |
| **Starter Dependencies**    | Provides "starter" packages to avoid manual dependency configuration.                                         |
| **Spring Boot CLI**         | Allows running and testing Spring Boot apps using command line with Groovy or Java.                           |
| **Minimal Configuration**   | Reduces the amount of boilerplate code and configuration required.                                            |

---

### ✅ Example: Hello World Spring Boot Application

Here’s a simple **Spring Boot REST API** example:

#### Step 1: Add dependencies via Maven (in `pom.xml`)

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
</dependencies>
```

#### Step 2: Create the Main Application class

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class HelloWorldApplication {
    public static void main(String[] args) {
        SpringApplication.run(HelloWorldApplication.class, args);
    }
}
```

#### Step 3: Create a REST Controller

```java
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloController {

    @GetMapping("/hello")
    public String sayHello() {
        return "Hello, Spring Boot!";
    }
}
```

#### Step 4: Run the App

* Just run the main method in `HelloWorldApplication`.
* Then go to: `http://localhost:8080/hello`
* Output: `Hello, Spring Boot!`

---

### ✅ Summary

| Point                    | Details                                                                                                         |
| ------------------------ | --------------------------------------------------------------------------------------------------------------- |
| **What is Spring Boot?** | A tool built on Spring to simplify development of production-ready apps.                                        |
| **Why use it?**          | Saves time, reduces boilerplate, auto-configures setup, supports embedded servers, and offers a rich ecosystem. |
| **Use Case**             | Creating microservices, REST APIs, enterprise-level applications, and more.                                     |

---

## 2. What are the main features of Spring Boot?

Here’s a detailed breakdown of the **main features of Spring Boot**, along with **explanations** and **real-world relevance**—essential for interview preparation.

---

## ✅ Main Features of Spring Boot

| Feature                                       | Description                                                                                       | Example/Use Case                                                                                         |
| --------------------------------------------- | ------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| **1. Auto-Configuration**                     | Spring Boot automatically configures your application based on the dependencies in the classpath. | If you include `spring-boot-starter-web`, it auto-configures Tomcat, Jackson, etc., to create a web app. |
| **2. Starter Dependencies**                   | Provides a set of convenient dependency descriptors to reduce dependency management.              | Using `spring-boot-starter-data-jpa` automatically includes JPA + Hibernate dependencies.                |
| **3. Embedded Web Servers**                   | Comes with embedded servers like Tomcat, Jetty, or Undertow, so no need to deploy WAR files.      | You can run your web application by simply executing the `main()` method.                                |
| **4. Production-Ready Features (Actuator)**   | Includes features like health checks, metrics, environment info, and monitoring.                  | Add `spring-boot-starter-actuator` to expose endpoints like `/actuator/health`.                          |
| **5. Externalized Configuration**             | Allows configuration via `application.properties` or `application.yml` for flexibility.           | Easily change port by adding `server.port=9090` in the properties file.                                  |
| **6. Command-Line Interface (CLI)**           | Optional tool to develop and test Spring Boot apps using Groovy or Java via terminal.             | Run `spring run app.groovy` to start your app from the command line.                                     |
| **7. Spring Boot DevTools**                   | Offers features like auto-restart, live reload, and enhanced logging for development.             | Great for boosting productivity during development.                                                      |
| **8. Easy Integration with Spring Ecosystem** | Seamlessly works with Spring modules like Spring Data, Spring Security, Spring MVC.               | Create a secure login system quickly with Spring Boot + Spring Security.                                 |
| **9. Minimal Spring Configuration**           | Reduces boilerplate code by removing the need for XML and complex configuration files.            | You don’t need to define `DispatcherServlet` or bean declarations manually.                              |
| **10. Microservices Friendly**                | Ideal for building and deploying microservices with minimal effort.                               | Easily register services with Eureka, use Spring Cloud Gateway, etc.                                     |

---

## ✅ Example of Feature in Action: Auto-Configuration

If you add the `spring-boot-starter-web` dependency:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

You **do NOT need** to:

* Configure DispatcherServlet
* Set up Jackson for JSON handling
* Define server port (default is 8080)

Spring Boot automatically does this for you.

---

## ✅ Summary Table for Quick Interview Revision

| Feature                    | Keyword                     |
| -------------------------- | --------------------------- |
| Auto-Configuration         | `@SpringBootApplication`    |
| Starter Dependencies       | Predefined starter packs    |
| Embedded Servers           | Tomcat, Jetty, Undertow     |
| Actuator                   | Health checks & metrics     |
| Externalized Configuration | `application.properties`    |
| Spring Boot CLI            | Groovy scripts              |
| DevTools                   | Auto-reload during dev      |
| Spring Integration         | Spring Security, Data, etc. |
| No XML                     | Annotations & Java config   |
| Microservices Support      | Spring Cloud ecosystem      |

---

## 3. What is the difference between Spring and Spring Boot?

### ✅ Difference Between Spring and Spring Boot

Both **Spring Framework** and **Spring Boot** are parts of the same **Spring ecosystem**, but they serve different purposes and have some important differences in terms of configuration, setup, and deployment. Let's break down the key distinctions:

---

| **Aspect**                | **Spring Framework**                                                                                                          | **Spring Boot**                                                                                  |
| ------------------------- | ----------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------ |
| **Purpose**               | A comprehensive framework for building Java applications.                                                                     | A framework to simplify the setup and development of Spring applications.                        |
| **Configuration**         | Requires extensive configuration, either through XML files or Java classes.                                                   | **Minimal configuration**; uses sensible defaults and auto-configuration.                        |
| **Boilerplate Code**      | High, requires writing a lot of code and XML for configuration.                                                               | Low, minimal setup and eliminates a lot of boilerplate code.                                     |
| **Dependency Management** | You need to manage individual dependencies manually.                                                                          | Uses "starter" dependencies (e.g., `spring-boot-starter-web`) to simplify dependency management. |
| **Deployment**            | Typically requires deploying to an external application server (e.g., Tomcat).                                                | Comes with **embedded servers** (like Tomcat, Jetty, etc.), so no need for external servers.     |
| **Ease of Use**           | More complex; developers need to configure multiple parts of the app.                                                         | Very easy to use, even for beginners. It’s designed to be **developer-friendly**.                |
| **XML Configuration**     | Spring uses **XML configuration** or Java-based configuration (via annotations) for setting up beans and application context. | **No XML configuration**—uses annotations like `@SpringBootApplication` and properties files.    |
| **Startup Time**          | Slower startup because of heavy configuration and multiple components.                                                        | Faster startup time due to fewer configurations and built-in server support.                     |
| **Use Case**              | Used for traditional Java-based enterprise applications where flexibility in configurations is required.                      | Ideal for microservices, REST APIs, and quick development of production-ready apps.              |
| **Learning Curve**        | Steeper learning curve due to the need to understand different components and configurations.                                 | Easier learning curve because it’s focused on simplicity and convention over configuration.      |

---

### ✅ Key Points in Detail:

#### **1. Configuration:**

* **Spring Framework** requires **manual configuration** of various components like beans, the application context, and data sources. Developers often need to configure beans in XML or Java files.

  Example:

  ```xml
  <bean id="myBean" class="com.example.MyBean"/>
  ```

* **Spring Boot** uses **auto-configuration** and **sensible defaults**, which significantly reduces the need for manual setup.

  Example:

  ```java
  @SpringBootApplication
  public class Application {
      public static void main(String[] args) {
          SpringApplication.run(Application.class, args);
      }
  }
  ```

#### **2. Dependency Management:**

* **Spring** requires you to add individual dependencies for each module you want to use, such as Spring Web, Spring Data, Spring Security, etc.

* **Spring Boot** simplifies this by providing **"starter" dependencies** that include all the necessary dependencies for a given functionality.

  Example:

    * For a web application, you would use:

      ```xml
      <dependency>
          <groupId>org.springframework.boot</groupId>
          <artifactId>spring-boot-starter-web</artifactId>
      </dependency>
      ```

#### **3. Embedded Server:**

* **Spring** needs to be deployed to an external server (like Tomcat, Jetty, or WildFly) for running a web application.

* **Spring Boot** comes with an **embedded server**, meaning you can run the application from the command line or within an IDE, without deploying it elsewhere.

#### **4. Deployment:**

* **Spring** applications typically require packaging as WAR files and deploying them to a server.

* **Spring Boot** applications can be packaged as executable JAR or WAR files, and you can run them directly from the command line.

#### **5. Microservices:**

* **Spring** is often used for monolithic applications, though it can also support microservices (via Spring Cloud, for example).

* **Spring Boot** is especially designed for building **microservices** and REST APIs with a minimal amount of configuration.

#### **6. Start Time:**

* **Spring** takes longer to start up, especially for larger applications, due to the extensive configuration and initialization.

* **Spring Boot** has **faster startup times** because it minimizes the configuration and uses embedded servers, allowing for quick testing and deployment.

---

### ✅ Example Scenarios:

#### 1. **Traditional Spring Framework:**

You might use **Spring Framework** for a large enterprise-level application where you need more control over configuration and deployment. For example, a **banking application** requiring a highly customized configuration.

#### 2. **Spring Boot:**

If you are building a **microservice** or **REST API**, Spring Boot would be a more suitable choice due to its simplicity, quick setup, and built-in server support. For example, creating a **user management service** as part of a larger microservice architecture.

---

### ✅ Summary Table for Quick Revision:

| **Feature**               | **Spring Framework**                                         | **Spring Boot**                                   |
| ------------------------- | ------------------------------------------------------------ | ------------------------------------------------- |
| **Configuration**         | Manual (XML/Java-based)                                      | Auto-configuration with sensible defaults         |
| **Boilerplate Code**      | High (XML files, verbose configuration)                      | Low (Minimal code, convention over configuration) |
| **Embedded Server**       | No (Requires external servers)                               | Yes (Embedded Tomcat, Jetty, etc.)                |
| **Deployment**            | WAR files, external servers                                  | Standalone JAR/WAR with embedded server           |
| **Microservices Support** | Supports microservices but requires additional configuration | Designed for microservices (via Spring Cloud)     |
| **Learning Curve**        | Steep, complex configuration                                 | Easier, more straightforward to learn             |

---

## 4. What is starter dependency in Spring Boot?

### ✅ What is a Starter Dependency in Spring Boot?

A **starter dependency** in Spring Boot is a **set of convenient dependency descriptors** provided by Spring Boot that you can include in your project to get all the required libraries for a specific functionality — **without having to declare each dependency manually**.

Think of it as a **pre-packaged collection of libraries** that make setup faster and easier.

---

### ✅ Why Use Starter Dependencies?

* **Reduces boilerplate** — no need to add multiple dependencies for common functionality.
* **Ensures compatibility** — all versions of included libraries are tested to work well together.
* **Simplifies configuration** — most starters come with Spring Boot’s auto-configuration features.

---

### ✅ Structure of a Starter Dependency

Spring Boot starter dependencies follow this naming convention:

```
spring-boot-starter-<feature>
```

For example:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

This starter includes:

* Spring MVC
* Embedded Tomcat server
* Jackson (for JSON)
* Logging (SLF4J, Logback)

---

### ✅ Commonly Used Starter Dependencies

| Starter                         | Description                                                                                   |
| ------------------------------- | --------------------------------------------------------------------------------------------- |
| `spring-boot-starter`           | Core starter that includes auto-configuration, logging, and YAML support.                     |
| `spring-boot-starter-web`       | Builds web applications using Spring MVC and RESTful services. Includes Tomcat, Jackson, etc. |
| `spring-boot-starter-data-jpa`  | Enables Spring Data JPA with Hibernate and database integration.                              |
| `spring-boot-starter-security`  | Adds Spring Security for authentication and authorization.                                    |
| `spring-boot-starter-test`      | Includes testing libraries like JUnit, Mockito, Hamcrest, etc.                                |
| `spring-boot-starter-thymeleaf` | Adds Thymeleaf templating engine support.                                                     |
| `spring-boot-starter-actuator`  | Adds production-ready features like health checks, metrics, etc.                              |
| `spring-boot-starter-mail`      | For sending emails using JavaMailSender.                                                      |

---

### ✅ Real-World Example

Suppose you're building a REST API. Without starters, you'd have to manually add:

* Spring Web
* Tomcat
* Jackson
* SLF4J and Logback

Instead, you just use:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

Spring Boot takes care of adding everything you need to get started.

---

### ✅ Behind the Scenes

Each starter is **just a POM file** with a list of dependencies. For example, the `spring-boot-starter-web` internally pulls in:

```xml
<dependencies>
    <dependency>spring-web</dependency>
    <dependency>spring-webmvc</dependency>
    <dependency>jackson-databind</dependency>
    <dependency>spring-boot-starter-tomcat</dependency>
    <dependency>spring-boot-starter-logging</dependency>
</dependencies>
```

---

### ✅ Summary

| Concept         | Description                                                                                     |
| --------------- | ----------------------------------------------------------------------------------------------- |
| **What is it?** | A curated set of dependencies for a specific use case.                                          |
| **Why use it?** | Simplifies project setup, saves time, avoids version conflicts.                                 |
| **Examples**    | `spring-boot-starter-web`, `spring-boot-starter-data-jpa`, `spring-boot-starter-security`, etc. |
| **Benefit**     | Faster development, cleaner POM files, fewer manual configuration headaches.                    |

---

## 5. What is the role of `@SpringBootApplication`?

### ✅ What is the Role of `@SpringBootApplication` in Spring Boot?

The `@SpringBootApplication` annotation is a **convenient, composite annotation** in Spring Boot that enables several key features for a Spring Boot application to run properly. It is **usually placed on the main class** of the application.

---

### ✅ In Simple Terms

`@SpringBootApplication` tells Spring Boot:

> “This is the main entry point for your application, start here and auto-configure everything.”

---

### ✅ Internally, `@SpringBootApplication` is a combination of 3 annotations:

```java
@SpringBootApplication
= @Configuration
+ @EnableAutoConfiguration
+ @ComponentScan
```

Let’s break each one down:

---

### 🔹 1. `@Configuration`

* Marks the class as a **source of bean definitions** for the Spring application context.
* Allows you to define beans using `@Bean` methods.
* It's like telling Spring: "This class contains configuration details."

---

### 🔹 2. `@EnableAutoConfiguration`

* **Enables Spring Boot’s auto-configuration mechanism**.
* Automatically configures Spring beans based on the classpath dependencies.
* Example: If you have `spring-boot-starter-web` in your project, it auto-configures:

    * DispatcherServlet
    * Tomcat
    * Jackson for JSON
    * Error handling, etc.

---

### 🔹 3. `@ComponentScan`

* Tells Spring to **scan the current package and all sub-packages** for Spring-managed components (like `@Component`, `@Service`, `@Repository`, `@Controller`).
* This is how Spring Boot finds your custom beans and controllers automatically.

---

### ✅ Example

```java
package com.example.demo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication  // 👈 This is the key annotation
public class DemoApplication {
    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }
}
```

* Spring Boot will automatically:

    * Scan `com.example.demo` and sub-packages
    * Configure beans
    * Set up an embedded server
    * Start the application

---

### ✅ Without `@SpringBootApplication`

If you don’t use `@SpringBootApplication`, you would have to declare the three annotations separately:

```java
@Configuration
@EnableAutoConfiguration
@ComponentScan
public class MyAppConfig {
    // your config
}
```

Using `@SpringBootApplication` just makes your code **cleaner and shorter**.

---

### ✅ Summary Table

| Feature            | Handled by                 | Purpose                                      |
| ------------------ | -------------------------- | -------------------------------------------- |
| Configuration      | `@Configuration`           | Declares bean methods                        |
| Auto Configuration | `@EnableAutoConfiguration` | Automatically sets up Spring Boot components |
| Component Scanning | `@ComponentScan`           | Scans packages for beans/components          |

---

### ✅ Bonus: Customizing `@ComponentScan`

By default, `@ComponentScan` scans from the package where the main class is located. To scan a different package:

```java
@SpringBootApplication(scanBasePackages = "com.mycompany.custom")
```

---

## 6. What happens in the background when you run a Spring Boot application?

One of the **commonly asked in Spring Boot interviews**! Here's a **detailed breakdown** of what happens **under the hood** when you run a Spring Boot application (i.e., when you run `SpringApplication.run()` in the `main()` method).

---

## ✅ What Happens in the Background When You Run a Spring Boot App?

When you run a Spring Boot application using:

```java
SpringApplication.run(MyApplication.class, args);
```

Spring Boot goes through several **important phases** to bootstrap and launch the application.

---

### 🧠 Step-by-Step Breakdown

---

### 🔹 1. **Class with `@SpringBootApplication` is Located**

* The class annotated with `@SpringBootApplication` is located.
* This composite annotation:

    * Marks it as a configuration class
    * Enables auto-configuration
    * Enables component scanning

---

### 🔹 2. **Creates a `SpringApplication` Instance**

* Internally, `SpringApplication.run()` creates a `SpringApplication` object.
* Sets up:

    * Application context
    * Environment (properties, system variables)
    * Listeners and initializers

---

### 🔹 3. **Runs `SpringApplication.run()`**

This triggers multiple background tasks:

#### a. **Banner Display (Optional)**

* Displays the default Spring Boot banner in the console.
* You can customize or disable it.

#### b. **Environment Preparation**

* Gathers and processes configuration from:

    * `application.properties` or `application.yml`
    * System environment variables
    * Command-line arguments
* Creates a `ConfigurableEnvironment` object.

#### c. **ApplicationContext Creation**

* Creates an appropriate `ApplicationContext`:

    * `AnnotationConfigServletWebServerApplicationContext` for web apps
    * `AnnotationConfigApplicationContext` for non-web apps

#### d. **Bean Definition Loading**

* Uses `@ComponentScan` to find and register beans in the package and sub-packages.
* Includes:

    * `@Controller`
    * `@Service`
    * `@Repository`
    * `@Component`
    * Beans declared using `@Bean`

#### e. **Auto-Configuration**

* Based on the classpath, Spring Boot uses `@EnableAutoConfiguration` to:

    * Detect which libraries are available
    * Automatically configure related beans (e.g., DataSource, Tomcat, Jackson)
* All configuration classes are listed in `spring.factories`.

#### f. **Embedded Server Startup**

* Starts an embedded server like:

    * Tomcat (default)
    * Jetty or Undertow (if configured)
* Registers DispatcherServlet if it's a web application.

#### g. **Application Runners Execution**

* Executes any `CommandLineRunner` or `ApplicationRunner` beans.
* Used for running custom code at startup.

#### h. **Ready to Accept Requests**

* Logs: `Started Application in X seconds`
* Application is now running and ready to handle HTTP requests if it’s a web app.

---

### ✅ Summary Flow Diagram

```
@SpringBootApplication
        ↓
SpringApplication.run()
        ↓
Create SpringApplication instance
        ↓
Initialize environment & properties
        ↓
Create ApplicationContext
        ↓
Scan and register beans
        ↓
Apply auto-configuration
        ↓
Start embedded server (Tomcat)
        ↓
Run CommandLineRunner / ApplicationRunner
        ↓
Application is ready to serve!
```

---

### ✅ Real-World Analogy

Think of `SpringApplication.run()` as pressing the **start button on a car**:

* It checks the fuel (environment config)
* Starts the engine (ApplicationContext)
* Loads necessary systems (auto-configuration)
* And finally, it lets you **drive the car** (handle web requests or run business logic)

---

### ✅ Bonus Tips (for Interviews)

* You can customize the startup process by adding:

    * `ApplicationListeners`
    * `ApplicationContextInitializers`
    * Override default beans

---

## 7. What is Spring Initializr?

### ✅ What is Spring Initializr?

**Spring Initializr** is a **web-based tool provided by the Spring team** that helps developers **quickly generate the basic structure of a Spring Boot project** with all necessary dependencies, configurations, and build files.

It eliminates the need to manually set up your project structure, classpath, and dependencies, making it **super fast to get started with Spring Boot**.

---

### 🌐 Official URL:

👉 [https://start.spring.io](https://start.spring.io)

---

### ✅ Why Use Spring Initializr?

| Feature                        | Benefit                                                                                                |
| ------------------------------ | ------------------------------------------------------------------------------------------------------ |
| 🎯 **Quick Project Setup**     | Saves time by generating all files you need to get started.                                            |
| 🧱 **Customizable**            | Choose your dependencies, build tool (Maven/Gradle), Java version, packaging type (Jar/War), and more. |
| 🔌 **Dependency Management**   | Automatically includes correct starter dependencies and their compatible versions.                     |
| ⚙️ **IDE Integration**         | Supported by IntelliJ IDEA, Eclipse, VS Code, and Spring Tool Suite (STS).                             |
| 🧪 **No Configuration Errors** | Prevents version mismatches and missing dependencies.                                                  |

---

### ✅ How It Works (Step-by-Step)

1. **Open Spring Initializr** → [start.spring.io](https://start.spring.io)

2. **Fill out basic details**:

    * **Project**: Maven / Gradle
    * **Language**: Java / Kotlin / Groovy
    * **Spring Boot version**: Choose latest stable
    * **Project Metadata**: Group, Artifact, Name, Description
    * **Packaging**: JAR / WAR
    * **Java version**: (e.g. 17 or 21)

3. **Choose Dependencies**:

    * Examples:

        * `Spring Web` – for REST APIs
        * `Spring Data JPA` – for database access
        * `Spring Security` – for auth
        * `H2 Database` – for in-memory DB

4. **Click "Generate"**:

    * Downloads a `.zip` file with the complete project.

5. **Import into IDE**:

    * Open in IntelliJ, Eclipse, or VS Code.
    * Run the app with the main class (annotated with `@SpringBootApplication`).

---

### ✅ Example Output from Spring Initializr

Here's what gets generated:

```
my-project/
├── pom.xml                 → Maven build file with dependencies
├── src/
│   └── main/
│       ├── java/
│       │   └── com/example/demo/
│       │       └── DemoApplication.java   → Main class with @SpringBootApplication
│       └── resources/
│           ├── application.properties     → Config file
│           └── static/, templates/        → For web content (optional)
└── test/
    └── java/...                          → Unit test class
```

---

### ✅ When Should You Use It?

* ✅ Starting a **new Spring Boot project**
* ✅ Learning or prototyping quickly
* ✅ Teaching Spring Boot to beginners
* ✅ Avoiding manual dependency setup

---

### ✅ Bonus: CLI Usage

If you prefer command line tools:

```bash
curl https://start.spring.io/starter.zip \
  -d dependencies=web,data-jpa \
  -d type=maven-project \
  -d language=java \
  -d name=demo \
  -o demo.zip
```

---

### ✅ Summary

| Feature  | Description                                                       |
| -------- | ----------------------------------------------------------------- |
| What     | Tool to create a Spring Boot project                              |
| URL      | [start.spring.io](https://start.spring.io)                        |
| Purpose  | Generate a ready-to-use Spring Boot skeleton                      |
| Benefits | Fast, error-free, IDE-friendly, customizable                      |
| Output   | Pre-configured Maven/Gradle project with all files & dependencies |

---

## 8. What are the default configurations in Spring Boot?

### ✅ What Are the Default Configurations in Spring Boot?

Spring Boot provides a powerful **auto-configuration mechanism** that **automatically configures your application** based on the dependencies present on the classpath and default settings. This greatly reduces the amount of manual setup required.

In other words:

> **Spring Boot chooses sensible defaults** for most configurations so developers can get started quickly.

---

### 🔧 Where Do Defaults Come From?

Spring Boot loads default configurations from:

* **`spring-boot-autoconfigure` module**
* **`META-INF/spring.factories`** (or `META-INF/spring/org.springframework.boot.autoconfigure.AutoConfiguration.imports` in newer versions)
* Internal `application.properties` files
* Dependency-specific auto-configuration classes

---

### ✅ Common Areas of Default Configuration

Here’s a list of what Spring Boot configures **by default** when the relevant dependency is added:

---

### 1. 🖥️ **Embedded Server Configuration (Web Apps)**

If `spring-boot-starter-web` is on the classpath:

* Embedded **Tomcat** is used (by default).
* Default port: `8080`
* Context path: `/`
* Static resources served from `/static`, `/public`, `/resources`, or `/META-INF/resources`

---

### 2. 📦 **Spring MVC Defaults**

* Registers a `DispatcherServlet`
* Maps `/` to the controller
* Jackson is used for JSON serialization/deserialization
* Error pages mapped to `/error`

---

### 3. 🛢️ **Database Configuration**

If JPA & database drivers are on the classpath:

* Uses **H2** in-memory database by default
* Automatically configures `DataSource`, `EntityManagerFactory`, and `TransactionManager`
* Creates schema automatically if `spring.jpa.hibernate.ddl-auto` is set (e.g., `create`, `update`)

---

### 4. 🧪 **Testing Configuration**

If `spring-boot-starter-test` is present:

* Includes JUnit 5, Mockito, Hamcrest
* Mocks certain beans and disables web server for unit tests by default

---

### 5. 🔒 **Security Defaults (if `spring-boot-starter-security` is added)**

* Adds a basic login page
* Protects all endpoints
* Creates a default in-memory user:

    * Username: `user`
    * Password: **Randomly generated and shown in the logs**

---

### 6. 📄 **Logging Configuration**

* Uses **Logback** by default
* Logs to the console
* Log level: `INFO`
* Log pattern can be customized via properties

---

### 7. 📁 **Static Resource Handling**

* Serves static files from:

    * `/static`
    * `/public`
    * `/resources`
    * `/META-INF/resources`
* Example: A file placed in `src/main/resources/static/index.html` will be available at `http://localhost:8080/index.html`

---

### 8. 🗂️ **Application Properties / YAML**

* Automatically reads from:

    * `application.properties`
    * `application.yml`
* Located in `src/main/resources`
* Externalized config overrides defaults

---

### 9. 🧠 **Actuator Endpoints**

If `spring-boot-starter-actuator` is added:

* Enables several endpoints like:

    * `/actuator/health`
    * `/actuator/info`
    * `/actuator/metrics`
* Secured by default

---

### ✅ Example of Default Behavior (No Configuration)

Just this code:

```java
@SpringBootApplication
public class DemoApp {
    public static void main(String[] args) {
        SpringApplication.run(DemoApp.class, args);
    }
}
```

With dependency:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

✅ Will:

* Start Tomcat on port `8080`
* Set up Spring MVC with Jackson
* Serve static files
* Load a blank `/error` page
* Auto-configure JSON converters and error handling

---

### ✅ Summary Table

| Area          | Default Behavior                         |
| ------------- | ---------------------------------------- |
| Web Server    | Embedded Tomcat on port 8080             |
| JSON Handling | Jackson                                  |
| Logging       | Logback, level INFO                      |
| Security      | Basic login with generated password      |
| Database      | H2 in-memory (if no other DB is defined) |
| Properties    | Loaded from `application.properties`     |
| Static Files  | Served from `/static`, `/public`, etc.   |

---

### ✅ Tip for Interviews

> You can override any default by providing values in `application.properties`, defining your own `@Bean`, or excluding auto-configuration using `@SpringBootApplication(exclude = …)`.

---

## 9. What is auto-configuration in Spring Boot?

### ✅ What is Auto-Configuration in Spring Boot?

**Auto-configuration** in Spring Boot is a powerful feature that **automatically configures your application based on the libraries (dependencies) available on the classpath** and predefined configuration logic.

---

### 🧠 Simple Definition

> Auto-configuration tries to **guess and configure** the beans you’ll need — **so you don’t have to write a lot of boilerplate code**.

This is what allows Spring Boot to work with “zero” or minimal configuration.

---

### ✅ Example to Understand

Let’s say you add this dependency:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

Spring Boot will:

* Detect you’re building a **web application**
* Automatically configure:

    * An **embedded Tomcat server**
    * A **`DispatcherServlet`**
    * Jackson (for JSON)
    * Logging, error handling, etc.

All **without you writing a single line of configuration**.

---

### ✅ How Does Auto-Configuration Work Internally?

1. **Triggered by `@EnableAutoConfiguration`**

    * This annotation is included in `@SpringBootApplication`
    * It activates Spring Boot's auto-configuration mechanism

2. **Loads Configuration from `spring.factories` or `AutoConfiguration.imports`**

    * Located in `spring-boot-autoconfigure.jar`
    * Lists all `@Configuration` classes eligible for auto-configuration

3. **Conditionally Applies Configurations**

    * Spring Boot uses **`@Conditional*` annotations** to decide **which configuration should be applied** based on:

        * Classpath presence (e.g., `@ConditionalOnClass`)
        * Missing or existing beans (e.g., `@ConditionalOnMissingBean`)
        * Property values (e.g., `@ConditionalOnProperty`)

   Example:

   ```java
   @Configuration
   @ConditionalOnClass(DataSource.class)
   public class DataSourceAutoConfiguration {
       // auto-configures a DataSource bean if present on classpath
   }
   ```

---

### ✅ Real-World Use Case

You add:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```

Spring Boot will:

* Auto-configure a **DataSource**
* Detect and configure **JPA EntityManagerFactory**
* Set up a default **Hibernate JPA Vendor Adapter**
* Run **schema.sql** or **data.sql** if present

And all of this without needing any XML or `@Bean` definitions.

---

### ✅ Benefits of Auto-Configuration

| Benefit              | Description                                                         |
| -------------------- | ------------------------------------------------------------------- |
| ✅ Faster development | No need for manual setup                                            |
| ✅ Less boilerplate   | You don’t write configuration unless you need to override something |
| ✅ Sensible defaults  | Comes preconfigured with good baseline behavior                     |
| ✅ Easy customization | Easily overridden using `application.properties` or `@Bean`         |

---

### ✅ How to Disable or Customize Auto-Configuration

1. **Disable specific auto-config classes**:

```java
@SpringBootApplication(exclude = {DataSourceAutoConfiguration.class})
```

2. **Override default beans**:
   Just define your own `@Bean`, and Spring Boot will skip its auto-configured version.

3. **Control with properties**:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.jpa.show-sql=true
```

---

### ✅ Summary

| Feature       | Description                                               |
| ------------- | --------------------------------------------------------- |
| What          | Automatically configures beans based on the classpath     |
| Triggered By  | `@EnableAutoConfiguration` (via `@SpringBootApplication`) |
| Based On      | Classpath, existing beans, properties                     |
| Customizable? | Yes (via properties or custom beans)                      |
| Benefit       | Zero configuration startup, faster development            |

---

## 10. How does Spring Boot handle dependency management?

Here's a detailed explanation of **how Spring Boot handles dependency management**, which is key for ensuring your project has the right versions of libraries without conflicts or manual hassle.

---

## ✅ How Does Spring Boot Handle Dependency Management?

---

### 1. **What is Dependency Management?**

Dependency management means controlling **which versions of libraries (dependencies) your project uses**, so:

* You avoid version conflicts (called "JAR hell")
* All dependencies work well together
* You don’t have to manually specify versions for every library

---

### 2. **Spring Boot’s Approach: Dependency Management via "Starters" and BOM**

---

#### 🔹 **Spring Boot Starters**

* Spring Boot provides **starter dependencies** (e.g., `spring-boot-starter-web`, `spring-boot-starter-data-jpa`) that bundle commonly used libraries together.
* Each starter specifies **compatible versions** of all required dependencies.
* You only add starters to your `pom.xml` or `build.gradle` without worrying about individual versions.

Example (Maven):

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

* This starter automatically pulls in compatible versions of Spring MVC, Jackson, Tomcat, and others.

---

#### 🔹 **BOM (Bill of Materials) Usage**

* Spring Boot uses a **BOM** to centrally manage versions of dependencies.
* A BOM is a special POM file that defines **a list of dependencies and their versions** that are tested to work well together.
* Spring Boot's BOM is imported automatically when you use Spring Boot starter parent.

Example:

If you use the Spring Boot Starter Parent in Maven:

```xml
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>3.0.5</version>
</parent>
```

* This parent POM **imports the Spring Boot BOM**, managing the versions of all Spring Boot dependencies and related libraries.

---

### 3. **How This Works in Practice**

* You **do NOT specify versions** for Spring Boot starters or their dependencies.
* The Spring Boot parent or BOM **provides all versions**.
* If you add a new starter, it automatically brings in the right versions.
* If you want to override a version, you can explicitly declare it in your `pom.xml` or `build.gradle`.

---

### 4. **Example of Dependency Management in Maven**

```xml
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>3.0.5</version>
    <relativePath/> <!-- lookup parent from repository -->
</parent>

<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
        <!-- No version needed! -->
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>
</dependencies>
```

Here:

* The parent handles dependency versions.
* You just add dependencies without versions.
* You get compatible versions guaranteed by Spring Boot.

---

### 5. **Advantages of Spring Boot Dependency Management**

| Advantage                    | Explanation                                                         |
| ---------------------------- | ------------------------------------------------------------------- |
| ✅ Simplifies configuration   | No need to manually manage versions                                 |
| ✅ Avoids version conflicts   | BOM tested to ensure compatible dependency versions                 |
| ✅ Consistent across projects | Same dependency versions used for multiple projects                 |
| ✅ Easy upgrades              | Upgrade Spring Boot version, and dependencies upgrade automatically |
| ✅ Flexibility                | You can still override versions when needed                         |

---

### 6. **How It Works in Gradle**

If using Gradle, you add:

```gradle
plugins {
    id 'org.springframework.boot' version '3.0.5'
    id 'io.spring.dependency-management' version '1.1.0'
}

dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-web'
    implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
}
```

The `io.spring.dependency-management` plugin ensures the BOM is applied and versions managed automatically.

---

### ✅ Summary

| Concept             | Spring Boot Approach                             |
| ------------------- | ------------------------------------------------ |
| Version management  | Managed by Spring Boot Parent or BOM             |
| Dependency versions | Predefined and tested versions in BOM            |
| Starters            | Bundled dependencies without version declaration |
| Override            | Explicitly declare versions to override defaults |

---

## 11. What is the use of `application.properties` or `application.yml`?

Here’s a detailed explanation of the purpose and usage of `application.properties` and `application.yml` files in Spring Boot.

---

## ✅ What is `application.properties` / `application.yml`?

These files are **configuration files** used by Spring Boot to **externalize configuration** from your code. Instead of hardcoding values (like database URLs, ports, API keys, etc.) inside your Java classes, you put them in these files. This makes your app more flexible, maintainable, and easier to manage in different environments (dev, test, prod).

---

## 🔑 Purpose of `application.properties` or `application.yml`

| Purpose                         | Description                                      |
| ------------------------------- | ------------------------------------------------ |
| **Centralized configuration**   | All important settings in one place              |
| **Environment-specific config** | Easily switch configs for different environments |
| **Override default behavior**   | Customize Spring Boot defaults                   |
| **Read at runtime**             | Spring Boot loads these on app startup           |

---

## ✅ Why two formats?

* **`application.properties`**: Traditional key-value pair format
  Example:

  ```properties
  server.port=8081
  spring.datasource.url=jdbc:mysql://localhost:3306/mydb
  spring.jpa.show-sql=true
  ```

* **`application.yml`**: YAML format, more hierarchical and readable for complex configurations
  Example:

  ```yaml
  server:
    port: 8081

  spring:
    datasource:
      url: jdbc:mysql://localhost:3306/mydb
    jpa:
      show-sql: true
  ```

You can use either one according to your preference — Spring Boot supports both, but **only one active at a time per environment**.

---

## ✅ Common Use Cases for `application.properties` or `application.yml`

* Configure server port:

  ```properties
  server.port=9090
  ```
* Database connection:

  ```properties
  spring.datasource.url=jdbc:mysql://localhost:3306/mydb
  spring.datasource.username=root
  spring.datasource.password=secret
  ```
* Enable debug logs:

  ```properties
  logging.level.org.springframework=DEBUG
  ```
* Customize error pages, CORS, security settings, cache, and more.

---

## ✅ How Does Spring Boot Use These Files?

1. **Loads on startup** — automatically read by Spring Boot from `src/main/resources`.
2. **Injects values** into Spring beans using `@Value` or `@ConfigurationProperties`.
3. Supports **profiles**: e.g., `application-dev.properties` for dev, `application-prod.yml` for production — automatically loaded based on active profile.

---

## ✅ Example: Using Properties in Code

```java
@Component
@ConfigurationProperties(prefix = "app")
public class AppConfig {
    private String name;
    private int timeout;

    // getters and setters
}
```

With `application.properties`:

```properties
app.name=MyApp
app.timeout=5000
```

Spring Boot will inject these values into the `AppConfig` bean.

---

## ✅ Summary

| File                     | Purpose                               | Format          | Use Case                     |
| ------------------------ | ------------------------------------- | --------------- | ---------------------------- |
| `application.properties` | Store app settings as key-value pairs | Properties file | Simple configs, traditional  |
| `application.yml`        | Store hierarchical app configs        | YAML file       | Complex configs, readability |

Both files make your app flexible by separating configuration from code, supporting multiple environments, and enabling easy customization.

---

## 12. What is a profile in Spring Boot?

Here’s a detailed explanation about **profiles in Spring Boot** and why they’re useful.

---

## ✅ What is a Profile in Spring Boot?

A **profile** in Spring Boot is a way to **group configuration settings** and beans so that they can be selectively enabled or disabled based on the environment or situation where your application runs.

Think of profiles as **environments** or **modes** for your app—such as **development**, **testing**, **production**—each having different configurations and behaviors.

---

## 🔑 Why Use Profiles?

* You often need **different configurations** for:

    * Local development (e.g., H2 in-memory database)
    * Testing (e.g., test database, logging settings)
    * Production (e.g., real database, security settings)

* Profiles help **manage these differences cleanly** without changing the codebase.

---

## ✅ How Profiles Work in Spring Boot

* You define **profile-specific properties files** like:

    * `application-dev.properties` or `application-dev.yml`
    * `application-prod.properties` or `application-prod.yml`

* When you activate a profile, Spring Boot loads both:

    * `application.properties` (common config)
    * The profile-specific file (overrides or adds config)

---

## ✅ Activating Profiles

### 1. **Via command line:**

```bash
java -jar myapp.jar --spring.profiles.active=dev
```

### 2. **In `application.properties`:**

```properties
spring.profiles.active=dev
```

### 3. **Programmatically in Java code:**

```java
SpringApplication app = new SpringApplication(MyApplication.class);
app.setAdditionalProfiles("dev");
app.run(args);
```

---

## ✅ Example of Profile-specific Properties

* `application.properties` (common):

```properties
spring.datasource.url=jdbc:h2:mem:testdb
logging.level.org.springframework=INFO
```

* `application-dev.properties`:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/devdb
logging.level.org.springframework=DEBUG
```

* `application-prod.properties`:

```properties
spring.datasource.url=jdbc:mysql://prod-db-server:3306/proddb
logging.level.org.springframework=ERROR
```

---

## ✅ Profile-specific Beans

You can also use `@Profile` annotation to **conditionally create beans** depending on the active profile:

```java
@Configuration
@Profile("dev")
public class DevConfig {
    @Bean
    public DataSource dataSource() {
        // Dev database config
    }
}

@Configuration
@Profile("prod")
public class ProdConfig {
    @Bean
    public DataSource dataSource() {
        // Prod database config
    }
}
```

---

## ✅ Summary Table

| Feature    | Description                                       |
| ---------- | ------------------------------------------------- |
| What       | Environment-specific configuration grouping       |
| Usage      | Separate properties and beans per environment     |
| Activation | Via command line, properties, or programmatically |
| Benefits   | Clean config management, environment flexibility  |

---

## 13. How do you create custom properties in Spring Boot?

Creating custom properties in Spring Boot is a common need to make your application configurable and flexible.

---

## ✅ How to Create Custom Properties in Spring Boot

You can define your own properties in `application.properties` or `application.yml` and then inject those values into your Spring beans.

---

### Step-by-Step Guide

---

### 1. **Define Custom Properties in `application.properties` or `application.yml`**

For example, in `application.properties`:

```properties
app.title=My Awesome App
app.description=This is a demo app for interview prep
app.version=1.0.0
```

Or in `application.yml`:

```yaml
app:
  title: My Awesome App
  description: This is a demo app for interview prep
  version: 1.0.0
```

---

### 2. **Create a POJO to Bind These Properties**

Create a class with fields matching the property names, using the **`@ConfigurationProperties`** annotation.

```java
import org.springframework.boot.context.properties.ConfigurationProperties;
import org.springframework.stereotype.Component;

@Component
@ConfigurationProperties(prefix = "app")
public class AppProperties {

    private String title;
    private String description;
    private String version;

    // Getters and Setters

    public String getTitle() {
        return title;
    }
    public void setTitle(String title) {
        this.title = title;
    }

    public String getDescription() {
        return description;
    }
    public void setDescription(String description) {
        this.description = description;
    }

    public String getVersion() {
        return version;
    }
    public void setVersion(String version) {
        this.version = version;
    }
}
```

---

### 3. **Enable Configuration Properties Scanning**

In your main application class, add:

```java
import org.springframework.boot.context.properties.EnableConfigurationProperties;

@SpringBootApplication
@EnableConfigurationProperties(AppProperties.class)
public class DemoApplication {
    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }
}
```

*(Note: In Spring Boot 2.2+, if your properties class is annotated with `@Component`, `@EnableConfigurationProperties` is optional.)*

---

### 4. **Use the Properties in Your Code**

Inject the `AppProperties` bean where needed:

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class InfoController {

    private final AppProperties appProperties;

    @Autowired
    public InfoController(AppProperties appProperties) {
        this.appProperties = appProperties;
    }

    @GetMapping("/info")
    public String getAppInfo() {
        return String.format("%s - %s (version %s)", 
            appProperties.getTitle(), 
            appProperties.getDescription(), 
            appProperties.getVersion());
    }
}
```

---

### Alternative: Inject Individual Property with `@Value`

You can also inject single property values directly:

```java
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;

@Component
public class SomeComponent {

    @Value("${app.title}")
    private String appTitle;

    // use appTitle in your logic
}
```

---

## ✅ Summary

| Step                      | What to Do                                                          |
| ------------------------- | ------------------------------------------------------------------- |
| 1. Define properties      | Add to `application.properties` or `application.yml`                |
| 2. Create POJO            | Use `@ConfigurationProperties` with prefix                          |
| 3. Enable config scanning | `@EnableConfigurationProperties` or annotate POJO with `@Component` |
| 4. Inject and use         | Inject the POJO or use `@Value` for individual properties           |

---

## 14. How do you override default properties?

Overriding default properties in Spring Boot is a common task when you want to customize the behavior of your app beyond the built-in defaults.

---

## ✅ How to Override Default Properties in Spring Boot

Spring Boot provides **default values** for many configuration properties, but you can easily override them in several ways.

---

### 1. **Override in `application.properties` or `application.yml`**

The simplest way is to add your desired property with a new value.

Example: Change the server port from default `8080` to `9090`

```properties
server.port=9090
```

Or in YAML:

```yaml
server:
  port: 9090
```

---

### 2. **Use Profile-Specific Property Files**

Override defaults only for a specific profile by defining them in:

* `application-dev.properties`
* `application-prod.yml`

Spring Boot will merge these with `application.properties` based on active profile.

---

### 3. **Override Properties via Command Line Arguments**

When running your jar, you can pass properties:

```bash
java -jar myapp.jar --server.port=9090
```

This has higher priority than properties files.

---

### 4. **Override Properties via Environment Variables**

Spring Boot reads environment variables, where dots are replaced by underscores and uppercased.

Example:

```bash
export SERVER_PORT=9090
```

---

### 5. **Override Programmatically in Code**

You can set default properties in code before running the app:

```java
SpringApplication app = new SpringApplication(MyApplication.class);
Map<String, Object> defaultProps = new HashMap<>();
defaultProps.put("server.port", "9090");
app.setDefaultProperties(defaultProps);
app.run(args);
```

---

### 6. **Override Specific Bean Configurations**

Sometimes, you override defaults by defining your own `@Bean`, which Spring Boot will use instead of its auto-configured bean.

---

## ✅ Priority Order of Property Sources in Spring Boot

Spring Boot loads properties from many places with the following **precedence order** (higher overrides lower):

1. **Command line arguments**
2. **Java System properties (`-D` options)**
3. **Environment variables**
4. **`application-{profile}.properties` or `.yml`**
5. **`application.properties` or `.yml`**
6. **Default properties (hardcoded in Spring Boot)**

---

## ✅ Summary Table

| Method                           | Description         | Priority |
| -------------------------------- | ------------------- | -------- |
| Command line arguments           | Run-time overrides  | Highest  |
| Java system properties           | `-Dproperty=value`  | High     |
| Environment variables            | OS environment vars | High     |
| Profile-specific properties file | Config per profile  | Medium   |
| Default properties file          | Common app config   | Low      |
| Spring Boot default values       | Built-in defaults   | Lowest   |

---

## 15. What is the difference between `@Component`, `@Service`, and `@Repository`?

These three annotations are part of Spring’s **stereotype annotations**, and while they all mark a class as a Spring-managed component (bean), they have different **semantics and typical usage** in the application layers.

---

## ✅ Overview: `@Component`, `@Service`, and `@Repository`

| Annotation    | Purpose/Layer            | Special Behavior                                                                                                                    |
| ------------- | ------------------------ | ----------------------------------------------------------------------------------------------------------------------------------- |
| `@Component`  | Generic stereotype       | Marks a class as a Spring-managed bean. General purpose, no special semantics.                                                      |
| `@Service`    | Service layer (business) | Indicates the class holds business logic. Primarily for clarity and better readability. No functional difference from `@Component`. |
| `@Repository` | Persistence layer (DAO)  | Marks a Data Access Object. Adds **exception translation** (converts DB exceptions into Spring's `DataAccessException`).            |

---

## 🔍 Detailed Explanation

### 1. `@Component`

* **Generic Spring bean stereotype**.
* Use when your class doesn’t clearly fit into service or repository.
* Spring scans and registers such classes as beans.

Example:

```java
@Component
public class UtilityHelper {
   // helper methods
}
```

### 2. `@Service`

* Specialization of `@Component`.
* Intended for **business service layer** classes.
* Improves readability and organization by clarifying the role of the class.
* No additional behavior beyond `@Component`.

Example:

```java
@Service
public class UserService {
    public void registerUser(User user) {
        // business logic
    }
}
```

### 3. `@Repository`

* Specialization of `@Component`.
* Used in the **DAO/persistence layer**.
* Adds **automatic exception translation**:

    * Converts low-level persistence exceptions (like `SQLException`) into Spring’s consistent `DataAccessException` hierarchy.
* Helps with database error handling uniformly.

Example:

```java
@Repository
public class UserRepository {
    // Database access methods
}
```

---

## 🔄 Summary Table

| Feature                | @Component      | @Service               | @Repository           |
| ---------------------- | --------------- | ---------------------- | --------------------- |
| Layer                  | Generic         | Service/business logic | Persistence/DAO       |
| Semantic clarity       | No              | Yes                    | Yes                   |
| Exception translation  | No              | No                     | Yes (DB exceptions)   |
| Scanned as Spring bean | Yes             | Yes                    | Yes                   |
| Usage example          | Utility classes | Business services      | Database repositories |

---

## ✅ When to use what?

* Use **`@Component`** for generic or utility classes.
* Use **`@Service`** to mark service classes where business logic lives.
* Use **`@Repository`** for data access or persistence layer classes.

This improves code organization, readability, and can help with framework features like exception translation.

---

## 16. How is component scanning done in Spring Boot?

**Component scanning** is a fundamental mechanism in Spring Boot that helps automatically detect and register beans (components) in the application context, so you don’t have to manually declare every bean.

---

## ✅ What is Component Scanning?

Component scanning is the process where Spring **searches the classpath for classes annotated with stereotype annotations** like:

* `@Component`
* `@Service`
* `@Repository`
* `@Controller`
* `@RestController`
* Custom annotations annotated with `@Component`

and automatically registers those classes as Spring beans.

---

## ✅ How Does Component Scanning Work in Spring Boot?

### 1. **Default Behavior**

* When you create a Spring Boot application and annotate your main class with `@SpringBootApplication`, it implicitly enables component scanning.
* The scanning **starts from the package of the main class** and scans all sub-packages recursively.
* This means **all classes with stereotypes inside the main package and its children** are picked up automatically.

Example:

```java
@SpringBootApplication
public class MyApplication {
    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }
}
```

If your main class is in `com.example.demo`, Spring Boot scans:

* `com.example.demo`
* `com.example.demo.service`
* `com.example.demo.controller`
* `com.example.demo.repository`
* etc.

---

### 2. **How `@SpringBootApplication` enables component scanning**

`@SpringBootApplication` is a composed annotation that includes:

* `@SpringBootConfiguration`
* `@EnableAutoConfiguration`
* **`@ComponentScan`**

So, it automatically applies `@ComponentScan` on the package where your main class resides.

---

### 3. **Customizing Component Scanning**

If you want to scan other packages (outside of the main package), you can customize it by specifying base packages in `@ComponentScan`:

```java
@SpringBootApplication
@ComponentScan(basePackages = {"com.example.service", "com.example.components"})
public class MyApplication {
    // ...
}
```

This tells Spring Boot to scan those packages as well.

---

### 4. **Excluding Specific Classes**

You can exclude certain components during scanning with:

```java
@ComponentScan(
    basePackages = "com.example",
    excludeFilters = @ComponentScan.Filter(type = FilterType.ANNOTATION, classes = Deprecated.class)
)
```

---

### 5. **Under the Hood**

* Spring uses `ClassPathScanningCandidateComponentProvider` to scan classpath resources.
* It looks for classes with annotations or matching filters.
* Registered classes become Spring beans in the ApplicationContext.

---

## ✅ Summary Table

| Feature                    | Details                                                      |
| -------------------------- | ------------------------------------------------------------ |
| Default scan scope         | Package of main class + sub-packages                         |
| Enabled by                 | `@SpringBootApplication` (via `@ComponentScan`)              |
| Typical target annotations | `@Component`, `@Service`, `@Repository`, `@Controller`, etc. |
| Custom scan packages       | Use `@ComponentScan(basePackages = {...})`                   |
| Exclude filters            | Use `excludeFilters` attribute of `@ComponentScan`           |

---

## 17. What are the different ways to create a Spring Boot application?

There are several ways to create a Spring Boot application, each suited for different preferences and situations. Here's a detailed overview:

---

## ✅ Different Ways to Create a Spring Boot Application

### 1. **Using Spring Initializr (Recommended for Beginners and Quick Start)**

* **What:** An online web tool or IDE-integrated tool to generate a ready-to-run Spring Boot project skeleton.
* **How:**

    * Visit [https://start.spring.io](https://start.spring.io)
    * Select project metadata (Group, Artifact, dependencies, Java version, etc.)
    * Generate and download a ZIP file with the project setup.
* **Also Available in IDEs:** IntelliJ IDEA, Eclipse, VS Code have Spring Initializr integration to create projects without leaving the IDE.

---

### 2. **Using IDE Support**

* **IntelliJ IDEA / Eclipse / Spring Tools Suite (STS):**

    * New Project → Spring Initializr integration or Spring Boot starter project wizard.
    * Select dependencies and generate the project directly.
* **Advantage:** IDE manages dependencies, setup, and runs your app.

---

### 3. **Manually Creating a Project**

* Create a Maven or Gradle project.
* Add Spring Boot dependencies manually to `pom.xml` or `build.gradle`.
* Create main application class with `@SpringBootApplication`.
* This way requires knowledge of dependencies and setup but offers more control.

Example (Maven `pom.xml` snippet):

```xml
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>3.0.0</version>
</parent>

<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
</dependencies>
```

---

### 4. **Using Command Line Interface (CLI)**

* Spring Boot CLI lets you create and run Spring Boot apps from the command line.
* Install CLI, then:

```bash
spring init --dependencies=web myapp
cd myapp
./mvnw spring-boot:run
```

* CLI generates a project with selected dependencies.
* Good for rapid prototyping or scripting.

---

### 5. **Using Build Tools Directly**

* Use Maven or Gradle commands with Spring Boot plugins to create and run apps.
* Example:

```bash
mvn archetype:generate -DgroupId=com.example -DartifactId=myapp ...
```

But this is less common than Spring Initializr or IDE support.

---

## ✅ Summary Table

| Method                | Description                                 | Best For                           |
| --------------------- | ------------------------------------------- | ---------------------------------- |
| Spring Initializr     | Web/IDE tool to generate projects           | Beginners, quick start             |
| IDE Project Wizards   | Integrated project creation inside IDE      | Developers using IntelliJ, Eclipse |
| Manual Setup          | Manually configure Maven/Gradle and classes | Custom or learning setup           |
| Spring Boot CLI       | Command line tool to create and run apps    | Rapid prototyping, scripting       |
| Build Tool Archetypes | Use Maven/Gradle archetypes                 | Advanced/legacy use cases          |

---

## 18. What is Spring Boot CLI?

Here’s a detailed explanation of **Spring Boot CLI** and how it can be useful.

---

## ✅ What is Spring Boot CLI?

**Spring Boot CLI (Command Line Interface)** is a command-line tool that allows you to quickly **create, run, and test Spring Boot applications** from the terminal or command prompt without needing to set up a full IDE project first.

It’s designed to speed up development, especially for **prototyping, learning, or quick testing**.

---

## ✅ Key Features of Spring Boot CLI

* **Rapid application development:** Write Spring Boot apps using Groovy or Java with minimal boilerplate.
* **Run apps instantly:** Run your application directly from the command line without building a JAR.
* **Dependency management:** Add dependencies easily with the `spring init` command or `@Grab` annotations in Groovy.
* **Supports Groovy:** Allows writing Spring apps in Groovy, making development faster and more concise.
* **Project initialization:** Quickly generate new Spring Boot projects with dependencies.

---

## ✅ How to Install Spring Boot CLI

* Download from the official Spring website or use SDKMAN! or package managers.
* Example (using SDKMAN! on Linux/macOS):

```bash
sdk install springboot
```

* Verify installation:

```bash
spring --version
```

---

## ✅ Basic Commands

### 1. **Initialize a new project**

```bash
spring init --dependencies=web,data-jpa myapp
cd myapp
```

This creates a new project with web and JPA dependencies.

### 2. **Run a Spring Boot application**

If you have a `.groovy` file with a Spring Boot app:

```bash
spring run app.groovy
```

Or in a project directory:

```bash
./mvnw spring-boot:run
```

### 3. **Compile and package**

```bash
spring jar myapp.jar *.groovy
```

---

## ✅ Example of a Simple Spring Boot App in Groovy Using CLI

Create `app.groovy`:

```groovy
@RestController
class HelloController {
    @RequestMapping("/")
    String home() {
        "Hello from Spring Boot CLI!"
    }
}
```

Run it:

```bash
spring run app.groovy
```

Then open `http://localhost:8080` in your browser to see the result.

---

## ✅ Why Use Spring Boot CLI?

| Benefit                    | Description                                      |
| -------------------------- | ------------------------------------------------ |
| Fast prototyping           | Write and run apps quickly                       |
| Minimal setup              | No need for full IDE project or build config     |
| Groovy support             | Use Groovy for concise code                      |
| Easy dependency management | Add dependencies via CLI commands or annotations |

---

## 19. What is the main class in a Spring Boot application?

The **main class** in a Spring Boot application is the **entry point** where the application starts running. It typically contains the `main()` method, which bootstraps the Spring context and launches the embedded server.

---

## ✅ What is the Main Class in Spring Boot?

* It’s a Java class annotated with `@SpringBootApplication`.
* It contains a `public static void main(String[] args)` method.
* This `main` method calls `SpringApplication.run()` to start the application.

---

## ✅ Role of the Main Class

* **Bootstrap the Spring application context**: Initialize all beans and configurations.
* **Start the embedded web server** (like Tomcat or Jetty) if it's a web application.
* **Trigger auto-configuration and component scanning** via `@SpringBootApplication`.

---

## ✅ Typical Structure of the Main Class

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class MyApplication {

    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }

}
```

---

## ✅ Explanation:

* `@SpringBootApplication` is a composite annotation combining:

    * `@Configuration` – marks this class as a source of bean definitions.
    * `@EnableAutoConfiguration` – tells Spring Boot to automatically configure beans based on classpath and settings.
    * `@ComponentScan` – scans the package (and sub-packages) for Spring components.

* `SpringApplication.run()` bootstraps the entire Spring context and starts the embedded server.

---

## ✅ Why is this Important?

* This class **acts as the launcher** for your Spring Boot app.
* Without it, the Spring context and auto-configuration won’t start.
* You usually keep this class in the root package to ensure component scanning works well.

---

## 20. Can you run a Spring Boot app without a web server?

Absolutely! You **can run a Spring Boot application without a web server** — this is common for non-web applications like batch jobs, command-line tools, or background services.

---

## ✅ Running Spring Boot Without a Web Server

### 1. **What Does This Mean?**

* Normally, Spring Boot starts an embedded web server like Tomcat or Jetty when you use `spring-boot-starter-web`.
* If you don’t want a web server, you just **don’t include web dependencies** or explicitly **disable the web server**.

---

### 2. **How to Disable the Embedded Web Server**

#### Option A: Exclude the Web Starter

* Don’t add `spring-boot-starter-web` or any web dependencies in your `pom.xml` or `build.gradle`.
* For example, use `spring-boot-starter` (core) or `spring-boot-starter-batch` for batch apps.

#### Option B: Set Application Type to `NONE`

In your main application, configure Spring Boot to not start a web server:

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.boot.WebApplicationType;

@SpringBootApplication
public class MyApp {

    public static void main(String[] args) {
        SpringApplication app = new SpringApplication(MyApp.class);
        app.setWebApplicationType(WebApplicationType.NONE);  // Disable web server
        app.run(args);
    }
}
```

---

### 3. **Use Cases for Non-Web Spring Boot Apps**

* **Batch processing** (e.g., using Spring Batch).
* **Command-line applications**.
* **Background services** or daemons.
* **Event-driven applications** (message queue consumers, etc.).

---

### 4. **Example: Simple Non-Web Spring Boot App**

```java
@SpringBootApplication
public class BatchApp implements CommandLineRunner {

    public static void main(String[] args) {
        SpringApplication app = new SpringApplication(BatchApp.class);
        app.setWebApplicationType(WebApplicationType.NONE);
        app.run(args);
    }

    @Override
    public void run(String... args) throws Exception {
        System.out.println("Running batch task...");
        // your logic here
    }
}
```

---

## ✅ Summary

| How to run without web server                  | Description                             |
| ---------------------------------------------- | --------------------------------------- |
| Exclude `spring-boot-starter-web`              | No web dependencies, no embedded server |
| Set `WebApplicationType.NONE` programmatically | Explicitly disable web environment      |
| Use `CommandLineRunner` or `ApplicationRunner` | For code execution after app startup    |

---

### 🔹 21–40: REST APIs & Web Layer

## 21. How do you create a RESTful service in Spring Boot?

Creating a RESTful service is one of the most common use cases for Spring Boot. Here's a step-by-step explanation with an example.

---

## ✅ How to Create a RESTful Service in Spring Boot

### Step 1: Setup Spring Boot Project

* Use **Spring Initializr** or your preferred way to create a Spring Boot project.
* Add **`spring-boot-starter-web`** dependency to enable web and REST support.

---

### Step 2: Create a Controller Class

* Use the `@RestController` annotation to mark the class as a REST controller.
* Use `@RequestMapping` or HTTP method-specific annotations (`@GetMapping`, `@PostMapping`, etc.) to map URLs.

---

### Step 3: Define REST Endpoints

* Each endpoint corresponds to a method in your controller.
* The method returns data (usually as JSON).
* Spring Boot auto-configures message converters (like Jackson) to serialize objects to JSON.

---

## ✅ Example: Simple RESTful Service

```java
import org.springframework.web.bind.annotation.*;

import java.util.*;

@RestController
@RequestMapping("/api/users")
public class UserController {

    private Map<Integer, String> users = new HashMap<>();

    // Constructor to add some sample users
    public UserController() {
        users.put(1, "Alice");
        users.put(2, "Bob");
    }

    // GET /api/users - get all users
    @GetMapping
    public Map<Integer, String> getAllUsers() {
        return users;
    }

    // GET /api/users/{id} - get user by ID
    @GetMapping("/{id}")
    public String getUserById(@PathVariable int id) {
        return users.getOrDefault(id, "User not found");
    }

    // POST /api/users - add a new user
    @PostMapping
    public String addUser(@RequestParam int id, @RequestParam String name) {
        users.put(id, name);
        return "User added successfully";
    }

    // DELETE /api/users/{id} - delete a user
    @DeleteMapping("/{id}")
    public String deleteUser(@PathVariable int id) {
        users.remove(id);
        return "User deleted successfully";
    }
}
```

---

### Explanation:

* `@RestController` = `@Controller + @ResponseBody` (response is serialized as JSON).
* `@RequestMapping("/api/users")` maps all methods under this URL path.
* `@GetMapping`, `@PostMapping`, `@DeleteMapping` map HTTP GET, POST, DELETE respectively.
* `@PathVariable` extracts data from the URL.
* `@RequestParam` extracts data from query parameters or form data.

---

### Step 4: Run Your Spring Boot App

* Run the main class with `SpringApplication.run()`.
* Test REST endpoints using Postman, curl, or browser:

```bash
curl http://localhost:8080/api/users
curl http://localhost:8080/api/users/1
curl -X POST "http://localhost:8080/api/users?id=3&name=Charlie"
curl -X DELETE http://localhost:8080/api/users/3
```

---

## ✅ Summary:

| Annotation        | Purpose                                  |
| ----------------- | ---------------------------------------- |
| `@RestController` | Defines RESTful controller, returns JSON |
| `@RequestMapping` | Maps HTTP paths                          |
| `@GetMapping`     | Maps GET requests                        |
| `@PostMapping`    | Maps POST requests                       |
| `@DeleteMapping`  | Maps DELETE requests                     |
| `@PathVariable`   | Bind URI path variables                  |
| `@RequestParam`   | Bind query/form parameters               |

---

## 22. What is the use of `@RestController`?

Here’s a detailed explanation of `@RestController` in Spring Boot.

---

## ✅ What is `@RestController`?

`@RestController` is a **specialized annotation** in Spring MVC used to create RESTful web services. It’s a combination of two annotations:

* `@Controller` — marks the class as a Spring MVC controller.
* `@ResponseBody` — tells Spring to serialize the returned object directly into the HTTP response body (usually JSON or XML) instead of rendering a view.

---

## ✅ Why Use `@RestController`?

* Simplifies creation of RESTful APIs.
* Eliminates the need to annotate every method with `@ResponseBody`.
* Makes your controller methods return data (like JSON) directly, suitable for client-side apps, mobile apps, or other services.

---

## ✅ How it Works

Without `@RestController`, you’d typically write:

```java
@Controller
public class MyController {

    @RequestMapping("/hello")
    @ResponseBody
    public String sayHello() {
        return "Hello, World!";
    }
}
```

With `@RestController`, it becomes:

```java
@RestController
public class MyController {

    @RequestMapping("/hello")
    public String sayHello() {
        return "Hello, World!";
    }
}
```

---

## ✅ Example

```java
@RestController
@RequestMapping("/api")
public class UserController {

    @GetMapping("/users")
    public List<String> getUsers() {
        return List.of("Alice", "Bob", "Charlie");
    }
}
```

* The list of users is returned as JSON.
* No view resolution happens.
* Clients get the raw JSON data.

---

## ✅ Summary Table

| Annotation        | Description                                                  |
| ----------------- | ------------------------------------------------------------ |
| `@Controller`     | Defines a web controller (returns views)                     |
| `@ResponseBody`   | Serializes return value to HTTP response                     |
| `@RestController` | Combination of `@Controller` + `@ResponseBody` for REST APIs |

---

## 23. What is the difference between `@Controller` and `@RestController`?

Understanding the difference between `@Controller` and `@RestController` is key when building web applications with Spring Boot.

---

## ✅ Difference Between `@Controller` and `@RestController`

| Aspect                 | `@Controller`                                                                                                              | `@RestController`                                                                                          |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| Purpose                | Used to mark a class as a Spring MVC controller that returns **views** (like JSP, Thymeleaf templates).                    | Used for RESTful web services where the controller returns **data directly** (usually JSON or XML).        |
| Response Body Handling | Does **not** include `@ResponseBody` by default. You need to add `@ResponseBody` to methods to send data as response body. | Combines `@Controller` and `@ResponseBody`, so data is automatically serialized and sent as HTTP response. |
| Typical Use Case       | Web applications serving HTML pages.                                                                                       | REST APIs serving JSON/XML to clients.                                                                     |
| View Resolution        | Returns the name of a view to render.                                                                                      | Returns the data object, not a view name.                                                                  |
| Example Method Output  | Returns `"index"` which corresponds to a view template named `index.html` or `index.jsp`.                                  | Returns an object like `User` or `List<User>`, which Spring converts to JSON.                              |

---

## ✅ Example Comparison

### Using `@Controller`:

```java
@Controller
public class WebController {

    @GetMapping("/hello")
    public String helloPage(Model model) {
        model.addAttribute("message", "Hello, World!");
        return "hello";  // Return view name "hello.html" or "hello.jsp"
    }

    @GetMapping("/api/data")
    @ResponseBody
    public String data() {
        return "This is raw data";
    }
}
```

### Using `@RestController`:

```java
@RestController
public class ApiController {

    @GetMapping("/api/hello")
    public String hello() {
        return "Hello, World!";  // Returned as raw response body (JSON/plain text)
    }
}
```

---

## ✅ Summary:

| Feature                  | @Controller                     | @RestController                  |
| ------------------------ | ------------------------------- | -------------------------------- |
| Default response         | View name (template)            | Data serialized to HTTP response |
| Need for `@ResponseBody` | Yes, on methods returning data  | No, implicit on all methods      |
| Suitable for             | Web MVC applications with views | RESTful APIs                     |

---

## 24. What are `@RequestMapping`, `@GetMapping`, `@PostMapping` etc.?

These annotations are essential for defining how your Spring Boot controller methods handle HTTP requests.

---

## ✅ What are `@RequestMapping`, `@GetMapping`, `@PostMapping`, etc.?

They are **Spring MVC annotations** used to map HTTP requests to handler methods in controller classes.

---

### 1. **`@RequestMapping`**

* The **most general and versatile** annotation for mapping HTTP requests.
* Can map any HTTP method (`GET`, `POST`, `PUT`, `DELETE`, etc.) by specifying `method` attribute.
* Can map URL paths, parameters, headers, and more.

**Example:**

```java
@RequestMapping(value = "/users", method = RequestMethod.GET)
public List<User> getUsers() {
    return userService.getAllUsers();
}
```

---

### 2. **HTTP Method Specific Annotations**

Spring provides convenient **specialized annotations** that act as shortcuts for `@RequestMapping` with a specific HTTP method:

| Annotation       | HTTP Method | Equivalent to                                    |
| ---------------- | ----------- | ------------------------------------------------ |
| `@GetMapping`    | GET         | `@RequestMapping(method = RequestMethod.GET)`    |
| `@PostMapping`   | POST        | `@RequestMapping(method = RequestMethod.POST)`   |
| `@PutMapping`    | PUT         | `@RequestMapping(method = RequestMethod.PUT)`    |
| `@DeleteMapping` | DELETE      | `@RequestMapping(method = RequestMethod.DELETE)` |
| `@PatchMapping`  | PATCH       | `@RequestMapping(method = RequestMethod.PATCH)`  |

---

### 3. **Examples**

```java
@RestController
@RequestMapping("/api/users")
public class UserController {

    // Handles GET requests to /api/users
    @GetMapping
    public List<User> getAllUsers() {
        return userService.getAllUsers();
    }

    // Handles POST requests to /api/users
    @PostMapping
    public User createUser(@RequestBody User user) {
        return userService.saveUser(user);
    }

    // Handles PUT requests to /api/users/{id}
    @PutMapping("/{id}")
    public User updateUser(@PathVariable Long id, @RequestBody User user) {
        return userService.updateUser(id, user);
    }

    // Handles DELETE requests to /api/users/{id}
    @DeleteMapping("/{id}")
    public void deleteUser(@PathVariable Long id) {
        userService.deleteUser(id);
    }
}
```

---

### 4. **Key Points**

* `@RequestMapping` is flexible and can handle any HTTP method.
* Specialized annotations improve readability and reduce boilerplate.
* You can specify more attributes like `params`, `headers`, `consumes` (for Content-Type), `produces` (for response Content-Type) with all of these annotations.

---

## ✅ Summary

| Annotation        | Purpose                              | HTTP Method | Typical Use                                    |
| ----------------- | ------------------------------------ | ----------- | ---------------------------------------------- |
| `@RequestMapping` | General mapping for all HTTP methods | Any         | When you want fine control or multiple methods |
| `@GetMapping`     | Maps GET requests                    | GET         | Fetching resources                             |
| `@PostMapping`    | Maps POST requests                   | POST        | Creating resources                             |
| `@PutMapping`     | Maps PUT requests                    | PUT         | Updating resources                             |
| `@DeleteMapping`  | Maps DELETE requests                 | DELETE      | Deleting resources                             |
| `@PatchMapping`   | Maps PATCH requests                  | PATCH       | Partial update                                 |

---

## 25. How do you handle request parameters and path variables?

Handling **request parameters** and **path variables** is fundamental for creating flexible REST APIs in Spring Boot. Here's how you do it:

---

## ✅ 1. Handling **Path Variables**

Path variables are **dynamic parts of the URI path** that you can capture and use in your controller methods.

### Example URL:

```
GET /users/42
```

Here, `42` is a path variable (usually representing user ID).

### How to capture:

Use `@PathVariable` annotation in your method parameter.

```java
@GetMapping("/users/{id}")
public User getUserById(@PathVariable("id") Long userId) {
    // userId will be 42 when the URL is /users/42
    return userService.findById(userId);
}
```

* If the parameter name matches the path variable name, you can omit the value:

```java
@GetMapping("/users/{id}")
public User getUserById(@PathVariable Long id) {
    return userService.findById(id);
}
```

---

## ✅ 2. Handling **Request Parameters**

Request parameters are typically sent in the **query string** (after `?`) or as **form data** in POST requests.

### Example URL:

```
GET /users?role=admin&active=true
```

### How to capture:

Use `@RequestParam` annotation in your method parameter.

```java
@GetMapping("/users")
public List<User> getUsersByRole(@RequestParam("role") String role,
                                 @RequestParam(value = "active", required = false, defaultValue = "true") boolean isActive) {
    return userService.findUsersByRoleAndStatus(role, isActive);
}
```

* `required = false` means the parameter is optional.
* `defaultValue` provides a default if the parameter is missing.

---

## ✅ 3. Complete Example

```java
@RestController
@RequestMapping("/users")
public class UserController {

    // Example of Path Variable
    @GetMapping("/{id}")
    public User getUser(@PathVariable Long id) {
        return userService.findById(id);
    }

    // Example of Request Parameters
    @GetMapping
    public List<User> getUsers(@RequestParam(required = false) String role,
                               @RequestParam(defaultValue = "true") boolean active) {
        return userService.findUsers(role, active);
    }
}
```

---

## ✅ Summary

| Use Case                 | Annotation      | Description                                 |
| ------------------------ | --------------- | ------------------------------------------- |
| Dynamic part of URL path | `@PathVariable` | Extracts variables embedded in the URL path |
| Query/form parameters    | `@RequestParam` | Extracts query parameters or form data      |

---

## 26. How do you return JSON response from a Spring Boot controller?

Returning JSON responses is a core feature of Spring Boot, especially when building RESTful APIs.

---

## ✅ How to Return JSON Response from a Spring Boot Controller?

### 1. Use `@RestController`

* The easiest way is to annotate your controller class with `@RestController`.
* This annotation implies that **all methods return data directly**, and Spring Boot automatically converts Java objects to JSON (using Jackson by default).

```java
@RestController
public class MyController {

    @GetMapping("/user")
    public User getUser() {
        return new User(1, "Alice");
    }
}
```

Here, the `User` object is automatically serialized into JSON and sent as the HTTP response.

---

### 2. Use `@ResponseBody` on Methods in a `@Controller`

If you use `@Controller` instead of `@RestController`, you need to annotate individual methods with `@ResponseBody` to indicate the response is data (not a view).

```java
@Controller
public class MyController {

    @GetMapping("/user")
    @ResponseBody
    public User getUser() {
        return new User(1, "Alice");
    }
}
```

---

### 3. Return Types Supported

* POJOs (Plain Old Java Objects), like your domain models.
* Collections like `List<User>`.
* Maps, primitive types, Strings (converted as JSON strings).
* Spring uses **Jackson** by default for serialization.

---

### 4. Example: Returning JSON Response

```java
@RestController
@RequestMapping("/api/users")
public class UserController {

    @GetMapping("/{id}")
    public User getUserById(@PathVariable int id) {
        return new User(id, "User" + id);
    }
}

class User {
    private int id;
    private String name;

    // Constructor, getters, setters

    public User(int id, String name) {
        this.id = id;
        this.name = name;
    }

    // Getters and setters omitted for brevity
}
```

Request:

```
GET /api/users/5
```

Response (JSON):

```json
{
  "id": 5,
  "name": "User5"
}
```

---

### 5. Customizing JSON Output

* Use Jackson annotations like `@JsonIgnore`, `@JsonProperty` on your model fields to control JSON.
* Configure custom ObjectMapper if needed (advanced).

---

## ✅ Summary:

| Approach                      | How it works                                       |
| ----------------------------- | -------------------------------------------------- |
| `@RestController`             | Class-level, all methods return JSON automatically |
| `@Controller + @ResponseBody` | Method-level, to return JSON from specific methods |

---

## 27. What is the role of `@RequestBody` and `@ResponseBody`?

`@RequestBody` and `@ResponseBody` are key annotations in Spring MVC that help handle HTTP request and response bodies, especially when working with JSON or XML data.

---

## ✅ What is `@RequestBody`?

* **Purpose:** Binds the HTTP request body to a Java object.
* Typically used in **POST**, **PUT**, or **PATCH** requests where the client sends data (usually JSON or XML).
* Spring uses **message converters** (like Jackson for JSON) to deserialize the incoming request body into the specified Java object.

### Example:

```java
@PostMapping("/users")
public User createUser(@RequestBody User user) {
    // 'user' is populated from the JSON request body
    return userService.save(user);
}
```

Client sends JSON like:

```json
{
  "name": "Alice",
  "email": "alice@example.com"
}
```

Spring converts this JSON into a `User` instance.

---

## ✅ What is `@ResponseBody`?

* **Purpose:** Tells Spring to serialize the returned Java object **directly** into the HTTP response body.
* Instead of rendering a view (like a JSP page), the returned object is converted to JSON, XML, or other formats using message converters.
* Used for REST APIs to return data.

### Example:

```java
@GetMapping("/users/{id}")
@ResponseBody
public User getUser(@PathVariable int id) {
    return userService.findById(id);
}
```

The returned `User` object is serialized to JSON and sent as the HTTP response.

---

## ✅ Relationship to `@RestController`

* `@RestController` is a **convenience annotation** that combines `@Controller` + `@ResponseBody`.
* So if your controller class is annotated with `@RestController`, you **don’t need** to put `@ResponseBody` on each method.

---

## ✅ Summary

| Annotation      | Used For                                     | Example Use Case                                      |
| --------------- | -------------------------------------------- | ----------------------------------------------------- |
| `@RequestBody`  | Deserialize HTTP request body to Java object | Receiving JSON input from client in POST/PUT requests |
| `@ResponseBody` | Serialize Java object to HTTP response body  | Returning JSON data in response                       |

---

## 28. How do you implement exception handling in Spring Boot REST API?

Exception handling is crucial for building robust and user-friendly REST APIs. Spring Boot provides several ways to handle exceptions gracefully and send meaningful error responses.

---

## ✅ How to Implement Exception Handling in Spring Boot REST API?

### 1. **Using `@ExceptionHandler` in Controller**

You can define methods in your controller (or a controller advice class) annotated with `@ExceptionHandler` to handle specific exceptions.

```java
@RestController
@RequestMapping("/api/users")
public class UserController {

    @GetMapping("/{id}")
    public User getUser(@PathVariable int id) {
        User user = userService.findById(id);
        if (user == null) {
            throw new UserNotFoundException("User not found with id " + id);
        }
        return user;
    }

    @ExceptionHandler(UserNotFoundException.class)
    public ResponseEntity<String> handleUserNotFound(UserNotFoundException ex) {
        return ResponseEntity.status(HttpStatus.NOT_FOUND).body(ex.getMessage());
    }
}
```

---

### 2. **Using `@ControllerAdvice` for Global Exception Handling**

To avoid repeating exception handlers in every controller, use a class annotated with `@ControllerAdvice` to handle exceptions application-wide.

```java
@ControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(UserNotFoundException.class)
    public ResponseEntity<ErrorResponse> handleUserNotFound(UserNotFoundException ex) {
        ErrorResponse error = new ErrorResponse(
            HttpStatus.NOT_FOUND.value(),
            ex.getMessage(),
            System.currentTimeMillis()
        );
        return new ResponseEntity<>(error, HttpStatus.NOT_FOUND);
    }

    @ExceptionHandler(Exception.class)
    public ResponseEntity<ErrorResponse> handleGenericException(Exception ex) {
        ErrorResponse error = new ErrorResponse(
            HttpStatus.INTERNAL_SERVER_ERROR.value(),
            "An unexpected error occurred",
            System.currentTimeMillis()
        );
        return new ResponseEntity<>(error, HttpStatus.INTERNAL_SERVER_ERROR);
    }
}
```

**ErrorResponse class example:**

```java
public class ErrorResponse {
    private int status;
    private String message;
    private long timestamp;

    public ErrorResponse(int status, String message, long timestamp) {
        this.status = status;
        this.message = message;
        this.timestamp = timestamp;
    }

    // getters and setters
}
```

---

### 3. **Using `ResponseStatusException`**

Spring Boot allows you to throw `ResponseStatusException` directly in your service or controller with an HTTP status and message.

```java
@GetMapping("/{id}")
public User getUser(@PathVariable int id) {
    return userService.findById(id).orElseThrow(() -> 
        new ResponseStatusException(HttpStatus.NOT_FOUND, "User not found"));
}
```

---

### 4. **Built-in Exception Handling**

Spring Boot automatically handles some exceptions (like `MethodArgumentNotValidException` for validation errors) and returns appropriate responses, but you can customize them using the methods above.

---

## ✅ Summary Table

| Approach                  | Description                                 | When to Use                      |
| ------------------------- | ------------------------------------------- | -------------------------------- |
| `@ExceptionHandler`       | Handle exceptions locally in controller     | For controller-specific handling |
| `@ControllerAdvice`       | Global exception handler across controllers | Centralized handling             |
| `ResponseStatusException` | Throw exceptions with HTTP status directly  | Quick inline exception handling  |

---

## 29. What is `@ControllerAdvice`?

`@ControllerAdvice` is a powerful feature in Spring Boot that helps you manage cross-cutting concerns related to controllers, such as **exception handling**, **data binding**, and **model attributes**, in a centralized way.

---

## ✅ What is `@ControllerAdvice`?

* It’s a **specialized component annotation** that allows you to write **global code** applicable to multiple controllers.
* Mainly used to handle exceptions **globally** across all controllers rather than writing repetitive code in each controller.
* Can also be used to apply common data binding or model attributes to multiple controllers.

---

## ✅ Key Use Cases of `@ControllerAdvice`

1. **Global Exception Handling**
   Handle exceptions thrown by any controller with centralized methods annotated with `@ExceptionHandler`.

2. **Global Data Binding**
   Customize how request parameters or path variables are bound to method parameters across all controllers.

3. **Global Model Attributes**
   Add attributes to the model available to all controllers.

---

## ✅ How Does it Work?

* Annotate a class with `@ControllerAdvice`.
* Define methods annotated with `@ExceptionHandler`, `@InitBinder`, or `@ModelAttribute`.
* These methods will apply **globally** to all controllers (or optionally filtered by base package, annotations, etc.).

---

## ✅ Example: Global Exception Handling

```java
@ControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(UserNotFoundException.class)
    public ResponseEntity<String> handleUserNotFound(UserNotFoundException ex) {
        return new ResponseEntity<>(ex.getMessage(), HttpStatus.NOT_FOUND);
    }

    @ExceptionHandler(Exception.class)
    public ResponseEntity<String> handleAllExceptions(Exception ex) {
        return new ResponseEntity<>("Internal server error", HttpStatus.INTERNAL_SERVER_ERROR);
    }
}
```

---

## ✅ Summary Table

| Annotation          | Purpose                                | Applies To                        |
| ------------------- | -------------------------------------- | --------------------------------- |
| `@ControllerAdvice` | Define global controller-related logic | All controllers (can be filtered) |
| `@ExceptionHandler` | Handle exceptions                      | Specific exceptions globally      |
| `@InitBinder`       | Customize data binding                 | Across controllers                |
| `@ModelAttribute`   | Add attributes to all models           | Across controllers                |

---

## 30. What is `@ResponseStatus`?

`@ResponseStatus` is a handy annotation in Spring used to specify the HTTP status code that should be returned by a controller method or exception class.

---

## ✅ What is `@ResponseStatus`?

* It allows you to **set the HTTP status code** that will be returned to the client when a particular exception is thrown or when a controller method is invoked.
* Can be applied on **exception classes** or **controller methods**.
* Helps in making your REST API responses more expressive and standardized without manually building `ResponseEntity` objects.

---

## ✅ Usage

### 1. On **Exception Classes**

You can annotate a custom exception class with `@ResponseStatus` to automatically send the specified HTTP status when that exception is thrown.

```java
@ResponseStatus(HttpStatus.NOT_FOUND)
public class UserNotFoundException extends RuntimeException {

    public UserNotFoundException(String message) {
        super(message);
    }
}
```

If this exception is thrown, Spring will respond with **404 Not Found** status.

---

### 2. On **Controller Methods**

You can annotate controller methods to return a specific status along with the response.

```java
@PostMapping("/users")
@ResponseStatus(HttpStatus.CREATED)  // 201 Created
public User createUser(@RequestBody User user) {
    return userService.save(user);
}
```

---

## ✅ Benefits

* Makes your code cleaner and easier to maintain.
* Avoids boilerplate code like building `ResponseEntity` manually.
* Helps standardize API responses by associating exceptions with HTTP statuses.

---

## ✅ Summary

| Use Case                   | Example                                 | HTTP Status Sent |
| -------------------------- | --------------------------------------- | ---------------- |
| Annotate custom exception  | `@ResponseStatus(HttpStatus.NOT_FOUND)` | 404 Not Found    |
| Annotate controller method | `@ResponseStatus(HttpStatus.CREATED)`   | 201 Created      |

---

## 31. How do you implement pagination in Spring Boot REST APIs?

Pagination is essential when dealing with large datasets in REST APIs to avoid sending too much data at once and improve performance.

---

## ✅ How to Implement Pagination in Spring Boot REST APIs?

Spring Boot, together with Spring Data JPA, provides built-in support for pagination using the **`Pageable`** interface.

---

### 1. Use Spring Data JPA's `Pageable` and `Page`

* `Pageable` represents pagination information like **page number**, **page size**, and **sorting**.
* `Page<T>` represents a page of results, including the content and metadata (total pages, total elements, etc.).

---

### 2. Repository Method Example

Assuming you have a `User` entity and a repository:

```java
public interface UserRepository extends JpaRepository<User, Long> {
    // JpaRepository already provides pagination methods by default
}
```

---

### 3. Controller Method Example

Inject `Pageable` into your controller method as a parameter:

```java
@RestController
@RequestMapping("/api/users")
public class UserController {

    @Autowired
    private UserRepository userRepository;

    @GetMapping
    public Page<User> getUsers(Pageable pageable) {
        return userRepository.findAll(pageable);
    }
}
```

---

### 4. How to Call API with Pagination Parameters

Spring Data REST understands the following query parameters automatically:

* `page` — page number (0-based index)
* `size` — number of records per page
* `sort` — sorting criteria in the format `property,asc|desc`

Example request:

```
GET /api/users?page=1&size=5&sort=name,asc
```

This fetches the second page (since page index starts at 0) with 5 users per page sorted by name ascending.

---

### 5. Example Response (JSON)

```json
{
  "content": [
    { "id": 6, "name": "Alice" },
    { "id": 7, "name": "Bob" }
    // other users on this page
  ],
  "pageable": {
    "sort": {
      "sorted": true,
      "unsorted": false,
      "empty": false
    },
    "pageNumber": 1,
    "pageSize": 5,
    "offset": 5,
    "paged": true,
    "unpaged": false
  },
  "totalPages": 4,
  "totalElements": 20,
  "last": false,
  "first": false,
  "sort": {
    "sorted": true,
    "unsorted": false,
    "empty": false
  },
  "numberOfElements": 5,
  "size": 5,
  "number": 1,
  "empty": false
}
```

---

### 6. Optional: Customizing Pageable Defaults

You can specify default page size and sorting if no parameters are provided:

```java
@GetMapping
public Page<User> getUsers(@PageableDefault(size = 10, sort = "name", direction = Sort.Direction.ASC) Pageable pageable) {
    return userRepository.findAll(pageable);
}
```

---

## ✅ Summary

| Component  | Role                                                                     |
| ---------- | ------------------------------------------------------------------------ |
| `Pageable` | Input pagination info (page, size, sort)                                 |
| `Page<T>`  | Output paginated result with metadata                                    |
| Repository | Use `findAll(Pageable pageable)` or custom query methods with `Pageable` |

---

## 32. How do you secure REST APIs in Spring Boot?

Securing REST APIs is crucial to protect your application and user data. In Spring Boot, the most common way to secure REST APIs is by using **Spring Security**.

---

## ✅ How to Secure REST APIs in Spring Boot?

### 1. **Add Spring Security Dependency**

If you’re using Maven, add this to your `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
```

---

### 2. **Basic Authentication Setup**

By default, when you add Spring Security, it enables **HTTP Basic Authentication** with a generated user and password.

You can customize this by creating a security configuration:

```java
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
          .csrf().disable() // Disable CSRF for APIs
          .authorizeRequests()
          .antMatchers("/api/public/**").permitAll() // Public endpoints
          .anyRequest().authenticated() // Secure all other endpoints
          .and()
          .httpBasic(); // Use basic auth
    }

    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception {
        auth.inMemoryAuthentication()
            .withUser("user")
            .password("{noop}password") // {noop} means no password encoding
            .roles("USER");
    }
}
```

---

### 3. **JWT (JSON Web Token) Authentication**

For stateless REST APIs, JWT is a popular choice.

* Client logs in with username/password.
* Server returns a JWT token.
* Client sends the JWT token in the `Authorization` header for subsequent requests.
* Server validates the token for authentication and authorization.

JWT implementation involves:

* Creating a login endpoint.
* Generating and signing JWT tokens.
* Adding filters to validate JWT on each request.

This is more complex but recommended for real-world applications.

---

### 4. **Other Security Features**

* **OAuth2 / OpenID Connect:** For single sign-on and social login.
* **Role-based access control:** Use annotations like `@PreAuthorize("hasRole('ADMIN')")` to secure methods.
* **CSRF protection:** Usually disabled for stateless APIs.
* **CORS configuration:** To allow/deny cross-origin requests.

---

### 5. **Example: Securing Endpoints with Roles**

```java
@RestController
@RequestMapping("/api")
public class MyController {

    @GetMapping("/public")
    public String publicEndpoint() {
        return "This is public";
    }

    @GetMapping("/user")
    @PreAuthorize("hasRole('USER')")
    public String userEndpoint() {
        return "This is for USER role";
    }

    @GetMapping("/admin")
    @PreAuthorize("hasRole('ADMIN')")
    public String adminEndpoint() {
        return "This is for ADMIN role";
    }
}
```

---

## ✅ Summary

| Security Aspect          | How to Implement                             |
| ------------------------ | -------------------------------------------- |
| Basic Authentication     | Spring Security with `httpBasic()`           |
| Token-based (JWT)        | Custom filters + JWT libraries               |
| Role-based Authorization | `@PreAuthorize` annotations                  |
| OAuth2 / Social Login    | Spring Security OAuth2 support               |
| CSRF                     | Disable for stateless REST APIs              |
| CORS                     | Configure allowed origins in security config |

---

## 33. How do you validate request bodies in Spring Boot?

Validating request bodies is essential to ensure that the data your API receives is correct and meets business rules. Spring Boot makes this easy by integrating with **Java Bean Validation** (JSR-380), typically using **Hibernate Validator** as the implementation.

---

## ✅ How to Validate Request Bodies in Spring Boot?

### 1. **Add Validation Dependency**

If you use Spring Boot Starter Web, the validation dependency is usually included. If not, add this to your `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-validation</artifactId>
</dependency>
```

---

### 2. **Annotate Your Model with Validation Constraints**

Use annotations like `@NotNull`, `@Size`, `@Email`, etc. on your request DTO/model fields.

```java
public class UserRequest {

    @NotNull(message = "Name is required")
    @Size(min = 2, max = 30, message = "Name must be between 2 and 30 characters")
    private String name;

    @NotNull(message = "Email is required")
    @Email(message = "Email should be valid")
    private String email;

    // getters and setters
}
```

---

### 3. **Use `@Valid` Annotation in Controller Method**

Annotate the request body parameter with `@Valid` to trigger validation.

```java
@RestController
@RequestMapping("/api/users")
public class UserController {

    @PostMapping
    public ResponseEntity<String> createUser(@Valid @RequestBody UserRequest userRequest) {
        // If validation fails, Spring automatically returns 400 Bad Request
        return ResponseEntity.ok("User created successfully");
    }
}
```

---

### 4. **Handling Validation Errors**

By default, if validation fails, Spring Boot returns a **400 Bad Request** with a default error response.

You can customize error handling by:

* Using a `@ControllerAdvice` with a method handling `MethodArgumentNotValidException`.
* Return custom error messages or formats.

Example:

```java
@ControllerAdvice
public class ValidationExceptionHandler {

    @ExceptionHandler(MethodArgumentNotValidException.class)
    public ResponseEntity<Map<String, String>> handleValidationExceptions(MethodArgumentNotValidException ex) {
        Map<String, String> errors = new HashMap<>();
        ex.getBindingResult().getFieldErrors().forEach(error -> 
            errors.put(error.getField(), error.getDefaultMessage())
        );
        return new ResponseEntity<>(errors, HttpStatus.BAD_REQUEST);
    }
}
```

---

### 5. **Example Request and Response**

**Request JSON (invalid):**

```json
{
  "name": "A",
  "email": "invalid-email"
}
```

**Response JSON (400 Bad Request):**

```json
{
  "name": "Name must be between 2 and 30 characters",
  "email": "Email should be valid"
}
```

---

## ✅ Summary

| Step                      | What to do                                                               |
| ------------------------- | ------------------------------------------------------------------------ |
| Add validation dependency | `spring-boot-starter-validation`                                         |
| Annotate model fields     | Use `@NotNull`, `@Size`, `@Email`, etc.                                  |
| Annotate controller param | Use `@Valid @RequestBody`                                                |
| Handle validation errors  | Customize with `@ControllerAdvice` and `MethodArgumentNotValidException` |

---

## 34. What is the use of `@Valid` and `@Validated`?

Both `@Valid` and `@Validated` are used in Spring Boot to trigger validation, but they have some differences in usage and capabilities.

---

## ✅ What is `@Valid`?

* It comes from **Javax Validation API** (`javax.validation.Valid`).
* Used to trigger **standard bean validation** on a method parameter or a field.
* Commonly used on **request bodies**, method parameters, and nested objects to activate validation annotations like `@NotNull`, `@Size`, etc.
* Supports **only one validation group** (default).

### Example:

```java
@PostMapping("/users")
public ResponseEntity<String> createUser(@Valid @RequestBody UserRequest userRequest) {
    // Validation of userRequest fields occurs here
    return ResponseEntity.ok("User created");
}
```

---

## ✅ What is `@Validated`?

* It comes from **Spring Framework** (`org.springframework.validation.annotation.Validated`).
* Extends `@Valid` by adding support for **validation groups**.
* Can be applied at the **class level** or **method level**.
* Useful when you want to perform **group-based validation** (e.g., different validation rules for create vs update).

### Example with validation groups:

```java
public class UserRequest {

    @NotNull(groups = Update.class)
    private Long id;

    @NotNull(groups = {Create.class, Update.class})
    private String name;

    // Validation groups marker interfaces
    public interface Create {}
    public interface Update {}
}
```

Then in your controller:

```java
@PostMapping("/users")
public ResponseEntity<String> createUser(@Validated(UserRequest.Create.class) @RequestBody UserRequest userRequest) {
    // Validates only constraints in Create group
    return ResponseEntity.ok("User created");
}
```

---

## ✅ Key Differences

| Feature                        | `@Valid`                      | `@Validated`                                          |
| ------------------------------ | ----------------------------- | ----------------------------------------------------- |
| Package                        | `javax.validation.Valid`      | `org.springframework.validation.annotation.Validated` |
| Supports Validation Groups     | No                            | Yes                                                   |
| Can be applied on class level? | No (usually method parameter) | Yes                                                   |
| Origin                         | Javax Validation API          | Spring Framework extension                            |

---

## ✅ When to Use Which?

* Use **`@Valid`** for simple validations without groups (most common).
* Use **`@Validated`** if you need group validation or class-level validation support.

---

## 35. How do you send and receive headers in Spring Boot?

Handling HTTP headers is a common task in REST APIs, and Spring Boot makes it straightforward to send and receive headers in your controllers.

---

## ✅ How to **Receive** Headers in Spring Boot

Use the `@RequestHeader` annotation in your controller method parameters to access HTTP headers sent by the client.

### Example: Receive a specific header

```java
@GetMapping("/greet")
public ResponseEntity<String> greetUser(@RequestHeader("User-Agent") String userAgent) {
    return ResponseEntity.ok("Your User-Agent is: " + userAgent);
}
```

If the header might be missing, you can make it optional:

```java
@GetMapping("/greet")
public ResponseEntity<String> greetUser(@RequestHeader(value = "User-Agent", required = false) String userAgent) {
    if (userAgent == null) {
        userAgent = "Unknown";
    }
    return ResponseEntity.ok("Your User-Agent is: " + userAgent);
}
```

### Example: Receive all headers as a Map

```java
@GetMapping("/headers")
public ResponseEntity<Map<String, String>> getAllHeaders(@RequestHeader Map<String, String> headers) {
    return ResponseEntity.ok(headers);
}
```

---

## ✅ How to **Send** Headers in Spring Boot Response

You can add headers to your response in several ways:

### 1. Using `ResponseEntity` builder

```java
@GetMapping("/custom-header")
public ResponseEntity<String> customHeader() {
    return ResponseEntity.ok()
        .header("X-Custom-Header", "MyValue")
        .body("Response with custom header");
}
```

### 2. Using `HttpServletResponse`

```java
@GetMapping("/custom-header-servlet")
public String customHeaderServlet(HttpServletResponse response) {
    response.setHeader("X-Custom-Header", "MyValue");
    return "Response with custom header";
}
```

---

## ✅ Summary

| Action              | How to Do It                                                   | Annotation / Class                      |
| ------------------- | -------------------------------------------------------------- | --------------------------------------- |
| Receive a header    | `@RequestHeader("Header-Name")`                                | `@RequestHeader`                        |
| Receive all headers | `@RequestHeader Map<String, String>`                           | `@RequestHeader`                        |
| Send headers        | `ResponseEntity.header()` or `HttpServletResponse.setHeader()` | `ResponseEntity`, `HttpServletResponse` |

---

## 36. How do you handle file upload/download in Spring Boot?

Handling file upload and download is a common requirement in many Spring Boot applications. Spring Boot makes it easy to implement both using built-in support.

---

## ✅ File Upload in Spring Boot

### 1. Add dependency (if using Maven):

If you use Spring Boot Starter Web, it includes multipart support by default. Otherwise:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

### 2. Enable multipart support (usually auto-enabled, but can be explicitly set in `application.properties`):

```properties
spring.servlet.multipart.enabled=true
spring.servlet.multipart.max-file-size=10MB
spring.servlet.multipart.max-request-size=10MB
```

### 3. Controller method to handle file upload:

```java
@PostMapping("/upload")
public ResponseEntity<String> uploadFile(@RequestParam("file") MultipartFile file) {
    if (file.isEmpty()) {
        return ResponseEntity.badRequest().body("File is empty");
    }
    try {
        // For example, save the file locally
        Path path = Paths.get("uploads/" + file.getOriginalFilename());
        Files.createDirectories(path.getParent());
        Files.write(path, file.getBytes());
        return ResponseEntity.ok("File uploaded successfully: " + file.getOriginalFilename());
    } catch (IOException e) {
        return ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR).body("Failed to upload file");
    }
}
```

---

## ✅ File Download in Spring Boot

### Controller method to send a file as a response:

```java
@GetMapping("/download/{filename:.+}")
public ResponseEntity<Resource> downloadFile(@PathVariable String filename) {
    try {
        Path filePath = Paths.get("uploads").resolve(filename).normalize();
        Resource resource = new UrlResource(filePath.toUri());

        if (!resource.exists()) {
            return ResponseEntity.notFound().build();
        }

        String contentType = "application/octet-stream";

        return ResponseEntity.ok()
            .contentType(MediaType.parseMediaType(contentType))
            .header(HttpHeaders.CONTENT_DISPOSITION, "attachment; filename=\"" + resource.getFilename() + "\"")
            .body(resource);

    } catch (MalformedURLException e) {
        return ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR).build();
    }
}
```

---

## ✅ Important Points

* Use `MultipartFile` to receive uploaded files.
* Store uploaded files wherever suitable (local disk, cloud storage, database).
* For downloads, use `Resource` to serve files with proper headers.
* Set `Content-Disposition` header to suggest file download.
* Always validate file size and type for security.

---

## ✅ Summary Table

| Operation     | Key Classes / Annotations        | Notes                            |
| ------------- | -------------------------------- | -------------------------------- |
| File Upload   | `MultipartFile`, `@RequestParam` | Enable multipart support         |
| File Download | `Resource`, `ResponseEntity`     | Set content type and disposition |

---

## 37. What is content negotiation?

**Content Negotiation** is an important concept in RESTful web services, including Spring Boot.

---

## ✅ What is Content Negotiation?

Content Negotiation is the process where the server selects the best representation (format) of a resource to send back to the client based on the client's capabilities or preferences.

---

### How it works:

* The **client** sends an HTTP request with an `Accept` header specifying which media types (formats) it can handle, for example:

    * `Accept: application/json`
    * `Accept: application/xml`
* The **server** examines the `Accept` header and responds with the resource in one of the requested formats, if possible.
* If no acceptable format is found, the server returns HTTP status **406 Not Acceptable**.

---

## ✅ Content Negotiation in Spring Boot

Spring Boot, using Spring MVC, supports content negotiation out of the box.

* Supports multiple formats like JSON, XML, YAML (with proper dependencies).
* Uses `HttpMessageConverters` to serialize Java objects into the requested format.

---

## ✅ How to Use Content Negotiation

### Example: Controller returns an object

```java
@GetMapping("/user")
public User getUser() {
    return new User(1L, "Alice");
}
```

* If client sends `Accept: application/json`, response will be JSON.
* If client sends `Accept: application/xml` and XML converter is available, response will be XML.

### To support XML, add dependency:

```xml
<dependency>
    <groupId>com.fasterxml.jackson.dataformat</groupId>
    <artifactId>jackson-dataformat-xml</artifactId>
</dependency>
```

---

## ✅ Configuring Content Negotiation (optional)

You can customize content negotiation in Spring Boot via configuration or Java config:

```java
@Configuration
public class WebConfig implements WebMvcConfigurer {

    @Override
    public void configureContentNegotiation(ContentNegotiationConfigurer configurer) {
        configurer
            .favorParameter(true)        // allow ?format=json
            .parameterName("format")
            .ignoreAcceptHeader(false)
            .defaultContentType(MediaType.APPLICATION_JSON)
            .mediaType("json", MediaType.APPLICATION_JSON)
            .mediaType("xml", MediaType.APPLICATION_XML);
    }
}
```

With this, clients can do:

```
GET /user?format=xml
```

to get XML instead of JSON.

---

## ✅ Summary

| Concept             | Description                                                                          |
| ------------------- | ------------------------------------------------------------------------------------ |
| Content Negotiation | Server chooses response format based on client `Accept` header or request parameters |
| Common Media Types  | JSON, XML, YAML                                                                      |
| Spring Boot Support | Via `HttpMessageConverters` and dependencies (Jackson JSON, Jackson XML)             |
| Customization       | Configure `ContentNegotiationConfigurer` to allow URL parameter or other behaviors   |

---

## 38. How do you return different formats (JSON, XML) in Spring Boot?

Returning different response formats like JSON or XML in Spring Boot is part of **content negotiation** and is quite straightforward thanks to Spring’s support for multiple message converters.

---

## ✅ How to Return Different Formats (JSON, XML) in Spring Boot

### 1. **Ensure Dependencies for Both Formats**

* JSON support is included by default via **Jackson** (`spring-boot-starter-web`).
* For XML support, add Jackson XML dependency:

```xml
<dependency>
    <groupId>com.fasterxml.jackson.dataformat</groupId>
    <artifactId>jackson-dataformat-xml</artifactId>
</dependency>
```

---

### 2. **Create Your POJO (Model)**

Make sure your model has getters/setters and optionally XML annotations (optional but helpful):

```java
import com.fasterxml.jackson.dataformat.xml.annotation.JacksonXmlRootElement;

@JacksonXmlRootElement(localName = "User")
public class User {
    private Long id;
    private String name;

    // constructors, getters, setters
}
```

---

### 3. **Write Controller Method Returning Object**

```java
@GetMapping("/user")
public User getUser() {
    return new User(1L, "Alice");
}
```

---

### 4. **Client Controls Format via `Accept` Header**

* Request JSON: `Accept: application/json`
* Request XML: `Accept: application/xml`

Spring Boot automatically serializes response according to the `Accept` header.

---

### 5. **Optional: Support Format via URL Parameter**

You can configure Spring to use a URL parameter like `?format=xml`:

```java
@Configuration
public class WebConfig implements WebMvcConfigurer {
    @Override
    public void configureContentNegotiation(ContentNegotiationConfigurer configurer) {
        configurer
            .favorParameter(true)
            .parameterName("format")
            .ignoreAcceptHeader(false)
            .defaultContentType(MediaType.APPLICATION_JSON)
            .mediaType("json", MediaType.APPLICATION_JSON)
            .mediaType("xml", MediaType.APPLICATION_XML);
    }
}
```

Now client can call:

```
GET /user?format=xml
```

---

### 6. **Testing**

Using `curl`:

```bash
curl -H "Accept: application/json" http://localhost:8080/user
```

Response (JSON):

```json
{
  "id": 1,
  "name": "Alice"
}
```

```bash
curl -H "Accept: application/xml" http://localhost:8080/user
```

Response (XML):

```xml
<User>
  <id>1</id>
  <name>Alice</name>
</User>
```

---

## ✅ Summary

| Step                           | Action                                               |
| ------------------------------ | ---------------------------------------------------- |
| Add XML dependency             | `jackson-dataformat-xml`                             |
| Write model POJO               | Optionally annotate with XML annotations             |
| Return POJO in controller      | Spring serializes based on `Accept` header           |
| (Optional) Configure URL param | Use `ContentNegotiationConfigurer` for `?format=xml` |

---

## 39. What is the role of `HttpMessageConverters`?

Understanding `HttpMessageConverters` is key to knowing how Spring Boot automatically handles data serialization and deserialization for REST APIs.

---

## ✅ What is `HttpMessageConverter`?

* It's an interface in Spring MVC used to **convert HTTP requests and responses** to and from Java objects.
* In other words, it **serializes** Java objects into HTTP responses (like JSON, XML) and **deserializes** HTTP request bodies into Java objects.

---

## ✅ Role of `HttpMessageConverters` in Spring Boot

When you write a controller method like:

```java
@PostMapping("/user")
public ResponseEntity<User> createUser(@RequestBody User user) {
    // ...
}
```

* Spring uses `HttpMessageConverters` behind the scenes to convert the incoming JSON/XML request body into a `User` object.
* Similarly, when returning the `User` object as a response, converters convert it back to JSON/XML based on content negotiation (client’s `Accept` header).

---

## ✅ Common Implementations of `HttpMessageConverter`

* **MappingJackson2HttpMessageConverter** — converts JSON using Jackson library (default for JSON).
* **MappingJackson2XmlHttpMessageConverter** — converts XML using Jackson XML extension.
* **StringHttpMessageConverter** — for plain text.
* **FormHttpMessageConverter** — for form data.
* **ByteArrayHttpMessageConverter** — for binary data.

---

## ✅ How Spring Boot Configures Them

* Spring Boot auto-configures a list of `HttpMessageConverters` based on the classpath dependencies (e.g., if Jackson JSON is on the classpath, it adds JSON converter).
* You can customize the converters by implementing `WebMvcConfigurer` and overriding `configureMessageConverters` or `extendMessageConverters`.

---

## ✅ Why is it Important?

* You don’t have to manually parse request bodies or serialize responses.
* Enables **content negotiation** automatically (serving JSON, XML, etc.).
* Supports many media types transparently.

---

## ✅ Summary Table

| Responsibility               | Description                                       |
| ---------------------------- | ------------------------------------------------- |
| Request body deserialization | Convert HTTP request (JSON/XML) → Java object     |
| Response body serialization  | Convert Java object → HTTP response (JSON/XML)    |
| Supports multiple formats    | JSON, XML, text, binary, form data, etc.          |
| Plugged in automatically     | Based on dependencies and Spring Boot auto-config |

---

## 40. How do you implement versioning in Spring Boot REST APIs?

Versioning your REST APIs is crucial for evolving your service without breaking existing clients. Spring Boot doesn’t enforce a specific versioning strategy, but it provides flexibility to implement various versioning approaches easily.

---

## ✅ Common Ways to Implement Versioning in Spring Boot REST APIs

### 1. **URI Versioning (Path Versioning)**

Add the version number in the URL path.

```java
@RestController
@RequestMapping("/api/v1/users")
public class UserControllerV1 {
    @GetMapping("/{id}")
    public UserV1 getUser(@PathVariable String id) {
        return new UserV1(id, "User V1");
    }
}

@RestController
@RequestMapping("/api/v2/users")
public class UserControllerV2 {
    @GetMapping("/{id}")
    public UserV2 getUser(@PathVariable String id) {
        return new UserV2(id, "User V2", "additional field");
    }
}
```

* **URL example:** `/api/v1/users/123` vs `/api/v2/users/123`

---

### 2. **Request Parameter Versioning**

Send version as a query parameter.

```java
@RestController
@RequestMapping("/api/users")
public class UserController {

    @GetMapping(value = "/{id}", params = "version=1")
    public UserV1 getUserV1(@PathVariable String id) {
        return new UserV1(id, "User V1");
    }

    @GetMapping(value = "/{id}", params = "version=2")
    public UserV2 getUserV2(@PathVariable String id) {
        return new UserV2(id, "User V2", "extra");
    }
}
```

* **Request example:** `/api/users/123?version=1`

---

### 3. **Header Versioning**

Use a custom header to specify the API version.

```java
@RestController
@RequestMapping("/api/users")
public class UserController {

    @GetMapping(value = "/{id}", headers = "X-API-VERSION=1")
    public UserV1 getUserV1(@PathVariable String id) {
        return new UserV1(id, "User V1");
    }

    @GetMapping(value = "/{id}", headers = "X-API-VERSION=2")
    public UserV2 getUserV2(@PathVariable String id) {
        return new UserV2(id, "User V2", "extra");
    }
}
```

* Client sends header: `X-API-VERSION: 1` or `2`

---

### 4. **Content Negotiation / Accept Header Versioning**

Use custom media types in the `Accept` header.

```java
@RestController
@RequestMapping("/api/users")
public class UserController {

    @GetMapping(value = "/{id}", produces = "application/vnd.company.app-v1+json")
    public UserV1 getUserV1(@PathVariable String id) {
        return new UserV1(id, "User V1");
    }

    @GetMapping(value = "/{id}", produces = "application/vnd.company.app-v2+json")
    public UserV2 getUserV2(@PathVariable String id) {
        return new UserV2(id, "User V2", "extra");
    }
}
```

* Client sends header: `Accept: application/vnd.company.app-v1+json`

---

## ✅ Summary of Versioning Strategies

| Versioning Type   | How It Works                          | Pros                                   | Cons                           |
| ----------------- | ------------------------------------- | -------------------------------------- | ------------------------------ |
| URI Versioning    | Version in URL path (`/v1/users`)     | Simple, cacheable URLs                 | Changes URL, can clutter paths |
| Request Parameter | Version as query param (`?version=1`) | Easy to implement                      | Less RESTful, caching issues   |
| Header Versioning | Custom header (`X-API-VERSION: 1`)    | Keeps URL clean                        | Harder to test in browsers     |
| Accept Header     | Custom media types in `Accept` header | Uses HTTP standard content negotiation | Complex client setup           |

---

## ✅ Example: URI Versioning in Spring Boot

```java
@RestController
@RequestMapping("/api/v1/users")
public class UserControllerV1 {
    @GetMapping("/{id}")
    public ResponseEntity<String> getUserV1(@PathVariable String id) {
        return ResponseEntity.ok("User V1 with id " + id);
    }
}

@RestController
@RequestMapping("/api/v2/users")
public class UserControllerV2 {
    @GetMapping("/{id}")
    public ResponseEntity<String> getUserV2(@PathVariable String id) {
        return ResponseEntity.ok("User V2 with id " + id);
    }
}
```

---

### 🔹 41–60: Data Access Layer (JPA, JDBC, Repositories)

## 41. How do you connect Spring Boot to a database?

Connecting Spring Boot to a database is one of the fundamental tasks for building data-driven applications. Spring Boot makes it easy by auto-configuring database connections and providing simple abstractions.

---

## ✅ Steps to Connect Spring Boot to a Database

---

### 1. **Add Database Dependency**

Depending on the database, add the appropriate dependency in your `pom.xml` (for Maven) or `build.gradle` (for Gradle).

Example for **MySQL**:

```xml
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <scope>runtime</scope>
</dependency>
```

If you use **H2 (in-memory database)** for development/testing:

```xml
<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
    <scope>runtime</scope>
</dependency>
```

---

### 2. **Add Spring Data JPA Dependency**

Spring Data JPA helps to interact with relational databases easily.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```

---

### 3. **Configure Database Connection in `application.properties` or `application.yml`**

Example for MySQL (`application.properties`):

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.username=root
spring.datasource.password=yourpassword
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL8Dialect
```

Explanation:

* `spring.jpa.hibernate.ddl-auto=update` — Automatically creates/updates tables based on your entities.
* `show-sql=true` — Logs generated SQL statements.
* Dialect tells Hibernate which SQL dialect to use.

---

### 4. **Create Entity Class**

Annotate your POJO with `@Entity` and define primary key.

```java
import jakarta.persistence.Entity;
import jakarta.persistence.Id;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.GenerationType;

@Entity
public class User {
  
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
  
    // getters and setters
}
```

---

### 5. **Create Repository Interface**

Extend Spring Data JPA’s `JpaRepository` to get CRUD methods automatically.

```java
import org.springframework.data.jpa.repository.JpaRepository;

public interface UserRepository extends JpaRepository<User, Long> {
    // You can add custom query methods here if needed
}
```

---

### 6. **Use Repository in Service or Controller**

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;

import java.util.List;

@RestController
@RequestMapping("/users")
public class UserController {
  
    @Autowired
    private UserRepository userRepository;
  
    @GetMapping
    public List<User> getAllUsers() {
        return userRepository.findAll();
    }
  
    @PostMapping
    public User createUser(@RequestBody User user) {
        return userRepository.save(user);
    }
}
```

---

## ✅ Summary

| Step                 | Description                                     |
| -------------------- | ----------------------------------------------- |
| Add dependencies     | JDBC driver, Spring Data JPA                    |
| Configure datasource | URL, username, password, driver class           |
| Create Entity        | Annotate POJO with `@Entity` and `@Id`          |
| Create Repository    | Interface extending `JpaRepository`             |
| Use Repository       | Inject and use repository in service/controller |

---

## 42. What is Spring Data JPA?

Spring Data JPA is a very popular and powerful part of the Spring ecosystem that simplifies working with databases using JPA (Java Persistence API).

---

## ✅ What is Spring Data JPA?

**Spring Data JPA** is a Spring module that:

* Provides an abstraction layer over JPA (Java Persistence API).
* Simplifies the implementation of data access layers.
* Reduces boilerplate code needed for interacting with relational databases.
* Offers powerful features like automatic query generation, pagination, sorting, and custom queries.

---

## ✅ Key Points:

* It builds on **JPA**, which is a Java specification for object-relational mapping (ORM).
* It supports popular JPA providers like **Hibernate** (which is the default in Spring Boot).
* You write repository interfaces, and Spring Data JPA creates the implementation at runtime.
* Supports both standard CRUD operations and complex queries without writing SQL.

---

## ✅ How Spring Data JPA Works — Example

### 1. Define Entity:

```java
import jakarta.persistence.Entity;
import jakarta.persistence.Id;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.GenerationType;

@Entity
public class User {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    // getters and setters
}
```

### 2. Create Repository Interface:

```java
import org.springframework.data.jpa.repository.JpaRepository;

public interface UserRepository extends JpaRepository<User, Long> {
    // Custom query methods (optional)
    List<User> findByName(String name);
}
```

### 3. Use Repository in Service/Controller:

```java
@Autowired
private UserRepository userRepository;

public List<User> getUsersByName(String name) {
    return userRepository.findByName(name);
}
```

Spring Data JPA automatically implements `findByName` by parsing the method name and generating the query.

---

## ✅ Benefits of Spring Data JPA

| Feature                | Description                                            |
| ---------------------- | ------------------------------------------------------ |
| CRUD Repository        | Predefined methods like save, findAll, delete          |
| Derived Query Methods  | Create queries by method naming conventions            |
| Pagination and Sorting | Built-in support with `Pageable` and `Sort`            |
| Custom Queries         | Use JPQL or native SQL with `@Query` annotation        |
| Auditing               | Automatic tracking of created/modified dates and users |

---

## ✅ Summary

Spring Data JPA lets you focus on business logic by handling data access details. It combines the power of JPA with Spring’s ease-of-use and dependency injection.

---

If you'd like, I can help you build a small Spring Boot project using Spring Data JPA with examples of custom queries and pagination!

---

## 43. What is the use of `CrudRepository` and `JpaRepository`?

Great question! Both `CrudRepository` and `JpaRepository` are interfaces in **Spring Data JPA** that provide convenient methods for database operations, but they have some differences.

---

## ✅ What is `CrudRepository`?

* The **base interface** for generic CRUD (Create, Read, Update, Delete) operations.
* Defines methods like:

    * `save()`
    * `findById()`
    * `findAll()`
    * `deleteById()`
    * `count()`
* Supports basic CRUD operations but **does not provide advanced features** like pagination or sorting.

---

## ✅ What is `JpaRepository`?

* Extends `CrudRepository` **and** `PagingAndSortingRepository`.
* Provides all CRUD operations **plus**:

    * Pagination (`Pageable` support)
    * Sorting (`Sort` support)
    * JPA-specific operations like `flush()`, `saveAndFlush()`, and batch deletes.
* Offers a richer set of methods for working with JPA.

---

## ✅ Interface Hierarchy

```
Repository (marker interface)
   └─ CrudRepository<T, ID>
         └─ PagingAndSortingRepository<T, ID>
               └─ JpaRepository<T, ID>
```

---

## ✅ When to Use Which?

| Interface        | Use Case                                                        |
| ---------------- | --------------------------------------------------------------- |
| `CrudRepository` | Simple CRUD operations without pagination/sorting               |
| `JpaRepository`  | Full JPA support with pagination, sorting, and batch operations |

---

## ✅ Example Usage

```java
public interface UserRepository extends JpaRepository<User, Long> {
    // You get CRUD + pagination + sorting methods automatically
}
```

With `JpaRepository`, you can do:

```java
Page<User> findAll(Pageable pageable);
List<User> findAll(Sort sort);
void flush();
User saveAndFlush(User entity);
```

---

## ✅ Summary

| Feature              | CrudRepository | JpaRepository |
| -------------------- | -------------- | ------------- |
| CRUD methods         | Yes            | Yes           |
| Pagination & Sorting | No             | Yes           |
| JPA-specific methods | No             | Yes           |

---

## 44. How do you define custom queries in Spring Data?

Defining custom queries in Spring Data JPA lets you write more complex or specific database queries beyond the automatically derived ones.

---

## ✅ Ways to Define Custom Queries in Spring Data JPA

### 1. **Method Name Query Derivation**

Spring Data JPA generates queries automatically based on the method name.

Example:

```java
List<User> findByLastName(String lastName);
```

Spring parses the method name and builds a query like:

```sql
SELECT * FROM user WHERE last_name = ?;
```

---

### 2. **Using `@Query` Annotation**

You can write **JPQL** (Java Persistence Query Language) or **native SQL** queries directly.

#### JPQL example:

```java
@Query("SELECT u FROM User u WHERE u.email = ?1")
User findByEmail(String email);
```

#### Native SQL example:

```java
@Query(value = "SELECT * FROM users WHERE email = ?1", nativeQuery = true)
User findByEmailNative(String email);
```

---

### 3. **Named Parameters in `@Query`**

Instead of positional parameters, use named parameters for clarity:

```java
@Query("SELECT u FROM User u WHERE u.email = :email")
User findByEmail(@Param("email") String email);
```

---

### 4. **Modifying Queries**

For update/delete operations, use `@Modifying` with `@Query` and add transaction support:

```java
@Transactional
@Modifying
@Query("UPDATE User u SET u.status = :status WHERE u.id = :id")
int updateUserStatus(@Param("id") Long id, @Param("status") String status);
```

---

### 5. **Using Specifications (Criteria API)**

For dynamic queries, use Spring Data JPA **Specifications** (more advanced topic):

```java
public interface UserSpecification extends Specification<User> {
    static Specification<User> hasName(String name) {
        return (root, query, cb) -> cb.equal(root.get("name"), name);
    }
}
```

---

## ✅ Summary Table

| Method              | Use Case                               | Notes                         |
| ------------------- | -------------------------------------- | ----------------------------- |
| Method Name Query   | Simple queries based on property names | Easy to use but limited       |
| `@Query` JPQL       | Custom JPQL queries                    | More flexible and powerful    |
| `@Query` Native SQL | Native SQL queries                     | Use when JPQL is insufficient |
| `@Modifying`        | Update/Delete queries                  | Needs transaction             |
| Specifications      | Dynamic and complex queries            | More advanced, type-safe      |

---

## 45. What are `@Entity`, `@Table`, `@Id`, and `@GeneratedValue`?

These annotations are fundamental in **JPA (Java Persistence API)**, which Spring Data JPA uses to map Java classes to database tables.

---

## ✅ Explanation of Each Annotation

### 1. `@Entity`

* Marks a Java class as a **JPA entity**, meaning it maps to a table in the database.
* The class will be managed by the JPA provider (like Hibernate).

```java
@Entity
public class User {
    // class content
}
```

---

### 2. `@Table`

* Specifies the **database table name** that the entity maps to.
* Optional: If omitted, JPA assumes the table name is the same as the entity class name.

```java
@Entity
@Table(name = "users")
public class User {
    // class content
}
```

---

### 3. `@Id`

* Defines the **primary key** of the entity.
* This field uniquely identifies each record in the table.

```java
@Id
private Long id;
```

---

### 4. `@GeneratedValue`

* Specifies how the primary key value is **automatically generated**.
* Common strategies:

    * `GenerationType.IDENTITY` — relies on database auto-increment.
    * `GenerationType.SEQUENCE` — uses a database sequence.
    * `GenerationType.AUTO` — lets JPA provider pick the strategy.
    * `GenerationType.TABLE` — uses a table to generate IDs.

Example:

```java
@Id
@GeneratedValue(strategy = GenerationType.IDENTITY)
private Long id;
```

---

## ✅ Complete Example

```java
import jakarta.persistence.Entity;
import jakarta.persistence.Table;
import jakarta.persistence.Id;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.GenerationType;

@Entity
@Table(name = "users")
public class User {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    // getters and setters
}
```

---

## ✅ Summary

| Annotation        | Purpose                                         |
| ----------------- | ----------------------------------------------- |
| `@Entity`         | Marks class as a JPA entity (mapped to a table) |
| `@Table`          | Specifies the table name in the database        |
| `@Id`             | Marks the primary key field                     |
| `@GeneratedValue` | Defines how primary key values are generated    |

---

## 46. How do you handle one-to-many and many-to-many relationships?

Handling relationships between entities is a core part of using JPA and Spring Data JPA. Let me explain how to manage **One-to-Many** and **Many-to-Many** relationships with examples.

---

## 1️⃣ One-to-Many Relationship

**Scenario:** One **Parent** entity has many **Child** entities.

### Example: One `Author` has many `Books`

### Entity Definitions:

```java
@Entity
public class Author {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    // One author can write many books
    @OneToMany(mappedBy = "author", cascade = CascadeType.ALL, orphanRemoval = true)
    private List<Book> books = new ArrayList<>();

    // getters and setters
}
```

```java
@Entity
public class Book {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String title;

    // Many books belong to one author
    @ManyToOne
    @JoinColumn(name = "author_id")
    private Author author;

    // getters and setters
}
```

### Key Points:

* `@OneToMany(mappedBy = "author")`: The `mappedBy` attribute tells JPA that the `author` field in `Book` owns the relationship.
* `@ManyToOne` in `Book`: Points back to `Author`.
* `cascade = CascadeType.ALL`: Changes to `Author` cascade to its `Books`.
* `orphanRemoval = true`: Removes child entities if removed from parent's collection.

---

## 2️⃣ Many-to-Many Relationship

**Scenario:** Multiple `Student`s enroll in multiple `Course`s.

### Entity Definitions:

```java
@Entity
public class Student {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    @ManyToMany
    @JoinTable(
      name = "student_course",
      joinColumns = @JoinColumn(name = "student_id"),
      inverseJoinColumns = @JoinColumn(name = "course_id")
    )
    private Set<Course> courses = new HashSet<>();

    // getters and setters
}
```

```java
@Entity
public class Course {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String title;

    @ManyToMany(mappedBy = "courses")
    private Set<Student> students = new HashSet<>();

    // getters and setters
}
```

### Key Points:

* Use `@ManyToMany` on both sides.
* `@JoinTable` defines the join table and foreign keys.
* `mappedBy` on the inverse side specifies the owning side (`Student` owns the relationship here).

---

## Summary Table

| Relationship | Annotation(s)                | Notes                         |
| ------------ | ---------------------------- | ----------------------------- |
| One-to-Many  | `@OneToMany` + `@ManyToOne`  | Use `mappedBy` on One side    |
| Many-to-Many | `@ManyToMany` + `@JoinTable` | Join table holds associations |

---

## Additional Tips:

* Always maintain both sides of the relationship in code to avoid inconsistencies.
* Consider `cascade` and `orphanRemoval` depending on your use case.
* Use `Set` for `@ManyToMany` to avoid duplicates.

---

## 47. What is the `@Transactional` annotation?

The `@Transactional` annotation is super important in Spring for managing database transactions declaratively.

---

## ✅ What is `@Transactional`?

* It’s an annotation that **defines the scope of a single database transaction**.
* Ensures that a set of operations either **complete successfully as a whole** or **roll back entirely** if any error occurs.
* Helps maintain **data integrity** and **consistency**.

---

## ✅ How Does It Work?

When a method is annotated with `@Transactional`:

* Spring starts a database transaction before the method runs.
* If the method completes without exceptions, Spring **commits** the transaction (saves changes).
* If a runtime exception occurs, Spring **rolls back** the transaction (undoes changes).

---

## ✅ Where to Use It?

Typically on:

* Service layer methods where you want atomic operations.
* Repository methods if needed (less common with Spring Data JPA since it manages transactions).

---

## ✅ Example

```java
@Service
public class UserService {

    @Autowired
    private UserRepository userRepository;

    @Transactional
    public void createUserAndUpdateStats(User user) {
        userRepository.save(user);
        // some other database operations
        // if any exception here, all changes roll back
    }
}
```

---

## ✅ Important Notes

* By default, only **unchecked exceptions (runtime exceptions)** cause rollback.
* You can customize rollback behavior using attributes like `rollbackFor`:

```java
@Transactional(rollbackFor = Exception.class)
public void someMethod() {
    // rolls back even for checked exceptions
}
```

* Transactions are usually **proxy-based**, so `@Transactional` on private methods or self-invocations may not work as expected.

---

## ✅ Summary Table

| Feature              | Description                                  |
| -------------------- | -------------------------------------------- |
| Start transaction    | Before method execution                      |
| Commit transaction   | After successful execution                   |
| Rollback transaction | On runtime exception or configured exception |
| Declarative          | No need for manual transaction code          |

---

Would you like me to explain how Spring manages transactions internally or show how to configure transaction managers?

---

## 48. How do you configure an embedded database?

Great question! Spring Boot makes it really easy to configure and use embedded databases for development and testing. Embedded databases run **in-memory** or as lightweight local files, so you don’t need to install or configure an external database server.

---

## ✅ What is an Embedded Database?

An embedded database runs **within your application process**, typically for lightweight use cases like testing or prototyping. Common embedded databases in Java/Spring Boot include:

* **H2** (most popular)
* **HSQLDB**
* **Derby**

---

## ✅ How to Configure an Embedded Database in Spring Boot?

### 1. **Add the Dependency**

For example, add H2 dependency in your `pom.xml` (Maven):

```xml
<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
    <scope>runtime</scope>
</dependency>
```

Or in Gradle:

```groovy
runtimeOnly 'com.h2database:h2'
```

---

### 2. **Configure in `application.properties`**

By default, Spring Boot auto-configures an embedded database if it finds H2 (or other embedded db) on the classpath **and** no external datasource is configured.

Example configuration for H2:

```properties
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=
spring.h2.console.enabled=true
spring.jpa.hibernate.ddl-auto=update
```

* `jdbc:h2:mem:testdb` means an **in-memory** H2 database named `testdb`.
* `spring.h2.console.enabled=true` enables the H2 web console at `/h2-console`.

---

### 3. **Access H2 Console**

* Start your Spring Boot app.
* Open browser and navigate to `http://localhost:8080/h2-console`.
* Use JDBC URL `jdbc:h2:mem:testdb`, username `sa`, and empty password (default).
* You can execute SQL queries and browse tables.

---

### 4. **No Manual Configuration Needed**

If you just include H2 in your dependencies and **don’t provide an external datasource config**, Spring Boot:

* Automatically creates an in-memory H2 database.
* Sets up a DataSource bean.
* Configures Hibernate or JPA to use the embedded database.

---

## ✅ Summary

| Step                         | Description                            |
| ---------------------------- | -------------------------------------- |
| Add embedded DB dependency   | H2, HSQLDB, Derby                      |
| (Optional) Configure URL     | `jdbc:h2:mem:testdb` for in-memory     |
| Enable console (optional)    | `spring.h2.console.enabled=true`       |
| No external DB config needed | Spring Boot auto-configures DataSource |

---

## 49. What is the difference between JPA and Hibernate?

The terms **JPA** and **Hibernate** are often mentioned together but they refer to different concepts. Here's a clear breakdown:

---

## ✅ What is JPA?

* **JPA (Java Persistence API)** is a **specification** — a set of interfaces and rules for managing relational data in Java.
* It defines a standard way to map Java objects (entities) to database tables.
* JPA itself **does not provide an implementation**; it's just an API specification.
* Part of the **Java EE (Jakarta EE)** specification but usable in Java SE.

---

## ✅ What is Hibernate?

* **Hibernate** is a **popular implementation** of the JPA specification.
* It’s an ORM (Object-Relational Mapping) tool that implements JPA interfaces and adds many extra features.
* Provides the actual code that interacts with the database.
* Offers features beyond JPA, like caching, advanced querying, and more.

---

## ✅ Key Differences

| Aspect   | JPA                          | Hibernate                                     |
| -------- | ---------------------------- | --------------------------------------------- |
| Type     | Specification (API)          | Implementation (ORM framework)                |
| Purpose  | Defines interfaces for ORM   | Implements those interfaces                   |
| Vendor   | Java Community Process (JCP) | Red Hat / JBoss                               |
| Features | Basic ORM mapping & querying | Extended features like caching, multi-tenancy |
| Usage    | Code against interfaces      | Use Hibernate-specific features if needed     |

---

## ✅ How They Work Together

* When you use JPA in your Spring Boot project, you usually pick an implementation — **Hibernate is the default**.
* You write your code using **JPA annotations and interfaces** (`@Entity`, `EntityManager`, `JpaRepository`).
* Under the hood, Hibernate executes those operations against the database.

---

## ✅ Example

```java
@Entity  // JPA annotation
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
}
```

* The above uses JPA annotations.
* Hibernate processes those annotations and generates SQL queries to persist `User`.

---

## ✅ Summary

* **JPA** = The rules & API for ORM in Java.
* **Hibernate** = A popular ORM framework that implements JPA and offers more features.

---

## 50. How do you enable pagination and sorting with Spring Data?

Pagination and sorting are essential features when dealing with large datasets in Spring Data JPA. Spring Data provides built-in support to handle both easily.

---

## ✅ How to Enable Pagination and Sorting in Spring Data JPA?

---

### 1. Use `PagingAndSortingRepository` or extend `JpaRepository`

* `JpaRepository` extends `PagingAndSortingRepository`, so if your repository interface extends `JpaRepository`, you already have pagination and sorting support.

```java
public interface UserRepository extends JpaRepository<User, Long> {
    // no extra code needed
}
```

---

### 2. Use `Pageable` and `Sort` in Repository Methods

* The methods `findAll(Pageable pageable)` and `findAll(Sort sort)` are available by default.

---

### 3. Example: Pagination with `Pageable`

```java
@Autowired
private UserRepository userRepository;

public Page<User> getUsers(int page, int size) {
    Pageable pageable = PageRequest.of(page, size);
    return userRepository.findAll(pageable);
}
```

* `PageRequest.of(page, size)` creates a `Pageable` object (page index starts from 0).
* The returned `Page<User>` includes pagination info like total pages, total elements, current page, etc.

---

### 4. Example: Sorting with `Sort`

```java
public List<User> getUsersSorted() {
    Sort sort = Sort.by(Sort.Direction.ASC, "lastName");
    return userRepository.findAll(sort);
}
```

* Sort by `lastName` in ascending order.
* You can combine multiple sorting fields.

---

### 5. Pagination + Sorting Together

```java
public Page<User> getUsersPageSorted(int page, int size) {
    Pageable pageable = PageRequest.of(page, size, Sort.by("lastName").descending());
    return userRepository.findAll(pageable);
}
```

---

## ✅ Using Pagination and Sorting in REST Controller

You can also accept pagination and sorting parameters from the client:

```java
@GetMapping("/users")
public Page<User> getUsers(
    @RequestParam(defaultValue = "0") int page,
    @RequestParam(defaultValue = "10") int size,
    @RequestParam(defaultValue = "lastName") String sortBy
) {
    Pageable pageable = PageRequest.of(page, size, Sort.by(sortBy));
    return userRepository.findAll(pageable);
}
```

---

## ✅ Summary

| Feature      | How to Use                                                               |
| ------------ | ------------------------------------------------------------------------ |
| Pagination   | Use `Pageable` parameter in repository methods and `Page<T>` return type |
| Sorting      | Use `Sort` parameter or combine with `Pageable`                          |
| Repository   | Extend `JpaRepository` or `PagingAndSortingRepository`                   |
| REST support | Accept pagination/sorting parameters from client requests                |

---

## 51. What is `EntityManager`?

`EntityManager` is a core concept in JPA and very important when working with persistence.

---

## ✅ What is `EntityManager`?

* It’s the **main interface** used by JPA to **interact with the persistence context** (the set of entities managed by JPA during a transaction).
* Responsible for managing the lifecycle of entities: persisting, removing, finding, and querying entities.
* Acts as a **bridge** between your Java application and the database.

---

## ✅ Key Responsibilities of `EntityManager`

| Operation                   | Description                                       |
| --------------------------- | ------------------------------------------------- |
| `persist(Object entity)`    | Insert a new entity into the database             |
| `find(Class<T>, Object id)` | Retrieve an entity by its primary key             |
| `merge(Object entity)`      | Update an existing entity or save detached entity |
| `remove(Object entity)`     | Delete an entity from the database                |
| `createQuery()`             | Create JPQL queries                               |
| `flush()`                   | Synchronize persistence context with the database |
| `clear()`                   | Detach all entities from persistence context      |

---

## ✅ How is `EntityManager` Used?

* Usually injected by the container or framework (like Spring) into DAO or repository classes.

Example in Spring:

```java
@Repository
public class UserRepository {

    @PersistenceContext
    private EntityManager entityManager;

    public void save(User user) {
        entityManager.persist(user);
    }

    public User find(Long id) {
        return entityManager.find(User.class, id);
    }
}
```

---

## ✅ Relationship with Spring Data JPA

* Spring Data JPA internally uses `EntityManager` to implement CRUD and query operations.
* When you use `JpaRepository`, you’re indirectly using `EntityManager` behind the scenes.
* You can get `EntityManager` if you need custom queries or more control.

---

## ✅ Summary

| Term            | Description                                              |
| --------------- | -------------------------------------------------------- |
| `EntityManager` | JPA interface for managing entity lifecycle and querying |
| Manages         | Persist, find, update, delete entities                   |
| Injected via    | `@PersistenceContext` annotation                         |
| Used by         | DAO/repository layers or Spring Data internally          |

---

## 52. What is Lazy vs Eager fetching?

**Lazy** and **Eager fetching** are important concepts in JPA/Hibernate that control **when related entities are loaded from the database**.

---

## ✅ What is Fetching in JPA?

Fetching determines **when** associated entities (like in relationships: `@OneToMany`, `@ManyToOne`, etc.) are loaded — either immediately or when accessed.

---

## ✅ Eager Fetching (`FetchType.EAGER`)

* The related entities are **loaded immediately** along with the parent entity.
* Happens **in the same query** (usually via a join) or as immediate subsequent queries.
* Useful when you *always* need the related data.

### Example:

```java
@OneToMany(fetch = FetchType.EAGER)
private List<Book> books;
```

**Behavior:** When you load an `Author`, all their `books` are fetched right away.

---

## ✅ Lazy Fetching (`FetchType.LAZY`)

* The related entities are loaded **only when accessed for the first time** (on demand).
* JPA returns a **proxy** or placeholder initially.
* Helps improve performance by **loading only what you need**.
* Default for `@OneToMany` and `@ManyToMany`.

### Example:

```java
@OneToMany(fetch = FetchType.LAZY)
private List<Book> books;
```

**Behavior:** When you load an `Author`, books are NOT loaded until you call `author.getBooks()`.

---

## ✅ Default Fetch Types

| Relationship  | Default Fetch Type |
| ------------- | ------------------ |
| `@ManyToOne`  | EAGER              |
| `@OneToMany`  | LAZY               |
| `@ManyToMany` | LAZY               |
| `@OneToOne`   | EAGER              |

---

## ✅ Why Does It Matter?

* **Eager fetching** can cause **performance issues** and **too much data loaded** if not needed.
* **Lazy fetching** can cause **`LazyInitializationException`** if accessed outside a transaction/session.

---

## ✅ Example Scenario of LazyInitializationException

```java
@Transactional
public Author getAuthor(Long id) {
    Author author = authorRepo.findById(id).get();
    // session open here, lazy loads work fine
    return author;
}

// Later in controller or service, if you try to access author.getBooks() outside transaction/session:
// Throws LazyInitializationException because books were never loaded.
```

---

## ✅ How to Handle Lazy Loading?

* Access lazy data **within a transaction**.
* Use **fetch joins** in JPQL to load associations eagerly on demand.
* Use **DTO projections** or **entity graphs** for optimized fetching.

---

## ✅ Summary Table

| Fetch Type | When Entities Are Loaded       | Use Case                           | Default for                 |
| ---------- | ------------------------------ | ---------------------------------- | --------------------------- |
| EAGER      | Immediately with parent entity | When related data is always needed | `@ManyToOne`, `@OneToOne`   |
| LAZY       | On-demand when accessed        | To improve performance             | `@OneToMany`, `@ManyToMany` |

---

## 53. What is a DTO and how do you use it?

**DTO** stands for **Data Transfer Object** and it's a key pattern in designing clean, maintainable applications, especially with Spring Boot APIs.

---

## ✅ What is a DTO?

* A **DTO** is a **plain Java object** that carries data between processes, usually between the server and client.
* It **only contains fields** and **no business logic**.
* Used to **transfer data** without exposing the internal domain or entity models directly.
* Helps **decouple** the API layer from the persistence layer.

---

## ✅ Why Use DTOs?

| Reason                       | Explanation                                            |
| ---------------------------- | ------------------------------------------------------ |
| Encapsulation                | Hide internal entity structure or sensitive fields     |
| Control Data Flow            | Send only the necessary data to clients                |
| Avoid Lazy Loading Issues    | Prevent serialization problems caused by entities      |
| API Versioning & Flexibility | Customize response structure without changing entities |
| Security                     | Avoid exposing sensitive data or fields                |

---

## ✅ How to Use DTOs?

1. **Create DTO Classes**

Example DTO for User:

```java
public class UserDTO {
    private String name;
    private String email;

    // constructors, getters, setters
}
```

2. **Map Entity to DTO**

You can manually map:

```java
public UserDTO convertToDto(User user) {
    UserDTO dto = new UserDTO();
    dto.setName(user.getName());
    dto.setEmail(user.getEmail());
    return dto;
}
```

Or use libraries like **ModelMapper** or **MapStruct** for automatic mapping.

3. **Use DTO in Controller**

Return DTOs from REST controllers instead of entities:

```java
@GetMapping("/users/{id}")
public UserDTO getUser(@PathVariable Long id) {
    User user = userRepository.findById(id).orElseThrow();
    return convertToDto(user);
}
```

---

## ✅ Example Scenario

Suppose your `User` entity has a password field you don’t want to expose via API:

```java
@Entity
public class User {
    private Long id;
    private String name;
    private String email;
    private String password; // sensitive data
}
```

Your `UserDTO` excludes the password:

```java
public class UserDTO {
    private String name;
    private String email;
}
```

---

## ✅ Summary

| Aspect   | Details                                        |
| -------- | ---------------------------------------------- |
| Purpose  | Transfer data safely between layers or systems |
| Contains | Only data fields, no logic                     |
| Benefits | Security, flexibility, decoupling              |
| Mapping  | Manual or via mapping libraries                |

---

## 54. How do you map native SQL queries?

In Spring Data JPA, you can map **native SQL queries** when JPQL (Java Persistence Query Language) doesn't fit your needs—like when you want database-specific SQL features or complex queries.

---

## ✅ What is a Native Query?

* A **native query** is a plain SQL query sent directly to the database.
* Unlike JPQL, it uses **database-specific SQL syntax**.
* Sometimes needed for performance or advanced SQL features.

---

## ✅ How to Map Native Queries in Spring Data JPA?

### 1. Using `@Query` Annotation with `nativeQuery = true`

You can write native SQL queries directly on repository methods.

```java
public interface UserRepository extends JpaRepository<User, Long> {

    @Query(value = "SELECT * FROM users WHERE status = ?1", nativeQuery = true)
    List<User> findUsersByStatusNative(String status);
}
```

* `nativeQuery = true` tells Spring Data this is a native SQL query.
* Table and column names must match the database schema.

---

### 2. Returning Entities or Projections

* If your query returns all columns matching your entity, Spring Data maps results to entity objects.
* You can also return **DTO projections** by selecting specific columns and mapping with a constructor or interface.

---

### 3. Mapping to DTO with `@SqlResultSetMapping` (Advanced)

If you want custom mapping of a native query result to a DTO (non-entity), you can:

* Define a result set mapping on your entity class.
* Use `EntityManager` to run the query.

Example:

```java
@SqlResultSetMapping(
    name = "UserDTOMapping",
    classes = @ConstructorResult(
        targetClass = UserDTO.class,
        columns = {
            @ColumnResult(name = "name"),
            @ColumnResult(name = "email")
        }
    )
)
@Entity
public class User {
    // fields...
}
```

Then, in repository or service:

```java
List<UserDTO> dtos = entityManager.createNativeQuery(
    "SELECT name, email FROM users WHERE status = :status", "UserDTOMapping")
    .setParameter("status", "ACTIVE")
    .getResultList();
```

---

### 4. Using `EntityManager` for Native Queries

```java
@Autowired
private EntityManager entityManager;

public List<User> findUsersByStatus(String status) {
    Query query = entityManager.createNativeQuery("SELECT * FROM users WHERE status = ?", User.class);
    query.setParameter(1, status);
    return query.getResultList();
}
```

---

## ✅ Summary

| Method                     | Description                             |
| -------------------------- | --------------------------------------- |
| `@Query(nativeQuery=true)` | Write native SQL directly in repository |
| `EntityManager`            | Run native queries programmatically     |
| `@SqlResultSetMapping`     | Map complex native results to DTOs      |

---

## 55. How do you integrate Spring Boot with MySQL/PostgreSQL?

Integrating **Spring Boot** with relational databases like **MySQL** or **PostgreSQL** is common and straightforward thanks to Spring Boot’s auto-configuration and starter dependencies.

---

## ✅ Steps to Integrate Spring Boot with MySQL/PostgreSQL

---

### 1. Add Database Dependency

In your **`pom.xml`** (for Maven) or **`build.gradle`** (for Gradle), add the JDBC driver dependency.

**For MySQL:**

```xml
<!-- Maven -->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <scope>runtime</scope>
</dependency>
```

**For PostgreSQL:**

```xml
<!-- Maven -->
<dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
    <scope>runtime</scope>
</dependency>
```

Also, include Spring Boot starter for JPA:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```

---

### 2. Configure `application.properties` or `application.yml`

Add your database connection settings.

**For MySQL:**

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/mydatabase
spring.datasource.username=root
spring.datasource.password=yourpassword
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL8Dialect
```

**For PostgreSQL:**

```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/mydatabase
spring.datasource.username=postgres
spring.datasource.password=yourpassword
spring.datasource.driver-class-name=org.postgresql.Driver

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.PostgreSQLDialect
```

---

### 3. Define Your Entity Classes

Example:

```java
@Entity
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
    private String email;
    // getters & setters
}
```

---

### 4. Create Repository Interface

```java
public interface UserRepository extends JpaRepository<User, Long> {}
```

---

### 5. Run the Application

* Spring Boot will auto-configure the data source and JPA based on your settings.
* It will connect to the database and create/update tables as per your entities (`ddl-auto=update`).
* You can then perform CRUD operations via your repositories.

---

## ✅ Optional Tips

* Use **connection pool** (e.g., HikariCP is default in Spring Boot).
* Set `spring.jpa.hibernate.ddl-auto` to `validate` or `none` in production.
* Use **Flyway** or **Liquibase** for database migrations.

---

## Summary

| Step                  | Description                                |
| --------------------- | ------------------------------------------ |
| Add JDBC Driver       | Include MySQL/PostgreSQL driver dependency |
| Configure DataSource  | Set DB URL, username, password, driver     |
| Set Hibernate Dialect | Specify correct SQL dialect for DB         |
| Define Entities       | Use `@Entity` classes                      |
| Use Spring Data JPA   | Repositories for DB operations             |

---

## 56. What is optimistic locking and how do you implement it?

**Optimistic locking** is a concurrency control mechanism used to prevent **lost updates** when multiple transactions try to update the same data simultaneously, especially in web applications.

---

## ✅ What is Optimistic Locking?

* Assumes **multiple transactions can complete without interfering**.
* Does **not lock the database rows** when reading.
* Checks for data conflicts **only at the time of update**.
* If a conflict is detected (someone else updated the data first), the transaction **fails** and can be retried.
* Helps maintain **data integrity** without heavy locking overhead.

---

## ✅ How Does Optimistic Locking Work?

* Each entity has a **version** attribute that increments on each update.
* When updating, JPA checks if the version in the DB matches the version in the entity.
* If versions differ, it means another transaction has updated the row, and an exception is thrown.

---

## ✅ How to Implement Optimistic Locking in Spring Boot / JPA?

### 1. Add a `@Version` field to your entity

```java
@Entity
public class Product {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;
    private double price;

    @Version
    private Integer version; // version field for optimistic locking

    // getters and setters
}
```

* The `@Version` field can be of type `Integer`, `Long`, `Timestamp`, etc.
* JPA uses this field to track changes.

---

### 2. What happens during update?

* When a transaction fetches the entity, it reads the current version.
* When it tries to update, it adds a condition like `WHERE id = ? AND version = ?`.
* If no rows are affected (meaning the version changed), JPA throws an **`OptimisticLockException`**.

---

### 3. Handling `OptimisticLockException`

You should catch this exception and handle it properly, for example:

* Inform the user the data has changed.
* Retry the transaction.
* Log and abort.

---

### 4. Example in Service Layer

```java
@Transactional
public void updateProduct(Long id, String newName, double newPrice) {
    Product product = productRepository.findById(id)
                          .orElseThrow(() -> new RuntimeException("Product not found"));

    product.setName(newName);
    product.setPrice(newPrice);

    // when transaction commits, version is checked
}
```

If another transaction updates the same product meanwhile, this update will fail with `OptimisticLockException`.

---

## ✅ Why Use Optimistic Locking?

* Useful when **conflicts are rare**.
* Avoids performance issues from locking.
* Suitable for **highly concurrent applications** where you want to minimize locking overhead.

---

## ✅ Summary

| Feature     | Details                                |
| ----------- | -------------------------------------- |
| What        | Concurrency control technique          |
| How         | Use `@Version` field in entity         |
| Behavior    | Checks version before updating         |
| On Conflict | Throws `OptimisticLockException`       |
| Use Case    | Low conflict, high concurrency systems |

---

## 57. What is the N+1 select problem?

The **N+1 select problem** is a common performance issue in ORMs like JPA/Hibernate that can cause serious inefficiencies in database access.

---

## ✅ What is the N+1 Select Problem?

* When fetching a list of entities (N entities), **1 query** is executed to fetch the main entities, and then **N additional queries** are executed to fetch related entities **one-by-one**.
* This leads to **N+1 queries** instead of a single optimized query with joins.
* Causes **significant performance degradation**, especially with large data sets.

---

## ✅ How Does It Happen?

Consider you have two entities:

```java
@Entity
public class Author {
    @Id
    private Long id;

    private String name;

    @OneToMany(mappedBy = "author", fetch = FetchType.LAZY)
    private List<Book> books;
}

@Entity
public class Book {
    @Id
    private Long id;

    private String title;

    @ManyToOne
    private Author author;
}
```

---

### Scenario:

You fetch **all authors** and then access their books:

```java
List<Author> authors = authorRepository.findAll();

for (Author author : authors) {
    System.out.println(author.getBooks().size());
}
```

---

### What happens behind the scenes?

1. **Query 1:** Fetch all authors (`SELECT * FROM author`)
2. **Queries 2 to N+1:** For each author, fetch their books (`SELECT * FROM book WHERE author_id = ?`)

If there are 100 authors, this results in **1 + 100 = 101 queries**.

---

## ✅ Why is N+1 Problem Bad?

* Many small queries cause **high latency**.
* Increased load on database.
* Poor scalability.

---

## ✅ How to Fix N+1 Problem?

### 1. Use **Eager Fetching** (cautiously)

Change fetch type to `EAGER`:

```java
@OneToMany(fetch = FetchType.EAGER)
private List<Book> books;
```

But beware: eager fetching everywhere can cause other performance problems (fetching too much data).

---

### 2. Use **`JOIN FETCH` in JPQL**

Fetch associations in a single query using `JOIN FETCH`:

```java
@Query("SELECT a FROM Author a JOIN FETCH a.books")
List<Author> findAllAuthorsWithBooks();
```

This executes one query with a join, loading authors and their books together.

---

### 3. Use **Entity Graphs**

Define fetch graphs to specify which associations to load eagerly at runtime without changing entity annotations.

```java
@EntityGraph(attributePaths = {"books"})
List<Author> findAll();
```

---

### 4. Batch Fetching (Hibernate-specific)

Configure Hibernate to batch load collections or entities.

---

## ✅ Summary Table

| Problem                     | Solution                                    |
| --------------------------- | ------------------------------------------- |
| N+1 queries                 | Use `JOIN FETCH` or Entity Graphs           |
| Lazy fetch causes N queries | Use batch fetching or eager fetch carefully |

---

## 58. What are projections in Spring Data JPA?

**Projections** in Spring Data JPA are a powerful way to **select and retrieve only specific parts (fields)** of an entity instead of fetching the entire entity. This improves performance and reduces unnecessary data transfer.

---

## ✅ What are Projections?

* Projections allow you to **fetch subsets of entity attributes**.
* Useful when you don't need all fields of an entity.
* Can be **interface-based** or **class-based** (DTO projections).
* Help optimize queries and improve application efficiency.

---

## ✅ Types of Projections in Spring Data JPA

### 1. Interface-based Projections

* Define an interface with **getter methods** for fields you want.
* Spring Data will dynamically create implementations for you.

**Example:**

```java
public interface UserNameOnly {
    String getName();
}
```

Repository method:

```java
List<UserNameOnly> findByActive(boolean active);
```

---

### 2. Class-based (DTO) Projections

* Create a DTO class with a constructor matching the selected fields.
* Use JPQL constructor expression in the repository query.

**Example:**

```java
public class UserDTO {
    private String name;
    private String email;

    public UserDTO(String name, String email) {
        this.name = name;
        this.email = email;
    }
    // getters
}
```

Repository method:

```java
@Query("SELECT new com.example.UserDTO(u.name, u.email) FROM User u WHERE u.active = true")
List<UserDTO> findActiveUsers();
```

---

### 3. Dynamic Projections

* Repository methods can return different projection types based on method signature.

Example:

```java
<T> List<T> findByActive(boolean active, Class<T> type);
```

Called as:

```java
List<UserNameOnly> users = userRepository.findByActive(true, UserNameOnly.class);
```

---

## ✅ Benefits of Projections

* Reduces data transfer size.
* Avoids fetching lazy-loaded associations unnecessarily.
* Improves performance.
* Helps with API design by sending only relevant data.

---

## ✅ Summary Table

| Projection Type   | Description                                  | Example Return Type     |
| ----------------- | -------------------------------------------- | ----------------------- |
| Interface-based   | Interface with getters for selected fields   | `List<UserNameOnly>`    |
| Class-based (DTO) | DTO class with constructor                   | `List<UserDTO>`         |
| Dynamic           | Generic method returning any projection type | `List<T>` with Class<T> |

---

## 59. What are Specifications and Criteria API?

Both **Specifications** and the **Criteria API** in Spring Data JPA help you build **dynamic, type-safe queries** programmatically without writing raw SQL or JPQL strings. They’re especially useful for complex search/filter operations.

---

## ✅ What is Criteria API?

* Part of **JPA specification** (javax.persistence.criteria).
* Allows building **type-safe, dynamic queries** using Java objects instead of query strings.
* Uses objects like `CriteriaBuilder`, `CriteriaQuery`, and `Root` to construct queries.

### Example:

```java
CriteriaBuilder cb = entityManager.getCriteriaBuilder();
CriteriaQuery<User> query = cb.createQuery(User.class);
Root<User> user = query.from(User.class);

Predicate namePredicate = cb.equal(user.get("name"), "Alice");
query.where(namePredicate);

List<User> result = entityManager.createQuery(query).getResultList();
```

---

## ✅ What is Specification?

* A **Spring Data JPA abstraction** built on top of Criteria API.
* Provides a **clean way to build reusable predicates** for queries.
* Implements the `Specification<T>` interface with a method:

```java
Predicate toPredicate(Root<T> root, CriteriaQuery<?> query, CriteriaBuilder cb);
```

* You can combine Specifications with `and()`, `or()`, etc.

---

## ✅ Why Use Specifications?

* To build **complex queries dynamically** at runtime.
* To **compose queries** by combining simple Specifications.
* Improves **code readability** and reusability.
* Works well with Spring Data JPA repositories.

---

## ✅ How to Use Specifications in Spring Boot

### 1. Create Specification

```java
public class UserSpecifications {
    public static Specification<User> hasName(String name) {
        return (root, query, cb) -> cb.equal(root.get("name"), name);
    }

    public static Specification<User> hasEmail(String email) {
        return (root, query, cb) -> cb.equal(root.get("email"), email);
    }
}
```

### 2. Use Specification in Repository

Make your repository extend `JpaSpecificationExecutor<T>`:

```java
public interface UserRepository extends JpaRepository<User, Long>, JpaSpecificationExecutor<User> {}
```

### 3. Query with Specifications

```java
Specification<User> spec = Specification.where(UserSpecifications.hasName("Alice"))
                                        .and(UserSpecifications.hasEmail("alice@example.com"));

List<User> users = userRepository.findAll(spec);
```

---

## ✅ Summary

| Concept       | Description                                                             |
| ------------- | ----------------------------------------------------------------------- |
| Criteria API  | JPA's way to build type-safe queries programmatically                   |
| Specification | Spring Data abstraction using Criteria API to build reusable predicates |
| Usage         | Combine predicates dynamically for complex queries                      |

---

## 60. How to use dynamic queries with Spring Data?

Building **dynamic queries** in Spring Data means creating database queries that can change based on the input parameters or conditions at runtime, without writing a separate query for each case.

---

## ✅ Ways to Use Dynamic Queries with Spring Data

---

### 1. **Using `JpaSpecificationExecutor` and Specifications**

This is the most flexible way to create dynamic queries by composing predicates.

* Your repository extends `JpaSpecificationExecutor<T>`.
* Build dynamic `Specification<T>` instances depending on input.

**Example:**

```java
public interface UserRepository extends JpaRepository<User, Long>, JpaSpecificationExecutor<User> {}
```

Create Specifications dynamically:

```java
public class UserSpecifications {
    public static Specification<User> hasName(String name) {
        return (root, query, cb) -> name == null ? null : cb.equal(root.get("name"), name);
    }
    
    public static Specification<User> hasEmail(String email) {
        return (root, query, cb) -> email == null ? null : cb.equal(root.get("email"), email);
    }
}
```

Use in service:

```java
Specification<User> spec = Specification.where(UserSpecifications.hasName(name))
                                       .and(UserSpecifications.hasEmail(email));

List<User> users = userRepository.findAll(spec);
```

This way, only non-null filters are applied.

---

### 2. **Query by Example (QBE)**

Spring Data supports **Query by Example** where you provide a probe (example entity), and Spring Data builds a query matching the non-null fields.

```java
User probe = new User();
probe.setName("Alice");

Example<User> example = Example.of(probe);
List<User> users = userRepository.findAll(example);
```

---

### 3. **Using `@Query` with SpEL or Dynamic JPQL**

You can write queries with conditional parts using SpEL or native queries, but this approach is limited and less flexible.

---

### 4. **Using QueryDSL**

If you integrate QueryDSL, you can build type-safe dynamic queries with fluent API.

---

### 5. **Programmatic JPQL or Criteria API**

You can use `EntityManager` with Criteria API to build dynamic queries manually.

---

## ✅ Summary Table

| Method                 | Description                         | Pros                    | Cons                        |
| ---------------------- | ----------------------------------- | ----------------------- | --------------------------- |
| Specifications         | Compose predicates dynamically      | Very flexible, reusable | Requires learning Specs API |
| Query by Example (QBE) | Example entity with matching fields | Easy to use             | Limited to simple queries   |
| `@Query` with SpEL     | Dynamic query strings               | Simple for small cases  | Limited flexibility         |
| QueryDSL               | Fluent, type-safe query building    | Powerful & readable     | Extra setup required        |
| Criteria API           | Programmatic query building         | Type-safe & flexible    | Verbose and complex         |

---

### 🔹 61–80: Spring Boot Security, Testing, & Configuration

## 61. How do you add security to a Spring Boot app?

Adding security to a Spring Boot application is essential to protect your app from unauthorized access, data breaches, and other threats. The most common way to secure a Spring Boot app is by using **Spring Security**, which is a powerful and highly customizable authentication and access-control framework.

---

## ✅ How to Add Security to a Spring Boot Application?

---

### 1. Add Spring Security Dependency

Add this to your `pom.xml` (Maven):

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
```

For Gradle:

```gradle
implementation 'org.springframework.boot:spring-boot-starter-security'
```

---

### 2. Basic Security Behavior Out of the Box

* By default, Spring Security **secures all HTTP endpoints**.
* It creates a **default user** with a generated password printed in the console.
* You can log in with this user to access protected endpoints.

---

### 3. Configure Custom Security (Optional but Recommended)

You can create a class that extends `WebSecurityConfigurerAdapter` (prior to Spring Security 6) or use the newer **component-based configuration** with beans (recommended in latest Spring Security versions):

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig {

    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        http
            .authorizeHttpRequests(authorize -> authorize
                .requestMatchers("/public/**").permitAll()  // Public URLs
                .anyRequest().authenticated()              // Others need auth
            )
            .formLogin(withDefaults())                      // Default login form
            .httpBasic(withDefaults());                      // Basic auth support

        return http.build();
    }

    @Bean
    public UserDetailsService users() {
        UserDetails user = User.builder()
                .username("user")
                .password("{noop}password")  // {noop} means no password encoding
                .roles("USER")
                .build();
        return new InMemoryUserDetailsManager(user);
    }
}
```

---

### 4. Common Security Features You Can Add

* **Authentication:** Validate user identity (login forms, basic auth, OAuth2).
* **Authorization:** Control access to resources (roles, permissions).
* **Password Encoding:** Use `BCryptPasswordEncoder` to store hashed passwords.
* **CSRF Protection:** Enabled by default for POST/PUT/DELETE.
* **JWT Token Authentication:** For stateless REST APIs.
* **OAuth2 / OpenID Connect:** Social logins or external identity providers.

---

### 5. Example: Securing REST APIs with JWT

* Use `spring-boot-starter-security` and `jjwt` or other JWT libs.
* Implement filter to check JWT tokens on each request.
* Configure stateless session management.

---

### 6. Disable Security (For Testing)

To disable Spring Security temporarily, add this in `application.properties`:

```properties
spring.security.enabled=false
```

or configure `http.authorizeHttpRequests().anyRequest().permitAll()` in your config.

---

## ✅ Summary

| Step                      | What it does                                    |
| ------------------------- | ----------------------------------------------- |
| Add dependency            | Pull in Spring Security libraries               |
| Default security          | Secures all endpoints with a default user       |
| Customize security config | Define users, roles, and URL access rules       |
| Add advanced features     | JWT, OAuth2, password encoding, CSRF protection |

---

## 62. What is Spring Security?

Here’s a detailed explanation:

---

## What is Spring Security?

**Spring Security** is a powerful and highly customizable **authentication and authorization framework** for Java applications, especially those built using the Spring ecosystem (like Spring Boot).

It provides comprehensive security services to protect your application from common vulnerabilities and attacks such as unauthorized access, CSRF, session fixation, clickjacking, and more.

---

## Key Features of Spring Security

* **Authentication:** Verifies user identity (e.g., login with username/password, OAuth2, LDAP).
* **Authorization:** Controls what authenticated users are allowed to do (role-based or permission-based access control).
* **Protection against attacks:** Includes CSRF protection, session management, clickjacking prevention.
* **Password encoding:** Supports secure password hashing algorithms like BCrypt.
* **Integration:** Works seamlessly with Spring MVC, REST APIs, method security, OAuth2, JWT.
* **Extensible:** Easily customizable to fit specific security requirements.

---

## How Spring Security Works

1. **Filters Chain:** Uses a chain of servlet filters to intercept HTTP requests and apply security logic.
2. **Authentication Manager:** Handles the process of authenticating user credentials.
3. **Security Context:** Stores details of the authenticated user for the current session or request.
4. **Access Decision Manager:** Decides if a user has permission to access a resource based on roles or authorities.

---

## Why Use Spring Security?

* Provides a solid and tested security foundation, saving development time.
* Easily configurable with annotations or Java config.
* Supports a wide range of authentication mechanisms.
* Keeps your application safe against many common security threats.

---

## Simple Example in Spring Boot

With minimal setup, Spring Boot + Spring Security secures all endpoints by default with HTTP Basic authentication.

Add dependency:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
```

Access protected URLs with default user/password generated at runtime or customize users and roles.

---

If you want, I can guide you through setting up Spring Security in a Spring Boot project with example code!

---

## 63. How does authentication and authorization work in Spring Security?

Great question! Understanding **authentication** and **authorization** is key to grasping how Spring Security protects applications. Here's a detailed explanation of how both work within Spring Security.

---

## Authentication vs Authorization

* **Authentication:** Verifying the identity of a user (Who are you?)
* **Authorization:** Determining if the authenticated user has permission to access a resource (What are you allowed to do?)

---

## How Authentication Works in Spring Security

1. **User Sends Credentials:**
   The user submits login credentials (e.g., username and password) via a login form, HTTP Basic Auth, OAuth2 flow, etc.

2. **Authentication Filter Intercepts Request:**
   Spring Security’s **filter chain** intercepts the request with filters like `UsernamePasswordAuthenticationFilter`.

3. **Authentication Manager Processes Credentials:**
   The filter creates an `Authentication` token (e.g., `UsernamePasswordAuthenticationToken`) with the credentials and passes it to the `AuthenticationManager`.

4. **Authentication Provider Validates Credentials:**
   The `AuthenticationManager` delegates to one or more `AuthenticationProvider`s (e.g., `DaoAuthenticationProvider` which uses a `UserDetailsService`).

5. **UserDetailsService Loads User:**
   The `UserDetailsService` loads user details (username, password, roles) from the database or another source.

6. **Password Verification:**
   The provided password is compared against the stored (usually encoded) password.

7. **Successful Authentication:**
   If valid, Spring Security creates a fully populated `Authentication` object, which is stored in the **SecurityContext**.

8. **SecurityContextHolder:**
   This holds the `Authentication` object and is associated with the current session or thread so Spring Security can identify the user on subsequent requests.

---

## How Authorization Works in Spring Security

1. **User Requests a Resource:**
   The authenticated user tries to access a secured URL or method.

2. **Security Filter Checks Access:**
   The Spring Security filter checks the current user’s `Authentication` object from the `SecurityContextHolder`.

3. **Access Decision Manager Evaluates:**
   The `AccessDecisionManager` compares the user's roles/authorities with the access rules configured (via annotations like `@PreAuthorize`, or URL security rules in config).

4. **Allow or Deny Access:**
   If the user has required permissions, access is granted. Otherwise, access is denied (usually HTTP 403 Forbidden).

---

## Summary Diagram

```plaintext
User Request
   ↓
Authentication Filter (e.g., UsernamePasswordAuthenticationFilter)
   ↓
AuthenticationManager --> AuthenticationProvider(s)
   ↓
UserDetailsService loads user data
   ↓
Password checked
   ↓
Authentication success → stored in SecurityContextHolder
   ↓
Authorization: Check user roles/permissions vs requested resource
   ↓
Access granted or denied
```

---

## Example: Basic Authentication Flow in Spring Boot

```java
@Override
protected void configure(HttpSecurity http) throws Exception {
    http
      .authorizeRequests()
        .antMatchers("/admin/**").hasRole("ADMIN")
        .anyRequest().authenticated()
      .and()
      .formLogin()
      .and()
      .httpBasic();
}
```

* Only users with role `ADMIN` can access `/admin/**`.
* All other requests require authentication.
* Login can be done via form or HTTP Basic.

---

## 64. How do you implement JWT authentication?

Implementing **JWT (JSON Web Token) authentication** in a Spring Boot app is a popular approach to build stateless, scalable REST APIs. JWTs allow clients to authenticate once and then send a signed token on every request to prove their identity.

---

# How to Implement JWT Authentication in Spring Boot: Step-by-Step

---

## 1. Add Required Dependencies

Add these to your `pom.xml`:

```xml
<!-- Spring Security -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>

<!-- JWT library -->
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt-api</artifactId>
    <version>0.11.5</version>
</dependency>
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt-impl</artifactId>
    <version>0.11.5</version>
    <scope>runtime</scope>
</dependency>
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt-jackson</artifactId>
    <version>0.11.5</version>
    <scope>runtime</scope>
</dependency>
```

---

## 2. Create a JWT Utility Class

Handles token creation and validation.

```java
@Component
public class JwtUtil {

    private final String SECRET_KEY = "mysecretkey"; // Use env vars or config in real apps

    public String generateToken(UserDetails userDetails) {
        return Jwts.builder()
                   .setSubject(userDetails.getUsername())
                   .setIssuedAt(new Date())
                   .setExpiration(Date.from(Instant.now().plus(1, ChronoUnit.HOURS)))
                   .signWith(SignatureAlgorithm.HS256, SECRET_KEY)
                   .compact();
    }

    public String extractUsername(String token) {
        return Jwts.parser()
                   .setSigningKey(SECRET_KEY)
                   .parseClaimsJws(token)
                   .getBody()
                   .getSubject();
    }

    public boolean validateToken(String token, UserDetails userDetails) {
        final String username = extractUsername(token);
        return (username.equals(userDetails.getUsername()) && !isTokenExpired(token));
    }

    private boolean isTokenExpired(String token) {
        Date expiration = Jwts.parser()
                              .setSigningKey(SECRET_KEY)
                              .parseClaimsJws(token)
                              .getBody()
                              .getExpiration();
        return expiration.before(new Date());
    }
}
```

---

## 3. Implement a Custom `UserDetailsService`

Loads user info from DB or in-memory.

```java
@Service
public class MyUserDetailsService implements UserDetailsService {
    @Override
    public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {
        // Lookup user from DB or any store
        if ("user".equals(username)) {
            return User.withUsername("user")
                       .password("{noop}password")  // {noop} = no encoding
                       .roles("USER")
                       .build();
        } else {
            throw new UsernameNotFoundException("User not found");
        }
    }
}
```

---

## 4. Create a JWT Request Filter

Intercepts requests, extracts and validates the JWT token.

```java
@Component
public class JwtRequestFilter extends OncePerRequestFilter {

    @Autowired
    private MyUserDetailsService userDetailsService;

    @Autowired
    private JwtUtil jwtUtil;

    @Override
    protected void doFilterInternal(HttpServletRequest request, HttpServletResponse response, FilterChain chain)
        throws ServletException, IOException {

        final String authorizationHeader = request.getHeader("Authorization");

        String username = null;
        String jwt = null;

        if (authorizationHeader != null && authorizationHeader.startsWith("Bearer ")) {
            jwt = authorizationHeader.substring(7);
            try {
                username = jwtUtil.extractUsername(jwt);
            } catch (Exception e) {
                // log or handle token parse error
            }
        }

        if (username != null && SecurityContextHolder.getContext().getAuthentication() == null) {
            UserDetails userDetails = this.userDetailsService.loadUserByUsername(username);
            if (jwtUtil.validateToken(jwt, userDetails)) {
                UsernamePasswordAuthenticationToken authToken =
                    new UsernamePasswordAuthenticationToken(userDetails, null, userDetails.getAuthorities());
                authToken.setDetails(new WebAuthenticationDetailsSource().buildDetails(request));

                SecurityContextHolder.getContext().setAuthentication(authToken);
            }
        }

        chain.doFilter(request, response);
    }
}
```

---

## 5. Configure Spring Security

Register the filter and configure endpoints.

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig {

    @Autowired
    private JwtRequestFilter jwtRequestFilter;

    @Autowired
    private MyUserDetailsService myUserDetailsService;

    @Bean
    public AuthenticationManager authenticationManager(AuthenticationConfiguration config) throws Exception {
        return config.getAuthenticationManager();
    }

    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        http.csrf().disable()
            .authorizeHttpRequests(auth -> auth
                .requestMatchers("/authenticate").permitAll()
                .anyRequest().authenticated())
            .sessionManagement(session -> session.sessionCreationPolicy(SessionCreationPolicy.STATELESS));

        http.addFilterBefore(jwtRequestFilter, UsernamePasswordAuthenticationFilter.class);

        return http.build();
    }
}
```

---

## 6. Create Authentication Controller

Endpoint to authenticate users and generate JWT token.

```java
@RestController
public class AuthController {

    @Autowired
    private AuthenticationManager authenticationManager;

    @Autowired
    private JwtUtil jwtUtil;

    @Autowired
    private MyUserDetailsService userDetailsService;

    @PostMapping("/authenticate")
    public ResponseEntity<?> createAuthToken(@RequestBody AuthRequest authRequest) throws Exception {
        try {
            authenticationManager.authenticate(
                new UsernamePasswordAuthenticationToken(authRequest.getUsername(), authRequest.getPassword())
            );
        } catch (BadCredentialsException e) {
            throw new Exception("Incorrect username or password", e);
        }

        final UserDetails userDetails = userDetailsService.loadUserByUsername(authRequest.getUsername());
        final String jwt = jwtUtil.generateToken(userDetails);

        return ResponseEntity.ok(new AuthResponse(jwt));
    }
}
```

---

## 7. Request and Response DTOs

```java
public class AuthRequest {
    private String username;
    private String password;
    // getters/setters
}

public class AuthResponse {
    private String jwt;

    public AuthResponse(String jwt) {
        this.jwt = jwt;
    }
    // getter
}
```

---

# Summary

| Step                  | Description                                     |
| --------------------- | ----------------------------------------------- |
| 1. Add dependencies   | Spring Security and JWT libs                    |
| 2. JWT Utility        | Create and validate tokens                      |
| 3. UserDetailsService | Load user info from DB or memory                |
| 4. JWT Filter         | Extract token from requests, validate, set auth |
| 5. Security Config    | Configure Spring Security and register filter   |
| 6. Auth Controller    | Authenticate user, generate JWT                 |
| 7. DTOs               | Request and response models                     |

---

## 65. How do you secure specific endpoints?

Securing specific endpoints in a Spring Boot application using Spring Security involves configuring **authorization rules** that specify which users or roles can access certain URLs or API paths.

---

## How to Secure Specific Endpoints in Spring Boot

You control access to endpoints primarily by configuring **URL-based authorization rules** in your Spring Security configuration.

---

### Step 1: Add Spring Security Dependency

Make sure you have this dependency:

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-security</artifactId>
</dependency>
```

---

### Step 2: Configure Security to Secure Specific Endpoints

You typically configure security in a class annotated with `@Configuration` and `@EnableWebSecurity`. Since Spring Security 5.7+, the recommended way is to define a `SecurityFilterChain` bean.

Here’s an example:

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig {

    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        http
            .csrf().disable()  // Disable CSRF for simplicity; enable in production
            .authorizeHttpRequests(authorize -> authorize
                .requestMatchers("/public/**").permitAll()     // Public endpoints accessible to everyone
                .requestMatchers("/admin/**").hasRole("ADMIN") // Only ADMIN role can access /admin/**
                .requestMatchers("/user/**").hasAnyRole("USER", "ADMIN") // USER or ADMIN roles
                .anyRequest().authenticated()                   // All other endpoints require authentication
            )
            .httpBasic();  // Enable HTTP Basic auth (you can use formLogin() or JWT etc.)

        return http.build();
    }

    @Bean
    public InMemoryUserDetailsManager userDetailsService() {
        UserDetails user = User.withDefaultPasswordEncoder()
            .username("user")
            .password("password")
            .roles("USER")
            .build();

        UserDetails admin = User.withDefaultPasswordEncoder()
            .username("admin")
            .password("password")
            .roles("ADMIN")
            .build();

        return new InMemoryUserDetailsManager(user, admin);
    }
}
```

---

### Explanation:

* `requestMatchers("/public/**").permitAll()` — Anyone can access URLs starting with `/public/`.
* `requestMatchers("/admin/**").hasRole("ADMIN")` — Only users with the `ADMIN` role can access `/admin/` paths.
* `requestMatchers("/user/**").hasAnyRole("USER", "ADMIN")` — Users with either `USER` or `ADMIN` roles can access `/user/`.
* `anyRequest().authenticated()` — All other endpoints require the user to be authenticated.

---

### Step 3: Test with Endpoints

Example endpoints:

```java
@RestController
public class DemoController {

    @GetMapping("/public/hello")
    public String publicHello() {
        return "Hello Public!";
    }

    @GetMapping("/user/hello")
    public String userHello() {
        return "Hello User!";
    }

    @GetMapping("/admin/hello")
    public String adminHello() {
        return "Hello Admin!";
    }
}
```

* Accessing `/public/hello` works without login.
* Accessing `/user/hello` requires login with `USER` or `ADMIN`.
* Accessing `/admin/hello` requires login with `ADMIN`.

---

### Additional Ways to Secure Specific Methods

You can also use **method-level security annotations** like:

* `@PreAuthorize("hasRole('ADMIN')")`
* `@Secured("ROLE_USER")`
* `@RolesAllowed("ROLE_ADMIN")`

Example:

```java
@RestController
public class MethodSecuredController {

    @PreAuthorize("hasRole('ADMIN')")
    @GetMapping("/secure/admin")
    public String adminOnly() {
        return "Admin access only";
    }
}
```

Enable method security by adding:

```java
@EnableMethodSecurity  // For Spring Security 6+
```

or

```java
@EnableGlobalMethodSecurity(prePostEnabled = true)  // For earlier versions
```

---

## Summary

| How to Secure | How to Configure                                                                     |
| ------------- | ------------------------------------------------------------------------------------ |
| URL-based     | Use `HttpSecurity.authorizeHttpRequests()` with `requestMatchers()` and role checks  |
| Method-based  | Use annotations like `@PreAuthorize`, `@Secured` on methods + enable method security |
| Roles & Users | Define roles and users via `UserDetailsService` or your user store                   |

---

## 66. What are roles and authorities?

Understanding **roles** and **authorities** is essential for managing security in Spring Security.

---

## What Are Roles and Authorities?

### Authorities

* Authorities represent **permissions** or **privileges** granted to a user.
* They are fine-grained and can be any string like `"READ_PRIVILEGES"`, `"WRITE_PRIVILEGES"`, `"DELETE_ACCOUNT"`.
* Internally, Spring Security treats these as simple strings (`GrantedAuthority` interface).

### Roles

* Roles are **special kinds of authorities** that represent a **group of authorities** or a user’s job function.
* Roles are usually prefixed with `"ROLE_"` by convention (e.g., `"ROLE_ADMIN"`, `"ROLE_USER"`).
* When you use `.hasRole("ADMIN")` in Spring Security, it actually checks for an authority `"ROLE_ADMIN"`.
* Roles simplify managing permissions by grouping multiple authorities.

---

## Key Differences

| Aspect              | Roles                                                   | Authorities                                                   |
| ------------------- | ------------------------------------------------------- | ------------------------------------------------------------- |
| Meaning             | High-level user category                                | Specific permission or action                                 |
| Naming              | Prefixed with `ROLE_`                                   | Any string                                                    |
| Usage               | Used for role-based access                              | Used for permission-based access                              |
| Spring Security API | `.hasRole("ADMIN")` checks for `"ROLE_ADMIN"` authority | `.hasAuthority("READ_PRIVILEGES")` checks for exact authority |

---

## Example

If a user has these authorities:

* `ROLE_ADMIN`
* `READ_PRIVILEGES`
* `WRITE_PRIVILEGES`

This means the user has the **admin role** plus the ability to read and write resources.

---

## How Roles and Authorities Are Used in Code

```java
// Assign roles to a user
UserDetails user = User.withUsername("john")
    .password("{noop}password")
    .roles("USER")  // Actually grants authority "ROLE_USER"
    .build();

// Assign authorities explicitly
UserDetails admin = User.withUsername("admin")
    .password("{noop}password")
    .authorities("ROLE_ADMIN", "READ_PRIVILEGES", "WRITE_PRIVILEGES")
    .build();
```

---

## Securing Endpoints

* `.hasRole("ADMIN")` → checks for `"ROLE_ADMIN"` authority
* `.hasAuthority("READ_PRIVILEGES")` → checks for exact authority

Example:

```java
http.authorizeHttpRequests(auth -> auth
    .requestMatchers("/admin/**").hasRole("ADMIN")
    .requestMatchers("/reports/**").hasAuthority("READ_PRIVILEGES")
);
```

---

## Summary

* **Roles** are high-level groupings of authorities with prefix `ROLE_`.
* **Authorities** are fine-grained permissions.
* Spring Security treats roles as a special kind of authority.
* Use roles for coarse access control and authorities for fine control.

---

## 67. How do you write unit tests in Spring Boot?

Writing **unit tests** in Spring Boot is crucial to ensure your application components work as expected. Spring Boot makes testing easier by providing testing support with annotations, utilities, and embedded environments.

---

# How to Write Unit Tests in Spring Boot: Detailed Explanation

---

## 1. Setup Testing Dependencies

Spring Boot’s starter includes test dependencies by default:

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-test</artifactId>
  <scope>test</scope>
</dependency>
```

This brings in JUnit 5, Mockito, AssertJ, Spring TestContext Framework, and more.

---

## 2. Write Unit Tests for Service Layer (Example)

### Why service layer?

* Unit test focuses on one component (like a service).
* You mock dependencies (like repositories) to isolate the test.

---

### Example Service

```java
@Service
public class UserService {

    private final UserRepository userRepository;

    public UserService(UserRepository repo) {
        this.userRepository = repo;
    }

    public User findUserById(Long id) {
        return userRepository.findById(id).orElse(null);
    }
}
```

---

### Test Class for UserService

```java
@ExtendWith(MockitoExtension.class)  // Enable Mockito in JUnit 5
public class UserServiceTest {

    @Mock
    private UserRepository userRepository;  // Mock dependency

    @InjectMocks
    private UserService userService;        // Class under test

    @Test
    void testFindUserById_UserExists() {
        // Arrange
        User user = new User(1L, "Alice");
        Mockito.when(userRepository.findById(1L)).thenReturn(Optional.of(user));

        // Act
        User foundUser = userService.findUserById(1L);

        // Assert
        assertNotNull(foundUser);
        assertEquals("Alice", foundUser.getName());
    }

    @Test
    void testFindUserById_UserNotFound() {
        // Arrange
        Mockito.when(userRepository.findById(1L)).thenReturn(Optional.empty());

        // Act
        User foundUser = userService.findUserById(1L);

        // Assert
        assertNull(foundUser);
    }
}
```

---

## 3. Write Unit Tests for Controller Layer

For controllers, Spring Boot offers **`@WebMvcTest`** to test only the web layer without loading the entire context.

Example:

```java
@WebMvcTest(UserController.class)
public class UserControllerTest {

    @Autowired
    private MockMvc mockMvc;  // Mock MVC for REST call simulation

    @MockBean
    private UserService userService;  // Mock service

    @Test
    public void testGetUser() throws Exception {
        User user = new User(1L, "Alice");
        Mockito.when(userService.findUserById(1L)).thenReturn(user);

        mockMvc.perform(get("/users/1"))
               .andExpect(status().isOk())
               .andExpect(jsonPath("$.name").value("Alice"));
    }
}
```

---

## 4. Use Annotations Commonly in Spring Boot Testing

| Annotation                            | Purpose                                                       |
| ------------------------------------- | ------------------------------------------------------------- |
| `@SpringBootTest`                     | Loads full Spring Boot context (integration test)             |
| `@WebMvcTest`                         | Loads only web layer (controller) for testing MVC controllers |
| `@MockBean`                           | Mock a bean in Spring ApplicationContext                      |
| `@Mock` & `@InjectMocks`              | Mockito annotations to create mocks and inject dependencies   |
| `@ExtendWith(MockitoExtension.class)` | Enable Mockito support in JUnit 5                             |

---

## 5. Example: Simple Unit Test with JUnit & Mockito

```java
@Test
void testSomeServiceMethod() {
    // Arrange
    when(dependency.call()).thenReturn("mocked result");

    // Act
    String result = service.doWork();

    // Assert
    assertEquals("expected result", result);
}
```

---

## Summary:

| Layer       | Annotation / Tool                                     | Purpose                                     |
| ----------- | ----------------------------------------------------- | ------------------------------------------- |
| Service     | `@ExtendWith(MockitoExtension.class)` + Mockito mocks | Isolate service testing                     |
| Controller  | `@WebMvcTest` + `MockMvc` + `@MockBean`               | Test REST endpoints without full context    |
| Integration | `@SpringBootTest`                                     | Load full app context for integration tests |

---

## 68. What is `@SpringBootTest`?

Here’s a detailed explanation of `@SpringBootTest`:

---

## What is `@SpringBootTest`?

`@SpringBootTest` is a **Spring Boot testing annotation** used to **load the full application context** for integration tests.

It tells Spring Boot to:

* Start the entire Spring application context (like when you run the app normally).
* Set up all beans, configurations, and auto-configurations.
* Allow you to test the application in an environment close to production.

---

## When to Use `@SpringBootTest`?

* When you want to write **integration tests** that involve multiple layers (controllers, services, repositories).
* When you need the **complete Spring context** loaded (including database, security, web environment).
* When you want to test if your app’s components work correctly **together**.

---

## Key Features

* By default, it **starts the embedded server** (like Tomcat) if your app is a web application.
* You can customize it to **not start the server** using `webEnvironment` attribute.
* Supports **transactional tests**, meaning the test data can be rolled back after each test.

---

## Example Usage

```java
@SpringBootTest
public class UserServiceIntegrationTest {

    @Autowired
    private UserService userService;

    @Test
    void testFindUser() {
        User user = userService.findUserById(1L);
        assertNotNull(user);
    }
}
```

---

## Controlling the Web Environment

You can configure the embedded web server behavior:

```java
@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.NONE)  // No web server
@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.MOCK)  // Mock servlet environment
@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)  // Random port server
@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.DEFINED_PORT)  // Default port
```

---

## Difference from Other Testing Annotations

| Annotation        | Loads Context? | Starts Server?   | Scope                 |
| ----------------- | -------------- | ---------------- | --------------------- |
| `@SpringBootTest` | Yes            | Yes (by default) | Full app, integration |
| `@WebMvcTest`     | Partial        | No               | Web layer only        |
| `@DataJpaTest`    | Partial        | No               | JPA/repository layer  |

---

## Summary

* `@SpringBootTest` loads **entire Spring Boot context**.
* Used for **integration testing**.
* Can start or not start embedded web server depending on config.
* Allows testing of multiple layers and real components.

---

## 69. How do you test a REST controller?

Testing REST controllers in Spring Boot is a common and important task. You want to verify that your controller endpoints behave correctly — returning the right status codes, responses, and handling requests properly.

---

## How to Test a REST Controller in Spring Boot

### 1. Use `@WebMvcTest` Annotation

* `@WebMvcTest` loads **only the web layer** (controller, filters, Jackson converters, etc.), **not the entire Spring context**.
* This keeps tests fast and focused on controller behavior.
* You mock service layers and dependencies injected into the controller.

---

### 2. Use `MockMvc` to Simulate HTTP Requests

* `MockMvc` allows you to perform HTTP requests **without running a server**.
* You can send GET, POST, PUT, DELETE requests and assert response status, content, headers, etc.

---

### Example: Testing a Simple REST Controller

Suppose you have this REST controller:

```java
@RestController
@RequestMapping("/api/users")
public class UserController {

    private final UserService userService;

    public UserController(UserService service) {
        this.userService = service;
    }

    @GetMapping("/{id}")
    public ResponseEntity<User> getUser(@PathVariable Long id) {
        return userService.findById(id)
                .map(ResponseEntity::ok)
                .orElse(ResponseEntity.notFound().build());
    }
}
```

---

### Test Class for `UserController`

```java
@WebMvcTest(UserController.class)  // Loads only UserController and related web components
public class UserControllerTest {

    @Autowired
    private MockMvc mockMvc;

    @MockBean  // Mock the service used by the controller
    private UserService userService;

    @Test
    public void testGetUser_Found() throws Exception {
        User user = new User(1L, "Alice");

        Mockito.when(userService.findById(1L)).thenReturn(Optional.of(user));

        mockMvc.perform(get("/api/users/1"))
               .andExpect(status().isOk())
               .andExpect(content().contentType(MediaType.APPLICATION_JSON))
               .andExpect(jsonPath("$.name").value("Alice"));
    }

    @Test
    public void testGetUser_NotFound() throws Exception {
        Mockito.when(userService.findById(1L)).thenReturn(Optional.empty());

        mockMvc.perform(get("/api/users/1"))
               .andExpect(status().isNotFound());
    }
}
```

---

### What Happens Here?

* `@WebMvcTest` loads the controller and configures Spring MVC infrastructure.
* `@MockBean` creates a mock of `UserService` and injects it into the controller.
* `mockMvc.perform()` simulates HTTP requests.
* `andExpect()` verifies the HTTP status, content type, and JSON response.

---

### Other Tips for REST Controller Testing

* Use `post()`, `put()`, `delete()` on `MockMvc` for other HTTP methods.
* Use `content()` to send JSON request bodies (with `contentType(MediaType.APPLICATION_JSON)`).
* Use `jsonPath()` to validate parts of the JSON response.
* You can test headers using `.andExpect(header().string(...))`.

---

### Summary

| Tool/Annotation | Purpose                                               |
| --------------- | ----------------------------------------------------- |
| `@WebMvcTest`   | Load only controller layer and web components         |
| `@MockBean`     | Mock dependencies (services) injected into controller |
| `MockMvc`       | Simulate HTTP requests and verify responses           |

---

## 70. How do you mock repositories in unit tests?

Mocking repositories is essential when unit testing service or business logic layers in Spring Boot apps because it isolates your tests from the database.

---

## How to Mock Repositories in Unit Tests

### Why Mock Repositories?

* You want to test your service logic **without hitting the actual database**.
* Mocking avoids slow tests and external dependencies.
* It allows you to simulate repository behavior and control return values.

---

### Using Mockito to Mock Repositories

The most common way is to use **Mockito** to create mock implementations of your repository interfaces.

---

### Step-by-step Example

Suppose you have a repository:

```java
public interface UserRepository extends JpaRepository<User, Long> {
    Optional<User> findByEmail(String email);
}
```

And a service using it:

```java
@Service
public class UserService {
    private final UserRepository userRepository;
    
    public UserService(UserRepository repo) {
        this.userRepository = repo;
    }
    
    public User findByEmail(String email) {
        return userRepository.findByEmail(email).orElse(null);
    }
}
```

---

### Writing Unit Test with Mocked Repository

```java
@ExtendWith(MockitoExtension.class)  // Enables Mockito annotations
public class UserServiceTest {

    @Mock
    private UserRepository userRepository;  // Mock repository

    @InjectMocks
    private UserService userService;        // Service with mock injected

    @Test
    void testFindByEmail_UserExists() {
        User user = new User(1L, "John", "john@example.com");

        // Define behavior of mock
        Mockito.when(userRepository.findByEmail("john@example.com"))
               .thenReturn(Optional.of(user));

        // Call method under test
        User foundUser = userService.findByEmail("john@example.com");

        // Assertions
        assertNotNull(foundUser);
        assertEquals("john@example.com", foundUser.getEmail());
    }

    @Test
    void testFindByEmail_UserNotFound() {
        Mockito.when(userRepository.findByEmail("unknown@example.com"))
               .thenReturn(Optional.empty());

        User foundUser = userService.findByEmail("unknown@example.com");

        assertNull(foundUser);
    }
}
```

---

### Explanation:

* `@Mock` creates a mock of `UserRepository`.
* `@InjectMocks` injects the mock into the `UserService` instance.
* `Mockito.when(...).thenReturn(...)` defines how the mock behaves on method calls.
* The service method is called as usual, but repository calls are intercepted by the mock.
* You assert expected results without involving a real database.

---

### Alternative: Using `@MockBean` in Spring Boot Tests

If you use `@SpringBootTest` or `@WebMvcTest`, you can mock repositories with `@MockBean`, which registers the mock in the Spring context:

```java
@MockBean
private UserRepository userRepository;
```

But for pure unit tests, Mockito annotations are simpler and faster.

---

### Summary

| Annotation/Tool  | Purpose                                       |
| ---------------- | --------------------------------------------- |
| `@Mock`          | Create mock instance of repository            |
| `@InjectMocks`   | Inject mocks into service under test          |
| `Mockito.when()` | Define mock method behavior                   |
| `@MockBean`      | Spring context-aware mock (integration tests) |

---

## 71. What is Mockito and how is it used?

Here’s a detailed explanation about **Mockito** and how it’s used in Java, especially in Spring Boot testing.

---

## What is Mockito?

* **Mockito** is a popular **mocking framework for Java**.
* It allows you to create **mock objects** for dependencies in your tests.
* With mocks, you can simulate and control the behavior of complex, real objects (like repositories, services, external APIs) without invoking their actual logic.
* Mockito helps isolate the unit of code under test by replacing its collaborators with mocks.

---

## Why Use Mockito?

* To **isolate unit tests** from external dependencies.
* To simulate various scenarios (like exceptions, return values).
* To verify interactions between objects.
* To keep tests fast, independent, and reliable.

---

## Key Concepts

| Concept      | Description                                  |
| ------------ | -------------------------------------------- |
| Mock         | A simulated object with programmed behavior  |
| Stubbing     | Defining what a mock returns on method calls |
| Verification | Checking that certain methods were called    |

---

## How to Use Mockito

### 1. Add Dependency

If using Maven:

```xml
<dependency>
  <groupId>org.mockito</groupId>
  <artifactId>mockito-core</artifactId>
  <version>4.+" (latest)</version>
  <scope>test</scope>
</dependency>
```

(Usually `spring-boot-starter-test` includes Mockito already.)

---

### 2. Create Mocks and Inject Them

Using JUnit 5 and Mockito:

```java
@ExtendWith(MockitoExtension.class)  // Enable Mockito support
public class UserServiceTest {

    @Mock
    private UserRepository userRepository;  // Mock dependency

    @InjectMocks
    private UserService userService;        // Class under test with mocks injected

    @Test
    void testFindUser() {
        User user = new User(1L, "Alice");

        // Stubbing: define mock behavior
        Mockito.when(userRepository.findById(1L)).thenReturn(Optional.of(user));

        User found = userService.findUserById(1L);

        // Assertions
        assertNotNull(found);
        assertEquals("Alice", found.getName());

        // Verify interaction
        Mockito.verify(userRepository).findById(1L);
    }
}
```

---

### 3. Common Mockito Methods

| Method                      | Purpose                                        |
| --------------------------- | ---------------------------------------------- |
| `mock(Class)`               | Create a mock object                           |
| `when(...).thenReturn(...)` | Stub method return values                      |
| `verify(...)`               | Verify method calls on mocks                   |
| `any()`, `eq()`             | Argument matchers for flexible matching        |
| `doThrow()`, `doAnswer()`   | Define behavior for void methods or exceptions |

---

## Summary

* Mockito helps **mock dependencies** so you can test units in isolation.
* Use `@Mock` and `@InjectMocks` annotations to create mocks and inject them.
* Stub methods with `when().thenReturn()` to simulate desired behavior.
* Verify method calls with `verify()` to ensure interactions happen as expected.

---

## 72. What is integration testing in Spring Boot?

### ✅ What is Integration Testing in Spring Boot?

**Integration testing** is a type of testing where **multiple components of the application are tested together** to ensure that they interact correctly. In Spring Boot, this means testing parts like controllers, services, repositories, and the database **as a whole** rather than in isolation.

---

### 🧩 Difference Between Unit Test and Integration Test

| Feature      | Unit Test                          | Integration Test                                  |
| ------------ | ---------------------------------- | ------------------------------------------------- |
| Scope        | Single class or method             | Multiple components working together              |
| Dependencies | Mocked                             | Real or embedded dependencies (like DB, services) |
| Speed        | Fast                               | Slower                                            |
| Tools        | `Mockito`, `@Mock`, `@InjectMocks` | `@SpringBootTest`, `TestRestTemplate`, etc.       |

---

### 🔧 Tools & Annotations for Integration Testing

1. **`@SpringBootTest`**

    * Loads the full application context (like when you run the app normally).
    * Can include `webEnvironment = RANDOM_PORT` or `DEFINED_PORT`.

2. **`@AutoConfigureMockMvc`** or **`TestRestTemplate`**

    * To test REST APIs without launching a full server.

3. **Embedded databases** (e.g., H2)

    * Used for database testing without external setup.

---

### ✅ Example: Integration Testing a REST Controller

Let’s say you have a REST controller:

```java
@RestController
@RequestMapping("/api/users")
public class UserController {
    @Autowired
    private UserService userService;

    @GetMapping("/{id}")
    public ResponseEntity<User> getUser(@PathVariable Long id) {
        return ResponseEntity.of(userService.findById(id));
    }
}
```

---

### 🧪 Integration Test

```java
@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
@AutoConfigureMockMvc
public class UserControllerIT {

    @Autowired
    private MockMvc mockMvc;

    @Autowired
    private UserRepository userRepository;

    @BeforeEach
    void setup() {
        userRepository.save(new User(1L, "Alice", "alice@example.com"));
    }

    @Test
    void testGetUser() throws Exception {
        mockMvc.perform(get("/api/users/1"))
               .andExpect(status().isOk())
               .andExpect(jsonPath("$.name").value("Alice"));
    }
}
```

---

### 🧪 Integration Test for Repository

```java
@DataJpaTest
public class UserRepositoryIT {

    @Autowired
    private UserRepository userRepository;

    @Test
    void testFindByEmail() {
        userRepository.save(new User(null, "Bob", "bob@example.com"));
        Optional<User> user = userRepository.findByEmail("bob@example.com");
        assertTrue(user.isPresent());
    }
}
```

---

### 📝 Summary

* **Integration testing** in Spring Boot ensures **real interactions** between components.
* Use annotations like `@SpringBootTest`, `@DataJpaTest`, and `@AutoConfigureMockMvc`.
* It’s great for testing real-world scenarios like full request-response cycles and database operations.

---

## 73. What is `@DataJpaTest`?

### ✅ What is `@DataJpaTest` in Spring Boot?

`@DataJpaTest` is a **specialized test annotation** provided by Spring Boot to test **JPA (Java Persistence API) components**, such as:

* Repositories
* Entity mappings
* JPQL/native queries

It is **not** meant to test the full application (no service or controller beans are loaded).

---

### 📌 Key Features of `@DataJpaTest`

| Feature                  | Description                                                              |
| ------------------------ | ------------------------------------------------------------------------ |
| Lightweight              | Loads only JPA-related components — not full Spring context.             |
| In-memory DB (default)   | Uses **H2** in-memory database by default for fast and isolated testing. |
| Rollback after each test | Each test runs in a **transaction** and is **rolled back** afterward.    |
| Repository injection     | You can `@Autowired` your `JpaRepository` interfaces directly.           |

---

### 🔧 When to Use `@DataJpaTest`?

* To test repository methods.
* To verify custom queries (`@Query`, JPQL, native).
* To check entity relationships (`@OneToMany`, etc.).
* To ensure correct persistence and retrieval behavior.

---

### 🧪 Example: Testing a JPA Repository

Let’s say you have an entity and repository:

```java
@Entity
public class User {
    @Id @GeneratedValue
    private Long id;
    private String name;
    private String email;
}

public interface UserRepository extends JpaRepository<User, Long> {
    Optional<User> findByEmail(String email);
}
```

---

### 🧪 Test with `@DataJpaTest`

```java
@DataJpaTest
public class UserRepositoryTest {

    @Autowired
    private UserRepository userRepository;

    @Test
    void testFindByEmail() {
        // Arrange
        User user = new User(null, "Alice", "alice@example.com");
        userRepository.save(user);

        // Act
        Optional<User> found = userRepository.findByEmail("alice@example.com");

        // Assert
        assertTrue(found.isPresent());
        assertEquals("Alice", found.get().getName());
    }
}
```

---

### ✅ Summary

| Annotation     | Purpose                                                                                            |
| -------------- | -------------------------------------------------------------------------------------------------- |
| `@DataJpaTest` | Quickly test JPA repositories, entity relationships, and database operations using an in-memory DB |

---

## 74. How to use profiles in tests?

Using **Spring profiles in tests** allows you to load different configurations, beans, or environments (like `test`, `dev`, or `prod`) depending on your testing needs.

---

### ✅ What Are Spring Profiles?

* **Profiles** define logical groupings of configuration.
* Useful for loading environment-specific beans or properties.
* Activated with: `spring.profiles.active`

---

### 🎯 Why Use Profiles in Tests?

* To load **test-specific configurations** (e.g., H2 database, mock beans).
* To isolate **unit, integration, and QA test environments**.
* To keep tests **clean, fast, and environment-agnostic**.

---

## 🔧 How to Use Profiles in Spring Boot Tests

### ✅ Option 1: Use `@ActiveProfiles` Annotation

```java
@ActiveProfiles("test")
@SpringBootTest
public class UserServiceTest {
    // This test will use application-test.properties or test beans
}
```

This activates the `test` profile for the test class.

---

### ✅ Option 2: Set Profile in `application.properties`

For example, in `src/test/resources/application.properties`:

```properties
spring.profiles.active=test
```

This activates the `test` profile for **all tests** when using `@SpringBootTest`.

---

### ✅ Option 3: Use `@Profile` on Beans

```java
@Configuration
@Profile("test")
public class TestConfig {
    @Bean
    public ExternalService mockExternalService() {
        return Mockito.mock(ExternalService.class);
    }
}
```

Beans inside this class will **only load if `test` profile is active**.

---

### ✅ Option 4: Use Profiles in `application-<profile>.properties`

You can define different property files:

* `application.properties` (default)
* `application-test.properties` (used when `test` profile is active)
* `application-dev.properties`, etc.

Spring Boot automatically picks the right file based on the active profile.

---

### 🧪 Example

#### File: `application-test.properties`

```properties
spring.datasource.url=jdbc:h2:mem:testdb
spring.jpa.hibernate.ddl-auto=create-drop
```

#### Test Class:

```java
@ActiveProfiles("test")
@SpringBootTest
public class UserRepositoryTest {
    @Autowired
    private UserRepository userRepository;

    @Test
    void testFindUser() {
        userRepository.save(new User("John", "john@example.com"));
        assertTrue(userRepository.findByEmail("john@example.com").isPresent());
    }
}
```

---

### ✅ Summary

| Feature                       | Use                               |
| ----------------------------- | --------------------------------- |
| `@ActiveProfiles("test")`     | Sets active profile in test class |
| `@Profile("test")`            | Loads beans only in test profile  |
| `application-test.properties` | Custom properties per environment |
| In `src/test/resources`       | Place test-specific files here    |

---

## 75. What is the use of `CommandLineRunner`?

### ✅ What is `CommandLineRunner` in Spring Boot?

`CommandLineRunner` is a **functional interface** in Spring Boot used to **execute code after the application context is loaded** and right before the Spring Boot application fully starts.

It is commonly used for:

* Running initialization logic (like inserting sample data).
* Running startup checks.
* Executing batch jobs or scheduled tasks.

---

### 🧩 Interface Definition

```java
@FunctionalInterface
public interface CommandLineRunner {
    void run(String... args) throws Exception;
}
```

---

### 🚀 How Does It Work?

* You implement `CommandLineRunner` and override the `run()` method.
* Spring Boot automatically detects it as a bean and runs it after the context is ready.

---

### 🔧 Example

```java
@Component
public class MyStartupRunner implements CommandLineRunner {

    @Override
    public void run(String... args) throws Exception {
        System.out.println(">>> Application has started!");
        System.out.println("Arguments: " + Arrays.toString(args));
    }
}
```

**Output (on app start):**

```
>>> Application has started!
Arguments: []
```

---

### 🔍 Use Cases

| Use Case         | Description                              |
| ---------------- | ---------------------------------------- |
| Database seeding | Insert initial data into DB at startup   |
| Validation       | Check environment variables/configs      |
| Debugging        | Log application startup info             |
| One-time setup   | Load cache, connect to external services |

---

### ⚙️ Multiple Runners?

Yes, you can define multiple `CommandLineRunner` beans. If needed, you can use `@Order` to control execution order:

```java
@Component
@Order(1)
public class FirstRunner implements CommandLineRunner {
    public void run(String... args) {
        System.out.println("First");
    }
}

@Component
@Order(2)
public class SecondRunner implements CommandLineRunner {
    public void run(String... args) {
        System.out.println("Second");
    }
}
```

---

### ✅ Summary

| Feature      | Details                                                           |
| ------------ | ----------------------------------------------------------------- |
| Interface    | `CommandLineRunner` (`run(String... args)`)                       |
| Purpose      | Code to run **after application context is loaded**               |
| Common Uses  | Initialization, DB seeding, configuration checks                  |
| Alternatives | `ApplicationRunner` (similar but receives `ApplicationArguments`) |

---

## 76. What is `@ConfigurationProperties`?

### ✅ What is `@ConfigurationProperties` in Spring Boot?

`@ConfigurationProperties` is an annotation used in Spring Boot to **bind external configuration values (like those from `application.properties` or `application.yml`) to a Java class**.

This allows you to **map hierarchical configuration** into a type-safe, structured object.

---

### 🔍 Why Use It?

Instead of reading each property using `@Value`, `@ConfigurationProperties` allows grouping related configurations in one class, improving readability and maintainability.

---

### 📦 Example: Binding Custom Properties

#### `application.yml`:

```yaml
app:
  name: MySpringApp
  version: 1.0
  features:
    enable-logging: true
    max-users: 100
```

#### Java Class:

```java
@Component
@ConfigurationProperties(prefix = "app")
public class AppProperties {
    private String name;
    private String version;
    private Features features;

    public static class Features {
        private boolean enableLogging;
        private int maxUsers;
        // getters and setters
    }

    // getters and setters
}
```

> Now `AppProperties` contains the entire `app.*` configuration in a structured way.

---

### 🔧 Required Setup

1. **Enable configuration properties scanning (Spring Boot 2.2+)**:

    * Spring Boot automatically detects `@ConfigurationProperties` if the class is annotated with `@Component`.

2. **Or register manually**:

```java
@Configuration
@EnableConfigurationProperties(AppProperties.class)
public class AppConfig {}
```

> Use this approach if you're not using `@Component` on the config class.

---

### ✅ Best Practices

* Use `@ConfigurationProperties` for **grouped or hierarchical settings**.
* Avoid using `@Value` for large or complex configurations.
* You can validate the configuration using JSR-303 annotations and `@Validated`.

#### Example:

```java
@Component
@ConfigurationProperties(prefix = "app")
@Validated
public class AppProperties {

    @NotBlank
    private String name;

    @Min(1)
    private int version;

    // getters and setters
}
```

---

### 🆚 `@Value` vs `@ConfigurationProperties`

| Feature                   | `@Value`          | `@ConfigurationProperties`  |
| ------------------------- | ----------------- | --------------------------- |
| Use case                  | Single property   | Group of related properties |
| Type-safe binding         | No (String-based) | Yes                         |
| Supports validation       | No                | Yes (`@Validated`)          |
| Complex/nested structures | Not suitable      | Ideal                       |

---

### ✅ Summary

| Annotation                 | Purpose                                     |
| -------------------------- | ------------------------------------------- |
| `@ConfigurationProperties` | Binds external config into structured class |
| `prefix = "xyz"`           | Specifies the base key in `application.yml` |
| Usage                      | For custom settings, third-party config     |

---

## 77. What is `@EnableAutoConfiguration`?

### ✅ What is `@EnableAutoConfiguration` in Spring Boot?

`@EnableAutoConfiguration` is a **core annotation** in Spring Boot that tells Spring to **automatically configure** your application based on the **dependencies present on the classpath**.

It is part of the **magic** behind Spring Boot's ability to minimize boilerplate configuration.

---

### 📌 Location

It is included inside the `@SpringBootApplication` annotation:

```java
@SpringBootApplication  // includes @EnableAutoConfiguration
public class MyApp {
    public static void main(String[] args) {
        SpringApplication.run(MyApp.class, args);
    }
}
```

So you typically don’t need to add it manually.

---

### 🧠 What Does It Do?

It looks at:

* **Classpath dependencies** (e.g., `spring-boot-starter-web`, `spring-boot-starter-data-jpa`)
* **Declared beans**
* **Configuration files (`application.properties`, `application.yml`)**

Then it:

* Automatically configures **Spring MVC** if `spring-boot-starter-web` is present.
* Configures **DataSource and JPA** if `spring-boot-starter-data-jpa` and a DB driver are present.
* Sets up **Thymeleaf**, **Jackson**, **Spring Security**, etc., as needed.

---

### 🔧 Example

Let’s say you have `spring-boot-starter-web` in your `pom.xml` or `build.gradle`:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

> Spring Boot automatically configures:

* DispatcherServlet
* Embedded Tomcat
* Jackson (for JSON)
* Default error handling

You didn’t configure any of this manually — that's `@EnableAutoConfiguration` at work.

---

### 🧪 Selective Control (Include/Exclude)

You can include or exclude specific auto-configurations:

```java
@EnableAutoConfiguration(exclude = {
    DataSourceAutoConfiguration.class
})
```

Or via properties:

```properties
spring.autoconfigure.exclude=org.springframework.boot.autoconfigure.jdbc.DataSourceAutoConfiguration
```

---

### 📦 Auto-Configuration Classes

Spring Boot auto-configuration classes are listed in:

```
META-INF/spring.factories
```

Each starter module includes its own auto-configurations (e.g., `WebMvcAutoConfiguration`, `JpaAutoConfiguration`, etc.).

---

### ✅ Summary

| Feature                              | Description                                             |
| ------------------------------------ | ------------------------------------------------------- |
| `@EnableAutoConfiguration`           | Enables Spring Boot’s automatic configuration mechanism |
| Included in `@SpringBootApplication` | No need to explicitly declare in most cases             |
| Driven by classpath & config         | Configures beans based on available dependencies        |
| Can be customized                    | Use `exclude`, profiles, or conditional annotations     |

---

## 78. What is `@PropertySource`?

### ✅ What is `@PropertySource` in Spring?

`@PropertySource` is a Spring annotation used to **explicitly load a `.properties` file** into the **Spring Environment**.

It's useful when:

* You have **custom property files** that are not named `application.properties`.
* You want to load additional property files from specific locations.

---

### 🔧 Syntax

```java
@PropertySource("classpath:myconfig.properties")
@Configuration
public class MyConfig {
    // You can use @Value to inject properties from myconfig.properties
}
```

---

### 🧠 How It Works

* Loads the specified file into Spring's `Environment`.
* Makes its values available via `@Value`, `Environment.getProperty()`, or `@ConfigurationProperties`.

---

### 📁 Example

#### 1. Create a custom file: `src/main/resources/custom.properties`

```properties
app.title=Spring Boot Interview Guide
app.version=2.0
```

#### 2. Create a config class

```java
@Configuration
@PropertySource("classpath:custom.properties")
public class AppConfig {
    
    @Value("${app.title}")
    private String title;

    @Value("${app.version}")
    private String version;

    @PostConstruct
    public void printProps() {
        System.out.println("Title: " + title);
        System.out.println("Version: " + version);
    }
}
```

---

### 📌 Notes

* If the file is **not found**, Spring will throw an exception by default.
  You can make it optional:

```java
@PropertySource(value = "classpath:missing.properties", ignoreResourceNotFound = true)
```

* Works with `.properties` files, not `.yml` (for `.yml`, use Spring Boot profiles instead).

---

### ✅ When to Use `@PropertySource`

| Scenario                    | Use it when…                                     |
| --------------------------- | ------------------------------------------------ |
| Loading extra `.properties` | You have a file like `custom-config.properties`  |
| Modular configuration       | You want different configs for different modules |
| Legacy apps or libraries    | External configs are already defined             |

---

### 🔄 Difference from `application.properties`?

| Feature        | `@PropertySource`        | `application.properties`   |
| -------------- | ------------------------ | -------------------------- |
| Scope          | Explicitly declared      | Auto-loaded by Spring Boot |
| Format support | `.properties` only       | `.properties` and `.yml`   |
| Best used for  | Custom or external files | Centralized config         |

---

### ✅ Summary

| Annotation        | Description                                 |
| ----------------- | ------------------------------------------- |
| `@PropertySource` | Loads custom `.properties` file into Spring |
| Key Benefit       | Makes custom values available to beans      |
| Scope             | Used inside `@Configuration` classes        |

---

## 79. How do you encrypt properties in Spring Boot?

Encrypting properties in Spring Boot is important when dealing with sensitive information like database passwords, API keys, or secrets.

---

### How to Encrypt Properties in Spring Boot

Spring Boot does **not** provide built-in encryption for properties out-of-the-box, but there are several ways to achieve encrypted properties:

---

## 1. Using Spring Cloud Config + Spring Cloud Vault / Spring Cloud Config Server

* This is the **recommended approach for enterprise apps**.
* Externalizes config to a Config Server or Vault that handles encryption and secure storage.
* Your app fetches decrypted properties at runtime.

---

## 2. Using Jasypt (Java Simplified Encryption)

[Jasypt](http://www.jasypt.org/) is a popular library that integrates well with Spring Boot for encrypting/decrypting properties.

### How to use Jasypt in Spring Boot

---

### Step 1: Add dependency

```xml
<!-- Maven -->
<dependency>
    <groupId>com.github.ulisesbocchio</groupId>
    <artifactId>jasypt-spring-boot-starter</artifactId>
    <version>3.0.4</version>
</dependency>
```

---

### Step 2: Encrypt your property

Use Jasypt CLI or any online tool to encrypt sensitive values.

Example encrypted property:

```
ENC(encryptedPasswordStringHere)
```

---

### Step 3: Use encrypted properties in `application.properties`

```properties
spring.datasource.password=ENC(qwertyEncryptedStringHere)
```

---

### Step 4: Provide the decryption password/key

You can provide the secret key to decrypt the properties via an environment variable or JVM argument:

```
-Djasypt.encryptor.password=mySecretKey
```

or in environment variables:

```bash
export JASYPT_ENCRYPTOR_PASSWORD=mySecretKey
```

---

### Step 5: Use normally in your app

Spring Boot with Jasypt will automatically decrypt any property starting with `ENC(...)`.

---

## Example

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.username=root
spring.datasource.password=ENC(5f4dcc3b5aa765d61d8327deb882cf99)
```

---

## 3. Other approaches

* **Custom PropertySources**: Write your own `PropertySource` that decrypts values.
* **Environment Variables / External Vaults**: Store secrets outside config files.

---

### Summary

| Method             | Description                                     | Use Case                       |
| ------------------ | ----------------------------------------------- | ------------------------------ |
| Spring Cloud Vault | Centralized secure secrets management           | Enterprise-grade secure config |
| Jasypt             | Simple encryption/decryption of properties      | Quick encryption in properties |
| Custom solutions   | Custom decryptors or external vault integration | Advanced or custom needs       |

---

If you want, I can provide a sample Spring Boot project showing Jasypt integration!

---

## 80. What is externalized configuration in Spring Boot?

### What is Externalized Configuration in Spring Boot?

**Externalized Configuration** in Spring Boot means that you can **keep configuration settings outside of your application’s code** and package, so they can be changed easily without rebuilding or redeploying your app.

---

### Why Externalize Configuration?

* To separate **configuration** from **code**.
* To enable different environments (dev, test, prod) to have different settings.
* To make changing configs easier and safer (no code changes needed).
* To allow secrets or sensitive data to be managed separately.

---

### How Spring Boot Supports Externalized Configuration

Spring Boot supports multiple sources of configuration, and it loads them in a defined order with **precedence**:

| Order | Source                                                        | Description                       |
| ----- | ------------------------------------------------------------- | --------------------------------- |
| 1     | **Command-line arguments**                                    | Passed during app startup         |
| 2     | **Java System properties**                                    | `-Dproperty=value` JVM arguments  |
| 3     | **OS environment variables**                                  | e.g. `MY_APP_PASSWORD`            |
| 4     | **`application.properties` or `.yml` in `/config` directory** | External config directory         |
| 5     | **`application.properties` or `.yml` in classpath root**      | Inside your jar or classpath      |
| 6     | **Default properties**                                        | Hardcoded defaults inside the app |

---

### Example of Externalized Config Locations

* `/config/application.properties` (next to the jar)
* `./application.properties` (current directory)
* Environment variables (`export SERVER_PORT=8081`)
* Command line (`java -jar app.jar --server.port=8081`)

---

### Benefits

* You can **override** defaults without changing code.
* Run the **same artifact** in different environments with different configs.
* Store **secrets or API keys** outside of your packaged JAR.

---

### How to Use in Spring Boot?

If you put an `application.properties` or `application.yml` outside your jar (e.g., `/config` folder next to the jar), Spring Boot will load it automatically and override packaged values.

You can also set environment variables:

```bash
export SPRING_DATASOURCE_URL=jdbc:mysql://localhost:3306/mydb
export SPRING_DATASOURCE_USERNAME=root
export SPRING_DATASOURCE_PASSWORD=secret
```

---

### Summary

| Feature                             | Description                                         |
| ----------------------------------- | --------------------------------------------------- |
| Externalized config                 | Store config outside your app code or jar           |
| Multiple sources                    | Command line, env vars, external files, classpath   |
| Priority order                      | Command line > env vars > external files > defaults |
| Allows environment-specific configs | Dev/test/prod configs without code changes          |

---

### 🔹 81–100: Advanced Topics, Actuator, Microservices, DevOps

## 81. What is Spring Boot Actuator?

**Spring Boot Actuator** is a powerful **production-ready feature** of Spring Boot that helps you **monitor and manage your application** once it’s running.

It provides **built-in endpoints** that expose useful information about your app’s health, metrics, environment, and more — all accessible over HTTP or JMX.

---

### Why Use Spring Boot Actuator?

* **Monitor application health** (disk space, database, etc.)
* **Expose metrics** like memory usage, CPU, HTTP requests
* **View environment variables and configuration properties**
* **Trace HTTP requests and application logs**
* **Manage application lifecycle** (shutdown, restart)
* Easily integrate with monitoring tools like Prometheus, Grafana

---

### How to Add Actuator to Your Spring Boot Project?

Add the dependency in your `pom.xml` or `build.gradle`:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

---

### Common Actuator Endpoints

| Endpoint               | Description                    |
| ---------------------- | ------------------------------ |
| `/actuator/health`     | Shows health status of the app |
| `/actuator/metrics`    | Provides various metrics       |
| `/actuator/env`        | Shows environment properties   |
| `/actuator/beans`      | Lists all Spring beans         |
| `/actuator/loggers`    | View/change logging levels     |
| `/actuator/heapdump`   | Provides a JVM heap dump       |
| `/actuator/threaddump` | Shows JVM thread dump          |

---

### Example: Access Health Endpoint

Start your app and visit:

```
http://localhost:8080/actuator/health
```

Response:

```json
{
  "status": "UP"
}
```

---

### Security Considerations

* By default, only a few endpoints (like `/health`) are exposed.
* You can configure which endpoints are enabled and exposed in `application.properties`:

```properties
management.endpoints.web.exposure.include=health,info,metrics
```

---

### Customizing Actuator

You can add **custom health indicators** or metrics by implementing interfaces like:

* `HealthIndicator`
* `MeterBinder`

---

### Summary

| Feature            | Description                      |
| ------------------ | -------------------------------- |
| Monitoring         | Real-time health and metrics     |
| Management         | Control and manage app remotely  |
| Easy integration   | Works well with monitoring tools |
| Built-in endpoints | Multiple useful operational APIs |

---

## 82. What endpoints are available in Actuator?

Spring Boot Actuator provides many built-in **management endpoints** to monitor and manage your application. Here are some of the most important and frequently used ones:

| Endpoint                   | Description                                                | Default Exposure                                |
| -------------------------- | ---------------------------------------------------------- | ----------------------------------------------- |
| `/actuator/health`         | Shows application health information (disk, db, etc.)      | Exposed publicly                                |
| `/actuator/info`           | Displays arbitrary application info (version, description) | Exposed publicly                                |
| `/actuator/metrics`        | Displays metrics gathered by the app (memory, HTTP, etc.)  | Not exposed by default, must include explicitly |
| `/actuator/env`            | Displays environment properties and system variables       | Not exposed by default                          |
| `/actuator/beans`          | Lists all Spring beans in the application context          | Not exposed by default                          |
| `/actuator/threaddump`     | Thread dump of the JVM                                     | Not exposed by default                          |
| `/actuator/loggers`        | Shows and allows modification of logging levels            | Not exposed by default                          |
| `/actuator/httptrace`      | Displays recent HTTP request-response exchanges            | Not exposed by default                          |
| `/actuator/mappings`       | Shows all @RequestMapping paths                            | Not exposed by default                          |
| `/actuator/heapdump`       | Provides a heap dump of the JVM                            | Not exposed by default                          |
| `/actuator/scheduledtasks` | Information on scheduled tasks                             | Not exposed by default                          |
| `/actuator/caches`         | Information about caches configured                        | Not exposed by default                          |

---

### How to Expose Endpoints

By default, **only `/health` and `/info` are exposed over HTTP**.

You can configure which endpoints are exposed via `application.properties` or `application.yml`:

```properties
management.endpoints.web.exposure.include=health,info,metrics,loggers
```

To expose all:

```properties
management.endpoints.web.exposure.include=*
```

---

### Example: List Available Endpoints

If you hit:

```
http://localhost:8080/actuator
```

You’ll get a JSON list of all exposed endpoints.

---

### Security Note

Some endpoints expose sensitive info (like `/env`, `/heapdump`) and should be **secured properly** in production.

---

If you want, I can show you how to customize and secure actuator endpoints!

---

## 83. How do you expose custom metrics?

Great question! Exposing **custom metrics** in Spring Boot Actuator lets you monitor your own application-specific data beyond the default JVM and system metrics.

---

## How to Expose Custom Metrics in Spring Boot

Spring Boot Actuator uses **Micrometer** as its metrics facade, which supports many monitoring systems (Prometheus, Graphite, etc.).

---

### Step 1: Add Actuator Dependency (if not already added)

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

---

### Step 2: Inject `MeterRegistry`

`MeterRegistry` is the main interface for creating and registering metrics.

Example in a service or component:

```java
import io.micrometer.core.instrument.MeterRegistry;
import io.micrometer.core.instrument.Counter;
import org.springframework.stereotype.Component;

@Component
public class CustomMetrics {

    private final Counter myCounter;

    public CustomMetrics(MeterRegistry registry) {
        // Create and register a counter metric named "my_custom_counter"
        this.myCounter = Counter.builder("my_custom_counter")
            .description("Counts custom events")
            .register(registry);
    }

    public void incrementCounter() {
        myCounter.increment();
    }
}
```

---

### Step 3: Use Your Metric

Call `incrementCounter()` method whenever you want to update the metric.

---

### Step 4: Access Metrics

Metrics will be available at:

```
http://localhost:8080/actuator/metrics/my_custom_counter
```

You can also see all metrics at:

```
http://localhost:8080/actuator/metrics
```

---

### Other Metric Types Supported

* `Gauge` – for measuring values that can go up/down (e.g., queue size)
* `Timer` – for measuring durations and counts
* `DistributionSummary` – for measuring sizes or amounts

Example of a Gauge:

```java
Gauge.builder("my_gauge_metric", someObject, obj -> obj.getValue())
    .description("A gauge metric example")
    .register(registry);
```

---

### Summary Table

| Metric Type         | Usage                                                               |
| ------------------- | ------------------------------------------------------------------- |
| Counter             | Increment-only counts (e.g. request count)                          |
| Gauge               | Measure values that can increase/decrease (e.g. current queue size) |
| Timer               | Time duration and count (e.g. method latency)                       |
| DistributionSummary | Track distribution of values (e.g. payload sizes)                   |

---

## 84. How do you enable or disable actuator endpoints?

Spring Boot Actuator lets you **enable, disable, expose, or hide** endpoints via properties in your `application.properties` or `application.yml`.

---

### 1. Enable/Disable Endpoints Globally

By default, all endpoints are enabled but **only some are exposed over HTTP** (usually `health` and `info`).

To disable an endpoint completely:

```properties
management.endpoint.<endpoint-name>.enabled=false
```

Example: Disable the `shutdown` endpoint

```properties
management.endpoint.shutdown.enabled=false
```

---

### 2. Control Endpoint Exposure Over HTTP

To configure **which endpoints are exposed over HTTP**, use:

```properties
management.endpoints.web.exposure.include=health,info,metrics
```

* This example **exposes only** `health`, `info`, and `metrics` endpoints.
* To **expose all endpoints**, use:

```properties
management.endpoints.web.exposure.include=*
```

* To **exclude certain endpoints**, use:

```properties
management.endpoints.web.exposure.exclude=env,beans
```

---

### 3. Example: Disable `beans` endpoint and expose only `health` and `info`

```properties
management.endpoint.beans.enabled=false
management.endpoints.web.exposure.include=health,info
```

---

### 4. Disable Actuator Over JMX or Other Interfaces

You can also control other exposure types:

* JMX exposure:

```properties
management.endpoints.jmx.exposure.include=health,info
```

---

### 5. Security Best Practices

* Be cautious exposing sensitive endpoints like `/env`, `/shutdown`, `/heapdump`.
* Secure actuator endpoints with authentication or network-level controls.

---

### Summary Table

| Property                                    | Purpose                              | Example                                      |
| ------------------------------------------- | ------------------------------------ | -------------------------------------------- |
| `management.endpoint.<name>.enabled`        | Enable/disable specific endpoint     | `management.endpoint.shutdown.enabled=false` |
| `management.endpoints.web.exposure.include` | List endpoints exposed over HTTP     | `health,info,metrics`                        |
| `management.endpoints.web.exposure.exclude` | List endpoints NOT exposed over HTTP | `beans,env`                                  |
| `management.endpoints.jmx.exposure.include` | List endpoints exposed over JMX      | `health,info`                                |

---

## 85. What is the difference between Actuator and Micrometer?

Understanding the difference between **Spring Boot Actuator** and **Micrometer** is key to mastering application monitoring in Spring Boot.

---

## Spring Boot Actuator vs Micrometer

| Aspect           | Spring Boot Actuator                                                                                                   | Micrometer                                                                                             |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| **What it is**   | A Spring Boot module that provides **production-ready features** like health checks, metrics, and monitoring endpoints | A **metrics instrumentation facade/library** used to collect and publish metrics from your application |
| **Primary Role** | Exposes endpoints (like `/health`, `/metrics`, `/info`) for monitoring and managing your Spring Boot app               | Provides the API to **create, record, and publish metrics** (counters, timers, gauges, etc.)           |
| **Integration**  | Uses Micrometer under the hood to collect and expose metrics                                                           | Micrometer integrates with many monitoring systems (Prometheus, Graphite, etc.)                        |
| **Usage**        | Enables you to **monitor and manage your app at runtime** via HTTP, JMX, etc.                                          | Allows you to **define custom metrics** and send metrics data to monitoring systems                    |
| **Provided by**  | Part of Spring Boot                                                                                                    | Independent library, included transitively via Actuator                                                |
| **Endpoints**    | Provides pre-built endpoints for health, metrics, logging, environment, etc.                                           | Does **not** provide endpoints — it's focused on metrics collection and reporting                      |
| **Example**      | Access `/actuator/metrics` endpoint to see collected metrics                                                           | Use `MeterRegistry` to create counters, timers, gauges programmatically                                |

---

### In Short

* **Actuator** = **Monitoring and Management** endpoints + health checks + info + integrating Micrometer.
* **Micrometer** = **Metrics collection and instrumentation** library used by Actuator and your app to gather data.

---

### Typical Flow

1. Your app **instruments metrics** using Micrometer API.
2. Spring Boot **Actuator exposes these metrics** via `/actuator/metrics` endpoint.
3. Metrics can be scraped by monitoring tools like **Prometheus**, **Graphite**, or sent to cloud monitoring systems.

---

If you want, I can provide a simple example showing how Micrometer metrics are exposed via Actuator!

---

## 86. What is Spring Boot Admin?

**Spring Boot Admin** is a community-driven web application that provides a **visual dashboard** to monitor and manage multiple Spring Boot applications in one place.

---

### Why Use Spring Boot Admin?

* To **centralize monitoring** for all your Spring Boot services.
* To get real-time information about application **health**, **metrics**, **logs**, and **environment**.
* To **manage application lifecycle** remotely (e.g., restart apps).
* Provides a user-friendly UI on top of Spring Boot Actuator endpoints.
* Useful in microservices environments where you have many Spring Boot apps running.

---

### How Does It Work?

* Each Spring Boot app includes the **Actuator** endpoints.
* The Spring Boot Admin Server **connects to these apps** and fetches actuator data.
* It presents the data in an easy-to-understand UI with charts, status, logs, etc.

---

### Components of Spring Boot Admin

| Component                    | Role                                                                        |
| ---------------------------- | --------------------------------------------------------------------------- |
| **Spring Boot Admin Server** | Central dashboard app that collects and shows monitoring info               |
| **Spring Boot Admin Client** | Client dependency added to each Spring Boot app to register with the server |

---

### How to Use Spring Boot Admin?

1. **Add Spring Boot Admin Server** to your monitoring project:

```xml
<dependency>
  <groupId>de.codecentric</groupId>
  <artifactId>spring-boot-admin-starter-server</artifactId>
  <version>2.x.x</version>
</dependency>
```

2. **Enable Admin Server** with `@EnableAdminServer` on your main class.

3. In each Spring Boot app to be monitored, add the **client dependency**:

```xml
<dependency>
  <groupId>de.codecentric</groupId>
  <artifactId>spring-boot-admin-starter-client</artifactId>
  <version>2.x.x</version>
</dependency>
```

4. Configure the client to point to the Admin Server (usually via `application.properties`):

```properties
spring.boot.admin.client.url=http://localhost:8080
```

---

### Features

* Real-time **health status** and metrics dashboard
* **Log file** access and log level management
* View application **environment properties**
* **Thread dumps** and **heap dumps**
* Notification support for status changes
* Integration with security for access control

---

### Summary

| Feature                     | Description                                 |
| --------------------------- | ------------------------------------------- |
| Centralized monitoring      | Dashboard for many Spring Boot apps         |
| Based on Actuator endpoints | Leverages Actuator data for monitoring      |
| Easy to set up              | Minimal configuration on server and clients |
| Supports management         | Restart apps, change log levels             |

---

## 87. What is Spring Cloud Config?

**Spring Cloud Config** is a **configuration management tool** for distributed systems and microservices architectures.

It provides **server-side and client-side support** for externalized configuration in a centralized way, making it easier to manage configuration properties across multiple applications and environments.

---

### Why Use Spring Cloud Config?

* Centralizes configuration for all microservices and applications.
* Enables dynamic configuration updates without redeploying apps.
* Supports **versioned configurations** stored in Git, SVN, or filesystem.
* Simplifies managing different profiles/environments (dev, test, prod).
* Securely stores sensitive configuration data.

---

### Key Components

| Component         | Description                                                                                |
| ----------------- | ------------------------------------------------------------------------------------------ |
| **Config Server** | Central service that serves configuration properties from a backend (e.g., Git repository) |
| **Config Client** | Spring Boot apps that fetch configuration from Config Server on startup or refresh         |

---

### How It Works

1. The **Config Server** reads configuration files (YAML, properties) from a repository like Git.
2. Client apps query the Config Server for their configuration based on app name and profile.
3. Clients receive configuration remotely and use it as if it were local.
4. Supports **dynamic refresh** using Spring Cloud Bus or actuator endpoints.

---

### Example: Config Server Setup

Add dependency:

```xml
<dependency>
  <groupId>org.springframework.cloud</groupId>
  <artifactId>spring-cloud-config-server</artifactId>
</dependency>
```

Enable the server:

```java
@SpringBootApplication
@EnableConfigServer
public class ConfigServerApplication {
  public static void main(String[] args) {
    SpringApplication.run(ConfigServerApplication.class, args);
  }
}
```

Configure the server to point to Git repo in `application.yml`:

```yaml
server:
  port: 8888

spring:
  cloud:
    config:
      server:
        git:
          uri: https://github.com/your-repo/config-repo
```

---

### Example: Config Client Setup

Add dependency:

```xml
<dependency>
  <groupId>org.springframework.cloud</groupId>
  <artifactId>spring-cloud-starter-config</artifactId>
</dependency>
```

Configure client `application.yml`:

```yaml
spring:
  application:
    name: my-app
  cloud:
    config:
      uri: http://localhost:8888
      profile: dev
```

The client will fetch configuration from:

```
http://localhost:8888/my-app/dev
```

---

### Benefits

* Decouples configuration from code.
* Version control for configurations.
* Supports multiple environments/profiles easily.
* Can refresh configuration without restarting apps.
* Integrates with Spring Boot Actuator for refresh management.

---

## 88. How do you implement distributed configuration in Spring Boot?

Implementing **distributed configuration** in Spring Boot typically means managing configuration centrally for multiple applications or microservices, allowing them to share and dynamically update their configuration from a single source.

---

## How to Implement Distributed Configuration in Spring Boot

The most common and robust way is by using **Spring Cloud Config**, which provides a centralized configuration server and client support.

---

### Step-by-Step Guide

#### 1. Set up the **Spring Cloud Config Server**

* This server acts as the centralized place to serve configuration properties.
* It reads configuration from a **version-controlled backend** like Git, SVN, or file system.

Example:

* Add dependency to the Config Server project:

```xml
<dependency>
  <groupId>org.springframework.cloud</groupId>
  <artifactId>spring-cloud-config-server</artifactId>
</dependency>
```

* Enable Config Server in main class:

```java
@SpringBootApplication
@EnableConfigServer
public class ConfigServerApplication {
  public static void main(String[] args) {
    SpringApplication.run(ConfigServerApplication.class, args);
  }
}
```

* Configure the server (e.g., to use Git repo):

```yaml
server:
  port: 8888

spring:
  cloud:
    config:
      server:
        git:
          uri: https://github.com/your-org/config-repo
          search-paths: config
```

---

#### 2. Set up **Spring Cloud Config Client** in each microservice or application

* Add client dependency:

```xml
<dependency>
  <groupId>org.springframework.cloud</groupId>
  <artifactId>spring-cloud-starter-config</artifactId>
</dependency>
```

* Configure the client application to fetch config from the server:

```yaml
spring:
  application:
    name: my-service
  cloud:
    config:
      uri: http://localhost:8888
      profile: dev
```

* The client will fetch configuration from:

```
http://localhost:8888/my-service/dev
```

---

#### 3. Use `@RefreshScope` for dynamic configuration refresh

* To update configuration without restarting the app, annotate beans with `@RefreshScope`.
* Trigger refresh by calling Actuator’s `/actuator/refresh` endpoint (requires Spring Boot Actuator and spring-cloud-starter-actuator).

```java
@RefreshScope
@RestController
public class MyController {

    @Value("${some.property}")
    private String someProperty;

    @GetMapping("/property")
    public String getProperty() {
        return someProperty;
    }
}
```

---

#### 4. Optionally, use Spring Cloud Bus for auto-refresh across multiple instances

* Spring Cloud Bus can broadcast refresh events using a message broker (RabbitMQ or Kafka).
* When config changes, all instances receive refresh signals automatically.

---

### Summary

| Component        | Role                             |
| ---------------- | -------------------------------- |
| Config Server    | Centralized configuration source |
| Config Client    | Fetches config from server       |
| `@RefreshScope`  | Enables dynamic refresh          |
| Spring Cloud Bus | Broadcasts refresh events        |

---

### Benefits of Distributed Configuration

* Centralized and consistent configuration management.
* Easy environment/profile management.
* Dynamic updates without restarts.
* Version control and audit trail of config changes.

---

## 89. How does Spring Boot support microservices?

Spring Boot is one of the most popular frameworks to build microservices because it simplifies development with its features and integrates smoothly with the Spring ecosystem.

---

### 1. **Standalone, Lightweight Services**

* Spring Boot lets you build **standalone, self-contained applications** that embed a web server (like Tomcat or Jetty).
* No need to deploy WAR files or manage external app servers — each microservice can run independently.

### 2. **Embedded Web Servers**

* Each microservice can run with its own embedded server, simplifying deployment and scalability.
* Services start quickly and can be packaged as executable JARs.

### 3. **Spring Boot Actuator**

* Provides built-in production-ready features like **health checks**, **metrics**, **tracing**, and **monitoring**.
* Essential for managing microservices in production.

### 4. **Externalized Configuration with Spring Cloud Config**

* Supports centralized configuration management for multiple microservices.
* Configuration changes can be refreshed dynamically without restarting services.

### 5. **Service Discovery**

* Integrates with service registries like **Eureka** to enable automatic discovery of microservices.
* Microservices can register themselves and discover others dynamically.

### 6. **Load Balancing & Client-Side Discovery**

* Spring Cloud Netflix Ribbon or Spring Cloud LoadBalancer provide client-side load balancing.
* Allows resilient and scalable inter-service communication.

### 7. **API Gateway Integration**

* Works with API gateways (like Spring Cloud Gateway or Netflix Zuul) to handle routing, security, rate limiting, and monitoring of microservices.

### 8. **Distributed Tracing and Logging**

* Integration with tools like **Sleuth** and **Zipkin** for distributed tracing across services.
* Helps debug and monitor microservice workflows.

### 9. **Messaging & Event-Driven Architecture**

* Supports integration with messaging platforms (Kafka, RabbitMQ) via Spring Cloud Stream.
* Enables asynchronous communication between microservices.

### 10. **Security**

* Easily integrates with **Spring Security** and **Spring Security OAuth** to secure microservices.
* Supports OAuth2, JWT, and custom authentication mechanisms.

---

### Summary Table

| Feature                      | Benefit for Microservices                  |
| ---------------------------- | ------------------------------------------ |
| Embedded Servers             | Lightweight, easy deployment               |
| Actuator                     | Health checks, monitoring                  |
| Spring Cloud Config          | Centralized configuration management       |
| Service Discovery (Eureka)   | Dynamic service registration and discovery |
| Load Balancer (Ribbon)       | Client-side load balancing                 |
| API Gateway                  | Routing, security, and API management      |
| Distributed Tracing (Sleuth) | Debug and monitor microservice calls       |
| Messaging Integration        | Asynchronous inter-service communication   |
| Security Integration         | Secure microservices                       |

---

### Quick Example

```java
@SpringBootApplication
@RestController
public class UserServiceApplication {

    public static void main(String[] args) {
        SpringApplication.run(UserServiceApplication.class, args);
    }

    @GetMapping("/users/{id}")
    public User getUser(@PathVariable String id) {
        return new User(id, "John Doe");
    }
}
```

This small service can be part of a larger microservice ecosystem, easily configured and monitored with Spring Boot features.

---

## 90. What is service discovery and how is it done using Eureka?

Service discovery is a fundamental concept in microservices architecture, and **Eureka** is a popular tool for implementing it in the Spring ecosystem.

---

## What is Service Discovery?

**Service Discovery** is the process by which microservices dynamically find the network locations (IP addresses and ports) of other services they need to communicate with.

* Instead of hardcoding service addresses, services register themselves with a **service registry**.
* When a service needs to call another, it queries the registry to get the current location.
* This allows services to scale, move, or restart without breaking communication.

---

## Why is Service Discovery Important?

* **Dynamic environments:** Services may run on different hosts or ports at different times.
* **Load balancing:** Discover multiple instances of a service to distribute requests.
* **Fault tolerance:** Automatically detect unavailable services and route traffic accordingly.

---

## What is Eureka?

**Eureka** is a REST-based service registry developed by Netflix and integrated into the Spring Cloud Netflix stack.

* It acts as the **service registry server**.
* Microservices act as **clients** that register themselves with Eureka.
* Clients can also query Eureka to discover other service instances.

---

## How Service Discovery Works Using Eureka

### 1. Eureka Server (Service Registry)

* A standalone Spring Boot app with `@EnableEurekaServer`.
* Maintains a list of all registered service instances.
* Provides endpoints for clients to register and query services.

### 2. Eureka Client (Microservice)

* Each microservice adds the Eureka client dependency.
* On startup, it registers itself with Eureka Server.
* Periodically sends heartbeat signals to renew registration.
* Queries Eureka to discover other services.

---

## Example Setup

### Step 1: Create Eureka Server

**Add dependency:**

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
</dependency>
```

**Main class:**

```java
@SpringBootApplication
@EnableEurekaServer
public class EurekaServerApplication {
  public static void main(String[] args) {
    SpringApplication.run(EurekaServerApplication.class, args);
  }
}
```

**application.yml:**

```yaml
server:
  port: 8761

eureka:
  client:
    register-with-eureka: false
    fetch-registry: false
```

---

### Step 2: Create Eureka Client (Microservice)

**Add dependency:**

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>
```

**Main class:**

```java
@SpringBootApplication
@EnableEurekaClient
public class UserServiceApplication {
  public static void main(String[] args) {
    SpringApplication.run(UserServiceApplication.class, args);
  }
}
```

**application.yml:**

```yaml
spring:
  application:
    name: user-service

eureka:
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka/
```

---

### Step 3: Service Discovery in Action

* User service registers itself with Eureka Server at startup.
* Other services can discover `user-service` by querying Eureka.
* Spring Cloud provides `DiscoveryClient` or **Feign clients** to interact with discovered services easily.

---

### Summary Table

| Term             | Description                                           |
| ---------------- | ----------------------------------------------------- |
| Eureka Server    | Central registry that keeps track of services         |
| Eureka Client    | Microservice that registers itself & discovers others |
| Service Registry | Database of service locations                         |
| Heartbeat        | Regular signal sent by clients to stay registered     |
| Discovery        | Querying the registry to find service instances       |

---

## 91. How do you use Feign client in Spring Boot?

**Feign** is a declarative HTTP client developed by Netflix, and Spring Cloud integrates it seamlessly to simplify calling REST services between microservices.

---

## What is Feign Client?

* A way to define web service clients with simple Java interfaces.
* Automatically handles HTTP requests and responses.
* Works well with **Eureka service discovery** to call services by name.
* Supports load balancing, fallback, and interceptors.

---

## How to Use Feign Client in Spring Boot?

### Step 1: Add Dependencies

If you're using Spring Cloud, add:

```xml
<dependency>
  <groupId>org.springframework.cloud</groupId>
  <artifactId>spring-cloud-starter-openfeign</artifactId>
</dependency>
```

Also, ensure Eureka Client is added if you want service discovery:

```xml
<dependency>
  <groupId>org.springframework.cloud</groupId>
  <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>
```

---

### Step 2: Enable Feign Clients

In your main Spring Boot application class, enable Feign clients:

```java
@SpringBootApplication
@EnableFeignClients
public class MyApplication {
  public static void main(String[] args) {
    SpringApplication.run(MyApplication.class, args);
  }
}
```

---

### Step 3: Define a Feign Client Interface

Create an interface to represent the remote service.

```java
@FeignClient(name = "user-service")  // The name of the service registered in Eureka
public interface UserServiceClient {

    @GetMapping("/users/{id}")
    User getUserById(@PathVariable("id") String id);
}
```

* `@FeignClient(name = "user-service")`: This tells Feign to call the service named `user-service`.
* The method signature corresponds to the REST endpoint you want to call.

---

### Step 4: Use the Feign Client in Your Service or Controller

```java
@RestController
public class OrderController {

    private final UserServiceClient userServiceClient;

    public OrderController(UserServiceClient userServiceClient) {
        this.userServiceClient = userServiceClient;
    }

    @GetMapping("/orders/{orderId}/user")
    public User getUserForOrder(@PathVariable String orderId) {
        // Just an example - get user by id "123"
        return userServiceClient.getUserById("123");
    }
}
```

---

### Benefits of Using Feign

* Simplifies HTTP client code — no manual REST template or web client needed.
* Integrates with Ribbon for client-side load balancing.
* Works with Hystrix for circuit breaker support.
* Supports request interceptors for headers/authentication.
* Supports fallback methods for resilience.

---

### Optional: Adding Fallback

You can add fallback logic when the remote service is down:

```java
@FeignClient(name = "user-service", fallback = UserServiceFallback.class)
public interface UserServiceClient {
    @GetMapping("/users/{id}")
    User getUserById(@PathVariable("id") String id);
}

@Component
public class UserServiceFallback implements UserServiceClient {
    @Override
    public User getUserById(String id) {
        return new User(id, "Fallback User");
    }
}
```

---

### Summary

| Step           | What to Do                               |
| -------------- | ---------------------------------------- |
| Add dependency | Include `spring-cloud-starter-openfeign` |
| Enable Feign   | Use `@EnableFeignClients`                |
| Define client  | Annotate interface with `@FeignClient`   |
| Use client     | Inject and call the interface methods    |

---

## 92. What is Hystrix and circuit breaker pattern?

Understanding **Hystrix** and the **circuit breaker pattern** is essential for building resilient microservices.

---

## What is the Circuit Breaker Pattern?

The **Circuit Breaker** pattern is a design pattern used to detect failures and encapsulate the logic of preventing a failure from constantly recurring during maintenance, temporary external system failure, or unexpected system difficulties.

### Why use it?

* To **avoid cascading failures** in distributed systems.
* To **fail fast** when a service is down instead of waiting for timeouts.
* To provide a **fallback** mechanism when a service is unavailable.
* To **improve system stability** and user experience.

### How does it work?

* The circuit breaker monitors calls to a remote service.
* If the failure rate crosses a threshold (e.g., too many timeouts or errors), it "opens" the circuit.
* When open, calls are blocked and a fallback is triggered immediately without calling the remote service.
* After a timeout, the circuit breaker enters a "half-open" state to test if the remote service has recovered.
* If successful, it closes the circuit and resumes normal calls.

---

## What is Hystrix?

**Hystrix** is a latency and fault tolerance library from Netflix implementing the circuit breaker pattern for Java applications.

### Features:

* Circuit breaker logic for service calls.
* Thread and semaphore isolation to limit resource exhaustion.
* Fallback methods when calls fail.
* Request caching and request collapsing.
* Metrics and monitoring for real-time insight.

---

## How Hystrix Works in Spring Boot?

* You annotate methods that call remote services with `@HystrixCommand`.
* Define fallback methods for graceful degradation.
* Hystrix monitors those calls, opens/closes the circuit as needed.
* You can configure thresholds like timeout, error percentage, etc.

---

## Example

```java
@Service
public class PaymentService {

    @HystrixCommand(fallbackMethod = "paymentFallback")
    public String processPayment(String userId) {
        // Call to remote payment gateway or service
        // This could fail or timeout
        return restTemplate.getForObject("http://payment-service/pay/" + userId, String.class);
    }

    public String paymentFallback(String userId) {
        return "Payment service is currently unavailable. Please try again later.";
    }
}
```

---

## Summary Table

| Term            | Description                                  |
| --------------- | -------------------------------------------- |
| Circuit Breaker | Prevents repeated failed calls to a service  |
| Hystrix         | Netflix library implementing circuit breaker |
| Fallback        | Alternate method called on failure           |
| Open State      | Circuit is open, calls are blocked           |
| Half-Open State | Testing if the service has recovered         |
| Closed State    | Normal operation                             |

---

### Important Note:

Hystrix is in maintenance mode now, and newer projects often use **Resilience4j** which offers similar functionality with more modular design.

---

## 93. What is the role of API Gateway (e.g., Zuul or Spring Cloud Gateway)?

In microservices architecture, an **API Gateway** plays a crucial role as the single entry point for all client requests.

---

## What is an API Gateway?

An **API Gateway** is a server that acts as an intermediary between clients (like browsers, mobile apps) and backend microservices.

It handles all the client requests by routing them to the appropriate microservice and also provides cross-cutting features like security, rate limiting, and monitoring.

---

## Role of API Gateway in Microservices

1. **Request Routing & Load Balancing**
   Routes incoming requests to the correct microservice based on URL, headers, or other criteria.
   Can distribute requests across multiple instances for load balancing.

2. **Security**
   Handles authentication and authorization, e.g., validating JWT tokens before forwarding requests.

3. **Protocol Translation**
   Translates between different protocols, such as HTTP/HTTPS, WebSocket, gRPC, etc.

4. **Rate Limiting & Throttling**
   Controls traffic to prevent overload by limiting the number of requests per client or IP.

5. **Request/Response Transformation**
   Modify requests/responses — e.g., adding headers, rewriting URLs, aggregating responses.

6. **Caching**
   Cache frequent responses to improve performance and reduce load on backend services.

7. **Centralized Logging and Monitoring**
   Collect metrics, logs, and trace information for all requests passing through.

8. **API Composition / Aggregation**
   Combine responses from multiple services into a single response (helpful for frontend apps).

---

## Popular API Gateway Implementations

### 1. **Zuul** (Netflix OSS)

* A JVM-based gateway built on Servlet technology.
* Supports routing, filtering, and load balancing.
* Integrates with Eureka for service discovery.
* Zuul 1 (based on blocking I/O) is legacy; Zuul 2 is more reactive but less integrated with Spring.

### 2. **Spring Cloud Gateway**

* Built on **Spring WebFlux** (reactive, non-blocking).
* Provides a modern, scalable API gateway with a simple, Java DSL-based configuration.
* Supports routing, filtering, predicates, and integrates well with Spring Security and Spring Cloud ecosystem.
* Recommended over Zuul for new Spring Boot projects.

---

## Example of Spring Cloud Gateway Configuration

```yaml
spring:
  cloud:
    gateway:
      routes:
        - id: user-service
          uri: lb://user-service
          predicates:
            - Path=/users/**
          filters:
            - StripPrefix=1
```

* `lb://user-service` tells the gateway to use load balancing with service discovery.
* Routes `/users/**` paths to the `user-service`.
* `StripPrefix=1` removes the first path segment before forwarding.

---

## Summary Table

| Role                            | Description                              |
| ------------------------------- | ---------------------------------------- |
| Routing                         | Forward requests to appropriate services |
| Security                        | Handle auth (JWT, OAuth)                 |
| Rate Limiting                   | Prevent abuse and throttling             |
| Protocol Translation            | Support multiple protocols               |
| Request/Response Transformation | Modify requests and responses            |
| Caching                         | Cache responses to improve performance   |
| Monitoring                      | Centralize logs and metrics              |
| API Composition                 | Aggregate data from multiple services    |

---

## 94. What is the difference between monolith and microservice architecture?

Understanding the difference between **monolith** and **microservice** architectures is fundamental when designing modern software systems.

---

## Monolith Architecture

### Definition:

* A **monolithic application** is built as a single, unified unit.
* All components (UI, business logic, data access) reside and run together in one process.

### Characteristics:

* **Single codebase** and **single deployment**.
* Usually packaged as one executable or WAR/JAR file.
* Components tightly coupled and interdependent.
* Simple to develop initially, easier to test locally.

### Advantages:

* Easy to develop, test, and deploy for small apps.
* Simpler to debug since everything runs in one place.
* No inter-service communication overhead.

### Disadvantages:

* Difficult to scale specific parts independently.
* Hard to maintain as the application grows.
* Any change requires redeploying the entire application.
* Limits technology diversity — typically one tech stack.
* Risk of slowing down the entire app if one part fails.

---

## Microservice Architecture

### Definition:

* Breaks down the application into **small, independent services**.
* Each microservice handles a specific business capability.
* Services communicate over lightweight protocols (usually HTTP/REST).

### Characteristics:

* Each service has its own codebase and deployment.
* Loosely coupled and independently deployable.
* Can be developed and maintained by separate teams.
* Often polyglot (different services can use different languages/technologies).

### Advantages:

* Independent scalability of services.
* Fault isolation: failure in one service does not crash the whole app.
* Faster deployment cycles and continuous delivery.
* Flexibility in choosing tech stacks per service.
* Easier to understand smaller codebases.

### Disadvantages:

* More complex infrastructure and deployment.
* Requires robust inter-service communication and monitoring.
* Increased latency due to network calls.
* Handling data consistency and transactions is more challenging.

---

## Side-by-Side Comparison

| Aspect            | Monolith                         | Microservices                                  |
| ----------------- | -------------------------------- | ---------------------------------------------- |
| Structure         | Single unified app               | Multiple independent services                  |
| Deployment        | One deployment unit              | Multiple independent deployments               |
| Scalability       | Scale entire app                 | Scale services independently                   |
| Fault Isolation   | Failures affect whole app        | Failures isolated to individual services       |
| Development Speed | Faster initially                 | Faster over time with small teams              |
| Technology Stack  | Usually one stack                | Polyglot possible                              |
| Communication     | Internal method calls            | Network calls (REST, messaging)                |
| Testing           | Simpler unit/integration testing | More complex (distributed testing)             |
| Data Management   | Single database                  | Decentralized, per service databases           |
| Complexity        | Simpler initially                | Requires DevOps, monitoring, config management |

---

## Summary

* **Monolith**: Simple, unified app, great for small projects but less flexible as it grows.
* **Microservices**: Collection of small, autonomous services, great for large, complex systems needing scalability and flexibility but requires more infrastructure and management.

---

## 95. How do you containerize a Spring Boot application using Docker?

Containerizing a Spring Boot application with Docker allows you to package your app with its environment so it can run consistently anywhere.

---

## Steps to Containerize a Spring Boot App Using Docker

### Step 1: Create a Spring Boot Application

Make sure you have a working Spring Boot app packaged as a **jar**. Usually, you build it with:

```bash
./mvnw clean package
```

This generates a `target/myapp.jar` file.

---

### Step 2: Write a Dockerfile

Create a file named `Dockerfile` in the root of your project (same level as `pom.xml`).

Example Dockerfile:

```dockerfile
# Use an official OpenJDK runtime as a parent image
FROM openjdk:17-jdk-alpine

# Set the working directory inside the container
WORKDIR /app

# Copy the jar file into the container
COPY target/myapp.jar app.jar

# Expose the port that your Spring Boot app listens on
EXPOSE 8080

# Run the jar file
ENTRYPOINT ["java", "-jar", "app.jar"]
```

---

### Step 3: Build the Docker Image

Run the following command in your project root (where the Dockerfile is):

```bash
docker build -t my-spring-boot-app .
```

* `-t` tags your image (name it something meaningful).

---

### Step 4: Run the Docker Container

Once built, start the container:

```bash
docker run -p 8080:8080 my-spring-boot-app
```

* `-p 8080:8080` maps your machine’s port 8080 to the container’s port 8080.
* Now your app will be accessible at `http://localhost:8080`.

---

### Optional: Multi-Stage Dockerfile for Smaller Images

```dockerfile
# Build stage
FROM maven:3.8.5-openjdk-17 AS build
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn clean package -DskipTests

# Run stage
FROM openjdk:17-jdk-alpine
WORKDIR /app
COPY --from=build /app/target/myapp.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
```

This builds the jar inside the container (avoiding local dependencies) and copies the artifact to a lightweight runtime image.

---

## Summary

| Step              | Command / Action                             |
| ----------------- | -------------------------------------------- |
| Build jar         | `./mvnw clean package`                       |
| Create Dockerfile | Write Dockerfile as above                    |
| Build image       | `docker build -t my-spring-boot-app .`       |
| Run container     | `docker run -p 8080:8080 my-spring-boot-app` |

---

## 96. How do you deploy a Spring Boot application to Kubernetes?

Deploying a Spring Boot app to **Kubernetes** involves packaging your app into a container and then creating Kubernetes resources to run and manage it.

---

## Steps to Deploy a Spring Boot Application to Kubernetes

### Step 1: Containerize the Spring Boot App

* First, create a Docker image of your Spring Boot app (as we discussed earlier).
* Push the image to a container registry accessible by your Kubernetes cluster (e.g., Docker Hub, Google Container Registry, AWS ECR).

Example:

```bash
docker build -t your-dockerhub-username/my-spring-boot-app:latest .
docker push your-dockerhub-username/my-spring-boot-app:latest
```

---

### Step 2: Write Kubernetes Deployment YAML

Create a file called `deployment.yaml` to define a **Deployment** resource, which manages pods running your app.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: springboot-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: springboot-app
  template:
    metadata:
      labels:
        app: springboot-app
    spec:
      containers:
      - name: springboot-container
        image: your-dockerhub-username/my-spring-boot-app:latest
        ports:
        - containerPort: 8080
        env:
        - name: SPRING_PROFILES_ACTIVE
          value: "prod"
```

* `replicas: 3` means 3 pod instances for high availability.
* Replace `your-dockerhub-username/my-spring-boot-app:latest` with your actual image.
* You can add environment variables, config maps, secrets, etc., here.

---

### Step 3: Create a Service to Expose Your Application

Create a `service.yaml` file for a **Service** resource, which exposes your app inside or outside the cluster.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: springboot-service
spec:
  selector:
    app: springboot-app
  ports:
  - protocol: TCP
    port: 80        # Port exposed inside the cluster
    targetPort: 8080  # Container port your app listens on
  type: LoadBalancer  # Use NodePort or ClusterIP if LoadBalancer is not available
```

* `type: LoadBalancer` is for cloud environments (AWS, GCP, Azure).
* For local Kubernetes (like minikube), you might use `NodePort`.

---

### Step 4: Apply the Kubernetes Configuration

Use `kubectl` to deploy your app:

```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

Check pods:

```bash
kubectl get pods
```

Check services:

```bash
kubectl get svc
```

---

### Step 5: Access Your Application

* If using `LoadBalancer`, get the external IP from `kubectl get svc`.
* If using `NodePort`, access via `node-ip:node-port`.
* For `ClusterIP`, use port forwarding or an ingress controller.

Example port forwarding:

```bash
kubectl port-forward svc/springboot-service 8080:80
```

Access the app at `http://localhost:8080`.

---

## Bonus: Using ConfigMaps and Secrets

You can externalize configuration by creating **ConfigMaps** and **Secrets** in Kubernetes and referencing them in your Deployment.

---

## Summary Table

| Step                      | Command/Action                                      |
| ------------------------- | --------------------------------------------------- |
| Build & push Docker image | `docker build` & `docker push`                      |
| Create Deployment YAML    | Define deployment resource                          |
| Create Service YAML       | Define service to expose app                        |
| Apply config              | `kubectl apply -f deployment.yaml` & `service.yaml` |
| Verify pods/services      | `kubectl get pods` & `kubectl get svc`              |
| Access app                | Use external IP, NodePort, or port-forward          |

---

## 97. What are some best practices in Spring Boot?

Absolutely! Following best practices in Spring Boot development helps build robust, maintainable, and scalable applications. Here are some key best practices with explanations:

---

### 1. **Use Spring Boot Starters**

* Leverage Spring Boot starter dependencies (like `spring-boot-starter-web`, `spring-boot-starter-data-jpa`) to avoid manual dependency management.
* This keeps your build files clean and compatible.

---

### 2. **Externalize Configuration**

* Use `application.properties` or `application.yml` to store configurations.
* Support multiple profiles (e.g., `dev`, `test`, `prod`) to handle environment-specific settings.
* Avoid hardcoding configurations in code.

---

### 3. **Use Profiles Effectively**

* Define separate configurations for different environments using Spring Profiles.
* Activate profiles via `spring.profiles.active` property or environment variables.
* Keeps environment concerns separated and clean.

---

### 4. **Handle Exceptions Globally**

* Use `@ControllerAdvice` with `@ExceptionHandler` to centralize exception handling.
* Provides consistent error responses and cleaner controllers.

---

### 5. **Use DTOs for API Layer**

* Avoid exposing entity classes directly in APIs.
* Use Data Transfer Objects (DTOs) to control data exposure and validation.

---

### 6. **Implement Validation**

* Use `@Valid` and validation annotations (`@NotNull`, `@Size`, etc.) in DTOs.
* Ensure API inputs are validated before processing.

---

### 7. **Use Logging Properly**

* Use a logging framework (SLF4J + Logback).
* Log meaningful info at appropriate levels (INFO, DEBUG, ERROR).
* Avoid logging sensitive info like passwords or personal data.

---

### 8. **Write Unit and Integration Tests**

* Use `@SpringBootTest` for integration tests and Mockito for mocking dependencies.
* Ensure your critical code paths are well-tested.

---

### 9. **Secure Your Application**

* Use Spring Security for authentication and authorization.
* Protect sensitive endpoints.
* Implement JWT or OAuth2 if applicable.

---

### 10. **Use Actuator for Monitoring**

* Enable Spring Boot Actuator to expose health, metrics, and info endpoints.
* Monitor application health and performance in real-time.

---

### 11. **Use Proper Dependency Injection**

* Prefer constructor injection over field injection.
* Improves testability and immutability.

---

### 12. **Avoid Business Logic in Controllers**

* Keep controllers thin and delegate business logic to service layer.
* Improves separation of concerns and maintainability.

---

### 13. **Use Pagination and Sorting**

* For APIs returning lists, use pagination and sorting to improve performance.
* Spring Data JPA provides out-of-the-box support.

---

### 14. **Use Cache Wisely**

* Use Spring Cache abstraction for frequently accessed data.
* Improves response time and reduces DB load.

---

### 15. **Handle Transactions Properly**

* Use `@Transactional` annotation to manage database transactions.
* Avoid manual transaction management for cleaner code.

---

### 16. **Document APIs**

* Use Swagger/OpenAPI (`springdoc-openapi` or `springfox`) to generate interactive API docs.
* Makes your API easy to understand and consume.

---

### 17. **Optimize Startup Time**

* Avoid heavy initialization in `@PostConstruct`.
* Use lazy loading where applicable.
* Minimizes startup delays.

---

### 18. **Version Your APIs**

* Implement versioning in URLs or headers for backward compatibility.

---

### 19. **Use Health Checks**

* Use custom health indicators if needed.
* Integrate with container orchestrators like Kubernetes for readiness and liveness probes.

---

### Summary Table

| Best Practice             | Why it matters                      |
| ------------------------- | ----------------------------------- |
| Use Starters              | Simplifies dependency management    |
| Externalize Config        | Environment flexibility             |
| Profiles                  | Separate env configs                |
| Global Exception Handling | Cleaner, consistent error responses |
| Use DTOs                  | Data security & validation          |
| Input Validation          | Prevents bad data                   |
| Proper Logging            | Easier debugging & monitoring       |
| Testing                   | Code quality & reliability          |
| Security                  | Protects resources                  |
| Actuator                  | Monitoring & health checks          |
| Constructor Injection     | Testability & clarity               |
| Thin Controllers          | Separation of concerns              |
| Pagination                | Performance optimization            |
| Caching                   | Performance & scalability           |
| Transactions              | Data integrity                      |
| API Documentation         | Developer friendliness              |
| Optimize Startup          | Faster deployments                  |
| API Versioning            | Backward compatibility              |
| Health Checks             | Reliability & monitoring            |

---

## 98. How do you enable logging in Spring Boot?

Logging is essential for monitoring and debugging your Spring Boot application. Here’s a detailed explanation on how to enable and configure logging in Spring Boot:

---

## Logging in Spring Boot: Overview

* Spring Boot uses **SLF4J** (Simple Logging Facade for Java) as the logging API.
* The default logging implementation is **Logback**.
* You can also use other logging frameworks like Log4j2 or JUL (Java Util Logging) by adding dependencies.

---

## How to Enable Logging in Spring Boot

### 1. **Default Logging**

By default, Spring Boot has logging enabled out of the box. When you run a Spring Boot app, you get logs printed on the console, typically like this:

```
2025-05-15 10:30:00.123  INFO 12345 --- [           main] com.example.MyApp                       : Started MyApp in 3.456 seconds
```

No additional configuration is needed to get basic logging.

---

### 2. **Configuring Logging Levels**

You can control logging levels via the `application.properties` or `application.yml` files.

| Log Level | Description            |
| --------- | ---------------------- |
| TRACE     | Most detailed info     |
| DEBUG     | Debug-level info       |
| INFO      | General runtime events |
| WARN      | Potential problems     |
| ERROR     | Serious failures       |

Example in `application.properties`:

```properties
# Set root logging level
logging.level.root=INFO

# Set logging level for your package
logging.level.com.example=DEBUG

# Disable logging for a package
logging.level.org.springframework=WARN
```

Or in `application.yml`:

```yaml
logging:
  level:
    root: INFO
    com.example: DEBUG
    org.springframework: WARN
```

---

### 3. **Change Log Output Location**

By default, logs go to the console, but you can also write logs to a file.

In `application.properties`:

```properties
# Log to a file named app.log
logging.file.name=app.log
```

Or specify a folder (file name will default to spring.log):

```properties
logging.file.path=/var/log/myapp
```

---

### 4. **Customize Log Format**

You can customize the log pattern in `application.properties`:

```properties
logging.pattern.console=%d{yyyy-MM-dd HH:mm:ss} %-5level %logger{36} - %msg%n
```

---

### 5. **Use External Logging Configuration Files**

If you want more advanced logging control, you can provide your own Logback configuration file:

* Place a file named `logback-spring.xml` or `logback.xml` in `src/main/resources`.

Example minimal `logback-spring.xml`:

```xml
<configuration>
  <include resource="org/springframework/boot/logging/logback/defaults.xml"/>
  <property name="LOG_FILE" value="app.log"/>

  <appender name="FILE" class="ch.qos.logback.core.FileAppender">
    <file>${LOG_FILE}</file>
    <encoder>
      <pattern>%d{yyyy-MM-dd HH:mm:ss} %-5level %logger{36} - %msg%n</pattern>
    </encoder>
  </appender>

  <root level="INFO">
    <appender-ref ref="FILE"/>
  </root>
</configuration>
```

---

### 6. **Logging with Other Frameworks**

To use Log4j2 instead of Logback:

* Exclude default logging and add Log4j2 dependencies in `pom.xml` or `build.gradle`.
* Provide a `log4j2-spring.xml` config file.

---

### 7. **Programmatic Logging**

In your Java classes, use the SLF4J API:

```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class MyService {
    private static final Logger logger = LoggerFactory.getLogger(MyService.class);

    public void doSomething() {
        logger.info("Doing something");
        logger.debug("Detailed debug message");
    }
}
```

---

## Summary

| Aspect               | How to configure or use                         |
| -------------------- | ----------------------------------------------- |
| Enable basic logging | Default enabled by Spring Boot                  |
| Set logging level    | `logging.level.<package>=<level>` in properties |
| Log to file          | `logging.file.name` or `logging.file.path`      |
| Customize pattern    | `logging.pattern.console`                       |
| External config file | `logback-spring.xml` in resources               |
| Use other frameworks | Add dependencies, exclude default logging       |
| Use in code          | SLF4J `Logger` with `LoggerFactory`             |

---

## 99. How do you schedule tasks in Spring Boot?

Scheduling tasks in Spring Boot is straightforward thanks to Spring’s built-in support for task scheduling. Here’s a detailed explanation with examples to help you prep for your interview:

---

## How to Schedule Tasks in Spring Boot

### 1. **Enable Scheduling**

First, you need to enable scheduling in your Spring Boot application by adding the `@EnableScheduling` annotation to a configuration class or the main application class.

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.scheduling.annotation.EnableScheduling;

@SpringBootApplication
@EnableScheduling
public class MySpringBootApp {
    public static void main(String[] args) {
        SpringApplication.run(MySpringBootApp.class, args);
    }
}
```

---

### 2. **Create Scheduled Tasks**

You can create scheduled tasks by annotating methods with `@Scheduled`. Spring will run these methods according to the scheduling configuration you provide.

```java
import org.springframework.scheduling.annotation.Scheduled;
import org.springframework.stereotype.Component;

@Component
public class ScheduledTasks {

    // Runs every 5 seconds
    @Scheduled(fixedRate = 5000)
    public void fixedRateTask() {
        System.out.println("Fixed Rate Task - " + System.currentTimeMillis() / 1000);
    }

    // Runs 5 seconds after the last execution finishes
    @Scheduled(fixedDelay = 5000)
    public void fixedDelayTask() {
        System.out.println("Fixed Delay Task - " + System.currentTimeMillis() / 1000);
    }

    // Runs at 10:15 AM every day
    @Scheduled(cron = "0 15 10 * * ?")
    public void cronTask() {
        System.out.println("Cron Task - " + System.currentTimeMillis() / 1000);
    }
}
```

---

### Scheduling Parameters Explained

| Parameter      | Description                                                    | Example                                             |
| -------------- | -------------------------------------------------------------- | --------------------------------------------------- |
| `fixedRate`    | Runs method at a fixed interval, measured from the start time  | `fixedRate = 5000` (every 5s)                       |
| `fixedDelay`   | Runs method at a fixed delay after the last execution finishes | `fixedDelay = 5000` (5s after last run ends)        |
| `initialDelay` | Delay before the first execution                               | `initialDelay = 10000` (10s delay before first run) |
| `cron`         | Uses cron expression for flexible scheduling                   | `cron = "0 0 * * * *"` (top of every hour)          |

---

### 3. **Using `initialDelay`**

You can delay the first execution of a scheduled task:

```java
@Scheduled(fixedRate = 10000, initialDelay = 5000)
public void fixedRateWithInitialDelay() {
    System.out.println("Task runs every 10 seconds, starts after 5 seconds delay");
}
```

---

### 4. **Important Notes**

* Scheduled methods must have `void` return type and no arguments.
* Use `@Component` or another stereotype annotation on the class containing scheduled methods.
* For complex scheduling, cron expressions are very powerful.

---

### 5. **Enable Async for Long-Running Tasks (Optional)**

If your scheduled task takes time and you don’t want it to block other scheduled tasks, enable asynchronous execution:

```java
@EnableScheduling
@EnableAsync
@SpringBootApplication
public class MySpringBootApp {
    //...
}
```

Add `@Async` to scheduled methods:

```java
@Async
@Scheduled(fixedRate = 5000)
public void asyncScheduledTask() {
    // long running task here
}
```

Don’t forget to add `@EnableAsync`.

---

## Example Output

```
Fixed Rate Task - 1684159200
Fixed Delay Task - 1684159205
Cron Task - 1684159210
```

---

## Summary Table

| Annotation / Feature | Purpose                             |
| -------------------- | ----------------------------------- |
| `@EnableScheduling`  | Enable scheduling support           |
| `@Scheduled`         | Define scheduled methods            |
| `fixedRate`          | Run method at fixed intervals       |
| `fixedDelay`         | Run method after fixed delay        |
| `cron`               | Run method based on cron expression |
| `initialDelay`       | Delay first execution               |
| `@Async`             | Run scheduled method asynchronously |

---

## 100. What are some performance optimization tips in Spring Boot?

Optimizing performance in Spring Boot applications is key to building scalable and responsive systems. Here are some practical tips with explanations:

---

### 1. **Use Lazy Initialization**

* By default, Spring creates all singleton beans at startup, which can slow down startup time.
* Enable lazy initialization so beans are created only when needed.

```properties
spring.main.lazy-initialization=true
```

This speeds up startup and reduces memory footprint.

---

### 2. **Use Proper Caching**

* Use Spring Cache abstraction (`@Cacheable`, `@CacheEvict`) to cache expensive method results.
* Reduces repetitive database calls or computations.

Example:

```java
@Cacheable("users")
public User getUserById(Long id) { ... }
```

---

### 3. **Optimize Database Access**

* Use **pagination** and **sorting** in queries to avoid loading huge datasets.
* Use **projections** to fetch only needed fields.
* Use **connection pooling** (e.g., HikariCP, default in Spring Boot).

Example pagination:

```java
Page<User> findAll(Pageable pageable);
```

---

### 4. **Avoid N+1 Query Problem**

* Use **fetch joins** or **entity graphs** to load related entities efficiently.
* Helps reduce excessive queries to the database.

---

### 5. **Use Asynchronous Processing**

* Offload long-running tasks to asynchronous threads using `@Async`.
* Keeps API responses fast.

---

### 6. **Minimize Auto-Configuration Overhead**

* Exclude unnecessary auto-configurations with `@SpringBootApplication(exclude = {...})`.
* Avoids starting unused services.

---

### 7. **Tune JVM and Garbage Collection**

* Optimize JVM options for heap size, GC algorithm (e.g., G1GC).
* Profile and monitor GC pauses.

---

### 8. **Use HTTP/2 and Compression**

* Enable HTTP/2 to improve latency.
* Enable GZIP compression in Spring Boot (`server.compression.enabled=true`).

---

### 9. **Use Efficient Serialization**

* For REST APIs, use efficient JSON libraries like Jackson with proper configuration.
* Avoid serializing unnecessary fields with `@JsonIgnore`.

---

### 10. **Profile and Monitor Your Application**

* Use Spring Boot Actuator with Micrometer for metrics.
* Use tools like JProfiler, VisualVM, or YourKit to identify bottlenecks.

---

### 11. **Optimize Startup Time**

* Use `spring-boot-devtools` for faster development restarts.
* Remove unused dependencies.

---

### 12. **Use Static Resources Efficiently**

* Cache static resources and use CDN if applicable.
* Set proper cache headers.

---

### Summary Table

| Tip                        | Why it helps                       |
| -------------------------- | ---------------------------------- |
| Lazy Initialization        | Faster startup, reduced memory use |
| Caching                    | Reduces expensive calls            |
| Pagination                 | Avoids loading huge data sets      |
| Avoid N+1 Queries          | Reduces database load              |
| Async Processing           | Improves response times            |
| Exclude Unused Auto-config | Less overhead                      |
| JVM Tuning                 | Better memory and CPU utilization  |
| HTTP/2 + Compression       | Faster and smaller responses       |
| Efficient Serialization    | Smaller payloads, faster parsing   |
| Profiling & Monitoring     | Identifies bottlenecks             |
| Optimize Startup           | Faster deploys                     |
| Static Resource Caching    | Faster frontend load               |

---