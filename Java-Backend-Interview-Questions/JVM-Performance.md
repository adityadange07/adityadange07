## 121. Explain JVM architecture in detail.

**Answer:**
The **JVM (Java Virtual Machine)** consists of three main subsystems:
1.  **Class Loader Subsystem:** Loads, links, and initializes class files (`.class`).
2.  **Runtime Data Areas (Memory):**
    *   **Method Area:** Class structures (metadata).
    *   **Heap:** Objects.
    *   **Stack:** Local variables, method calls.
    *   **PC Register:** Current instruction address.
    *   **Native Method Stack:** For native methods.
3.  **Execution Engine:**
    *   **Interpreter:** Reads bytecode line by line and executes.
    *   **JIT Compiler:** Compiles hot code to native code for performance.
    *   **Garbage Collector:** Manages memory.
4.  **JNI (Java Native Interface):** Interacts with Native Method Libraries (C/C++).

---

## 122. What are JVM memory areas?

**Answer:**
JVM memory is divided into 5 parts:
1.  **Heap Area:** Stores objects and arrays. Shared among all threads.
2.  **Java Stack Area:** Stores frames for method execution (local variables, operand stack). Per-thread.
3.  **Method Area (Metaspace):** Stores class structures (constants, fields, method data). Shared.
4.  **PC Register:** Holds the address of the current instruction being executed. Per-thread.
5.  **Native Method Stack:** Stores frames for native methods. Per-thread.

---

## 123. What is Heap vs Stack?

**Answer:**

| Feature | Heap (Memory) | Stack (Memory) |
| :--- | :--- | :--- |
| **Storage** | Objects and Instance Variables. | Local Variables and Method Calls. |
| **Visibility** | **Global** (Shared by all threads). | **Thread-Local** (Private to a thread). |
| **Size** | Large. Managed by Xms, Xmx. | Small. Managed by Xss. |
| **Cleanup** | Garbage Collector (GC). | Automatically when block/method exits (LIFO). |
| **Access** | Slower (Reference access). | Faster. |

**Code Snippet:**
```java
public void method() {
    int x = 10; // Stored in STACK
    Person p = new Person(); // Reference 'p' in STACK, Object in HEAP
}
```

---

## 124. What is Metaspace?

**Answer:**
**Metaspace** is a native memory region that replaced **PermGen** (Permanent Generation) in Java 8.
*   **Purpose:** Stores **Class Metadata** (Structure of classes, methods, fields).
*   **Location:** **Native Heap** (OS Memory), not the JVM Heap.
*   **Advantage:** Unlike PermGen (which had a fixed size leading to `OutOfMemoryError: PermGen space`), Metaspace auto-resizes based on OS memory availability.
*   **Tuning:** `-XX:MaxMetaspaceSize`.

---

## 125. What is Runtime Constant Pool?

**Answer:**
The **Runtime Constant Pool** is a per-class or per-interface runtime representation of the `constant_pool` table in a class file.
*   **Content:** Contains compile-time known numeric literals, method and field references.
*   **Location:** Stored within the **Method Area**.
*   **Resolution:** Symbolic references in the pool are resolved to direct references during runtime (Dynamic Linking).

---

## 126. What is Program Counter Register?

**Answer:**
The **PC (Program Counter) Register** is a small memory area.
*   **Per-Thread:** Each thread has its own PC Register.
*   **Function:** It holds the address of the **current instruction** being executed by the thread.
*   **Native Methods:** If the thread executes a native method, the PC register is undefined.

---

## 127. What is Native Method Stack?

**Answer:**
The **Native Method Stack** is similar to the Java Stack but is used for **Native Methods** (code written in C/C++).
*   **Usage:** Used when the JVM invokes JNI (Java Native Interface) methods.
*   **Allocation:** Usually allocated in C-Stack (native memory).
*   **Error:** Can throw `StackOverflowError` if recursion is too deep.

---

## 128. What is Class Loader subsystem?

**Answer:**
The **Class Loader Subsystem** is responsible for locating, loading, and initializing Java classes from `.class` files.
It performs three major roles:
1.  **Loading:** Finding the binary representation of a class and creating a `Class` object.
2.  **Linking:**
    *   **Verification:** Checks bytecode validity.
    *   **Preparation:** Allocates memory for static variables (default values).
    *   **Resolution:** Replaces symbolic references with direct references.
3.  **Initialization:** Executes static blocks and static variable assignments.

---

## 129. What is parent delegation model?

**Answer:**
The **Parent Delegation Model** is the hierarchy used by ClassLoaders to load a class.
*   **Flow:** When a ClassLoader receives a request to load a class:
    1.  It checks if the class is already loaded.
    2.  If not, it **delegates** the request to its **Parent**.
    3.  This continues up to the **Bootstrap ClassLoader**.
    4.  If the parent cannot find the class, the child ClassLoader attempts to load it.
*   **Hierarchy:** `Bootstrap` -> `Platform (Ext)` -> `App (System)`.
*   **Goal:** Security (prevents replacing core Java classes like `java.lang.String`).

---

## 130. What happens when a class is loaded?

**Answer:**
When a class is first referenced (e.g., `new MyClass()` or `MyClass.staticVar`):
1.  **Loading:** The JVM reads the `.class` file into memory.
2.  **Linking:** Bytecode is verified. Static variables get default memory (e.g., `int=0`).
3.  **Initialization:** The `<clinit>` method executes:
    *   Static initializers run.
    *   Static variables are assigned their actual values.
    *   This happens **only once** per class.

**Code Snippet:**
```java
class Demo {
    static int x = 10;
    static {
        System.out.println("Class Initialized");
    }
}
// Usage: Demo.x; // Loads class, prints "Class Initialized"
```

---



---

## 131. What objects are eligible for GC?

**Answer:**
An object is eligible for Garbage Collection when it is **unreachable** from any **GC Root**.
*   **scenarios:**
    1.  **Nullifying references:** `obj = null;`
    2.  **Reassigning references:** `obj = new Object();`
    3.  **Object created inside a method:** Becomes eligible after method execution completes.
    4.  **Island of Isolation:** Two objects reference each other but are not referenced by any active part of the application.

**Code Snippet:**
```java
public void test() {
    Person p1 = new Person();
    Person p2 = new Person();
    p1.friend = p2;
    p2.friend = p1;
    
    p1 = null;
    p2 = null;
    // Both p1 and p2 are eligible for GC (Island of Isolation)
}
```

---

## 132. How does GC work internally?

**Answer:**
GC works based on the **Generational Hypothesis**: "Most objects die young."
*   **Memory Structure:** Heap is divided into **Young Generation** (Eden, Survivor S0, S1) and **Old Generation** (Tenured).
*   **Process:**
    1.  New objects are created in **Eden**.
    2.  When Eden fills up, **Minor GC** runs. Alive objects move to Survivor spaces.
    3.  Objects that survive multiple GC cycles (threshold age) assume to be long-lived and move to **Old Generation**.
    4.  When Old Gen fills up, **Major/Full GC** runs.

---

## 133. What are GC roots?

**Answer:**
**GC Roots** are objects that are accessible from outside the heap and serve as the starting point for the reachability analysis (Marking phase).
*   **Examples:**
    *   **Class:** Classes loaded by system class loader.
    *   **Stack Local:** Local variables and parameters in the stack of valid threads.
    *   **JNI Local/Global:** References held by native code.
    *   **Synchronization Monitor:** Objects used as a monitor for synchronization.

---

## 134. Minor GC vs Major GC vs Full GC.

**Answer:**
| Type | Region Cleaned | Trigger | Impact |
| :--- | :--- | :--- | :--- |
| **Minor GC** | **Young Generation** (Eden + Survivor). | When Eden space is full. | Very fast. efficient. Frequent. |
| **Major GC** | **Old Generation**. | When Old Gen is full. | Slower than Minor GC. Often triggers Stop-the-world. |
| **Full GC** | **Entire Heap** (Young + Old) + **Metaspace**. | System.gc(), Low Memory. | Very Slow. Heavy "Stop-the-world" pause. |

---

## 135. What are different GC algorithms?

**Answer:**
1.  **Mark-Sweep:** Marks reachable objects, then sweeps (deletes) unreachable ones. **Issue:** Memory Fragmentation.
2.  **Mark-Sweep-Compact:** Marks, Sweeps, then Compacts memory (moves objects together) to solve fragmentation. **Issue:** Higher pause time.
3.  **Copying:** Splits memory into two halves. Copies live objects to the other half. **Used in:** Young Generation (Survivor spaces).

---

## 136. What is Serial GC?

**Answer:**
**Serial GC** is the simplest collector designed for **single-threaded** environments.
*   **Threads:** Uses a single thread for GC (Stop-the-world).
*   **Usage:** Client-side apps, small heaps, single-core CPUs.
*   **Flag:** `-XX:+UseSerialGC`

---

## 137. What is Parallel GC?

**Answer:**
**Parallel GC** (Throughput Collector) is the default in Java 8.
*   **Threads:** Uses **multiple threads** for Young Generation GC (Minor GC) and Old Generation GC (Major GC).
*   **Goal:** Maximize **Throughput** (Total work done / Time).
*   **Usage:** Backend servers where high throughput is prioritized over latency.
*   **Flag:** `-XX:+UseParallelGC`

---

## 138. What is CMS GC?

**Answer:**
**CMS (Concurrent Mark Sweep)** is designed for **Low Latency**.
*   **Mechanism:** It performs most of the GC work (marking) **concurrently** with the application threads (no stop-the-world).
*   **Drawback:** CPU intensive, suffers from memory fragmentation (no compaction).
*   **Status:** Deprecated in Java 9, Removed in Java 14.
*   **Flag:** `-XX:+UseConcMarkSweepGC`

---

## 139. What is G1 GC?

**Answer:**
**G1 (Garbage First) GC** is the default collector in Java 9+.
*   **Structure:** Divides the heap into many small, equal-sized **regions** (instead of contiguous Young/Old generations).
*   **Mechanism:** It prioritizes cleaning regions with the most garbage (Garbage-First).
*   **Goal:** Predictable **Pause Times** (Soft real-time). It compacts memory on the go.
*   **Usage:** Large Heap sizes (>4GB).
*   **Flag:** `-XX:+UseG1GC`

---

## 140. What is ZGC / Shenandoah?

**Answer:**
**ZGC** (Z Garbage Collector) and **Shenandoah** are ultra-low latency collectors.
*   **Goal:** Pause times **< 10ms** (often < 1ms), regardless of heap size (Scalable to Terabytes).
*   **Mechanism:** Performs strictly nearly all work (marking, compaction, relocation) **concurrently**.
*   **Usage:** Time-sensitive applications requiring consistent responsiveness.
*   **Flag:** `-XX:+UseZGC`, `-XX:+UseShenandoahGC`

---

## 141. How to analyze heap dump?

**Answer:**
A **Heap Dump** is a snapshot of the Java memory (Heap) at a specific moment.
*   **Tools:** Eclipse Memory Analyzer (MAT), VisualVM, jhat.
*   **Analysis:**
    1.  **Dominator Tree:** Find largest objects retaining memory.
    2.  **Histogram:** Count of instances per class (e.g., millions of String objects?).
    3.  **Leak Suspects Report:** Automated report identifying potential leaks.
    4.  **Path to GC Roots:** Why is an object being kept alive?

---

## 142. What is memory leak in Java?

**Answer:**
A **Memory Leak** in Java occurs when objects are **no longer needed** by the application but are **still referenced** (often unintentionally), preventing the Garbage Collector from removing them.
*   **Unintentional References:** Static collections (HashMap, List), Unclosed Resources (Streams, Connections), Listener/Callback registration without deregistration.
*   **Result:** `OutOfMemoryError: Java heap space`.

---

## 143. How to detect memory leak?

**Answer:**
1.  **Monitor Heap Usage:** Check visuals in **JConsole** or **VisualVM**. A healthy app has a "sawtooth" pattern (memory rises, GC drops it). A leak shows memory consistently rising until the crash.
2.  **Verbose GC:** Enable GC logging (`-Xlog:gc*`) to see if full GCs are failing to reclaim memory.
3.  **Heap Dump Comparison:** Take two dumps (one at start, one later) and compare instance counts.

---

## 144. What is JVisualVM / JConsole?

**Answer:**
Both are monitoring tools provided with the JDK (up to JDK 8, VisualVM separate later).
*   **JConsole:** Uses JMX (Java Management Extensions) to monitor Memory, Threads, Classes, and MBeans. Good for quick, high-level checks.
*   **VisualVM (jvisualvm):** More powerful "All-in-One". It integrates profiling, thread dumps, heap dumps, and plugins. It provides a better visual interface for CPU and Memory profiling.

---

## 145. What is JProfiler?

**Answer:**
**JProfiler** is a popular, commercial, third-party Java Profiler (alternatives: YourKit, Java Flight Recorder).
*   **Features:** Deep analysis of CPU hotspots, Memory allocations, Database connections (JDBC/JPA/Hibernate), Threads, and Deadlocks.
*   **Advantage:** Much more detailed and user-friendly than free tools. Capable of remote profiling production servers with low overhead.

---

## 146. What is thread dump?

**Answer:**
A **Thread Dump** is a snapshot of the state of all threads in the JVM at a specific moment.
*   **Content:** Thread Name, ID, State (RUNNABLE, BLOCKED, WAITING, TIMED_WAITING), Stack Trace (method calls).
*   **Command:** `jstack <pid>`, `kill -3 <pid>` (Linux), or via VisualVM.

---

## 147. How to analyze thread dump?

**Answer:**
Analyze top-down looking for:
1.  **BLOCKED Threads:** Threads waiting to acquire a lock held by another thread.
2.  **Deadlock:** Two threads cyclically waiting for each other (Dump usually says "Found one Java-level deadlock").
3.  **High CPU:** Look for RUNNABLE threads executing complex code.
4.  **Tools:** `fastthread.io`, TDA (Thread Dump Analyzer), Samurai.

---

## 148. What causes high CPU usage in Java app?

**Answer:**
1.  **Infinite Loops:** `while(true)` without sleep.
2.  **Complex Algorithms:** O(n^2) or worse on large datasets.
3.  **GC Thrashing:** Frequent Full GCs because heap is too small (CPU spent on GC, not app logic).
4.  **Heavy Serialization/Deserialization.**
5.  **Context Switching:** Too many threads competing for CPU.

---

## 149. What is OutOfMemoryError types?

**Answer:**
`java.lang.OutOfMemoryError` has several messages:
1.  **Java heap space:** Heap is full. Solution: Increase `-Xmx` or fix leak.
2.  **GC Overhead limit exceeded:** GC is spending 98% of time reclaiming < 2% of heap. Solution: Check for leaks/inefficient code.
3.  **Metaspace:** Metadata area full (too many classes). Solution: Increase `-XX:MaxMetaspaceSize`.
4.  **Request size bytes for reason. Out of swap space?**: Native memory issue.
5.  **StackOverflowError:** Deep recursion (technically separate error, but related to memory/stack limit `-Xss`).

---

## 150. How to tune JVM parameters?

**Answer:**
Key JVM flags for tuning:
*   **Heap Size:** `-Xms<size>` (Initial), `-Xmx<size>` (Max). Best practice: Set them equal to avoid resizing overhead.
*   **Stack Size:** `-Xss<size>` (Per-thread stack size).
*   **Metaspace:** `-XX:MaxMetaspaceSize=<size>`.
*   **GC Logging:** `-Xlog:gc*` (Java 9+).
*   **Heap Dump:** `-XX:+HeapDumpOnOutOfMemoryError` (Essential for post-mortem analysis).
*   **GC Algorithm:** `-XX:+UseG1GC` (Recommended mostly).

---

## 151. What is JIT compiler?

**Answer:**
The **JIT (Just-In-Time) Compiler** improves performance by compiling bytecode into native machine code at **runtime**.
*   **Process:**
    1.  The JVM initially interprets the bytecode.
    2.  It monitors ("profiles") the code to find "Hot Spots" (frequently executed methods/loops).
    3.  The JIT compiler compiles these hot spots into optimized native code.
    4.  Subsequent calls execute the native code directly, bypassing the interpreter.

---

## 152. What is escape analysis?

**Answer:**
**Escape Analysis** is an optimization technique used by the JIT compiler to determine the scope of a new object.
*   **Scope:** If an object is created in a method and *never escapes* that method (e.g., not returned, not assigned to a static field), it is considered "local".
*   **Result (Stack Allocation):** The JIT may allocate this object on the **Stack** instead of the Heap. This reduces GC pressure significantly.
*   **Result (Scalar Replacement):** It might break the object into its primitive fields and store them in registers.

---

## 153. What is biased locking?

**Answer:**
**Biased Locking** is an optimization for synchronized blocks that are accessed by only **one thread** most of the time.
*   **Concept:** The JVM "biases" the lock towards the first thread that acquires it.
*   **Benefit:** Subsequent lock acquisitions by the *same* thread are extremely cheap (no atomic CAS operations).
*   **Revocation:** If another thread tries to acquire the lock, the bias is revoked, and it upgrades to a normal lightweight lock.
*   **Status:** Deprecated in Java 15 due to complexity and cost of revocation.

---

## 154. What is lock elision?

**Answer:**
**Lock Elision** (or Lock Coarsening) involves removing unnecessary synchronization.
*   **Elision:** If Escape Analysis proves a lock object is local to a thread and never shared, the JIT removes the `synchronized` block entirely (e.g., using `StringBuffer` inside a method).
*   **Coarsening:** If the JIT sees repeated lock/unlock on the same object (e.g., inside a loop), it merges them into a single larger lock block.

---

## 155. What is safepoint?

**Answer:**
A **Safepoint** is a point in execution where the state of the JVM is consistent and known, allowing the JVM to perform maintenance tasks.
*   **Tasks:** Garbage Collection, JIT Deoptimization, Thread Dump, Revoking Biased Locks.
*   **Mechanism:** All application threads are paused (suspended) at a safe point before the JVM operation begins.
*   **Location:** Method exit, Loop back-edge.

---

## 156. What is stop-the-world event?

**Answer:**
A **Stop-The-World (STW)** event is a pause where all application threads are suspended by the JVM.
*   **Reason:** Usually triggered by **Garbage Collection** (specifically Major/Full GC) or other Safepoint operations.
*   **Impact:** The application becomes unresponsive during this time. Minimizing STW pauses is a primary goal of Low-Latency GCs (ZGC, Shenandoah).

---

## 157. What is inline caching?

**Answer:**
**Inline Caching** is an optimization for **Dynamic Dispatch** (virtual method calls).
*   **Concept:** The JVM caches the result of a method lookup (target method address) at the call site.
*   **Morphic:** If the call site always invokes the same implementation (e.g., `list.add` is always `ArrayList.add`), the JIT "inlines" the call, replacing the lookup with a direct call or the method body itself.
*   **Polymorphic:** If it calls different implementations, it falls back to a slower lookup.

---

## 158. What is AOT compilation?

**Answer:**
**AOT (Ahead-Of-Time) Compilation** compiles Java classes to native code **before** the application starts (at build time).
*   **Pros:** faster startup time (no JIT warmup needed), lower memory footprint.
*   **Cons:** Less peak performance than JIT (JIT can optimize based on runtime data which AOT lacks).
*   **Tool:** `jaotc` (Experimental in JDK 9, Removed in JDK 17). GraalVM Native Image is the modern successor.

---

## 159. What is GraalVM?

**Answer:**
**GraalVM** is a high-performance JDK distribution designed to accelerate execution of applications written in Java and other languages.
*   **Key Feature (Native Image):** Compiles Java apps into standalone native binaries (AOT). Instant startup, low memory. Ideal for Microservices/Serverless.
*   **Polyglot:** Allows mixing languages (Java, JS, Python, R) in the same runtime.
*   **Graal Compiler:** A new JIT compiler written in Java (can be used in standard HotSpot via `-XX:+UseJVMCICompiler`).

---

## 160. What is Java Flight Recorder?

**Answer:**
**JFR (Java Flight Recorder)** is a profiling and event collection framework built into the JVM.
*   **Low Overhead:** Designed to run continuously in production (< 1% performance impact).
*   **Data:** Captures GC events, Method execution, I/O latency, Thread stalls, Exceptions, CPU usage.
*   **Analysis:** Recordings (`.jfr` files) are analyzed using **Java Mission Control (JMC)**.


---

## 161. How to improve startup time?

**Answer:**
1.  **Class Data Sharing (CDS):** Share loaded class metadata between JVM processes to reduce loading time.
2.  **AOT Compilation:** Use `GraalVM Native Image` for instant startup.
3.  **Lazy Loading:** Initialize beans/resources only when needed (e.g., Spring `@Lazy`).
4.  **Reduce Classpath Scanning:** Limit the packages scanned by frameworks like Spring.
5.  **Minimize Static Initializers:** Avoid heavy logic in `static {}` blocks.

---

## 162. How to reduce GC pause time?

**Answer:**
1.  **Choice of GC:** Use Low-Latency collectors like **ZGC** or **Shenandoah** (sub-millisecond pauses).
2.  **Heap Size:** A very large heap might increase pause time in older GCs (G1 handles this better).
3.  **Reduce Allocation Rate:** Create fewer temporary objects (Reuse buffers, Flyweight pattern). Less garbage = Less frequent GC.
4.  **Object Pooling:** (Use with caution) Reuse expensive objects (e.g., DB Connections) to avoid churn.

---

## 163. How to optimize large collections?

**Answer:**
1.  **Sizing:** Always set **initial capacity** to avoid resizing overhead (array copying). `new ArrayList<>(10000)`.
2.  **Primitive Collections:** Use library like **Eclipse Collections** or **FastUtil** to avoid Auto-boxing overhead (saving generic `Integer` wrappers).
3.  **Off-Heap:** Store massive data in **DirectByteBuffer** or memory-mapped files to avoid GC overhead entirely.

---

## 164. When to use primitive collections?

**Answer:**
Use **Primitive Collections** (e.g., `IntList` instead of `List<Integer>`) when dealing with **large datasets** (millions of items).
*   **Memory:** `int` takes 4 bytes. `Integer` object takes ~24 bytes (Header + int + Ref). A `List<Integer>` has huge overhead.
*   **Performance:** Avoids CPU cost of **Autoboxing/Unboxing**.
*   **Libraries:** **Eclipse Collections**, **Trove**, **FastUtil**.

---

## 165. How to design memory-efficient objects?

**Answer:**
1.  **Object Header:** Remember every object in Java has a header (~12-16 bytes). Small objects have high overhead.
2.  **Primitives:** Use primitives (`int`, `long`) over wrappers (`Integer`, `Long`).
3.  **Arrays vs Objects:** Arrays have lower overhead than `ArrayList`.
4.  **Flyweight Pattern:** Share common instances (like `Boolean.TRUE`, `Integer.valueOf(1)`).

---

## 166. How to reduce object creation?

**Answer:**
1.  **String Concatenation:** Use `StringBuilder` explicitly in loops, or `String.format` (be careful with regex).
2.  **Reuse Mutable Objects:** Reuse `StringBuilder`, buffers, or arrays instead of creating new ones.
3.  **Singleton:** Use singletons for stateless service classes.
4.  **Canonicalization:** Intern strings/objects if they are duplicates.

---

## 167. How to optimize multi-threaded performance?

**Answer:**
1.  **Minimize Locking:** Use `java.util.concurrent` (ConcurrentHashMap) instead of `synchronized` collections.
2.  **Lock Granularity:** Use **Striped Locking** (e.g., LongAdder) to reduce contention.
3.  **Non-Blocking Algos:** Use **CAS** (Compare-And-Swap) via `AtomicInteger` for counters.
4.  **False Sharing:** Pad variables (`@Contended`) to prevent cache line ping-pong between threads.

---

## 168. What are common production performance issues?

**Answer:**
1.  **Slow Database Queries:** Missing indexes, N+1 problem.
2.  **Memory Leaks:** Unclosed resources, static collections growing indefinitely.
3.  **Thread Pool Exhaustion:** All threads blocked waiting for external service/DB.
4.  **CPU Spikes:** Infinite loops, excessive GC, or extensive crypto/regex operations.

---

## 169. What metrics do you monitor in production?

**Answer:**
Use the **RED** (Rate, Errors, Duration) or **USE** (Utilization, Saturation, Errors) method.
1.  **Latency:** Response time (Average, p95, p99).
2.  **Throughput:** Requests per second (RPS).
3.  **Error Rate:** Percentage of 5xx/4xx errors.
4.  **Saturation:** CPU Usage, Memory Usage, Disk I/O, Thread Pool active count.

---

## 170. How do you perform load testing?

**Answer:**
**Load Testing** simulates real-world usage to check system behavior.
*   **Tools:** **JMeter**, **Gatling**, **Locust**, **K6**.
*   **Types:**
    *   **Load Test:** Expected normal load.
    *   **Stress Test:** Push beyond limits to find breaking point.
    *   **Soak Test:** Run for long duration (24h+) to find memory leaks.
    *   **Spike Test:** Sudden burst of traffic.
