
## 911. Reverse a string without using built-in methods.

**Answer:**
```java
public static String reverse(String str) {
    if (str == null) return null;
    char[] chars = str.toCharArray();
    int left = 0;
    int right = chars.length - 1;
    while (left < right) {
        char temp = chars[left];
        chars[left] = chars[right];
        chars[right] = temp;
        left++;
        right--;
    }
    return new String(chars);
}
```

---

## 912. Find duplicate elements in array.

**Answer:**
```java
// Using Set (O(n))
public static Set<Integer> findDuplicates(int[] nums) {
    Set<Integer> seen = new HashSet<>();
    Set<Integer> duplicates = new HashSet<>();
    for (int num : nums) {
        if (!seen.add(num)) {
            duplicates.add(num);
        }
    }
    return duplicates;
}
```

---

## 913. Find first non-repeating character.

**Answer:**
```java
public static Character firstNonRepeating(String str) {
    Map<Character, Integer> counts = new LinkedHashMap<>(); // Preserves order
    for (char c : str.toCharArray()) {
        counts.put(c, counts.getOrDefault(c, 0) + 1);
    }
    for (Map.Entry<Character, Integer> entry : counts.entrySet()) {
        if (entry.getValue() == 1) {
            return entry.getKey();
        }
    }
    return null;
}
```

---

## 914. Check if two strings are anagram.

**Answer:**
```java
public static boolean isAnagram(String s1, String s2) {
    if (s1.length() != s2.length()) return false;
    int[] count = new int[26]; // Assuming lowercase English letters
    for (int i = 0; i < s1.length(); i++) {
        count[s1.charAt(i) - 'a']++;
        count[s2.charAt(i) - 'a']--;
    }
    for (int c : count) {
        if (c != 0) return false;
    }
    return true;
}
```

---

## 915. Find factorial using recursion.

**Answer:**
```java
public static long factorial(int n) {
    if (n <= 1) return 1;
    return n * factorial(n - 1);
}
```

---

## 916. Fibonacci series using DP.

**Answer:**
```java
// Memoization (Top-Down)
public static int fib(int n, int[] memo) {
    if (n <= 1) return n;
    if (memo[n] != 0) return memo[n];
    memo[n] = fib(n - 1, memo) + fib(n - 2, memo);
    return memo[n];
}
```

---

## 917. Detect cycle in linked list.

**Answer:**
**Floyd’s Cycle-Finding Algorithm (Tortoise and Hare):**
```java
public boolean hasCycle(ListNode head) {
    if (head == null) return false;
    ListNode slow = head;
    ListNode fast = head;
    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
        if (slow == fast) return true; // Cycle detected
    }
    return false;
}
```

---

## 918. Reverse linked list.

**Answer:**
```java
public ListNode reverseList(ListNode head) {
    ListNode prev = null;
    ListNode current = head;
    while (current != null) {
        ListNode nextTemp = current.next;
        current.next = prev;
        prev = current;
        current = nextTemp;
    }
    return prev;
}
```

---

## 919. Implement stack using queue.

**Answer:**
```java
class MyStack {
    Queue<Integer> q = new LinkedList<>();

    public void push(int x) {
        q.add(x);
        // Rotate all previous elements to the back
        int size = q.size();
        while (size > 1) {
            q.add(q.remove());
            size--;
        }
    }

    public int pop() {
        return q.remove();
    }
}
```

---

## 920. Implement queue using stack.

**Answer:**
```java
class MyQueue {
    Stack<Integer> s1 = new Stack<>(); // Input
    Stack<Integer> s2 = new Stack<>(); // Output

    public void enQueue(int x) {
        s1.push(x);
    }

    public int deQueue() {
        if (s2.isEmpty()) {
            while (!s1.isEmpty()) {
                s2.push(s1.pop());
            }
        }
        return s2.pop();
    }
}
```

---

## 921. Find longest substring without repeating characters.

**Answer:**
**Sliding Window Technique:**
```java
public int lengthOfLongestSubstring(String s) {
    Set<Character> set = new HashSet<>();
    int left = 0, right = 0, max = 0;
    while (right < s.length()) {
        if (!set.contains(s.charAt(right))) {
            set.add(s.charAt(right++));
            max = Math.max(max, right - left);
        } else {
            set.remove(s.charAt(left++));
        }
    }
    return max;
}
```

---

## 922. Find majority element.

**Answer:**
Element appearing > n/2 times. **Boyer-Moore Voting Algorithm**:
```java
public int majorityElement(int[] nums) {
    int count = 0;
    Integer candidate = null;
    for (int num : nums) {
        if (count == 0) candidate = num;
        count += (num == candidate) ? 1 : -1;
    }
    return candidate;
}
```

---

## 923. Binary search implementation.

**Answer:**
(Requires sorted array).
```java
public int binarySearch(int[] arr, int target) {
    int left = 0, right = arr.length - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == target) return mid;
        if (arr[mid] < target) left = mid + 1;
        else right = mid - 1;
    }
    return -1;
}
```

---

## 924. Merge two sorted arrays.

**Answer:**
```java
public int[] merge(int[] arr1, int[] arr2) {
    int n1 = arr1.length, n2 = arr2.length;
    int[] result = new int[n1 + n2];
    int i = 0, j = 0, k = 0;
    while (i < n1 && j < n2) {
        if (arr1[i] <= arr2[j]) result[k++] = arr1[i++];
        else result[k++] = arr2[j++];
    }
    while (i < n1) result[k++] = arr1[i++];
    while (j < n2) result[k++] = arr2[j++];
    return result;
}
```

---

## 925. Find missing number in array.

**Answer:**
Array contains 0 to n, one missing.
```java
public int missingNumber(int[] nums) {
    int n = nums.length;
    int expectedSum = n * (n + 1) / 2;
    int actualSum = 0;
    for (int num : nums) actualSum += num;
    return expectedSum - actualSum;
}
```

---

## 926. Two sum problem.

**Answer:**
Find indices of two numbers that add up to target.
```java
public int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        int complement = target - nums[i];
        if (map.containsKey(complement)) {
            return new int[] { map.get(complement), i };
        }
        map.put(nums[i], i);
    }
    throw new IllegalArgumentException("No solution");
}
```

---

## 927. LRU cache implementation.

**Answer:**
Using Java's `LinkedHashMap`:
```java
class LRUCache<K, V> extends LinkedHashMap<K, V> {
    private final int capacity;

    public LRUCache(int capacity) {
        super(capacity, 0.75f, true); // true = access-order
        this.capacity = capacity;
    }

    @Override
    protected boolean removeEldestEntry(Map.Entry<K, V> eldest) {
        return size() > capacity;
    }
}
```

---

## 928. Implement custom HashMap.

**Answer:**
Simple Chaining implementation:
```java
class MyHashMap<K, V> {
    class Node { K key; V value; Node next; }
    private Node[] buckets = new Node[16];

    public void put(K key, V value) {
        int idx = key.hashCode() % buckets.length;
        Node node = buckets[idx];
        while (node != null) {
            if (node.key.equals(key)) { node.value = value; return; }
            node = node.next;
        }
        Node newNode = new Node();
        newNode.key = key; newNode.value = value; newNode.next = buckets[idx];
        buckets[idx] = newNode;
    }
    // get() similar logic...
}
```

---

## 929. Producer-consumer problem.

**Answer:**
Using `BlockingQueue` (Thread-safe):
```java
BlockingQueue<Integer> queue = new ArrayBlockingQueue<>(10);

// Producer
new Thread(() -> {
    try { while(true) queue.put(produce()); } catch (InterruptedException e) {}
}).start();

// Consumer
new Thread(() -> {
    try { while(true) consume(queue.take()); } catch (InterruptedException e) {}
}).start();
```

---

## 930. Thread-safe singleton implementation.

**Answer:**
**Double-Checked Locking:**
```java
public class Singleton {
    private static volatile Singleton instance;
    private Singleton() {}

    public static Singleton getInstance() {
        if (instance == null) {
            synchronized (Singleton.class) {
                if (instance == null) {
                    instance = new Singleton();
                }
            }
        }
        return instance;
    }
}
```

---

## 931. Deadlock example and solution.

**Answer:**
**Deadlock** occurs when two threads wait for each other to release a lock.
```java
// Deadlock Scenario
Thread 1: locks A, waits for B
Thread 2: locks B, waits for A

// Solution: Lock Order
// Always acquire locks in the same order (e.g., A then B) to avoid cyclical dependency.
synchronized(A) {
    synchronized(B) {
        // critical section
    }
}
```

---

## 932. Design rate limiter in code.

**Answer:**
**Token Bucket Algorithm (Simplified):**
```java
public class RateLimiter {
    private int tokens;
    private final int maxTokens;
    private long lastRefillTime;

    public synchronized boolean allowRequest() {
        refill();
        if (tokens > 0) {
            tokens--;
            return true;
        }
        return false;
    }

    private void refill() {
        long now = System.currentTimeMillis();
        if (now - lastRefillTime > 1000) { // Refill every second
            tokens = maxTokens;
            lastRefillTime = now;
        }
    }
}
```

---

## 933. Find top K frequent elements.

**Answer:**
Using **Min-Heap**:
```java
public int[] topKFrequent(int[] nums, int k) {
    Map<Integer, Integer> count = new HashMap<>();
    for (int n : nums) count.put(n, count.getOrDefault(n, 0) + 1);

    PriorityQueue<Integer> heap = new PriorityQueue<>(
        (a, b) -> count.get(a) - count.get(b) // Min heap based on frequency
    );

    for (int n : count.keySet()) {
        heap.add(n);
        if (heap.size() > k) heap.poll();
    }

    return heap.stream().mapToInt(i -> i).toArray();
}
```

---

## 934. Implement Trie (Prefix Tree).

**Answer:**
```java
class Trie {
    class Node {
        Node[] children = new Node[26];
        boolean isEnd;
    }
    Node root = new Node();

    public void insert(String word) {
        Node node = root;
        for (char c : word.toCharArray()) {
            if (node.children[c - 'a'] == null)
                node.children[c - 'a'] = new Node();
            node = node.children[c - 'a'];
        }
        node.isEnd = true;
    }
    // search() and startWith() follow similar path traversal logic.
}
```

---

## 935. Check palindrome in linked list.

**Answer:**
1.  Find Middle (Slow/Fast pointers).
2.  Reverse the second half.
3.  Compare first half and reversed second half.

---

## 936. Rotate array.

**Answer:**
Rotate right by K steps.
**Algorithm:**
1.  Reverse entire array.
2.  Reverse first K elements.
3.  Reverse remaining elements.
*   Example: `[1,2,3,4,5]`, k=2 -> `[5,4,3,2,1]` -> `[4,5,3,2,1]` -> `[4,5,1,2,3]`.

---

## 937. Find median of two sorted arrays.

**Answer:**
**Binary Search** on the smaller array to partition both arrays such that:
*   `left_part_size == right_part_size`
*   `max(left_part) <= min(right_part)`
*   Time Complexity: **O(log(min(n, m)))**.

---

## 938. Design parking lot system.

**Answer:**
**LLD (Low Level Design) Key Classes:**
*   `ParkingLot`: Singleton pattern, manages levels.
*   `Level`: Contains list of spots.
*   `Spot`: Type (Compact, Large), Availability status.
*   `Vehicle`: (Car, Truck, Bike).
*   `Ticket`: EntryTime, SpotID.
*   **Logic:** `findSpot()` iterates levels/spots to find first available for vehicle type.

---

## 939. Design elevator system.

**Answer:**
**LLD Key Classes:**
*   `ElevatorController`: Manages multiple elevators (Strategy to pick best one).
*   `Elevator`: CurrentFloor, Direction (UP/DOWN/IDLE), RequestQueue.
*   `Request`: Floor, Direction.
*   **Algorithm:** **SCAN (Elevator Algorithm)** - Move same direction until no requests, then switch.

---

## 940. Design ATM system.

**Answer:**
**LLD Key Classes:**
*   `ATM`: Has CardReader, Keypad, Dispenser, connect to BankAPI.
*   `Account`: CheckBalance, Deduct.
*   `Transaction`: (Withdrawal, Deposit, BalanceCheck) - **Strategy Pattern**.
*   **States:** Idle -> CardInserted -> PinEntered -> SelectingOption -> Transaction -> EjectCard (**State Pattern**).

---

## 941. Implement Observer pattern.

**Answer:**
Defines a one-to-many dependency between objects.
```java
interface Observer { void update(String msg); }

class Subscriber implements Observer {
    public void update(String msg) { System.out.println("Received: " + msg); }
}

class Topic {
    private List<Observer> observers = new ArrayList<>();
    public void addObserver(Observer o) { observers.add(o); }
    public void notifyObservers(String msg) {
        for (Observer o : observers) o.update(msg);
    }
}
```

---

## 942. Implement Strategy pattern.

**Answer:**
Defines a family of algorithms and makes them interchangeable.
```java
interface PaymentStrategy { void pay(int amount); }

class CreditCardPayment implements PaymentStrategy {
    public void pay(int amount) { System.out.println("Paid " + amount + " via Card"); }
}

class PayPalPayment implements PaymentStrategy {
    public void pay(int amount) { System.out.println("Paid " + amount + " via PayPal"); }
}

class ShoppingCart {
    public void checkout(int amount, PaymentStrategy strategy) {
        strategy.pay(amount);
    }
}
```

---

## 943. Implement custom annotation.

**Answer:**
Creating a `@LogExecutionTime` annotation.
```java
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
public @interface LogExecutionTime {}

// Usage with AspectJ usually:
@Around("@annotation(LogExecutionTime)")
public Object logTime(ProceedingJoinPoint joinPoint) throws Throwable {
    long start = System.currentTimeMillis();
    Object proceed = joinPoint.proceed();
    long executionTime = System.currentTimeMillis() - start;
    System.out.println(joinPoint.getSignature() + " executed in " + executionTime + "ms");
    return proceed;
}
```

---

## 944. Implement thread pool.

**Answer:**
Simplified version:
```java
class SimpleThreadPool {
    private final BlockingQueue<Runnable> taskQueue;
    private final List<Thread> workers;

    public SimpleThreadPool(int numThreads) {
        taskQueue = new LinkedBlockingQueue<>();
        workers = new ArrayList<>();
        for (int i = 0; i < numThreads; i++) {
            Thread worker = new Thread(() -> {
                while (true) {
                    try { taskQueue.take().run(); } catch (InterruptedException e) {}
                }
            });
            worker.start();
            workers.add(worker);
        }
    }

    public void submit(Runnable task) { taskQueue.offer(task); }
}
```

---

## 945. Solve concurrency issue in code snippet.

**Answer:**
**Problem:** `count++` is not atomic. Multi-threaded access causes lost updates / race conditions.
**Solution:**
1.  Use `AtomicInteger`: `count.incrementAndGet()`.
2.  Or `synchronized` block/method.
3.  Or `ReentrantLock`.

---

## 946. Optimize slow algorithm.

**Answer:**
**Scenario:** Finding duplicates in an array using nested loops (O(n²)).
**Optimization:** Use a `HashSet` to track seen elements.
*   **Time Complexity:** O(n).
*   **Space Complexity:** O(n).

---

## 947. Debug memory leak.

**Answer:**
**Common Causes:**
1.  **Static Collections:** Adding objects to a `static List/Map` and never removing them.
2.  **Unclosed Resources:** Database connections, InputStreams not closed in `finally` or `try-with-resources`.
3.  **Listeners:** Registering listeners but never deregistering them.
    **Tool:** **VisualVM** or **Eclipse MAT** (Memory Analyzer Tool) to analyze Heap Dump.

---

## 948. Write SQL for complex join.

**Answer:**
Find users who have placed more than 5 orders.
```sql
SELECT u.name, COUNT(o.id) as order_count
FROM Users u
JOIN Orders o ON u.id = o.user_id
GROUP BY u.id, u.name
HAVING COUNT(o.id) > 5;
```

---

## 949. Optimize REST API latency.

**Answer:**
1.  **Caching:** Use Redis to cache expensive DB queries.
2.  **N+1 Problem:** Fix Hibernate fetching (Use `JOIN FETCH`).
3.  **Database Indexing:** Ensure queries hit indexes.
4.  **Asynchronous Processing:** Offload heavy tasks (e.g., sending emails) to a message queue (Kafka/RabbitMQ).
5.  **Payload Size:** Use GZIP compression, Pagination.

---

## 950. Improve DB performance issue.

**Answer:**
1.  **Analyze Query Plan:** Use `EXPLAIN ANALYZE` to find full table scans.
2.  **Indexing:** Add indexes on columns used in `WHERE`, `JOIN`, and `ORDER BY`.
3.  **Connection Pooling:** Use HikariCP to reuse connections.
4.  **Partitioning:** Split large tables into smaller chunks (e.g., by date).
5.  **Read Replicas:** Direct read traffic to replicas, writes to primary.

---

## 951. Handle high traffic scenario.

**Answer:**
**Strategy:**
1.  **Scale Out:** Add more instances (Horizontal Scaling) behind a Load Balancer.
2.  **Caching:** Cache static assets (CDN) and hot data (Redis) to offload DB.
3.  **Asynchronous:** Move non-critical tasks to queues (Kafka).
4.  **Rate Limiting:** Protect services from being overwhelmed (429 Too Many Requests).
5.  **Degradation:** Turn off non-essential features to save resources.

---

## 952. Debug production crash.

**Answer:**
**Steps:**
1.  **Check Logs:** Look for Exceptions/Errors in ELK/Splunk.
2.  **Metrics:** Check CPU/Memory/Disk spikes in Grafana/Prometheus.
3.  **Recent Changes:** Did a deployment or config change happen recently?
4.  **Reproduce:** Try to reproduce in Staging.
5.  **Fix/Rollback:** If crucial, rollback immediately. If fixable, push hotfix.

---

## 953. Design scalable chat system.

**Answer:**
**Key Components:**
*   **Protocol:** WebSocket for real-time bi-directional communication.
*   **Storage:** HBase/Cassandra for storing billions of messages (Write-heavy).
*   **Pub/Sub:** Redis Pub/Sub or Kafka to route messages between users connected to different servers.
*   **Presence:** Redis to track user online/offline status.

---

## 954. Write efficient pagination query.

**Answer:**
**Avoid Offset Pagination** (`LIMIT 10 OFFSET 100000`) as it scans prior rows.
**Use Keyset/Cursor Pagination:**
```sql
SELECT * FROM Messages
WHERE id < last_seen_id
ORDER BY id DESC
LIMIT 10;
```
*   **Pros:** O(1) time complexity with index.

---

## 955. Implement consistent hashing.

**Answer:**
Used in distributed caching/databases to minimize data movement when nodes are added/removed.
**Concept:** Map both Nodes and Keys to a circle (0-360 degrees). Key is stored in the first Node found clockwise.
**Virtual Nodes:** Add multiple points per physical node to ensure even distribution.

---

## 956. Build caching mechanism.

**Answer:**
**Cache-Aside Pattern:**
```java
public Data getData(String key) {
    Data data = cache.get(key);
    if (data == null) {
        data = db.get(key);
        if (data != null) {
            cache.put(key, data);
        }
    }
    return data;
}
```

---

## 957. Implement distributed lock.

**Answer:**
Using **Redis (Redlock Algorithm)** or **ZooKeeper**.
**Redis Example (Simple):**
```java
// Set key only if not exists, with expiry (TTL) to prevent deadlock if app crashes
boolean locked = redis.set(lockKey, uniqueId, "NX", "EX", 10);
if (locked) {
    try { /* critical section */ }
    finally {
        // Lua script to ensure we only delete our own lock
        if (redis.get(lockKey).equals(uniqueId)) redis.del(lockKey);
    }
}
```

---

## 958. Handle race condition.

**Answer:**
Occurs when order of execution affects the result.
**Fixes:**
1.  **Atomic Operations:** Database Row Locking (`SELECT ... FOR UPDATE`).
2.  **Synchronized:** Java `synchronized` keyword.
3.  **Optimistic Locking:** Use a `version` column in DB. Update fails if version changed.

---

## 959. Optimize CPU-bound application.

**Answer:**
1.  **Parallelism:** Use `ForkJoinPool` or `Parallel Streams` to utilize all Cores.
2.  **Algorithm efficiently:** Reduce complexity (e.g., O(n) instead of O(n²)).
3.  **Avoid Blocking:** Don't do I/O in CPU-intensive threads.
4.  **Profiling:** Use `AsyncProfiler` to find hot methods.

---

## 960. Refactor legacy code.

**Answer:**
**Strangler Fig Pattern:**
1.  Identify a specific functionality to modernize.
2.  Build new microservice/module for it.
3.  Route calls to the new service.
4.  Remove old code.
    **Code Level:** Extract Method, Rename Variables, Introduce Design Patterns, Add Unit Tests **before** changing logic.

---
