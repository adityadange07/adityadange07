## 96. What is thread lifecycle?

**Answer:**
A thread in Java goes through the following states (Lifecycle):
1.  **New:** Created but not yet started (`new Thread()`).
2.  **Runnable:** Ready to run. Waiting for CPU time (`thread.start()`).
3.  **Running:** Typically executing the `run()` method.
4.  **Blocked/Waiting:** Waiting for a resource (lock, I/O) or another thread (`wait()`, `join()`).
5.  **Terminated (Dead):** Finished execution or crashed.

**Code Snippet:**
```java
Thread t = new Thread(() -> {});
System.out.println(t.getState()); // NEW
t.start();
System.out.println(t.getState()); // RUNNABLE
```

---

## 97. Runnable vs Callable.

**Answer:*

| Feature | Runnable | Callable |
| :--- | :--- | :--- |
| **Return Type** | `void`. Cannot return a result. | `V`. Returns a result (Generic). |
| **Exception** | Cannot throw checked exceptions. | Can throw `Exception`. |
| **Package** | `java.lang` | `java.util.concurrent` |
| **Method** | `run()` | `call()` |
| **Usage** | Threads, ExecutorService (`execute()`). | ExecutorService (`submit()`). |

**Code Snippet:**
```java
// Runnable
Runnable r = () -> System.out.println("Running");

// Callable
Callable<Integer> c = () -> { return 42; };

ExecutorService exec = Executors.newFixedThreadPool(1);
exec.execute(r);
Future<Integer> future = exec.submit(c);
```

---

## 98. What is ExecutorService?

**Answer:**
`ExecutorService` is a higher-level replacement for working directly with `Thread`.
*   **Purpose:** It manages a pool of threads and assigns tasks (Runnable/Callable) to them.
*   **Benefits:**
    *   **Thread Reusability:** Avoids overhead of creating new threads for every task.
    *   **Task Scheduling:** Supports delayed and periodic execution (`ScheduledExecutorService`).
    *   **Lifecycle Management:** Provides methods to shut down the pool gracefully (`shutdown()`, `shutdownNow()`).

**Code Snippet:**
```java
ExecutorService es = Executors.newFixedThreadPool(2);
es.submit(() -> System.out.println("Task 1"));
es.submit(() -> System.out.println("Task 2"));
es.shutdown();
```

---

## 99. What is ThreadPool?

**Answer:**
A **Thread Pool** is a collection of pre-initialized threads standing by, ready to execute tasks.
*   **Mechanism:** Instead of creating a new thread for every request (which is expensive in terms of memory and CPU), tasks are submitted to a queue. The pool's threads consume tasks from this queue.
*   **Advantages:**
    *   Control over the number of active threads (prevents resource exhaustion).
    *   Faster response time (threads are already created).

---

## 100. Types of thread pools.

**Answer:**
The `Executors` factory class provides common thread pool configurations:
1.  **FixedThreadPool(n):** Fixed number of threads. Reuses them. Good for steady load.
2.  **CachedThreadPool:** Creates new threads as needed, but reuses idle ones. Threads terminate if idle for 60s. Good for many short-lived tasks.
3.  **SingleThreadExecutor:** Only one thread. Executes tasks sequentially. Good for ordering constraints.
4.  **ScheduledThreadPool:** Supports delayed and periodic execution.
5.  **WorkStealingPool (Java 8):** Creates a pool that uses all available processors (ForkJoinPool).

**Code Snippet:**
```java
ExecutorService fixed = Executors.newFixedThreadPool(5);
ExecutorService cached = Executors.newCachedThreadPool();
ExecutorService single = Executors.newSingleThreadExecutor();
```

---


## 101. What is Future?

**Answer:**
`Future` represents the **result of an asynchronous computation**.
*   **Purpose:** When you submit a task to an `ExecutorService`, it returns a `Future` object immediately. You can use this object to:
    1.  Check if the task is complete (`isDone()`).
    2.  Wait for the result (`get()` - blocks until ready).
    3.  Cancel the task (`cancel()`).
*   **Limitation:** The `get()` method is blocking. You cannot explicitly complete it or chain multiple futures (solved by `CompletableFuture` in Java 8).

**Code Snippet:**
```java
ExecutorService es = Executors.newFixedThreadPool(1);
Future<Integer> future = es.submit(() -> {
    Thread.sleep(1000);
    return 10;
});

// Do other work...
Integer result = future.get(); // Blocks for 1 sec
```

---

## 102. What is synchronization?

**Answer:**
Synchronization is a mechanism to control access to shared resources by multiple threads to prevent **Race Conditions** and ensuring **Thread Safety**.
*   **Monitor Lock:** Java uses an internal entity called a monitor (or lock) for synchronization.
*   **Keywords:**
    *   `synchronized` method: Locks the instance (this) or class (Class object for static methods).
    *   `synchronized` block: Locks a specific object. Preferred for smaller scope (better performance).

**Code Snippet:**
```java
class Counter {
    private int count = 0;
    
    // Only one thread can execute this at a time
    public synchronized void increment() {
        count++;
    }
}
```

---

## 103. What is intrinsic lock?

**Answer:**
Every object in Java has an **Intrinsic Lock** (or Monitor Lock) associated with it.
*   When a thread enters a `synchronized` method or block, it acquires the intrinsic lock of that object.
*   No other thread can acquire the same lock until the first thread releases it (exits the method/block).
*   It ensures **Mutual Exclusion** and **Visibility** of changes.

---

## 104. What is ReentrantLock?

**Answer:**
`ReentrantLock` (from `java.util.concurrent.locks`) is an advanced alternative to the `synchronized` keyword.
*   **Features:**
    *   **Fairness:** Can favor the longest-waiting thread (`new ReentrantLock(true)`).
    *   **TryLock:** Attempt to acquire lock without blocking (`tryLock()`).
    *   **Interruptible:** Can be interrupted while waiting for lock (`lockInterruptibly()`).
    *   **Explicit:** Must manually `lock()` and `unlock()` in a `finally` block.

**Code Snippet:**
```java
Lock lock = new ReentrantLock();
try {
    lock.lock();
    // Critical Section
} finally {
    lock.unlock(); // Always release in finally
}
```

---

## 105. What is ReadWriteLock?

**Answer:**
`ReadWriteLock` maintains a pair of locks: one for **Reading** and one for **Writing**.
*   **Rules:**
    *   **Multiple Readers:** Many threads can hold the Read Lock simultaneously (as long as no thread holds the Write Lock).
    *   **Single Writer:** Only one thread can hold the Write Lock (exclusive).
*   **Benefit:** Improves performance when reads are much more frequent than writes.

**Code Snippet:**
```java
ReadWriteLock rwLock = new ReentrantReadWriteLock();

// Reader
rwLock.readLock().lock();
try { /* Read data */ } finally { rwLock.readLock().unlock(); }

// Writer
rwLock.writeLock().lock();
try { /* Write data */ } finally { rwLock.writeLock().unlock(); }
```

---

## 106. What is volatile?

**Answer:**
The `volatile` keyword guarantees **Visibility** of changes to variables across threads.
*   **Problem:** Threads perform caching (CPU cache). A change by Thread A might not be immediately visible to Thread B.
*   **Solution:** Reads/Writes to a `volatile` variable bypass the cache and go directly to **Main Memory**.
*   **Constraint:** It does **NOT** guarantee Atomicity (e.g., `count++` is not safe with just `volatile`). Use it for flags or status variables.

**Code Snippet:**
```java
private volatile boolean running = true;

public void stop() { running = false; } // Thread safe visibility

public void run() {
    while (running) { // Will see the change immediately
        // Work
    }
}
```

---

## 107. What is happens-before relationship?

**Answer:**
**Happens-Before** is a concept in the Java Memory Model (JMM) that defines the partial ordering of actions.
*   If Action A *happens-before* Action B, then the JMM guarantees that the results of A are **visible** to B.
*   **Rules:**
    1.  **Program Order:** Each action in a thread happens-before later actions in that thread.
    2.  **Monitor Lock:** Unlocking a monitor happens-before locking same monitor.
    3.  **Volatile:** Write to `volatile` happens-before subsequent read of same volatile.
    4.  **Thread Start:** `thread.start()` happens-before any action in the started thread.

---

## 108. What is atomic variable?

**Answer:**
Atomic Variables (in `java.util.concurrent.atomic`) allow thread-safe, lock-free operations on single variables.
*   **Mechanism:** They use low-level CPU instructions like **CAS (Compare-And-Swap)** instead of locks.
*   **Classes:** `AtomicInteger`, `AtomicLong`, `AtomicBoolean`, `AtomicReference`.
*   **Performance:** Generally faster than `synchronized` for simple counters/flags.

**Code Snippet:**
```java
AtomicInteger count = new AtomicInteger(0);

// Thread-safe increment
int newValue = count.incrementAndGet(); // Returns updated value
```

---

## 109. What is CAS?

**Answer:**
**CAS (Compare-And-Swap)** is an atomic instruction supported by modern CPUs used to achieve synchronization without locks (Optimistic Concurrency).
*   **Logic:** It takes 3 operands:
    1.  **Memory Location (V)**
    2.  **Expected Old Value (A)**
    3.  **New Value (B)**
*   **Operation:** "If V == A, update V to B. Otherwise, do nothing."
*   **Loop:** Java loops this operation (retry) until it succeeds.

**Code Snippet:**
```java
// Conceptual implementation of increment()
do {
    int oldVal = get();
    int newVal = oldVal + 1;
} while (!compareAndSet(oldVal, newVal));
```

---

## 110. What is Deadlock?

**Answer:**
Deadlock is a situation where two or more threads are blocked forever, waiting for each other to release a lock.
*   **Scenario:** Thread A holds Lock 1 and waits for Lock 2. Thread B holds Lock 2 and waits for Lock 1.
*   **Prevention:**
    1.  **Lock Ordering:** Always acquire locks in a consistent fixed order (e.g., Lock 1 then Lock 2).
    2.  **Timeouts:** Use `tryLock(timeout)` to avoid waiting indefinitely.
    3.  **Global Lock:** Use a single coarse-grained lock (reduces concurrency).

**Code Snippet:**
```java
// Deadlock Example
Thread 1: synchronized(A) { synchronized(B) { ... } }
Thread 2: synchronized(B) { synchronized(A) { ... } } 
// If both start at same time -> Deadlock.

// Fix (Consistent Order)
Thread 2: synchronized(A) { synchronized(B) { ... } }
```

---

## 111. How to avoid deadlock?

**Answer:**
Deadlock can be avoided by breaking one of the four necessary conditions (Mutual Exclusion, Hold and Wait, No Preemption, Circular Wait).
**Strategies:**
1.  **Avoid Circular Wait:** Acquire locks in a consistent, **fixed global order**. If Thread A and Thread B need locks X and Y, both must acquire X first, then Y.
2.  **Avoid Hold and Wait:** Try to acquire all resources at once or release current locks before waiting for new ones.
3.  **Timeout:** Use `Lock.tryLock(long time, TimeUnit unit)` instead of blocking indefinitely. If the lock isn't acquired, back off and retry.
4.  **Deadlock Detection:** Use tools (JConsole, VisualVM) to detect deadlocks in running applications.

---

## 112. What is starvation?

**Answer:**
**Starvation** describes a situation where a thread is unable to gain regular access to shared resources and is unable to make progress.
*   **Causes:**
    *   **Priority:** Higher priority threads constantly preempt lower priority threads.
    *   **Greedy Threads:** A thread holds a lock for a very long time (e.g., infinite loop in `synchronized` block).
*   **Difference from Deadlock:** In deadlock, *threads are blocked forever waiting for each other*. In starvation, threads are *ready to run but never get selected by the scheduler*.
*   **Solution:** Use **Fair Locks** (`new ReentrantLock(true)`) which grant access in FIFO order.

---

## 113. What is livelock?

**Answer:**
**Livelock** is a situation where two or more threads act in response to each other to resolve a deadlock, but typically end up in a loop of state changes without making actual progress.
*   **Example:** Two people meeting in a narrow corridor. Person A moves left to let B pass, B moves right to let A pass. They block each other. Then A moves right, B moves left. They are *active* (moving), but stuck.
*   **Solution:** Introduce **Randomness** in the retry mechanism (e.g., Ethernet backoff algorithm).

---

## 114. What is ThreadLocal?

**Answer:**
`ThreadLocal` is a class that provides **Thread-Local Variables**.
*   These variables differ from normal variables in that each thread that accesses one (via `get` or `set` method) has its own, independently initialized copy of the variable.
*   **Isolation:** Changes made by one thread are **invisible** to other threads.
*   **Use Case:** Storing User ID, Transaction ID, or Database Connection for the duration of a request without passing it as a parameter to every method.
*   **Warning:** Must be cleaned up (`remove()`) to avoid **Memory Leaks**, especially in thread pools (e.g., Tomcat).

**Code Snippet:**
```java
ThreadLocal<Integer> threadLocalValue = ThreadLocal.withInitial(() -> 1);

new Thread(() -> {
    threadLocalValue.set(100);
    System.out.println(threadLocalValue.get()); // 100
}).start();

new Thread(() -> {
    System.out.println(threadLocalValue.get()); // 1 (Default)
}).start();
```

---

## 115. What is CyclicBarrier?

**Answer:**
`CyclicBarrier` is a synchronization aid that allows a set of threads to wait for each other to reach a common barrier point.
*   **Usage:** Breaking a large task into subtasks. All threads must finish their subtask before *any* thread proceeds to the next step.
*   **Reusable:** Unlike CountDownLatch, CyclicBarrier can be reset and reused after the barrier is broken.
*   **Action:** Can run a "barrier action" (Runnable) once all threads reach the barrier.

**Code Snippet:**
```java
CyclicBarrier barrier = new CyclicBarrier(3, () -> System.out.println("Barrier Broken!"));

Runnable r = () -> {
    System.out.println("Wait...");
    try { barrier.await(); } catch (Exception e) {}
    System.out.println("Proceed");
};
// Start 3 threads running 'r'
```

---

## 116. What is CountDownLatch?

**Answer:**
`CountDownLatch` is a synchronization aid that allows one or more threads to wait until a set of operations being performed in other threads completes.
*   **Mechanism:** Initialized with a `count`. Threads call `countDown()` to decrement. Waiting threads block on `await()` until count reaches zero.
*   **One-Shot:** Once the count reaches zero, it cannot be reset.
*   **Use Case:** Ensuring a server works only after all services (DB, Cache) are initialized.

**Code Snippet:**
```java
CountDownLatch latch = new CountDownLatch(3);

// Service Threads
latch.countDown(); 
latch.countDown();
latch.countDown();

// Main Server Thread
latch.await(); // Blocks until count is 0
System.out.println("All services up!");
```

---

## 117. What is Semaphore?

**Answer:**
`Semaphore` maintains a set of **permits**.
*   **Purpose:** To restrict the number of threads that can access a shared resource (Throttling/Rate Limiting).
*   **Methods:**
    *   `acquire()`: Takes a permit. Blocks if none available.
    *   `release()`: Returns a permit.
*   **Binary Semaphore:** A semaphore with 1 permit acts like a Lock (Mutex).

**Code Snippet:**
```java
Semaphore sem = new Semaphore(3); // Only 3 concurrent accesses

try {
    sem.acquire();
    // Access Resource
} finally {
    sem.release();
}
```

---

## 118. What is Phaser?

**Answer:**
`Phaser` (Java 7) is a reusable synchronization barrier, similar to CyclicBarrier and CountDownLatch, but more **flexible**.
*   **Dynamic:** The number of registered parties can change over time (register/deregister workers).
*   **Phasing:** Supports multiple phases of execution.
*   **Use Case:** Parallel algorithms where the number of tasks varies per phase.

---

## 119. What is parallel stream?

**Answer:**
A `parallelStream()` splits the stream into multiple chunks and processes them concurrently using the **ForkJoinPool.commonPool()**.
*   **Syntax:** `collection.parallelStream()` or `stream.parallel()`.
*   **Benefit:** Faster processing for large datasets on multi-core CPUs.
*   **Warning:**
    *   Order is not guaranteed (use `forEachOrdered` if needed).
    *   Shared mutable state must be synchronized.
    *   Can affect other tasks using the common pool.

**Code Snippet:**
```java
List<Integer> list = Arrays.asList(1, 2, 3, 4, 5);
list.parallelStream()
    .map(n -> n * 2)
    .forEach(System.out::println); // Order is random
```

---

## 120. What is ForkJoinPool?

**Answer:**
`ForkJoinPool` is an `ExecutorService` optimized for **recursive** divide-and-conquer tasks.
*   **Work-Stealing:** Threads that run out of tasks "steal" work from other busy threads' queues (Deques). This keeps all CPU cores busy.
*   **Common Pool:** Java 8 introduces a static common pool (`ForkJoinPool.commonPool()`) used by Parallel Streams and CompletableFuture by default.

**Code Snippet:**
```java
ForkJoinPool pool = new ForkJoinPool();
pool.invoke(new RecursiveTask<Integer>() { ... });
```
