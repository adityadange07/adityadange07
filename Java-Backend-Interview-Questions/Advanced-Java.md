## 41. What is JDBC architecture?

**Answer:**
JDBC (Java Database Connectivity) is a standard Java API (application programming interface) for database-independent connectivity between the Java programming language and a wide range of databases (SQL).
**Architecture Layers:**
1.  **JDBC API:** Provide standard interfaces (Connection, Statement, ResultSet) for application-to-JDBC Manager communication.
2.  **JDBC Driver Manager:** Manages a list of database drivers. It matches connection requests from the java application with the proper database driver.
3.  **JDBC Driver:** Communicates with the respective database server.

**Code Snippet:**
```java
// Standard Architecture Usage
Class.forName("com.mysql.cj.jdbc.Driver"); // Load Driver
Connection con = DriverManager.getConnection(url, user, password); // Connect
Statement stmt = con.createStatement(); // Create Statement
ResultSet rs = stmt.executeQuery("SELECT * FROM users"); // Execute Query
```

---

## 42. What are JDBC drivers types?

**Answer:**
There are 4 types of JDBC drivers:
1.  **Type-1 (JDBC-ODBC Bridge):** Translates JDBC calls to ODBC calls. Deprecated and removed in Java 8. **Slowest.**
2.  **Type-2 (Native-API Driver):** Converts JDBC calls into native C/C++ API calls of the database. Requires client-side library installation.
3.  **Type-3 (Network Protocol Driver):** Converts JDBC calls into a database-independent network protocol, which is then translated to a database protocol by a middleware server.
4.  **Type-4 (Thin Driver):** Converts JDBC calls directly into the vendor-specific database protocol. Pure Java. **Fastest** and most commonly used today.

**Code Snippet:**
```java
// Type-4 Driver (Most common in modern apps)
// Example: MySQL Connector/J
String url = "jdbc:mysql://localhost:3306/mydb";
// No native libraries needed on client machine.
```

---

## 43. What is connection pooling?

**Answer:**
Connection Pooling is a technique used to enhance performance by maintaining a **cache of database connections**.
*   **Problem:** Creating a new database connection for every request is expensive (network handshake, authentication).
*   **Solution:** A pool of connections is created at startup. When an application needs a connection, it borrows one from the pool, uses it, and returns it to the pool (instead of closing it).
*   **Tools:** HikariCP (Default in Spring Boot), Apache DBCP, C3P0.

**Code Snippet:**
```java
// HikariCP Configuration Example (Conceptual)
HikariConfig config = new HikariConfig();
config.setJdbcUrl("jdbc:mysql://localhost:3306/simpsons");
config.setUsername("bart");
config.setPassword("51mp50n");
config.setMaximumPoolSize(10); // Pool Size

HikariDataSource ds = new HikariDataSource(config);
Connection conn = ds.getConnection(); // Get from pool
// ... use conn ...
conn.close(); // Returns to pool, doesn't actually close
```

---

## 44. What is JNDI?

**Answer:**
JNDI (Java Naming and Directory Interface) is an API that allows applications to look up data and resources (like Databases, EJBs, JMS Queues) via a name.
*   **Use Case:** In a web server (Tomcat/JBoss), you configure the DataSource (DB connection) once in the server configuration. The web application uses JNDI to "lookup" this DataSource by name, decoupling the app from the database configuration.

**Code Snippet:**
```java
// JNDI Lookup in Java Code
Context ctx = new InitialContext();
// "jdbc/MyDataSource" is the name configured in server.xml/context.xml
DataSource ds = (DataSource) ctx.lookup("java:/comp/env/jdbc/MyDataSource");
Connection conn = ds.getConnection();
```

---

## 45. What is servlet lifecycle?

**Answer:**
A Servlet is a Java object that runs on a web server to handle HTTP requests. Its lifecycle is managed by the **Servlet Container** (e.g., Tomcat):
1.  **Loading & Instantiation:** The container loads the class and creates an instance.
2.  **Initialization (`init()`):** Called **once** to initialize resources (db connection, parameters).
3.  **Request Handling (`service()`):** Called **for each request**. It dispatches the request to `doGet()`, `doPost()`, etc. Multi-threaded.
4.  **Destruction (`destroy()`):** Called **once** when the servlet is removed or server shuts down. Used for cleanup.

**Code Snippet:**
```java
public class MyServlet extends HttpServlet {
    public void init() { 
        System.out.println("Servlet Initialized"); 
    }
    public void doGet(HttpServletRequest req, HttpServletResponse res) {
        System.out.println("Handling Request");
    }
    public void destroy() { 
        System.out.println("Servlet Destroyed"); 
    }
}
```

---

## 46. What is filter in servlet?

**Answer:**
A Filter is an object that can transform the request or response (header or content) or intercept the request **before** it reaches the Servlet.
*   **Usage:** Authentication checks, Logging, Data compression, Encryption, input validation.
*   It functions like a "Chain of Responsibility."

**Code Snippet:**
```java
public class AuthFilter implements Filter {
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) 
            throws IOException, ServletException {
        
        System.out.println("Checking Authentication...");
        // If valid, pass to next resource/servlet
        chain.doFilter(request, response);
        System.out.println("Response Generated.");
    }
}
```

---

## 47. What is session management?

**Answer:**
HTTP is a **stateless** protocol (server forgets client after response). Session Management is a mechanism to maintain the state (conversational state) of a user across multiple requests.
**Techniques:**
1.  **Cookies:** Small text data stored on the client browser.
2.  **URL Rewriting:** Appending session ID to the URL (`url;jsessionid=...`).
3.  **Hidden Form Fields:** Storing data in hidden HTML inputs.
4.  **HttpSession API:** Server-side session object (most secure and common).

**Code Snippet:**
```java
// Using HttpSession
HttpSession session = request.getSession(); // Create or Get existing
session.setAttribute("username", "JohnDoe"); // Store data

// In another request
String user = (String) session.getAttribute("username"); // Retrieve data
```

---

## 48. What is JSP lifecycle?

**Answer:**
JSP (JavaServer Pages) pages are eventually compiled into Servlets.
**Lifecycle Phases:**
1.  **Translation:** JSP file (.jsp) is translated into a Servlet source file (.java).
2.  **Compilation:** .java is compiled into .class.
3.  **Loading & Initialization (`jspInit()`):** Servlet class loaded and instance created.
4.  **Execution (`_jspService()`):** Handles requests (generates HTML).
5.  **Destruction (`jspDestroy()`):** Cleanup.

**Code Snippet:**
```jsp
<%-- This JSP code --%>
<html>
<body>
    <% out.println("Hello World"); %>
</body>
</html>

<%-- Becomes a Servlet roughly like: --%>
// public void _jspService(request, response) {
//     out.write("<html><body>");
//     out.print("Hello World");
//     out.write("</body></html>");
// }
```

---

## 49. Difference between forward and redirect.

**Answer:**
Both are used to navigate to a new resource, but they work differently.

| Feature | `request.getRequestDispatcher().forward()` | `response.sendRedirect()` |
| :--- | :--- | :--- |
| **Location** | Server-side (Internal). | Client-side (External). |
| **URL Bar** | **Unchanged**. User doesn't know. | **Changes** to the new URL. |
| **Requests** | Single Request (1 Round trip). | Two Requests (2 Round trips). |
| **Speed** | Faster. | Slower. |
| **Scope** | Can share request attributes. | Cannot share request attributes (new request). |

**Code Snippet:**
```java
// Forward: Pass data internally to JSP
request.setAttribute("msg", "Hi");
request.getRequestDispatcher("welcome.jsp").forward(request, response);

// Redirect: Tell browser to go to Google
response.sendRedirect("https://www.google.com");
```

---

## 50. What is cookie vs session?

**Answer:**

| Feature | Cookie | Session (HttpSession) |
| :--- | :--- | :--- |
| **Storage Location** | Client-side (Browser). | Server-side (Memory/DB). |
| **Security** | Less Secure (Can be edited/stolen). | More Secure (Only ID stored on client). |
| **Capacity** | Limited (~4KB). | Limited by Server Memory. |
| **Expiration** | Can persist indefinitely if set. | Expires after timeout (default 30 mins) or logout. |
| **Usage** | Storing trivial data (preferences, session ID). | Storing sensitive user data (Login state, Cart). |

**Code Snippet:**
```java
// Cookie
Cookie c = new Cookie("color", "blue");
c.setMaxAge(3600); // 1 hour
response.addCookie(c);

// Session
HttpSession s = request.getSession();
s.setAttribute("color", "blue"); // Stored on server
```

---


---

## 51. What is RMI?

**Answer:**
RMI (Remote Method Invocation) is an API that provides a mechanism to create distributed applications in Java.
*   It allows an object running in one JVM (Client) to invoke methods on an object running in another JVM (Server), possibly on a different machine.
*   **Key Components:**
    1.  **Stub:** Client-side proxy.
    2.  **Skeleton:** Server-side proxy (deprecated in newer versions).
    3.  **RMI Registry:** A directory service where the server registers the object and the client looks it up.

**Code Snippet:**
```java
// Server Interface
public interface Hello extends Remote {
    String sayHello() throws RemoteException;
}

// Client Lookup
Registry registry = LocateRegistry.getRegistry("localhost");
Hello stub = (Hello) registry.lookup("Hello");
String result = stub.sayHello(); // Remote call
```

---

## 52. What is serialization?

**Answer:**
Serialization is the process of converting the **state of an object into a byte stream**.
*   **Purpose:** To save the state of an object (Persistence) or to send it over a network (RMI, JMS).
*   **Mechanism:** The class must implement the `java.io.Serializable` marker interface.
*   **Deserialization:** The reverse process of converting a byte stream back into an object.

**Code Snippet:**
```java
// Serialization
User user = new User(1, "Alice");
ObjectOutputStream out = new ObjectOutputStream(new FileOutputStream("user.ser"));
out.writeObject(user);
out.close();

// Deserialization
ObjectInputStream in = new ObjectInputStream(new FileInputStream("user.ser"));
User u = (User) in.readObject();
```

---

## 53. What is transient keyword?

**Answer:**
The `transient` keyword is used in serialization.
*   If you define any data member as `transient`, it will **not be serialized**.
*   During deserialization, the transient variable gets its **default value** (e.g., `0` for int, `null` for objects), losing its original value.
*   **Use Case:** Security (sensitive fields like passwords) or saving space (calculated fields).

**Code Snippet:**
```java
class User implements Serializable {
    String username;
    transient String password; // Will not be saved

    // Constructor...
}
// After deserialization: username="Alice", password=null
```

---

## 54. What is Externalizable?

**Answer:**
`Externalizable` is an interface that extends `Serializable` and allows you to customize the serialization process.
*   **Control:** Unlike `Serializable` (where JVM handles everything automatically), `Externalizable` gives you full control over what to read/write.
*   **Methods:** You must implement `writeExternal(ObjectOutput out)` and `readExternal(ObjectInput in)`.
*   **Performance:** It can be faster than `Serializable` because you only serialize what is needed.
*   **Requirement:** The class **must** have a public no-arg constructor.

**Code Snippet:**
```java
public class User implements Externalizable {
    String name;
    
    @Override
    public void writeExternal(ObjectOutput out) throws IOException {
        out.writeObject(name); // Manually write fields
    }

    @Override
    public void readExternal(ObjectInput in) throws IOException, ClassNotFoundException {
        name = (String) in.readObject(); // Manually read fields
    }
}
```

---

## 55. What is ClassLoader?

**Answer:**
A ClassLoader is a part of the JRE that dynamically loads Java classes into the JVM during runtime.
*   Java classes are not loaded all at once; they are loaded when required by the application.
*   The `ClassLoader` utilizes the "Delegation Hierarchy Principle" to load classes.

**Code Snippet:**
```java
public class ClassLoaderTest {
    public static void main(String[] args) {
        // App ClassLoader
        System.out.println(ClassLoaderTest.class.getClassLoader()); 
        
        // Bootstrap ClassLoader (Returns null as it's written in C/C++)
        System.out.println(String.class.getClassLoader()); 
    }
}
```

---

## 56. Types of class loaders.

**Answer:**
There are 3 built-in ClassLoaders in Java:
1.  **Bootstrap ClassLoader:** The root. Loads core Java libraries located in `/jre/lib` (e.g., `rt.jar`, `java.lang.*`). Written in native code.
2.  **Extension (Platform) ClassLoader:** Loads extensions from `/jre/lib/ext` directory.
3.  **Application (System) ClassLoader:** Loads user-defined classes from the **Classpath** (environment variable or `-cp` flag).

**Hierarchy:** App -> delegates to Ext -> delegates to Bootstrap.

---

## 57. What is SPI?

**Answer:**
SPI (Service Provider Interface) is a mechanism for loose coupling and extensibility. It allows a service (interface) to have multiple implementations (providers) that can be discovered and loaded at runtime.
*   **Components:** Service Interface, Service Provider, `ServiceLoader` class.
*   **Use Case:** JDBC Drivers (DriverManager uses SPI to find drivers), SLF4J (finding logging implementation).

**Code Snippet:**
```java
// 1. Define Service
public interface PaymentGateway { void pay(); }

// 2. Client uses ServiceLoader to find implementations
ServiceLoader<PaymentGateway> loader = ServiceLoader.load(PaymentGateway.class);
for (PaymentGateway pg : loader) {
    pg.pay();
}
```

---

## 58. What is annotation processing?

**Answer:**
Annotation Processing is a compile-time tool that scans and processes annotations (`@Annotation`) in your source code.
*   **Processor:** A plugin to `javac` that can inspect code and generate new source files (Java, XML, etc.).
*   It **cannot verify** or modify existing methods/code, strictly generates **new** files.
*   **Use Case:** Lombok (generates getters/setters), Dagger (generates dependency injection code), JPA (metamodel generation).

**Code Snippet:**
```java
@SupportedAnnotationTypes("com.example.AutoLog")
public class LogProcessor extends AbstractProcessor {
    @Override
    public boolean process(Set<? extends TypeElement> annotations, RoundEnvironment roundEnv) {
        // Scan for @AutoLog and generate logging code...
        return true;
    }
}
```

---

## 59. What is dynamic proxy?

**Answer:**
Dynamic Proxy allows you to create an implementation of an interface **at runtime**, without writing a concrete class.
*   You provide an `InvocationHandler`. When a method is called on the proxy instance, it is redirected to the `invoke()` method of your handler.
*   It is the backbone of **AOP (Aspect Oriented Programming)** (e.g., Spring Transaction Management).

**Code Snippet:**
```java
interface Service { void execute(); }

Service proxy = (Service) Proxy.newProxyInstance(
    Service.class.getClassLoader(),
    new Class[]{Service.class},
    (proxyObj, method, argsList) -> { // InvocationHandler
        System.out.println("Before method");
        return null; 
    }
);

proxy.execute(); // Prints "Before method"
```

---

## 60. What is Bytecode?

**Answer:**
Bytecode is the instruction set for the Java Virtual Machine (JVM).
*   When you compile a Java file (`javac Test.java`), it produces a `.class` class file containing bytecode.
*   It is **platform-independent**. The same bytecode can run on any OS that has a JVM.
*   The JVM (Interpreter/JIT Compiler) translates this bytecode into machine-native code (binary) for execution.

**Code Snippet:**
```bash
# Compile to Bytecode
javac HelloWorld.java 

# View Bytecode (Human readable)
javap -c HelloWorld.class

# Output snippet:
# 0: getstatic     #2 // Field java/lang/System.out:Ljava/io/PrintStream;
# 3: ldc           #3 // String Hello
# 5: invokevirtual #4 // Method java/io/PrintStream.println:(Ljava/lang/String;)V
```
---

## 61. What is Java Agent?

**Answer:**
A Java Agent is a specialized JVM component that allows you to instrument programs running on the JVM.
*   It utilizes the **Instrumentation API** (`java.lang.instrument`).
*   **Purpose:** To modify bytecode at runtime (e.g., adding logging, performance monitoring, security checks) without changing the original source code.
*   **Execution:** Java Agents run **before** the `main` method of the application (via `premain` method).
*   **Usage:** APM tools (New Relic, AppDynamics), Profilers.

**Code Snippet:**
```java
// Agent Class
public class MyAgent {
    public static void premain(String agentArgs, Instrumentation inst) {
        System.out.println("Java Agent Running...");
        // inst.addTransformer(...) to modify bytecode
    }
}
// Run: java -javaagent:myagent.jar -jar myapp.jar
```

---

## 62. What is NIO?

**Answer:**
NIO (New IO, or Non-blocking IO) is a collection of Java APIs (from Java 1.4) that offer an alternative to standard IO.
*   **Key Components:**
    1.  **Buffers:** Containers for data (e.g., `ByteBuffer`). Data is read into a buffer and written from a buffer.
    2.  **Channels:** Open connections to I/O devices (Files, Sockets). They support non-blocking reads/writes.
    3.  **Selectors:** Allow a single thread to monitor multiple channels for events (Connect, Accept, Read, Write).

**Code Snippet:**
```java
RandomAccessFile file = new RandomAccessFile("data.txt", "r");
FileChannel channel = file.getChannel();
ByteBuffer buffer = ByteBuffer.allocate(48);

int bytesRead = channel.read(buffer); // Read into buffer
```

---

## 63. What is Blocking vs Non-blocking IO?

**Answer:**
*   **Blocking IO (Old IO - `java.io`):** When a thread invokes a read() or write(), it **blocks** (waits) until the data is fully read or written. The thread sits idle during this time. Good for simple apps, bad for scalability (requires one thread per connection).
*   **Non-blocking IO (NIO - `java.nio`):** A thread requests a read/write. If data is ready, it proceeds. If not, the thread **returns immediately** (doesn't wait/block) and can do other work. Ideal for handling thousands of concurrent connections (e.g., Chat servers).

**Code Snippet:**
```java
// Blocking (ServerSocket)
Socket socket = serverSocket.accept(); // Blocks until client connects

// Non-blocking (ServerSocketChannel)
channel.configureBlocking(false);
SocketChannel sc = channel.accept(); 
if (sc != null) { 
    // Connected 
} else { 
    // Not connected yet, continue doing other work 
}
```

---

## 64. What is memory-mapped file?

**Answer:**
A Memory-Mapped File is a feature of Java NIO (`FileChannel.map`) that maps a region of a file directly into the **virtual memory** of the process.
*   **Speed:** It is incredibly fast for large files because the OS handles the actual reading/writing (paging) directly between disk and memory, bypassing the JVM's heap and IO buffers.
*   **Risk:** If the program crashes, the OS eventually syncs data, but explicit `force()` ensures safety.
*   **Use Case:** High-performance DBs, large data processing (Kafka uses this).

**Code Snippet:**
```java
FileChannel channel = FileChannel.open(path, StandardOpenOption.READ, StandardOpenOption.WRITE);
// Map 10 MB file into memory
MappedByteBuffer mbb = channel.map(FileChannel.MapMode.READ_WRITE, 0, 1024 * 1024 * 10);

mbb.put(0, (byte) 97); // Write byte directly to memory/file
```

---

## 65. What is ForkJoin framework?

**Answer:**
The Fork/Join Framework (Java 7) is designed to simplify parallel programming for tasks that can be broken down recursively (Divide and Conquer).
*   **Work-Stealing Algorithm:** Idle threads "steal" tasks from the back of the queue of busy threads, ensuring all CPU cores are utilized efficiently.
*   **Core Classes:** `ForkJoinPool` (Executor), `RecursiveTask` (Task with result), `RecursiveAction` (Task without result).
*   It is the underlying engine for **Java 8 Parallel Streams**.

**Code Snippet:**
```java
class SumTask extends RecursiveTask<Long> {
    // ... splitting logic ...
    @Override
    protected Long compute() {
        if (workload < THRESHOLD) {
            return computeDirectly();
        } else {
            SumTask left = new SumTask(...);
            SumTask right = new SumTask(...);
            left.fork(); // Async execution
            return right.compute() + left.join(); // Wait and Combine
        }
    }
}
```

---

## 66. What is CompletableFuture chaining?

**Answer:**
`CompletableFuture` allows chaining multiple asynchronous steps, where the result of one step is passed to the next.
*   **`thenApply`:** Transform the result (Map). Returns `CompletableFuture<U>`.
*   **`thenCompose`:** Chain another asynchronous operation (FlatMap). Returns `CompletableFuture<U>`.
*   **`thenAccept`:** Consume the result (void return).

**Code Snippet:**
```java
CompletableFuture.supplyAsync(() -> getUser(1)) // Step 1: Get User
    .thenCompose(user -> getOrder(user.id))    // Step 2: Get Order (Async)
    .thenApply(order -> order.totalPrice)      // Step 3: Extract Price
    .thenAccept(price -> System.out.println("Total: " + price)); // Step 4: Print
```

---

## 67. What is reactive programming in Java?

**Answer:**
Reactive Programming is a paradigm focused on **asynchronous data streams** and the propagation of changes.
*   **Core Concept:** Non-blocking, Event-driven, Backpressure (Subscriber tells Publisher how much data it can handle).
*   **Libraries:** **Project Reactor** (Spring WebFlux), **RxJava**.
*   **Java 9 Flow API:** Standardized the interfaces (`Publisher`, `Subscriber`, `Subscription`, `Processor`) but didn't provide a full implementation.

**Code Snippet:**
```java
// Project Reactor Example
Flux.just("Red", "Green", "Blue")
    .map(String::toUpperCase)
    .subscribe(System.out::println); // Output: RED, GREEN, BLUE
```

---

## 68. What is WebSocket?

**Answer:**
WebSocket is a communication protocol that provides full-duplex (two-way) communication channels over a single TCP connection.
*   **Difference from HTTP:** HTTP is request-response (Client asks, Server gives). WebSocket allows the Server to **push** data to the Client anytime.
*   **Handshake:** Starts as an HTTP request with an `Upgrade` header, then switches to WebSocket protocol.
*   **Java Support:** `javax.websocket` (Reference Implementation: Tyrus), Spring WebSocket.

**Code Snippet:**
```java
// Server Endpoint
@ServerEndpoint("/chat")
public class ChatServer {
    @OnMessage
    public void onMessage(String message, Session session) throws IOException {
        System.out.println("Received: " + message);
        session.getBasicRemote().sendText("Echo: " + message);
    }
}
```

---

## 69. What is JMX?

**Answer:**
JMX (Java Management Extensions) is a technology for monitoring and managing Java applications, system objects, and devices.
*   **MBeans (Managed Beans):** Java objects that represent resources (memory, garbage collector, custom app stats) that you want to manage.
*   **JMX Agent:** Managing agent (MBeanServer) that exposes these MBeans.
*   **Client:** Tools like **JConsole** or **VisualVM** connect to the JMX Agent to view stats or invoke operations (e.g., clear cache, change log level runtime).

**Code Snippet:**
```java
// MBean Interface
public interface SystemConfigMBean {
    void setLogLevel(String level);
    String getLogLevel();
}

// Managed Resource
public class SystemConfig implements SystemConfigMBean { 
    // implementation 
}

// Registration
MBeanServer mbs = ManagementFactory.getPlatformMBeanServer();
mbs.registerMBean(new SystemConfig(), new ObjectName("com.example:type=SystemConfig"));
```

---

## 70. What is Java Module System?

**Answer:**
Introduced in **Java 9** (Project Jigsaw), the Java Module System allows grouping packages and resources into a **Module**.
*   **Goals:** Strong encapsulation (hide internal packages), explicit dependencies, smaller runtime images (jlink).
*   **`module-info.java`:** The descriptor file placed at the root of the module.
*   **Keywords:**
    *   `exports com.my.package`: Makes package public to other modules.
    *   `requires java.sql`: Declares dependency on another module.

**Code Snippet:**
```java
// module-info.java
module com.my.app {
    requires java.sql;       // Depends on SQL module
    exports com.my.service;  // Exposes service package
    // com.my.util package is HIDDEN by default (Encapsulation)
}
```