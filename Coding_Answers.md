# Coding Interview Questions & Answers (Loop vs Stream)

## 1. Find the first non-repeated character in a string

**Approach 1: Traditional (HashMap + Loop)**
```java
public char firstUniqCharLoop(String s) {
    Map<Character, Integer> counts = new LinkedHashMap<>(); // Preserves insertion order
    for (char c : s.toCharArray()) {
        counts.put(c, counts.getOrDefault(c, 0) + 1);
    }
    for (Map.Entry<Character, Integer> entry : counts.entrySet()) {
        if (entry.getValue() == 1) return entry.getKey();
    }
    throw new RuntimeException("No unique char");
}
```

**Approach 2: Java 8 Stream API**
```java
public char firstUniqCharStream(String s) {
    return s.chars()      // IntStream
        .mapToObj(c -> (char)c)
        .collect(Collectors.groupingBy(Function.identity(), LinkedHashMap::new, Collectors.counting()))
        .entrySet().stream()
        .filter(entry -> entry.getValue() == 1)
        .map(Map.Entry::getKey)
        .findFirst()
        .orElseThrow(() -> new RuntimeException("No unique char"));
}
```

## 2. Check if two strings are anagrams

**Approach 1: Traditional (Sorting)**
```java
public boolean isAnagramTraditional(String s1, String s2) {
    if (s1.length() != s2.length()) return false;
    char[] c1 = s1.toCharArray();
    char[] c2 = s2.toCharArray();
    Arrays.sort(c1);
    Arrays.sort(c2);
    return Arrays.equals(c1, c2);
}
```

**Approach 2: Java 8 Stream API (Grouping & Counting)**
```java
public boolean isAnagramStream(String s1, String s2) {
    if (s1.length() != s2.length()) return false;
    
    Map<Character, Long> map1 = s1.chars().mapToObj(c -> (char)c)
        .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()));
        
    Map<Character, Long> map2 = s2.chars().mapToObj(c -> (char)c)
        .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()));
        
    return map1.equals(map2);
}
```

## 3. Find the second largest number in an array

**Approach 1: Traditional (Loop)**
```java
public int findSecondLargestLoop(int[] arr) {
    int max = Integer.MIN_VALUE, secondMax = Integer.MIN_VALUE;
    for (int num : arr) {
        if (num > max) {
            secondMax = max;
            max = num;
        } else if (num > secondMax && num != max) {
            secondMax = num;
        }
    }
    return secondMax;
}
```

**Approach 2: Java 8 Stream API**
```java
public int findSecondLargestStream(int[] arr) {
    return Arrays.stream(arr)
        .distinct()
        .boxed()
        .sorted(Comparator.reverseOrder())
        .skip(1)
        .findFirst()
        .orElseThrow(() -> new RuntimeException("Array too small"));
}
```

## 4. Count occurrence of each character

**Approach 1: Traditional (HashMap)**
```java
public Map<Character, Integer> countCharsLoop(String str) {
    Map<Character, Integer> map = new HashMap<>();
    for (char c : str.toCharArray()) {
        map.put(c, map.getOrDefault(c, 0) + 1);
    }
    return map;
}
```

**Approach 2: Java 8 Stream API**
```java
public Map<Character, Long> countCharsStream(String str) {
    return str.chars()
        .mapToObj(c -> (char)c)
        .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()));
}
```

## 5. Reverse a string

**Approach 1: Traditional (StringBuilder / Two Pointers)**
```java
public String reverseLoop(String str) {
    char[] chars = str.toCharArray();
    int left = 0, right = chars.length - 1;
    while (left < right) {
        char temp = chars[left];
        chars[left++] = chars[right];
        chars[right--] = temp;
    }
    return new String(chars);
}
```

**Approach 2: Java 8 Stream API**
```java
public String reverseStream(String str) {
    return Stream.of(str.split(""))
        .reduce((a, b) -> b + a)
        .orElse("");
}
```

## 6. Sort a List of Employees by Salary

**Approach 1: Traditional (Collections.sort)**
```java
public void sortEmployeesLoop(List<Employee> employees) {
    Collections.sort(employees, new Comparator<Employee>() {
        @Override
        public int compare(Employee e1, Employee e2) {
            return Double.compare(e2.getSalary(), e1.getSalary()); // Descending
        }
    });
}
```

**Approach 2: Java 8 Stream API**
```java
public List<Employee> sortEmployeesStream(List<Employee> employees) {
    return employees.stream()
        .sorted(Comparator.comparingDouble(Employee::getSalary).reversed())
        .collect(Collectors.toList());
}
```

## 7. Find Common Elements in Two Arrays

**Approach 1: Traditional (HashSet)**
```java
public void findCommonLoop(int[] arr1, int[] arr2) {
    Set<Integer> set = new HashSet<>();
    for (int i : arr1) set.add(i);
    for (int i : arr2) {
        if (set.contains(i)) {
            System.out.println(i);
        }
    }
}
```

**Approach 2: Java 8 Stream API**
```java
public void findCommonStream(int[] arr1, int[] arr2) {
    List<Integer> list1 = Arrays.stream(arr1).boxed().collect(Collectors.toList());
    Arrays.stream(arr2)
        .filter(list1::contains)
        .distinct()
        .forEach(System.out::println);
}
```

## 8. Remove Duplicates from List

**Approach 1: Traditional (Set)**
```java
public List<Integer> removeDuplicatesLoop(List<Integer> list) {
    return new ArrayList<>(new HashSet<>(list)); // Note: Loss of order unless LinkedHashSet used
}
```

**Approach 2: Java 8 Stream API**
```java
public List<Integer> removeDuplicatesStream(List<Integer> list) {
    return list.stream().distinct().collect(Collectors.toList());
}
```

## 9. Find Longest String in List

**Approach 1: Traditional (Loop)**
```java
public String longestStringLoop(List<String> list) {
    String longest = "";
    for (String s : list) {
        if (s.length() > longest.length()) {
            longest = s;
        }
    }
    return longest;
}
```

**Approach 2: Java 8 Stream API**
```java
public String longestStringStream(List<String> list) {
    return list.stream()
        .max(Comparator.comparingInt(String::length))
        .orElse("");
}
```

## 10. Check if number is Prime

**Approach 1: Traditional (Loop)**
```java
public boolean isPrimeLoop(int n) {
    if (n <= 1) return false;
    for (int i = 2; i <= Math.sqrt(n); i++) {
        if (n % i == 0) return false;
    }
    return true;
}
```

**Approach 2: Java 8 Stream API**
```java
public boolean isPrimeStream(int n) {
    return n > 1 && IntStream.rangeClosed(2, (int) Math.sqrt(n))
        .noneMatch(i -> n % i == 0);
}
```

## 11. Sum of numbers in List

**Approach 1: Traditional**
```java
int sum = 0;
for(int i : list) sum += i;
```

**Approach 2: Stream API**
```java
int sum = list.stream().mapToInt(Integer::intValue).sum();
// OR
int sum = list.stream().reduce(0, Integer::sum);
```
