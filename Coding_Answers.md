# Coding Interview Questions & Solutions (Stream vs Iterative)

## 1. Find the first non-repeated character in a string.
**Detailed Explanation**: Count frequency of each char. Return the first one with count 1.

**Approach 1: Java 8 Streams**
```java
String input = "swiss";

Character result = input.chars()           
    .mapToObj(c -> (char) c)               
    .collect(Collectors.groupingBy(Function.identity(), LinkedHashMap::new, Collectors.counting()))
    .entrySet().stream()
    .filter(entry -> entry.getValue() == 1L)
    .map(Map.Entry::getKey)
    .findFirst().orElse(null);

System.out.println(result); // w
```

**Approach 2: Iterative (For Loop)**
```java
String input = "swiss";
Map<Character, Integer> map = new LinkedHashMap<>(); // Maintains order

// Count Frequencies
for (char c : input.toCharArray()) {
    map.put(c, map.getOrDefault(c, 0) + 1);
}

// Find First
for (Map.Entry<Character, Integer> entry : map.entrySet()) {
    if (entry.getValue() == 1) {
        System.out.println(entry.getKey());
        break;
    }
}
```

---

## 2. Check if two strings are anagrams.
**Detailed Explanation**: "listen" and "silent" are anagrams.

**Approach 1: Java 8 Streams (Sorting)**
```java
String s1 = "listen", s2 = "silent";

boolean isAnagram = Stream.of(s1.split("")).sorted().collect(Collectors.joining())
    .equals(Stream.of(s2.split("")).sorted().collect(Collectors.joining()));
```

**Approach 2: Iterative (Frequency Array)**
```java
if (s1.length() != s2.length()) return false;
int[] count = new int[256]; // Assuming ASCII

for (int i = 0; i < s1.length(); i++) {
    count[s1.charAt(i)]++;
    count[s2.charAt(i)]--;
}

boolean isAnagram = true;
for (int c : count) {
    if (c != 0) { isAnagram = false; break; }
}
```

---

## 3. Find the second largest number in an array/list.
**Detailed Explanation**: Skip the largest, take the next.

**Approach 1: Java 8 Streams**
```java
List<Integer> list = Arrays.asList(10, 20, 35, 20, 35, 5);
Integer second = list.stream().distinct()
    .sorted(Comparator.reverseOrder()).skip(1).findFirst().orElse(null);
```

**Approach 2: Iterative (One Pass)**
```java
int largest = Integer.MIN_VALUE;
int secondLargest = Integer.MIN_VALUE;

for (int num : list) {
    if (num > largest) {
        secondLargest = largest;
        largest = num;
    } else if (num > secondLargest && num != largest) {
        secondLargest = num;
    }
}
System.out.println(secondLargest);
```

---

## 4. Count occurrence of each character in a string.

**Approach 1: Java 8 Streams**
```java
String input = "banana";
Map<String, Long> counts = Arrays.stream(input.split(""))
    .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()));
```

**Approach 2: Iterative**
```java
String input = "banana";
Map<Character, Integer> map = new HashMap<>();

for (char c : input.toCharArray()) {
    if (map.containsKey(c)) {
        map.put(c, map.get(c) + 1);
    } else {
        map.put(c, 1);
    }
}
System.out.println(map);
```

---

## 5. Reverse a string/sentence.

**Approach 1: Java 8 Streams (Sentence)**
```java
String str = "Hello World";
String reversed = Arrays.stream(str.split(" "))
    .reduce((first, second) -> second + " " + first).orElse("");
```

**Approach 2: Iterative (String)**
```java
String str = "Hello";
String params = "";
for (int i = str.length() - 1; i >= 0; i--) {
    params += str.charAt(i); // Not recommended for large strings (Use StringBuilder)
}
```

---

## 6. Fibonacci Series.
**Detailed Explanation**: 0, 1, 1, 2, 3, 5...

**Approach 1: Java 8 Streams**
```java
Stream.iterate(new int[]{0, 1}, t -> new int[]{t[1], t[0] + t[1]})
    .limit(10)
    .map(t -> t[0])
    .forEach(System.out::println);
```

**Approach 2: Iterative**
```java
int n = 10, first = 0, second = 1;
for (int i = 0; i < n; i++) {
    System.out.print(first + " ");
    int next = first + second;
    first = second;
    second = next;
}
```

---

## 7. Check if a string is a Palindrome.

**Approach 1: Java 8 Streams**
```java
String s = "madam";
boolean isPal = IntStream.range(0, s.length() / 2)
    .noneMatch(i -> s.charAt(i) != s.charAt(s.length() - i - 1));
```

**Approach 2: Iterative (Two Pointers)**
```java
String s = "madam";
boolean isPal = true;
int i = 0, j = s.length() - 1;
while (i < j) {
    if (s.charAt(i) != s.charAt(j)) {
        isPal = false;
        break;
    }
    i++; j--;
}
```

---

## 8. Sort a list of objects based on a field.

**Approach 1: Java 8 Streams**
```java
List<Emp> sorted = list.stream()
    .sorted(Comparator.comparing(Emp::getSalary))
    .collect(Collectors.toList());
```

**Approach 2: Collections.sort (Pre-Java 8 style)**
```java
Collections.sort(list, new Comparator<Emp>() {
    @Override
    public int compare(Emp e1, Emp e2) {
        return Double.compare(e1.getSalary(), e2.getSalary());
    }
});
```

---

## 9. Merge two lists.

**Approach 1: Java 8 Streams**
```java
List<Integer> merged = Stream.concat(l1.stream(), l2.stream())
    .collect(Collectors.toList());
```

**Approach 2: Iterative**
```java
List<Integer> merged = new ArrayList<>(l1);
merged.addAll(l2); // Internally iterates
```

---

## 10. Find common elements between two arrays.

**Approach 1: Java 8 Streams**
```java
List<Integer> common = list1.stream()
    .filter(list2::contains).collect(Collectors.toList());
```

**Approach 2: Iterative**
```java
List<Integer> common = new ArrayList<>();
for (Integer num : list1) {
    if (list2.contains(num)) {
        common.add(num);
    }
}
```

---

## 11. Pattern printing (Star pattern).
**Detailed Explanation**: Prints a triangle. Best done iteratively.

**Approach 1: Iterative**
```java
for(int i=1; i<=5; i++) {
    for(int j=1; j<=i; j++) {
        System.out.print("*");
    }
    System.out.println();
}
```
*(Stream approach is overly complex for nested loops printing, not recommended).*

---

## 12. Remove duplicates from a list.

**Approach 1: Java 8 Streams**
```java
List<Integer> unique = list.stream().distinct().collect(Collectors.toList());
```

**Approach 2: Iterative (Set)**
```java
Set<Integer> set = new HashSet<>();
List<Integer> unique = new ArrayList<>();
for (Integer num : list) {
    if (set.add(num)) {
        unique.add(num);
    }
}
```

---

## 13. Find the longest string in a list.

**Approach 1: Java 8 Streams**
```java
String longest = list.stream()
    .max(Comparator.comparingInt(String::length)).orElse("");
```

**Approach 2: Iterative**
```java
String longest = "";
for (String str : list) {
    if (str.length() > longest.length()) {
        longest = str;
    }
}
```

---

## 14. Prime numbers between 1 to 100.

**Approach 1: Java 8 Streams**
```java
List<Integer> primes = IntStream.rangeClosed(2, 100)
    .filter(n -> IntStream.range(2, (int)Math.sqrt(n) + 1).noneMatch(i -> n % i == 0))
    .boxed().collect(Collectors.toList());
```

**Approach 2: Iterative**
```java
for (int n = 2; n <= 100; n++) {
    boolean isPrime = true;
    for (int i = 2; i <= Math.sqrt(n); i++) {
        if (n % i == 0) { isPrime = false; break; }
    }
    if (isPrime) System.out.println(n);
}
```

---

## 15. Move all zeros to the end of the array.

**Approach 1: Iterative (Best)**
```java
int[] arr = {0, 1, 0, 3, 12};
int index = 0;
for (int num : arr) {
    if (num != 0) arr[index++] = num;
}
while (index < arr.length) arr[index++] = 0;
```
*(Stream not suitable for in-place array modification).*

---

## 16. Valid Parentheses problem.

**Approach 1: Iterative (Stack)**
```java
Stack<Character> stack = new Stack<>();
for (char c : s.toCharArray()) {
    if (c == '(') stack.push(')');
    // ... checks ...
}
return stack.isEmpty();
```

---

## 17. Find missing number in an array.

**Approach 1: Arithmetic (Best)**
```java
int total = n * (n + 1) / 2;
int sum = 0;
for (int num : arr) sum += num;
return total - sum;
```

---

## 18. Singleton Class
*(Design Pattern - Code provided in Design Patterns file)*.

---

## 19. Find maximum number of occurrences of a substring.
**Approach 1: String Split**
```java
int count = str.split(sub, -1).length - 1;
```
**Approach 2: Iterative**
```java
int count = 0, idx = 0;
while ((idx = str.indexOf(sub, idx)) != -1) {
    count++;
    idx += sub.length();
}
```
