## ✅ Top 100 DSA Interview Questions

---

### 🔹 **1–15: Arrays & Matrix**

## 1. Find the missing number in an array of 1 to N.

This is a classic interview question: **Find the missing number in an array containing numbers from 1 to N with one number missing.**

---

### Problem Statement:

You have an array of size **N-1** containing distinct integers from **1 to N** but one number is missing. You need to find the missing number.

---

### Example:

```java
Input: arr = [1, 2, 4, 5, 6], N = 6
Output: 3
Explanation: Number 3 is missing in the array.
```

---

### Approach 1: Using Sum Formula

The sum of the first N natural numbers is:

$$
S = \frac{N \times (N + 1)}{2}
$$

If you sum all elements of the array and subtract from S, you get the missing number.

---

### Step-by-step:

1. Calculate sum of numbers from 1 to N using the formula.
2. Calculate sum of elements in the array.
3. Missing number = (Sum from 1 to N) - (Sum of array elements)

---

### Java Code:

```java
public class MissingNumber {
    public static int findMissingNumber(int[] arr, int N) {
        // Step 1: Calculate total sum of numbers from 1 to N
        int totalSum = N * (N + 1) / 2;

        // Step 2: Calculate sum of elements in the array
        int arrSum = 0;
        for (int num : arr) {
            arrSum += num;
        }

        // Step 3: The difference is the missing number
        return totalSum - arrSum;
    }

    public static void main(String[] args) {
        int[] arr = {1, 2, 4, 5, 6};
        int N = 6;
        System.out.println("Missing number is: " + findMissingNumber(arr, N));
    }
}
```

**Output:**

```
Missing number is: 3
```

---

### Time and Space Complexity:

* **Time Complexity:** O(N) — We traverse the array once to calculate sum.
* **Space Complexity:** O(1) — We use constant extra space.

---

### Alternative Approach 2: Using XOR

Another neat approach uses XOR operation.

**Property:**
`a ^ a = 0` and `a ^ 0 = a`

1. XOR all numbers from 1 to N.
2. XOR all elements in the array.
3. XOR of above two results gives the missing number.

---

### Code for XOR approach:

```java
public static int findMissingNumberXOR(int[] arr, int N) {
    int xorAll = 0;
    int xorArr = 0;

    // XOR all numbers from 1 to N
    for (int i = 1; i <= N; i++) {
        xorAll ^= i;
    }

    // XOR all elements in the array
    for (int num : arr) {
        xorArr ^= num;
    }

    // XOR of both gives missing number
    return xorAll ^ xorArr;
}
```

---

### Why XOR works?

* XOR of all numbers 1 to N cancels out all numbers present in the array.
* The remaining value after XOR operations is the missing number.

---

## 2. Find the duplicate number in an array.

Finding a duplicate number in an array is a common and important DSA problem asked in Java interviews.

---

### Problem Statement:

Given an array of **N+1** integers where each integer is between **1 and N** (inclusive), **at least one number is duplicated**. Find the duplicate number.

---

### Example:

```java
Input: arr = [1, 3, 4, 2, 2]
Output: 2
Explanation: 2 is the duplicate number.
```

---

## Multiple Approaches to Solve This Problem

---

### Approach 1: Using HashSet (Simple & Intuitive)

* Use a HashSet to track visited numbers.
* Iterate over the array.
* If the number is already in the set, that’s the duplicate.
* Else, add the number to the set.

---

### Java Code:

```java
import java.util.HashSet;

public class FindDuplicate {
    public static int findDuplicate(int[] arr) {
        HashSet<Integer> seen = new HashSet<>();
        for (int num : arr) {
            if (seen.contains(num)) {
                return num; // duplicate found
            }
            seen.add(num);
        }
        return -1; // no duplicate found (though problem guarantees one)
    }

    public static void main(String[] args) {
        int[] arr = {1, 3, 4, 2, 2};
        System.out.println("Duplicate number is: " + findDuplicate(arr));
    }
}
```

**Output:**

```
Duplicate number is: 2
```

---

### Time and Space Complexity:

* Time: **O(N)**
* Space: **O(N)** due to extra HashSet

---

### Approach 2: Sorting the Array (Modify the Array)

* Sort the array.
* Then check consecutive elements for duplicates.

---

### Code:

```java
import java.util.Arrays;

public class FindDuplicateSorting {
    public static int findDuplicate(int[] arr) {
        Arrays.sort(arr);
        for (int i = 1; i < arr.length; i++) {
            if (arr[i] == arr[i - 1]) {
                return arr[i];
            }
        }
        return -1;
    }
}
```

**Time Complexity:** O(N log N) due to sorting.
**Space Complexity:** O(1) if sorting in-place.

---

### Approach 3: Floyd’s Tortoise and Hare (Cycle Detection) — Optimal

This is the most optimal approach with:

* **Time Complexity:** O(N)
* **Space Complexity:** O(1)

---

#### Why cycle detection?

* The array elements point to indices.
* Duplicate numbers create a cycle like in linked lists.
* Floyd’s algorithm detects the cycle and finds the duplicate.

---

### Step-by-step:

1. Use two pointers `slow` and `fast`.
2. Move `slow` by one step and `fast` by two steps until they meet.
3. Reset `slow` to start and move both by one step.
4. The point where they meet again is the duplicate.

---

### Java Code:

```java
public class FindDuplicateFloyd {
    public static int findDuplicate(int[] nums) {
        int slow = nums[0];
        int fast = nums[0];
        
        // Phase 1: Find the intersection point of the two runners.
        do {
            slow = nums[slow];
            fast = nums[nums[fast]];
        } while (slow != fast);
        
        // Phase 2: Find the entrance to the cycle.
        slow = nums[0];
        while (slow != fast) {
            slow = nums[slow];
            fast = nums[fast];
        }
        
        return slow; // or fast, both are at duplicate number
    }
    
    public static void main(String[] args) {
        int[] arr = {1, 3, 4, 2, 2};
        System.out.println("Duplicate number is: " + findDuplicate(arr));
    }
}
```

---

### How does this work?

* Think of array values as pointers to indices.
* Duplicate number causes a cycle.
* Floyd’s algorithm finds the start of that cycle.

---

## 3. Kadane's Algorithm (Maximum Subarray Sum).

**Kadane’s Algorithm** is a classic for finding the **maximum sum of a contiguous subarray** within a one-dimensional array. It’s a very popular and efficient algorithm often asked in Java interviews for DSA.

---

### Problem Statement:

Given an integer array, find the contiguous subarray (containing at least one number) which has the **largest sum** and return its sum.

---

### Example:

```java
Input: arr = [-2, 1, -3, 4, -1, 2, 1, -5, 4]
Output: 6
Explanation: The subarray [4, -1, 2, 1] has the largest sum = 6.
```

---

## Intuition Behind Kadane's Algorithm:

* Traverse the array while keeping track of:

    * `currentSum`: Maximum sum of subarray ending at current position.
    * `maxSum`: Maximum sum encountered so far.
* At each step, decide whether to:

    * Add current element to `currentSum` or
    * Start a new subarray from current element (if current element is greater than `currentSum + current element`).

---

## Step-by-step Example:

Given: `[-2, 1, -3, 4, -1, 2, 1, -5, 4]`

| Index | Element | currentSum (max subarray ending here) | maxSum (max so far) |
| ----- | ------- | ------------------------------------- | ------------------- |
| 0     | -2      | max(-2, 0 + -2) = -2                  | -2                  |
| 1     | 1       | max(1, -2 + 1) = 1                    | max(-2,1) = 1       |
| 2     | -3      | max(-3, 1 + -3) = -2                  | max(1,-2) = 1       |
| 3     | 4       | max(4, -2 + 4) = 4                    | max(1,4) = 4        |
| 4     | -1      | max(-1, 4 + -1) = 3                   | max(4,3) = 4        |
| 5     | 2       | max(2, 3 + 2) = 5                     | max(4,5) = 5        |
| 6     | 1       | max(1, 5 + 1) = 6                     | max(5,6) = 6        |
| 7     | -5      | max(-5, 6 + -5) = 1                   | max(6,1) = 6        |
| 8     | 4       | max(4, 1 + 4) = 5                     | max(6,5) = 6        |

---

### Java Code for Kadane’s Algorithm:

```java
public class KadaneAlgorithm {
    public static int maxSubArraySum(int[] arr) {
        int maxSum = arr[0];      // Initialize maxSum to first element
        int currentSum = arr[0];  // currentSum also starts with first element

        for (int i = 1; i < arr.length; i++) {
            // Decide whether to start new subarray at current element or extend existing
            currentSum = Math.max(arr[i], currentSum + arr[i]);
            // Update maxSum if currentSum is larger
            maxSum = Math.max(maxSum, currentSum);
        }
        return maxSum;
    }

    public static void main(String[] args) {
        int[] arr = {-2, 1, -3, 4, -1, 2, 1, -5, 4};
        System.out.println("Maximum subarray sum is: " + maxSubArraySum(arr));
    }
}
```

---

### Output:

```
Maximum subarray sum is: 6
```

---

### Time and Space Complexity:

* **Time Complexity:** O(N) — One pass through the array.
* **Space Complexity:** O(1) — Only a few variables used.

---

### Why Kadane’s Algorithm is Important:

* It efficiently finds max sum subarray in linear time.
* Helps you understand dynamic programming basics.
* It’s a great example of optimal substructure and greedy choice.

---

## 4. Merge two sorted arrays.

Merging two sorted arrays is a fundamental problem in data structures and algorithms, often used as a building block in merge sort and other algorithms.

---

### Problem Statement:

Given two **sorted** arrays, merge them into a single sorted array.

---

### Example:

```java
Input: arr1 = [1, 3, 5], arr2 = [2, 4, 6]
Output: [1, 2, 3, 4, 5, 6]
```

---

## Approach:

We can use two pointers to traverse both arrays simultaneously and pick the smaller element at each step.

---

### Step-by-step:

* Initialize two pointers, `i` for `arr1` and `j` for `arr2`, both starting at 0.
* Compare elements at `arr1[i]` and `arr2[j]`.
* Append the smaller element to the result array and move the corresponding pointer forward.
* When one array is exhausted, append the remaining elements of the other array.

---

### Java Code:

```java
import java.util.Arrays;

public class MergeSortedArrays {
    public static int[] merge(int[] arr1, int[] arr2) {
        int n1 = arr1.length, n2 = arr2.length;
        int[] merged = new int[n1 + n2];

        int i = 0, j = 0, k = 0;

        // Traverse both arrays and merge
        while (i < n1 && j < n2) {
            if (arr1[i] <= arr2[j]) {
                merged[k++] = arr1[i++];
            } else {
                merged[k++] = arr2[j++];
            }
        }

        // Append remaining elements of arr1, if any
        while (i < n1) {
            merged[k++] = arr1[i++];
        }

        // Append remaining elements of arr2, if any
        while (j < n2) {
            merged[k++] = arr2[j++];
        }

        return merged;
    }

    public static void main(String[] args) {
        int[] arr1 = {1, 3, 5};
        int[] arr2 = {2, 4, 6};

        int[] mergedArray = merge(arr1, arr2);

        System.out.println("Merged array: " + Arrays.toString(mergedArray));
    }
}
```

---

### Output:

```
Merged array: [1, 2, 3, 4, 5, 6]
```

---

### Time and Space Complexity:

* **Time Complexity:** O(n1 + n2), where n1 and n2 are sizes of the input arrays.
* **Space Complexity:** O(n1 + n2) for the merged output array.

---

## 5. Rotate array by K positions.

Rotating an array by **K** positions is another common problem in interviews.

---

### Problem Statement:

Given an array, rotate it to the right by **K** steps, where **K** is non-negative.

---

### Example:

```java
Input: arr = [1, 2, 3, 4, 5, 6, 7], K = 3
Output: [5, 6, 7, 1, 2, 3, 4]

Explanation:  
Rotate the array to the right by 3 steps.
```

---

## Approach 1: Using Extra Array (Simple but uses extra space)

* Create a new array of the same size.
* For each element at index `i` in the original array, place it at `(i + K) % N` in the new array.
* Copy the new array back to the original array.

---

### Java Code:

```java
import java.util.Arrays;

public class RotateArray {
    public static void rotate(int[] arr, int k) {
        int n = arr.length;
        k = k % n; // Handle k greater than n
        int[] rotated = new int[n];

        for (int i = 0; i < n; i++) {
            rotated[(i + k) % n] = arr[i];
        }

        // Copy back to original array
        for (int i = 0; i < n; i++) {
            arr[i] = rotated[i];
        }
    }

    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4, 5, 6, 7};
        int k = 3;
        rotate(arr, k);
        System.out.println("Rotated array: " + Arrays.toString(arr));
    }
}
```

---

### Output:

```
Rotated array: [5, 6, 7, 1, 2, 3, 4]
```

---

## Approach 2: In-Place Rotation Using Reversal (Optimal)

* **Step 1:** Reverse the whole array.
* **Step 2:** Reverse the first K elements.
* **Step 3:** Reverse the remaining N-K elements.

---

### Why it works?

Reversing the whole array puts the last K elements in front but reversed. Reversing them again restores their order, same for the rest.

---

### Java Code:

```java
import java.util.Arrays;

public class RotateArrayInPlace {
    public static void rotate(int[] arr, int k) {
        int n = arr.length;
        k = k % n;

        // Step 1: Reverse whole array
        reverse(arr, 0, n - 1);

        // Step 2: Reverse first k elements
        reverse(arr, 0, k - 1);

        // Step 3: Reverse remaining elements
        reverse(arr, k, n - 1);
    }

    private static void reverse(int[] arr, int start, int end) {
        while (start < end) {
            int temp = arr[start];
            arr[start] = arr[end];
            arr[end] = temp;
            start++;
            end--;
        }
    }

    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4, 5, 6, 7};
        int k = 3;
        rotate(arr, k);
        System.out.println("Rotated array: " + Arrays.toString(arr));
    }
}
```

---

### Output:

```
Rotated array: [5, 6, 7, 1, 2, 3, 4]
```

---

### Time and Space Complexity:

* **Time Complexity:** O(N) — Three reversals each take O(N) but overall linear.
* **Space Complexity:** O(1) — In-place rotation with constant extra space.

---

## 6. Find all pairs with a given sum.

Finding all pairs in an array that sum up to a given target is a classic problem and very common in Java DSA interviews.

---

### Problem Statement:

Given an integer array and a target sum, find **all pairs** of elements whose sum equals the target.

---

### Example:

```java
Input: arr = [2, 4, 3, 5, 7, 8, 9], target = 7
Output: (2, 5), (4, 3)
Explanation: Pairs whose sum is 7 are (2,5) and (4,3).
```

---

## Approach 1: Using HashMap / HashSet (Efficient)

* Use a HashSet to track numbers we’ve seen.
* For each number, check if `target - number` is already in the set.
* If yes, print the pair.
* Else, add the number to the set.

---

### Java Code:

```java
import java.util.HashSet;

public class PairsWithSum {
    public static void findPairs(int[] arr, int target) {
        HashSet<Integer> seen = new HashSet<>();
        HashSet<String> printed = new HashSet<>();  // To avoid duplicate pairs

        for (int num : arr) {
            int complement = target - num;
            if (seen.contains(complement)) {
                // Sort pair to avoid duplicates like (3,4) and (4,3)
                int low = Math.min(num, complement);
                int high = Math.max(num, complement);
                String pair = low + "," + high;

                if (!printed.contains(pair)) {
                    System.out.println("(" + low + ", " + high + ")");
                    printed.add(pair);
                }
            }
            seen.add(num);
        }
    }

    public static void main(String[] args) {
        int[] arr = {2, 4, 3, 5, 7, 8, 9};
        int target = 7;
        findPairs(arr, target);
    }
}
```

---

### Output:

```
(2, 5)
(3, 4)
```

---

### Time and Space Complexity:

* **Time Complexity:** O(N), one pass through the array.
* **Space Complexity:** O(N), for the HashSet.

---

## Approach 2: Sorting + Two Pointers

* Sort the array.
* Use two pointers: one at start (`left`), one at end (`right`).
* Calculate sum of elements at pointers:

    * If sum == target, print pair, move both pointers.
    * If sum < target, move left pointer.
    * If sum > target, move right pointer.
* Stop when left >= right.

---

### Java Code:

```java
import java.util.Arrays;

public class PairsWithSumTwoPointers {
    public static void findPairs(int[] arr, int target) {
        Arrays.sort(arr);

        int left = 0, right = arr.length - 1;

        while (left < right) {
            int sum = arr[left] + arr[right];

            if (sum == target) {
                System.out.println("(" + arr[left] + ", " + arr[right] + ")");
                left++;
                right--;
            } else if (sum < target) {
                left++;
            } else {
                right--;
            }
        }
    }

    public static void main(String[] args) {
        int[] arr = {2, 4, 3, 5, 7, 8, 9};
        int target = 7;
        findPairs(arr, target);
    }
}
```

---

### Time and Space Complexity:

* **Time Complexity:** O(N log N) due to sorting.
* **Space Complexity:** O(1) or O(N) depending on sorting method.

---

## 7. Two Sum problem.

The **Two Sum** problem is one of the most famous coding interview problems, often asked in Java DSA interviews. It's very similar to the pairs-with-sum problem, but usually you have to return the **indices** of the two numbers that add up to the target.

---

### Problem Statement:

Given an integer array `nums` and an integer `target`, return indices of the **two numbers** such that they add up to `target`.

You may assume that each input would have **exactly one solution**, and you may not use the same element twice.

---

### Example:

```java
Input: nums = [2, 7, 11, 15], target = 9
Output: [0, 1]

Explanation: nums[0] + nums[1] == 9
```

---

## Approach: Using HashMap for Efficient Lookup

* Use a HashMap to store number and its index.
* Traverse the array:

    * For each element `nums[i]`, check if `target - nums[i]` exists in the map.
    * If yes, return `[index of complement, i]`.
    * Otherwise, add `nums[i]` with index `i` to the map.

---

### Java Code:

```java
import java.util.HashMap;
import java.util.Arrays;

public class TwoSum {
    public static int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> map = new HashMap<>();

        for (int i = 0; i < nums.length; i++) {
            int complement = target - nums[i];

            if (map.containsKey(complement)) {
                return new int[] { map.get(complement), i };
            }

            map.put(nums[i], i);
        }

        // In case no solution found (problem guarantees one)
        return new int[] {-1, -1};
    }

    public static void main(String[] args) {
        int[] nums = {2, 7, 11, 15};
        int target = 9;

        int[] result = twoSum(nums, target);
        System.out.println("Indices of two numbers: " + Arrays.toString(result));
    }
}
```

---

### Output:

```
Indices of two numbers: [0, 1]
```

---

### Time and Space Complexity:

* **Time Complexity:** O(N) — One pass through the array.
* **Space Complexity:** O(N) — HashMap stores elements.

---

### Why this works:

* HashMap lookup is O(1), so you efficiently check for the complement.
* By storing indices, you can quickly return the answer.

---

## 8. Find the majority element (Boyer-Moore Voting).

The **Majority Element** problem is classic and Boyer-Moore Voting Algorithm is the most optimal way to solve it with **O(N)** time and **O(1)** space. It’s a great topic for Java DSA interviews.

---

### Problem Statement:

Given an array of size `n`, find the **majority element**. The majority element is the element that appears **more than n/2 times**.

You can assume the majority element always exists in the array.

---

### Example:

```java
Input: arr = [2, 2, 1, 1, 1, 2, 2]
Output: 2
Explanation: 2 appears 4 times which is more than n/2 = 3.5.
```

---

## Intuition Behind Boyer-Moore Voting Algorithm:

* The algorithm works by maintaining a **candidate** for majority and a **count**.
* Iterate over the array:

    * If count is 0, set the current element as the candidate.
    * If the current element is the candidate, increment count.
    * Otherwise, decrement count.
* The candidate at the end of the iteration is the majority element.

---

### Why does it work?

* The count increases for candidate occurrences and decreases for others.
* Majority element count will always be positive at the end because it appears more than half the time.

---

## Java Code:

```java
public class MajorityElement {
    public static int majorityElement(int[] nums) {
        int count = 0;
        Integer candidate = null;

        for (int num : nums) {
            if (count == 0) {
                candidate = num;
            }
            count += (num == candidate) ? 1 : -1;
        }

        return candidate;
    }

    public static void main(String[] args) {
        int[] arr = {2, 2, 1, 1, 1, 2, 2};
        System.out.println("Majority element is: " + majorityElement(arr));
    }
}
```

---

### Output:

```
Majority element is: 2
```

---

### Time and Space Complexity:

* **Time Complexity:** O(N), single pass through array.
* **Space Complexity:** O(1), constant extra space.

---

### Bonus:

If the majority element is **not guaranteed**, you can run a second pass to verify if the candidate actually appears more than n/2 times.

---

## 9. Rearrange array in alternating positive and negative numbers.

Rearranging an array to alternate positive and negative numbers is a classic array manipulation problem often asked in interviews.

---

### Problem Statement:

Given an array of positive and negative numbers, rearrange the array such that positive and negative numbers alternate. If there are extra positive or negative numbers, they appear at the end.

---

### Example:

```java
Input: arr = [2, 3, -4, -1, 6, -9]
Output: [2, -4, 3, -1, 6, -9]

Explanation: Positive and negative numbers alternate.
```

---

## Important Notes:

* The relative order of positive or negative numbers **does not need to be maintained** unless specified.
* If counts of positive and negative numbers are unequal, extra elements appear at the end.

---

## Approach 1: Using Extra Space (Simpler)

* Separate positive and negative numbers into two arrays.
* Alternate picking from these arrays to fill original array.

---

### Java Code:

```java
import java.util.ArrayList;
import java.util.List;

public class AlternatePosNeg {
    public static void rearrange(int[] arr) {
        List<Integer> positives = new ArrayList<>();
        List<Integer> negatives = new ArrayList<>();

        // Separate positive and negative
        for (int num : arr) {
            if (num >= 0) {
                positives.add(num);
            } else {
                negatives.add(num);
            }
        }

        int i = 0, p = 0, n = 0;

        // Alternate filling from positives and negatives
        while (p < positives.size() && n < negatives.size()) {
            arr[i++] = positives.get(p++);
            arr[i++] = negatives.get(n++);
        }

        // Append remaining positives
        while (p < positives.size()) {
            arr[i++] = positives.get(p++);
        }

        // Append remaining negatives
        while (n < negatives.size()) {
            arr[i++] = negatives.get(n++);
        }
    }

    public static void main(String[] args) {
        int[] arr = {2, 3, -4, -1, 6, -9};
        rearrange(arr);

        for (int num : arr) {
            System.out.print(num + " ");
        }
    }
}
```

---

### Output:

```
2 -4 3 -1 6 -9
```

---

## Approach 2: In-place Rearrangement (When order doesn't matter)

1. Partition array similar to quicksort: all negatives on one side, positives on the other.
2. Use two pointers: one at the start for positives, another after negatives for negatives.
3. Swap elements to alternate.

---

### Java Code:

```java
public class AlternatePosNegInPlace {
    public static void rearrange(int[] arr) {
        int n = arr.length;
        int i = 0, j = 1;

        while (i < n && j < n) {
            // Find misplaced positive at even index
            while (i < n && arr[i] >= 0) i += 2;

            // Find misplaced negative at odd index
            while (j < n && arr[j] < 0) j += 2;

            if (i < n && j < n) {
                int temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }
    }

    public static void main(String[] args) {
        int[] arr = {2, 3, -4, -1, 6, -9};
        rearrange(arr);

        for (int num : arr) {
            System.out.print(num + " ");
        }
    }
}
```

---

### Output:

```
2 -4 3 -1 6 -9
```

---

### Time and Space Complexity:

* Approach 1: O(N) time, O(N) extra space.
* Approach 2: O(N) time, O(1) space (in-place).

---

## 10. Sort 0s, 1s, and 2s (Dutch National Flag).

The **Dutch National Flag** problem is a classic algorithm problem, frequently asked in Java DSA interviews.

---

### Problem Statement:

Given an array containing only 0s, 1s, and 2s, sort the array **in-place** so that all 0s come first, followed by 1s, then 2s.

---

### Example:

```java
Input: arr = [2, 0, 2, 1, 1, 0]
Output: [0, 0, 1, 1, 2, 2]
```

---

## Intuition:

* The problem is about partitioning the array into three parts.
* Use **three pointers**:

    * `low`: boundary for 0s
    * `mid`: current element
    * `high`: boundary for 2s

---

## Algorithm (Dutch National Flag):

* Initialize:

    * `low = 0`, `mid = 0`, `high = arr.length - 1`
* Traverse while `mid <= high`:

    * If `arr[mid] == 0`, swap with `arr[low]`, increment `low` and `mid`.
    * If `arr[mid] == 1`, just increment `mid`.
    * If `arr[mid] == 2`, swap with `arr[high]`, decrement `high`.

---

### Java Code:

```java
import java.util.Arrays;

public class DutchNationalFlag {
    public static void sortColors(int[] arr) {
        int low = 0, mid = 0;
        int high = arr.length - 1;

        while (mid <= high) {
            switch (arr[mid]) {
                case 0:
                    swap(arr, low, mid);
                    low++;
                    mid++;
                    break;
                case 1:
                    mid++;
                    break;
                case 2:
                    swap(arr, mid, high);
                    high--;
                    break;
            }
        }
    }

    private static void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    public static void main(String[] args) {
        int[] arr = {2, 0, 2, 1, 1, 0};
        sortColors(arr);
        System.out.println(Arrays.toString(arr));
    }
}
```

---

### Output:

```
[0, 0, 1, 1, 2, 2]
```

---

### Time and Space Complexity:

* **Time Complexity:** O(N), single traversal.
* **Space Complexity:** O(1), in-place sorting.

---

This algorithm is optimal because it does **only one pass** and uses **constant extra space**.

---

## 11. Subarray with given sum (Sliding Window).

Finding a **subarray with a given sum** is a classic problem and using a **sliding window** technique is often the optimal approach — especially when the array contains **only non-negative numbers**.

---

## Problem Statement:

Given an array of **non-negative integers** and a target sum, find a continuous subarray that sums to the target. Return the start and end indices of the subarray or indicate if no such subarray exists.

---

### Example:

```java
Input: arr = [1, 2, 3, 7, 5], target = 12
Output: Subarray found from index 1 to 3 (2 + 3 + 7 = 12)
```

---

## Approach: Sliding Window

* Use two pointers: `start` and `end` to represent the window.
* Expand the `end` pointer to include elements and keep track of the window sum.
* If the sum exceeds the target, move `start` forward to reduce the sum.
* Continue until you find the sum or end of array is reached.

---

### Java Code:

```java
public class SubarrayWithGivenSum {
    public static void findSubarray(int[] arr, int target) {
        int start = 0, currentSum = 0;

        for (int end = 0; end < arr.length; end++) {
            currentSum += arr[end];

            // Shrink the window as long as currentSum > target
            while (currentSum > target && start <= end) {
                currentSum -= arr[start];
                start++;
            }

            if (currentSum == target) {
                System.out.println("Subarray found from index " + start + " to " + end);
                return;
            }
        }

        System.out.println("No subarray with given sum found.");
    }

    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 7, 5};
        int target = 12;
        findSubarray(arr, target);
    }
}
```

---

### Output:

```
Subarray found from index 1 to 3
```

---

## Important Notes:

* This works only if array has **non-negative** numbers because the window sum only increases when expanding and decreases when shrinking.
* If the array can have **negative numbers**, sliding window doesn’t always work. You may need a **HashMap** approach to solve it.

---

## HashMap approach for arrays with negative numbers:

* Maintain a prefix sum and store prefix sums in a HashMap.
* If `prefixSum - target` exists in map, subarray found.

---

## 12. Maximum product subarray.

The **Maximum Product Subarray** is a classic and slightly trickier problem compared to maximum sum subarray, because the product can flip signs due to negative numbers.

---

## Problem Statement:

Given an integer array, find the contiguous subarray within the array which has the **largest product**.

---

### Example:

```java
Input: arr = [2, 3, -2, 4]
Output: 6
Explanation: Subarray [2, 3] has the maximum product 6.
```

---

## Key Insight:

* Because multiplying by a negative number flips the sign, we need to keep track of:

    * The **maximum product** ending at the current position.
    * The **minimum product** ending at the current position (which could become maximum if multiplied by a negative).
* At each step, update max and min products accordingly.

---

## Algorithm:

1. Initialize:

    * `max_so_far = arr[0]`
    * `max_ending_here = arr[0]`
    * `min_ending_here = arr[0]`
2. Iterate over the array starting from index 1:

    * If current number is negative, swap max and min.
    * Update `max_ending_here` = max(current number, max\_ending\_here \* current number)
    * Update `min_ending_here` = min(current number, min\_ending\_here \* current number)
    * Update `max_so_far` = max(max\_so\_far, max\_ending\_here)
3. Return `max_so_far`

---

## Java Code:

```java
public class MaximumProductSubarray {
    public static int maxProduct(int[] nums) {
        int max_so_far = nums[0];
        int max_ending_here = nums[0];
        int min_ending_here = nums[0];

        for (int i = 1; i < nums.length; i++) {
            int curr = nums[i];

            // If negative, swap max and min
            if (curr < 0) {
                int temp = max_ending_here;
                max_ending_here = min_ending_here;
                min_ending_here = temp;
            }

            max_ending_here = Math.max(curr, max_ending_here * curr);
            min_ending_here = Math.min(curr, min_ending_here * curr);

            max_so_far = Math.max(max_so_far, max_ending_here);
        }

        return max_so_far;
    }

    public static void main(String[] args) {
        int[] arr = {2, 3, -2, 4};
        System.out.println("Maximum product subarray is: " + maxProduct(arr));
    }
}
```

---

### Output:

```
Maximum product subarray is: 6
```

---

## Time and Space Complexity:

* **Time Complexity:** O(N), one pass through array.
* **Space Complexity:** O(1), constant extra space.

---

## 13. Merge intervals.

**Merge Intervals** is a classic interval manipulation problem often asked in Java DSA interviews.

---

## Problem Statement:

Given a collection of intervals, merge all overlapping intervals and return an array of the non-overlapping intervals that cover all the intervals in the input.

---

### Example:

```java
Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]

Explanation: Intervals [1,3] and [2,6] overlap and are merged into [1,6].
```

---

## Approach:

1. **Sort** intervals based on their start times.
2. Initialize a result list with the first interval.
3. Iterate through intervals:

    * If current interval's start is less than or equal to the end of the last interval in result, merge them by updating the end.
    * Otherwise, add the current interval to the result list.
4. Return the result list.

---

## Java Code:

```java
import java.util.*;

public class MergeIntervals {
    public static int[][] merge(int[][] intervals) {
        if (intervals.length <= 1) return intervals;

        // Sort intervals by start time
        Arrays.sort(intervals, Comparator.comparingInt(a -> a[0]));

        List<int[]> merged = new ArrayList<>();
        int[] currentInterval = intervals[0];
        merged.add(currentInterval);

        for (int[] interval : intervals) {
            int currentEnd = currentInterval[1];
            int nextStart = interval[0];
            int nextEnd = interval[1];

            if (nextStart <= currentEnd) {
                // Overlapping intervals, merge them
                currentInterval[1] = Math.max(currentEnd, nextEnd);
            } else {
                // No overlap, add interval
                currentInterval = interval;
                merged.add(currentInterval);
            }
        }

        return merged.toArray(new int[merged.size()][]);
    }

    public static void main(String[] args) {
        int[][] intervals = {{1,3}, {2,6}, {8,10}, {15,18}};
        int[][] merged = merge(intervals);

        System.out.println("Merged intervals:");
        for (int[] interval : merged) {
            System.out.println(Arrays.toString(interval));
        }
    }
}
```

---

### Output:

```
Merged intervals:
[1, 6]
[8, 10]
[15, 18]
```

---

## Time and Space Complexity:

* **Time Complexity:** O(N log N) because of sorting.
* **Space Complexity:** O(N) for the output list.

---

## 14. Search in a rotated sorted array.

**Search in a Rotated Sorted Array** is a classic and popular interview problem related to binary search and array manipulation.

---

## Problem Statement:

Given a sorted array that has been **rotated** at some pivot unknown beforehand, search for a target value in the array. Return its index if found, otherwise return -1.

---

### Example:

```java
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4
```

---

## Key Insight:

The array is originally sorted but rotated, so it has two sorted subarrays. We can modify binary search to work here by determining which side is properly sorted and narrowing search accordingly.

---

## Approach: Modified Binary Search

1. Initialize `low = 0` and `high = nums.length - 1`.
2. While `low <= high`:

    * Find `mid = (low + high) / 2`.
    * If `nums[mid] == target`, return `mid`.
    * Check which side is sorted:

        * If `nums[low] <= nums[mid]` (left side is sorted):

            * Check if target is in `[nums[low], nums[mid]]`, then move `high = mid - 1`, else `low = mid + 1`.
        * Else (right side is sorted):

            * Check if target is in `[nums[mid], nums[high]]`, then move `low = mid + 1`, else `high = mid - 1`.
3. Return -1 if target is not found.

---

## Java Code:

```java
public class SearchRotatedSortedArray {
    public static int search(int[] nums, int target) {
        int low = 0, high = nums.length - 1;

        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (nums[mid] == target) {
                return mid;
            }

            // Check if left side is sorted
            if (nums[low] <= nums[mid]) {
                // Target in left half?
                if (nums[low] <= target && target < nums[mid]) {
                    high = mid - 1;
                } else {
                    low = mid + 1;
                }
            } 
            // Right side must be sorted
            else {
                // Target in right half?
                if (nums[mid] < target && target <= nums[high]) {
                    low = mid + 1;
                } else {
                    high = mid - 1;
                }
            }
        }

        return -1;  // target not found
    }

    public static void main(String[] args) {
        int[] nums = {4,5,6,7,0,1,2};
        int target = 0;

        int index = search(nums, target);
        System.out.println("Target found at index: " + index);
    }
}
```

---

### Output:

```
Target found at index: 4
```

---

## Time and Space Complexity:

* **Time Complexity:** O(log N), binary search modified.
* **Space Complexity:** O(1).

---

## 15. Set matrix zeroes.

The **Set Matrix Zeroes** problem is a common matrix manipulation problem often asked in interviews.

---

## Problem Statement:

Given an `m x n` matrix, if an element is `0`, set its entire row and column to `0` **in-place**.

---

### Example:

```java
Input:
[
  [1,1,1],
  [1,0,1],
  [1,1,1]
]

Output:
[
  [1,0,1],
  [0,0,0],
  [1,0,1]
]
```

---

## Approaches:

### 1. Using Extra Space (Simpler):

* Use two boolean arrays to mark which rows and columns should be zeroed.
* Then update the matrix.

### 2. Optimized In-Place (Using matrix first row and column as markers):

* Use the **first row and first column** of the matrix as markers to indicate which row or column should be zeroed.
* Also keep two flags to check if the first row or first column themselves have any zero.

---

## Step-by-step Optimized Approach:

1. Scan the first row and first column to check if they contain zeroes (store in flags).
2. Traverse the rest of the matrix:

    * If `matrix[i][j] == 0`, mark `matrix[i][0] = 0` and `matrix[0][j] = 0`.
3. Iterate over the matrix (excluding first row and column):

    * If `matrix[i][0] == 0` or `matrix[0][j] == 0`, set `matrix[i][j] = 0`.
4. Zero the first row and column if their flags are true.

---

## Java Code:

```java
public class SetMatrixZeroes {
    public static void setZeroes(int[][] matrix) {
        int rows = matrix.length;
        int cols = matrix[0].length;

        boolean firstRowZero = false;
        boolean firstColZero = false;

        // Check if first row has zero
        for (int j = 0; j < cols; j++) {
            if (matrix[0][j] == 0) {
                firstRowZero = true;
                break;
            }
        }

        // Check if first column has zero
        for (int i = 0; i < rows; i++) {
            if (matrix[i][0] == 0) {
                firstColZero = true;
                break;
            }
        }

        // Use first row and column as markers
        for (int i = 1; i < rows; i++) {
            for (int j = 1; j < cols; j++) {
                if (matrix[i][j] == 0) {
                    matrix[i][0] = 0;
                    matrix[0][j] = 0;
                }
            }
        }

        // Set zeroes based on markers
        for (int i = 1; i < rows; i++) {
            for (int j = 1; j < cols; j++) {
                if (matrix[i][0] == 0 || matrix[0][j] == 0) {
                    matrix[i][j] = 0;
                }
            }
        }

        // Zero first row if needed
        if (firstRowZero) {
            for (int j = 0; j < cols; j++) {
                matrix[0][j] = 0;
            }
        }

        // Zero first column if needed
        if (firstColZero) {
            for (int i = 0; i < rows; i++) {
                matrix[i][0] = 0;
            }
        }
    }

    public static void printMatrix(int[][] matrix) {
        for (int[] row : matrix) {
            for (int val : row) {
                System.out.print(val + " ");
            }
            System.out.println();
        }
    }

    public static void main(String[] args) {
        int[][] matrix = {
            {1,1,1},
            {1,0,1},
            {1,1,1}
        };

        setZeroes(matrix);
        printMatrix(matrix);
    }
}
```

---

### Output:

```
1 0 1 
0 0 0 
1 0 1 
```

---

## Time and Space Complexity:

* **Time Complexity:** O(M\*N), where M and N are matrix dimensions.
* **Space Complexity:** O(1), in-place modification.

---

### 🔹 **16–25: Strings**

## 16. Check if two strings are anagrams.

Checking if two strings are **anagrams** means verifying if they contain the **same characters with the same frequency**, just possibly in a different order.

---

## Problem Statement:

Given two strings `s1` and `s2`, check if they are anagrams of each other.

---

### Example:

```java
Input: s1 = "listen", s2 = "silent"
Output: true

Input: s1 = "hello", s2 = "bello"
Output: false
```

---

## Approaches:

### 1. Sort and Compare:

* Sort both strings.
* If sorted strings are equal, they are anagrams.

### 2. Frequency Count (Using HashMap or Array):

* Count frequency of each character in both strings.
* If frequencies match, they are anagrams.

---

## Java Code using Frequency Count (efficient for large strings):

```java
import java.util.Arrays;

public class AnagramCheck {
    public static boolean areAnagrams(String s1, String s2) {
        if (s1.length() != s2.length()) return false;

        int[] count = new int[26]; // Assuming lowercase letters

        for (int i = 0; i < s1.length(); i++) {
            count[s1.charAt(i) - 'a']++;
            count[s2.charAt(i) - 'a']--;
        }

        for (int c : count) {
            if (c != 0) return false;
        }

        return true;
    }

    public static void main(String[] args) {
        String s1 = "listen";
        String s2 = "silent";

        System.out.println("Are anagrams? " + areAnagrams(s1, s2));
    }
}
```

---

### Output:

```
Are anagrams? true
```

---

## Time and Space Complexity:

* **Time Complexity:** O(N), where N is string length.
* **Space Complexity:** O(1), fixed-size array for character count.

---

Want to know how to modify this to handle Unicode characters or case-insensitive checks?

---

## 17. Longest common prefix.

Sure! The **Longest Common Prefix** problem is a classic string manipulation question often asked in Java DSA interviews.

---

## Problem Statement:

Given an array of strings, find the longest common prefix string among them. If there is no common prefix, return an empty string `""`.

---

### Example:

```java
Input: ["flower", "flow", "flight"]
Output: "fl"

Input: ["dog", "racecar", "car"]
Output: ""
```

---

## Approaches:

### 1. Horizontal Scanning:

* Start with the prefix as the first string.
* Compare prefix with each string and update the prefix by trimming mismatched characters.
* Stop if prefix becomes empty.

### 2. Vertical Scanning:

* Compare characters one by one across all strings.
* Stop at the first mismatch.

---

## Java Code using Horizontal Scanning:

```java
public class LongestCommonPrefix {
    public static String longestCommonPrefix(String[] strs) {
        if (strs == null || strs.length == 0) return "";

        String prefix = strs[0];

        for (int i = 1; i < strs.length; i++) {
            // Update prefix by comparing with current string
            while (!strs[i].startsWith(prefix)) {
                prefix = prefix.substring(0, prefix.length() - 1);
                if (prefix.isEmpty()) return "";
            }
        }

        return prefix;
    }

    public static void main(String[] args) {
        String[] strs = {"flower", "flow", "flight"};
        System.out.println("Longest Common Prefix: " + longestCommonPrefix(strs));
    }
}
```

---

### Output:

```
Longest Common Prefix: fl
```

---

## Time and Space Complexity:

* **Time Complexity:** O(S), where S is the sum of all characters in all strings.
* **Space Complexity:** O(1), only prefix string is stored.

---

## 18. Reverse words in a string.

**Reversing words in a string** is a classic string manipulation problem.

---

## Problem Statement:

Given a string, reverse the order of the words. A word is defined as a sequence of non-space characters. The string may contain leading or trailing spaces and multiple spaces between words — the reversed string should have words separated by a single space with no leading or trailing spaces.

---

### Example:

```java
Input: "  the sky  is blue  "
Output: "blue is sky the"
```

---

## Approach:

1. **Trim** the string to remove leading and trailing spaces.
2. **Split** the string by spaces.
3. Filter out empty words caused by multiple spaces.
4. Reverse the list of words.
5. Join them with a single space.

---

## Java Code:

```java
public class ReverseWordsInString {
    public static String reverseWords(String s) {
        s = s.trim(); // remove leading and trailing spaces

        String[] words = s.split("\\s+"); // split by one or more spaces

        StringBuilder reversed = new StringBuilder();

        for (int i = words.length - 1; i >= 0; i--) {
            reversed.append(words[i]);
            if (i != 0) reversed.append(" ");
        }

        return reversed.toString();
    }

    public static void main(String[] args) {
        String input = "  the sky  is blue  ";
        System.out.println("Reversed: \"" + reverseWords(input) + "\"");
    }
}
```

---

### Output:

```
Reversed: "blue is sky the"
```

---

## Time and Space Complexity:

* **Time Complexity:** O(N), where N is the length of the string.
* **Space Complexity:** O(N), to store words and reversed string.

---

## 19. Longest substring without repeating characters.

The **Longest Substring Without Repeating Characters** is a popular sliding window problem.

---

## Problem Statement:

Given a string, find the length of the longest substring without repeating characters.

---

### Example:

```java
Input: "abcabcbb"
Output: 3
Explanation: The answer is "abc", with length 3.
```

---

## Approach: Sliding Window with HashMap / HashSet

* Use two pointers (`start` and `end`) to create a sliding window.
* Use a set or map to track characters in the current window.
* Expand `end` pointer by adding characters until a duplicate is found.
* When duplicate found, move `start` forward until the duplicate is removed.
* Keep track of the maximum window size during iteration.

---

## Java Code (Using HashSet):

```java
import java.util.HashSet;

public class LongestSubstringWithoutRepeating {
    public static int lengthOfLongestSubstring(String s) {
        int n = s.length();
        int maxLen = 0;
        int start = 0, end = 0;

        HashSet<Character> set = new HashSet<>();

        while (end < n) {
            char c = s.charAt(end);
            if (!set.contains(c)) {
                set.add(c);
                end++;
                maxLen = Math.max(maxLen, end - start);
            } else {
                set.remove(s.charAt(start));
                start++;
            }
        }

        return maxLen;
    }

    public static void main(String[] args) {
        String s = "abcabcbb";
        System.out.println("Length of longest substring without repeating characters: " + lengthOfLongestSubstring(s));
    }
}
```

---

### Output:

```
Length of longest substring without repeating characters: 3
```

---

## Time and Space Complexity:

* **Time Complexity:** O(N), each character visited at most twice.
* **Space Complexity:** O(min(N, M)), where M is character set size (e.g., 26 for lowercase letters).

---

## 20. Valid palindrome (with/without removing one character).

The **Valid Palindrome** problem has two common variations:

---

## 1. Valid Palindrome (Simple)

### Problem:

Check if a given string is a palindrome considering only alphanumeric characters and ignoring cases.

---

## 2. Valid Palindrome II (With removing one character)

### Problem:

Check if the string can be a palindrome **after removing at most one character**.

---

# 1. Valid Palindrome (Simple)

### Approach:

* Use two pointers `left` and `right` starting from ends.
* Move towards center, ignoring non-alphanumeric characters.
* Compare characters ignoring case.
* If mismatch, return false.

---

## Java Code:

```java
public class ValidPalindrome {
    public static boolean isPalindrome(String s) {
        int left = 0, right = s.length() - 1;

        while (left < right) {
            // Skip non-alphanumeric
            while (left < right && !Character.isLetterOrDigit(s.charAt(left))) left++;
            while (left < right && !Character.isLetterOrDigit(s.charAt(right))) right--;

            if (Character.toLowerCase(s.charAt(left)) != Character.toLowerCase(s.charAt(right))) {
                return false;
            }

            left++;
            right--;
        }

        return true;
    }

    public static void main(String[] args) {
        String s = "A man, a plan, a canal: Panama";
        System.out.println(isPalindrome(s));  // true
    }
}
```

---

# 2. Valid Palindrome II (Remove at most one character)

### Approach:

* Use two pointers.
* When mismatch found, try skipping either left or right character and check if substring is palindrome.
* If any of those work, return true.

---

## Java Code:

```java
public class ValidPalindromeII {
    public static boolean validPalindrome(String s) {
        int left = 0, right = s.length() - 1;

        while (left < right) {
            if (s.charAt(left) != s.charAt(right)) {
                // Try skipping left or right character
                return isPalindromeRange(s, left + 1, right) || isPalindromeRange(s, left, right - 1);
            }
            left++;
            right--;
        }
        return true;
    }

    private static boolean isPalindromeRange(String s, int left, int right) {
        while (left < right) {
            if (s.charAt(left) != s.charAt(right)) return false;
            left++;
            right--;
        }
        return true;
    }

    public static void main(String[] args) {
        System.out.println(validPalindrome("abca"));  // true (remove 'c')
        System.out.println(validPalindrome("abc"));   // false
    }
}
```

---

## Time Complexity:

* Both solutions run in **O(N)** time.

---

## 21. String compression.

The **String Compression** problem is a common coding interview question focused on in-place modification of strings (or arrays of characters).

---

## Problem Statement:

Given a string, compress it using the counts of repeated characters. For example, the string `"aabcccccaaa"` would become `"a2b1c5a3"`. If the compressed string is not smaller than the original string, return the original string.

---

### Example:

```java
Input: "aabcccccaaa"
Output: "a2b1c5a3"

Input: "abc"
Output: "abc"  // compressed string "a1b1c1" is longer, so return original
```

---

## Approach:

* Iterate over the string.
* Count consecutive repeated characters.
* Append the character and count to a `StringBuilder`.
* After building the compressed string, compare its length with the original.
* Return the compressed string if shorter; otherwise, return the original.

---

## Java Code:

```java
public class StringCompression {
    public static String compress(String s) {
        if (s == null || s.length() == 0) return s;

        StringBuilder compressed = new StringBuilder();

        int count = 1;
        for (int i = 1; i <= s.length(); i++) {
            if (i < s.length() && s.charAt(i) == s.charAt(i - 1)) {
                count++;
            } else {
                compressed.append(s.charAt(i - 1));
                compressed.append(count);
                count = 1;
            }
        }

        String compressedStr = compressed.toString();
        return compressedStr.length() < s.length() ? compressedStr : s;
    }

    public static void main(String[] args) {
        System.out.println(compress("aabcccccaaa")); // Output: a2b1c5a3
        System.out.println(compress("abc"));         // Output: abc
    }
}
```

---

### Output:

```
a2b1c5a3
abc
```

---

## Time and Space Complexity:

* **Time Complexity:** O(N), where N is the length of the string.
* **Space Complexity:** O(N), for the compressed string in the worst case.

---

## 22. Group anagrams.

**Grouping anagrams** is a common interview question that tests your understanding of hash maps and string manipulation.

---

## Problem Statement:

Given an array of strings, group the strings that are anagrams of each other.

---

### Example:

```java
Input: ["eat", "tea", "tan", "ate", "nat", "bat"]

Output:
[
  ["eat", "tea", "ate"],
  ["tan", "nat"],
  ["bat"]
]
```

---

## Approach:

### Using Sorted String as Key

* For each string, sort its characters to form a key.
* Use a HashMap to group strings by this key.
* The map's values will be lists of anagrams.

---

## Java Code:

```java
import java.util.*;

public class GroupAnagrams {
    public static List<List<String>> groupAnagrams(String[] strs) {
        if (strs == null || strs.length == 0) return new ArrayList<>();

        Map<String, List<String>> map = new HashMap<>();

        for (String s : strs) {
            // Sort the string to get the key
            char[] chars = s.toCharArray();
            Arrays.sort(chars);
            String key = new String(chars);

            // Add to map
            map.computeIfAbsent(key, k -> new ArrayList<>()).add(s);
        }

        return new ArrayList<>(map.values());
    }

    public static void main(String[] args) {
        String[] input = {"eat", "tea", "tan", "ate", "nat", "bat"};

        List<List<String>> result = groupAnagrams(input);

        for (List<String> group : result) {
            System.out.println(group);
        }
    }
}
```

---

### Output:

```
[eat, tea, ate]
[tan, nat]
[bat]
```

---

## Time and Space Complexity:

* **Time Complexity:** O(N \* K log K), where N = number of strings and K = max length of a string (sorting each string).
* **Space Complexity:** O(N \* K) for storing the grouped anagrams.

---

### Alternative (Counting Character Frequencies as Key):

* Instead of sorting, you can create a frequency count string as key to avoid sorting overhead.
* Useful if string length is large.

---

## 23. Implement strStr() / indexOf().

Implementing **strStr()** (similar to `indexOf()` in Java) means finding the first occurrence of a substring (**needle**) inside another string (**haystack**).

---

## Problem Statement:

Return the index of the first occurrence of the substring `needle` in the string `haystack`. If `needle` is not part of `haystack`, return `-1`.

---

### Example:

```java
Input: haystack = "hello", needle = "ll"
Output: 2

Input: haystack = "aaaaa", needle = "bba"
Output: -1

Input: haystack = "abc", needle = ""
Output: 0
```

---

## Approach 1: Brute Force

* Check every possible starting position in `haystack`.
* Compare substring starting at that position with `needle`.
* Return the index if match found.

---

## Java Code (Brute Force):

```java
public class StrStr {
    public static int strStr(String haystack, String needle) {
        if (needle.isEmpty()) return 0;

        int hLen = haystack.length();
        int nLen = needle.length();

        for (int i = 0; i <= hLen - nLen; i++) {
            int j = 0;
            while (j < nLen && haystack.charAt(i + j) == needle.charAt(j)) {
                j++;
            }
            if (j == nLen) return i;
        }

        return -1;
    }

    public static void main(String[] args) {
        System.out.println(strStr("hello", "ll"));   // Output: 2
        System.out.println(strStr("aaaaa", "bba"));  // Output: -1
        System.out.println(strStr("abc", ""));       // Output: 0
    }
}
```

---

## Time Complexity:

* Worst case: **O((H - N) \* N)** where H = length of haystack, N = length of needle.

---

## Approach 2: KMP Algorithm (Efficient)

* Preprocess the `needle` to create a longest prefix suffix (LPS) array.
* Use LPS to avoid rechecking characters.
* Achieves **O(H + N)** time complexity.

---

## 24. Check for rotation of strings.

Checking if one string is a **rotation** of another is a classic string problem.

---

## Problem Statement:

Given two strings `s1` and `s2`, check if `s2` is a rotation of `s1`.

---

### Example:

```java
Input: s1 = "waterbottle", s2 = "erbottlewat"
Output: true

Input: s1 = "hello", s2 = "llohe"
Output: true

Input: s1 = "hello", s2 = "olelh"
Output: false
```

---

## Key Insight:

* If you concatenate `s1` with itself (i.e., `s1 + s1`), any rotation of `s1` will be a substring of that concatenated string.
* So, check if `s2` is a substring of `s1 + s1`.

---

## Java Code:

```java
public class StringRotationCheck {
    public static boolean isRotation(String s1, String s2) {
        if (s1 == null || s2 == null) return false;
        if (s1.length() != s2.length()) return false;
        if (s1.isEmpty() && s2.isEmpty()) return true;

        String concatenated = s1 + s1;
        return concatenated.contains(s2);
    }

    public static void main(String[] args) {
        System.out.println(isRotation("waterbottle", "erbottlewat")); // true
        System.out.println(isRotation("hello", "llohe"));             // true
        System.out.println(isRotation("hello", "olelh"));             // false
    }
}
```

---

## Time Complexity:

* Concatenation: O(N)
* Substring search: O(N) (depends on the implementation of `contains()`)
* Overall: O(N)

---

## 25. Count and say problem.

The **Count and Say** problem is a classic iterative string sequence problem often asked in interviews.

---

## Problem Statement:

The "Count and Say" sequence is a sequence of digit strings defined by the recursive formula:

* `countAndSay(1) = "1"`
* `countAndSay(n)` is the way you would **"say"** the digit string from `countAndSay(n-1)`, describing the count of digits appearing consecutively.

---

### Example:

```
Input: n = 4

Sequence:
1. "1"
2. "11"        (one 1)
3. "21"        (two 1s)
4. "1211"      (one 2, one 1)

Output: "1211"
```

---

## Approach:

* Start from "1".
* For each iteration from 2 to n, read the previous string.
* Count consecutive characters and append count + character to build the next string.

---

## Java Code:

```java
public class CountAndSay {
    public static String countAndSay(int n) {
        if (n <= 0) return "";

        String result = "1";

        for (int i = 2; i <= n; i++) {
            StringBuilder sb = new StringBuilder();

            int count = 1;
            char prev = result.charAt(0);

            for (int j = 1; j < result.length(); j++) {
                if (result.charAt(j) == prev) {
                    count++;
                } else {
                    sb.append(count);
                    sb.append(prev);
                    prev = result.charAt(j);
                    count = 1;
                }
            }

            // Append the last counted character
            sb.append(count);
            sb.append(prev);

            result = sb.toString();
        }

        return result;
    }

    public static void main(String[] args) {
        int n = 4;
        System.out.println("Count and Say for n=" + n + ": " + countAndSay(n));
    }
}
```

---

### Output:

```
Count and Say for n=4: 1211
```

---

## Time Complexity:

* Each iteration processes the previous string, which can grow exponentially, so roughly O(2^n) in the worst case.

---

### 🔹 **26–35: Linked List**

## 26. Reverse a linked list (iterative & recursive).

Reversing a linked list is a fundamental problem in data structures and a common interview question. I'll explain both **iterative** and **recursive** methods with examples.

---

# Problem Statement:

Given the head of a singly linked list, reverse the list and return the new head.

---

## Definition of Linked List Node in Java:

```java
class ListNode {
    int val;
    ListNode next;

    ListNode(int val) {
        this.val = val;
        this.next = null;
    }
}
```

---

# 1. Iterative Approach

### Idea:

* Maintain three pointers: `prev`, `current`, and `next`.
* Iterate through the list, reverse the `next` pointer of each node to point to `prev`.
* Move pointers forward until the list ends.
* Return `prev` as the new head.

---

### Code:

```java
public class ReverseLinkedList {

    public static ListNode reverseIterative(ListNode head) {
        ListNode prev = null;
        ListNode current = head;

        while (current != null) {
            ListNode next = current.next; // save next node
            current.next = prev;          // reverse pointer
            prev = current;               // move prev forward
            current = next;               // move current forward
        }

        return prev; // new head
    }
    
    // Helper method to print the linked list
    public static void printList(ListNode head) {
        ListNode curr = head;
        while (curr != null) {
            System.out.print(curr.val + " -> ");
            curr = curr.next;
        }
        System.out.println("null");
    }

    public static void main(String[] args) {
        // Create linked list: 1 -> 2 -> 3 -> 4 -> null
        ListNode head = new ListNode(1);
        head.next = new ListNode(2);
        head.next.next = new ListNode(3);
        head.next.next.next = new ListNode(4);

        System.out.print("Original List: ");
        printList(head);

        head = reverseIterative(head);

        System.out.print("Reversed List (Iterative): ");
        printList(head);
    }
}
```

---

# 2. Recursive Approach

### Idea:

* Recursively reverse the sublist starting from `head.next`.
* When recursion reaches the end (base case), start unwinding:
* For each node, make the next node point back to current node.
* Set current node’s `next` to null (to avoid cycle).
* Return new head up the recursion.

---

### Code:

```java
public class ReverseLinkedListRecursive {

    public static ListNode reverseRecursive(ListNode head) {
        // Base case: empty list or single node
        if (head == null || head.next == null) return head;

        // Reverse rest of list
        ListNode newHead = reverseRecursive(head.next);

        // Make next node point back to current
        head.next.next = head;
        head.next = null;

        return newHead;
    }

    // Reuse printList and ListNode from previous example

    public static void main(String[] args) {
        // Create linked list: 1 -> 2 -> 3 -> 4 -> null
        ListNode head = new ListNode(1);
        head.next = new ListNode(2);
        head.next.next = new ListNode(3);
        head.next.next.next = new ListNode(4);

        System.out.print("Original List: ");
        ReverseLinkedList.printList(head);

        head = reverseRecursive(head);

        System.out.print("Reversed List (Recursive): ");
        ReverseLinkedList.printList(head);
    }
}
```

---

## Output:

```
Original List: 1 -> 2 -> 3 -> 4 -> null
Reversed List (Iterative): 4 -> 3 -> 2 -> 1 -> null
Original List: 1 -> 2 -> 3 -> 4 -> null
Reversed List (Recursive): 4 -> 3 -> 2 -> 1 -> null
```

---

## Time and Space Complexity:

| Approach  | Time Complexity | Space Complexity            |
| --------- | --------------- | --------------------------- |
| Iterative | O(N)            | O(1)                        |
| Recursive | O(N)            | O(N) due to recursion stack |

---

## 27. Detect a cycle in a linked list (Floyd’s Algorithm).

Detecting a cycle in a linked list using **Floyd’s Cycle Detection Algorithm (Tortoise and Hare algorithm)** is a classic problem.

---

## Problem Statement:

Given the head of a linked list, determine if the linked list has a cycle (loop) in it.

---

## Idea (Floyd’s Algorithm):

* Use two pointers: `slow` and `fast`.
* `slow` moves one step at a time.
* `fast` moves two steps at a time.
* If there is no cycle, `fast` will reach the end (`null`).
* If there is a cycle, at some point, `fast` and `slow` will meet inside the cycle.

---

## Linked List Node Definition:

```java
class ListNode {
    int val;
    ListNode next;
    ListNode(int val) { this.val = val; this.next = null; }
}
```

---

## Java Code:

```java
public class CycleDetection {

    public static boolean hasCycle(ListNode head) {
        if (head == null || head.next == null) return false;

        ListNode slow = head;
        ListNode fast = head;

        while (fast != null && fast.next != null) {
            slow = slow.next;           // move slow by 1
            fast = fast.next.next;      // move fast by 2

            if (slow == fast) {         // cycle detected
                return true;
            }
        }

        return false; // no cycle
    }

    public static void main(String[] args) {
        // Create a list with cycle: 1 -> 2 -> 3 -> 4 -> 2 ...
        ListNode head = new ListNode(1);
        head.next = new ListNode(2);
        head.next.next = new ListNode(3);
        head.next.next.next = new ListNode(4);
        head.next.next.next.next = head.next; // cycle here

        System.out.println("Has Cycle? " + hasCycle(head)); // true

        // Create a list without cycle: 1 -> 2 -> 3 -> 4 -> null
        ListNode noCycleHead = new ListNode(1);
        noCycleHead.next = new ListNode(2);
        noCycleHead.next.next = new ListNode(3);
        noCycleHead.next.next.next = new ListNode(4);

        System.out.println("Has Cycle? " + hasCycle(noCycleHead)); // false
    }
}
```

---

## Explanation:

* If a cycle exists, the fast pointer will eventually “lap” the slow pointer, making them equal.
* If no cycle, fast pointer hits the end (`null`).

---

## Time and Space Complexity:

* **Time Complexity:** O(N)
* **Space Complexity:** O(1)

---

## 28. Find the middle of a linked list.

Finding the middle of a linked list is a classic problem and can be efficiently solved using the **slow and fast pointer technique**.

---

## Problem Statement:

Given the head of a singly linked list, find the middle node of the linked list. If there are two middle nodes (i.e., even length), return the second middle node.

---

### Example:

```
Input: 1 -> 2 -> 3 -> 4 -> 5 -> null
Output: 3

Input: 1 -> 2 -> 3 -> 4 -> 5 -> 6 -> null
Output: 4
```

---

## Approach (Slow and Fast Pointer):

* Use two pointers: `slow` and `fast`.
* `slow` moves 1 step at a time.
* `fast` moves 2 steps at a time.
* When `fast` reaches the end (`null`), `slow` will be at the middle node.

---

## Java Code:

```java
class ListNode {
    int val;
    ListNode next;
    ListNode(int val) { this.val = val; this.next = null; }
}

public class MiddleOfLinkedList {
    public static ListNode findMiddle(ListNode head) {
        if (head == null) return null;

        ListNode slow = head;
        ListNode fast = head;

        // Move fast by 2 and slow by 1
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }

        return slow;  // slow is now at the middle
    }

    public static void main(String[] args) {
        // Create linked list: 1 -> 2 -> 3 -> 4 -> 5 -> null
        ListNode head = new ListNode(1);
        head.next = new ListNode(2);
        head.next.next = new ListNode(3);
        head.next.next.next = new ListNode(4);
        head.next.next.next.next = new ListNode(5);

        ListNode middle = findMiddle(head);
        System.out.println("Middle node value: " + middle.val);  // Output: 3

        // Even length list: 1 -> 2 -> 3 -> 4 -> 5 -> 6 -> null
        head.next.next.next.next.next = new ListNode(6);

        middle = findMiddle(head);
        System.out.println("Middle node value: " + middle.val);  // Output: 4
    }
}
```

---

## Time Complexity:

* O(N), where N is the number of nodes.

## Space Complexity:

* O(1), constant extra space.

---

## 29. Merge two sorted linked lists.

Merging two sorted linked lists into one sorted linked list is a classic problem and often asked in interviews.

---

## Problem Statement:

Given two sorted linked lists, merge them into one sorted linked list and return the head of the merged list.

---

### Example:

```
Input:
List 1: 1 -> 3 -> 5 -> null
List 2: 2 -> 4 -> 6 -> null

Output:
1 -> 2 -> 3 -> 4 -> 5 -> 6 -> null
```

---

## Approach:

* Use two pointers to traverse both lists.
* Compare the current nodes of both lists.
* Attach the smaller node to the merged list.
* Move the pointer in the list from which the node was taken.
* Continue until all nodes from both lists are processed.

---

## Java Code:

```java
class ListNode {
    int val;
    ListNode next;
    ListNode(int val) { this.val = val; this.next = null; }
}

public class MergeSortedLists {
    public static ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        // Dummy node to act as the start of the merged list
        ListNode dummy = new ListNode(0);
        ListNode current = dummy;

        // Traverse both lists
        while (l1 != null && l2 != null) {
            if (l1.val < l2.val) {
                current.next = l1;
                l1 = l1.next;
            } else {
                current.next = l2;
                l2 = l2.next;
            }
            current = current.next;
        }

        // Attach remaining nodes, if any
        if (l1 != null) {
            current.next = l1;
        } else {
            current.next = l2;
        }

        // Return merged list starting from the next of dummy node
        return dummy.next;
    }

    // Helper method to print linked list
    public static void printList(ListNode head) {
        ListNode current = head;
        while (current != null) {
            System.out.print(current.val + " -> ");
            current = current.next;
        }
        System.out.println("null");
    }

    public static void main(String[] args) {
        // List 1: 1 -> 3 -> 5 -> null
        ListNode l1 = new ListNode(1);
        l1.next = new ListNode(3);
        l1.next.next = new ListNode(5);

        // List 2: 2 -> 4 -> 6 -> null
        ListNode l2 = new ListNode(2);
        l2.next = new ListNode(4);
        l2.next.next = new ListNode(6);

        ListNode mergedHead = mergeTwoLists(l1, l2);

        System.out.print("Merged List: ");
        printList(mergedHead);
    }
}
```

---

## Output:

```
Merged List: 1 -> 2 -> 3 -> 4 -> 5 -> 6 -> null
```

---

## Time Complexity:

* O(N + M), where N and M are the lengths of the two lists.

## Space Complexity:

* O(1), since merging is done in place without extra space.

---

## 30. Remove N-th node from end.

Removing the N-th node from the end of a linked list is a classic problem and a good test of pointer manipulation.

---

## Problem Statement:

Given the head of a linked list, remove the **N-th node from the end** of the list and return its head.

---

### Example:

```
Input: 1 -> 2 -> 3 -> 4 -> 5, n = 2
Output: 1 -> 2 -> 3 -> 5
```

(The 2nd node from the end is "4", which is removed.)

---

## Approach: Two Pointers (Fast & Slow)

* Use two pointers `fast` and `slow`.
* Move `fast` pointer `n` steps ahead.
* Then move both pointers one step at a time until `fast` reaches the end.
* Now, `slow` is right before the node to remove.
* Adjust pointers to skip the target node.
* Use a dummy node to handle edge cases (like removing the head).

---

## Java Code:

```java
class ListNode {
    int val;
    ListNode next;
    ListNode(int val) { this.val = val; this.next = null; }
}

public class RemoveNthFromEnd {
    public static ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;

        ListNode fast = dummy;
        ListNode slow = dummy;

        // Move fast n+1 steps ahead to maintain a gap of n between fast and slow
        for (int i = 0; i <= n; i++) {
            fast = fast.next;
        }

        // Move both pointers until fast reaches the end
        while (fast != null) {
            fast = fast.next;
            slow = slow.next;
        }

        // Skip the target node
        slow.next = slow.next.next;

        return dummy.next;
    }

    // Helper method to print linked list
    public static void printList(ListNode head) {
        ListNode current = head;
        while (current != null) {
            System.out.print(current.val + " -> ");
            current = current.next;
        }
        System.out.println("null");
    }

    public static void main(String[] args) {
        // Create linked list: 1 -> 2 -> 3 -> 4 -> 5
        ListNode head = new ListNode(1);
        head.next = new ListNode(2);
        head.next.next = new ListNode(3);
        head.next.next.next = new ListNode(4);
        head.next.next.next.next = new ListNode(5);

        System.out.print("Original List: ");
        printList(head);

        int n = 2;
        head = removeNthFromEnd(head, n);

        System.out.print("List after removing " + n + "-th node from end: ");
        printList(head);
    }
}
```

---

## Explanation:

* The `fast` pointer advances `n+1` steps to maintain a gap of `n` nodes with the `slow` pointer.
* When `fast` reaches the end, `slow` points to the node **before** the target node.
* We then remove the target by changing `slow.next`.

---

## Time Complexity:

* O(N), where N is the number of nodes.

## Space Complexity:

* O(1)

---

## 31. Add two numbers represented by linked lists.

Adding two numbers represented by linked lists is a classic problem, often seen in interviews.

---

## Problem Statement:

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in **reverse order**, and each node contains a single digit. Add the two numbers and return the sum as a linked list, also in reverse order.

---

### Example:

```
Input:
List1: 2 -> 4 -> 3  (represents 342)
List2: 5 -> 6 -> 4  (represents 465)

Output:
7 -> 0 -> 8  (represents 807, since 342 + 465 = 807)
```

---

## Approach:

* Use two pointers to traverse both lists simultaneously.
* Add digits plus carry from previous addition.
* Create new nodes for the resulting linked list.
* Continue until both lists and carry are exhausted.

---

## Java Code:

```java
class ListNode {
    int val;
    ListNode next;
    ListNode(int val) { this.val = val; this.next = null; }
}

public class AddTwoNumbers {
    public static ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(0);
        ListNode current = dummy;

        int carry = 0;
        while (l1 != null || l2 != null || carry != 0) {
            int sum = carry;

            if (l1 != null) {
                sum += l1.val;
                l1 = l1.next;
            }

            if (l2 != null) {
                sum += l2.val;
                l2 = l2.next;
            }

            carry = sum / 10;
            int digit = sum % 10;

            current.next = new ListNode(digit);
            current = current.next;
        }

        return dummy.next;
    }

    // Helper method to print linked list
    public static void printList(ListNode head) {
        ListNode current = head;
        while (current != null) {
            System.out.print(current.val + " -> ");
            current = current.next;
        }
        System.out.println("null");
    }

    public static void main(String[] args) {
        // List 1: 2 -> 4 -> 3 (342)
        ListNode l1 = new ListNode(2);
        l1.next = new ListNode(4);
        l1.next.next = new ListNode(3);

        // List 2: 5 -> 6 -> 4 (465)
        ListNode l2 = new ListNode(5);
        l2.next = new ListNode(6);
        l2.next.next = new ListNode(4);

        ListNode result = addTwoNumbers(l1, l2);
        System.out.print("Sum List: ");
        printList(result); // Output: 7 -> 0 -> 8 -> null
    }
}
```

---

## Explanation:

* Add corresponding digits from each list along with any carry.
* Create a new node with the resulting digit.
* Propagate the carry to the next addition.
* When both lists end, if carry is non-zero, add a new node with carry.

---

## Time Complexity:

* O(max(N, M)), where N and M are the lengths of the two lists.

## Space Complexity:

* O(max(N, M)) for the result linked list.

---

## 32. Check if linked list is a palindrome.

Checking if a linked list is a palindrome is a common interview problem that tests your understanding of linked list manipulation.

---

## Problem Statement:

Given the head of a singly linked list, determine if the linked list reads the same forwards and backwards.

---

### Example:

```
Input: 1 -> 2 -> 3 -> 2 -> 1 -> null
Output: true

Input: 1 -> 2 -> 3 -> 4 -> null
Output: false
```

---

## Approach:

To check if a linked list is a palindrome, the most efficient way is:

1. **Find the middle of the linked list** using slow and fast pointers.
2. **Reverse the second half** of the linked list.
3. **Compare** the first half and reversed second half node-by-node.
4. **Restore the list** (optional, if you want to keep the original list).
5. Return `true` if both halves are identical; otherwise, `false`.

---

## Java Code:

```java
class ListNode {
    int val;
    ListNode next;
    ListNode(int val) { this.val = val; this.next = null; }
}

public class PalindromeLinkedList {

    public static boolean isPalindrome(ListNode head) {
        if (head == null || head.next == null) return true;

        // Step 1: Find middle of linked list
        ListNode slow = head;
        ListNode fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }

        // Step 2: Reverse second half
        ListNode secondHalfStart = reverseList(slow);

        // Step 3: Compare first half and reversed second half
        ListNode firstHalfStart = head;
        ListNode secondHalfIter = secondHalfStart;
        boolean palindrome = true;
        while (secondHalfIter != null) {
            if (firstHalfStart.val != secondHalfIter.val) {
                palindrome = false;
                break;
            }
            firstHalfStart = firstHalfStart.next;
            secondHalfIter = secondHalfIter.next;
        }

        // Step 4 (optional): Restore the list
        reverseList(secondHalfStart);

        return palindrome;
    }

    // Helper method to reverse linked list
    private static ListNode reverseList(ListNode head) {
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

    // Helper method to print list (for testing)
    public static void printList(ListNode head) {
        ListNode current = head;
        while (current != null) {
            System.out.print(current.val + " -> ");
            current = current.next;
        }
        System.out.println("null");
    }

    public static void main(String[] args) {
        // Palindrome list: 1 -> 2 -> 3 -> 2 -> 1
        ListNode head1 = new ListNode(1);
        head1.next = new ListNode(2);
        head1.next.next = new ListNode(3);
        head1.next.next.next = new ListNode(2);
        head1.next.next.next.next = new ListNode(1);

        System.out.println("Is palindrome? " + isPalindrome(head1)); // true

        // Non-palindrome list: 1 -> 2 -> 3 -> 4
        ListNode head2 = new ListNode(1);
        head2.next = new ListNode(2);
        head2.next.next = new ListNode(3);
        head2.next.next.next = new ListNode(4);

        System.out.println("Is palindrome? " + isPalindrome(head2)); // false
    }
}
```

---

## Explanation:

* Use slow and fast pointers to find midpoint.
* Reverse second half of the list.
* Compare nodes of first half and reversed second half.
* If all nodes match, list is palindrome.
* Optionally restore original list to keep data intact.

---

## Time Complexity:

* O(N) — traversing the list a few times.

## Space Complexity:

* O(1) — only pointers used, no extra data structures.

---

## 33. Flatten a multilevel linked list.

Flattening a multilevel linked list is a classic linked list problem that involves handling nodes with both next pointers and child pointers.

---

## Problem Statement:

Given a **multilevel doubly linked list**, where in addition to the next and previous pointers, some nodes have a **child pointer** that may point to another doubly linked list, flatten the list so that all nodes appear in a single-level doubly linked list. The flattened list should follow the depth-first traversal order.

---

### Visual Example:

```
Input:
1 - 2 - 3 - 4 - 5 - 6 - null
        |
        7 - 8 - 9 - 10 - null
             |
             11 - 12 - null

Output (flattened):
1 - 2 - 3 - 7 - 8 - 11 - 12 - 9 - 10 - 4 - 5 - 6 - null
```

---

## Approach:

* Traverse the list.
* Whenever you find a node with a child:

    * Recursively flatten the child list.
    * Insert the flattened child list between the current node and the next node.
    * Update `prev` and `next` pointers accordingly.
* Continue traversal until the entire list is flattened.

---

## Java Code:

```java
class Node {
    int val;
    Node prev;
    Node next;
    Node child;

    Node(int val) {
        this.val = val;
        this.prev = null;
        this.next = null;
        this.child = null;
    }
}

public class FlattenMultilevelList {

    public static Node flatten(Node head) {
        if (head == null) return head;

        Node current = head;

        while (current != null) {
            if (current.child == null) {
                current = current.next;
                continue;
            }

            // Save next node after current
            Node next = current.next;

            // Flatten child list recursively
            Node childHead = flatten(current.child);

            // Insert the child list between current and next
            current.next = childHead;
            childHead.prev = current;
            current.child = null; // Clear child pointer

            // Find the tail of the flattened child list
            Node tail = childHead;
            while (tail.next != null) {
                tail = tail.next;
            }

            // Connect tail to next
            tail.next = next;
            if (next != null) {
                next.prev = tail;
            }

            // Move current to next
            current = next;
        }

        return head;
    }

    // Helper function to print doubly linked list
    public static void printList(Node head) {
        Node curr = head;
        while (curr != null) {
            System.out.print(curr.val + " <-> ");
            curr = curr.next;
        }
        System.out.println("null");
    }

    public static void main(String[] args) {
        /*
        Construct the example multilevel list:
        1 - 2 - 3 - 4 - 5 - 6
                |
                7 - 8 - 9 - 10
                     |
                     11 - 12
        */

        Node node1 = new Node(1);
        Node node2 = new Node(2);
        Node node3 = new Node(3);
        Node node4 = new Node(4);
        Node node5 = new Node(5);
        Node node6 = new Node(6);
        Node node7 = new Node(7);
        Node node8 = new Node(8);
        Node node9 = new Node(9);
        Node node10 = new Node(10);
        Node node11 = new Node(11);
        Node node12 = new Node(12);

        // Setup next pointers
        node1.next = node2; node2.prev = node1;
        node2.next = node3; node3.prev = node2;
        node3.next = node4; node4.prev = node3;
        node4.next = node5; node5.prev = node4;
        node5.next = node6; node6.prev = node5;

        node7.next = node8; node8.prev = node7;
        node8.next = node9; node9.prev = node8;
        node9.next = node10; node10.prev = node9;

        node11.next = node12; node12.prev = node11;

        // Setup child pointers
        node3.child = node7;
        node8.child = node11;

        System.out.println("Original list:");
        printList(node1);

        Node flattenedHead = flatten(node1);
        System.out.println("Flattened list:");
        printList(flattenedHead);
    }
}
```

---

## Explanation:

* The algorithm recursively flattens any child lists it encounters.
* Inserts the flattened child list between the current node and its next node.
* Properly connects `prev` and `next` pointers.
* Sets child pointers to `null` after flattening.

---

## Time Complexity:

* O(N), where N is total number of nodes (including all child lists).

## Space Complexity:

* O(N) due to recursion stack in worst case.

---

## 34. Clone a linked list with random pointers.

Cloning a linked list where each node has a **random pointer** (which can point to any node or null) is a classic tricky problem.

---

## Problem Statement:

Given a linked list where each node has two pointers:

* `next` pointer to the next node in the list,
* `random` pointer to any node in the list or null,

Create a **deep copy** (clone) of the list.

---

### Example:

Original list:

```
Node1(val=1) -> Node2(val=2) -> Node3(val=3) -> null
  |               |               |
 random         random          random
  |               |               |
 Node3           Node1           null
```

---

## Approach:

### Intuition:

* We need to copy both `next` and `random` pointers properly.
* Naive approach: Use a hash map to store old node → new node mapping.
* Optimized approach (without extra space) uses clever interleaving of nodes.

---

### Method 1: Using HashMap (simpler)

1. Traverse original list and create new nodes copying only values.
2. Use a hashmap to map original node → cloned node.
3. Traverse again to assign `next` and `random` pointers to cloned nodes using the map.

---

### Java Code (HashMap method):

```java
import java.util.HashMap;

class Node {
    int val;
    Node next;
    Node random;

    Node(int val) {
        this.val = val;
        this.next = null;
        this.random = null;
    }
}

public class CloneRandomList {

    public static Node copyRandomList(Node head) {
        if (head == null) return null;

        HashMap<Node, Node> map = new HashMap<>();

        // Step 1: Create clone nodes and store in map
        Node current = head;
        while (current != null) {
            map.put(current, new Node(current.val));
            current = current.next;
        }

        // Step 2: Assign next and random pointers
        current = head;
        while (current != null) {
            Node clone = map.get(current);
            clone.next = (current.next != null) ? map.get(current.next) : null;
            clone.random = (current.random != null) ? map.get(current.random) : null;
            current = current.next;
        }

        return map.get(head);
    }

    // Helper method to print list (show val and random.val)
    public static void printList(Node head) {
        Node curr = head;
        while (curr != null) {
            int randomVal = (curr.random != null) ? curr.random.val : -1;
            System.out.println("Node val: " + curr.val + ", Random points to: " + randomVal);
            curr = curr.next;
        }
    }

    public static void main(String[] args) {
        // Creating original list
        Node node1 = new Node(1);
        Node node2 = new Node(2);
        Node node3 = new Node(3);

        node1.next = node2;
        node2.next = node3;

        node1.random = node3; // 1 -> 3
        node2.random = node1; // 2 -> 1
        node3.random = null;  // 3 -> null

        System.out.println("Original list:");
        printList(node1);

        Node clonedHead = copyRandomList(node1);
        System.out.println("\nCloned list:");
        printList(clonedHead);
    }
}
```

---

### Method 2: Optimized without extra space (Interleaving nodes)

**Steps:**

1. For each node in the original list, create a new node and insert it **right after** the original node.
2. Assign random pointers for the cloned nodes: `clone.random = original.random.next`.
3. Separate the cloned list from the original list.

---

If you want, I can provide the code and explanation for the optimized method too!

---

## Time Complexity:

* O(N), where N is number of nodes.

## Space Complexity:

* O(N) for hashmap method.
* O(1) for optimized interleaving method.

---

## 35. Intersection point of two linked lists.

Finding the **intersection point of two singly linked lists** is a classic interview problem.

---

## Problem Statement:

Given two singly linked lists, determine if they intersect, and if yes, find the node at which they intersect. Intersection means the two lists share the **same node by reference**, not just by value.

---

### Example:

```
List A: 1 -> 3 -> 5
                   \
                    7 -> 9 -> null
                   /
List B:      2 -> 4
```

Intersection point is node with value `7`.

---

## Approach 1: Using Length Difference

1. Find the length of both lists.
2. Move the pointer of the longer list ahead by the length difference.
3. Traverse both lists in sync until the pointers are equal (intersection) or both reach null (no intersection).

---

## Approach 2: Two-pointer technique (Optimal)

* Initialize two pointers `p1` and `p2` at the heads of the two lists.
* Move both forward one node at a time.
* When `p1` reaches the end, redirect it to head of list 2.
* When `p2` reaches the end, redirect it to head of list 1.
* If the lists intersect, the pointers will meet at the intersection node after at most 2 passes.
* If not, both pointers will eventually be null.

---

## Java Code (Two-pointer technique):

```java
class ListNode {
    int val;
    ListNode next;
    ListNode(int val) { this.val = val; this.next = null; }
}

public class IntersectionPoint {

    public static ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        if (headA == null || headB == null) return null;

        ListNode p1 = headA;
        ListNode p2 = headB;

        // If they intersect, pointers will meet; else both null after second pass
        while (p1 != p2) {
            p1 = (p1 == null) ? headB : p1.next;
            p2 = (p2 == null) ? headA : p2.next;
        }

        return p1;  // Either intersection node or null
    }

    public static void main(String[] args) {
        // Creating nodes
        ListNode common = new ListNode(7);
        common.next = new ListNode(9);

        // List A: 1 -> 3 -> 5 -> 7 -> 9
        ListNode headA = new ListNode(1);
        headA.next = new ListNode(3);
        headA.next.next = new ListNode(5);
        headA.next.next.next = common;

        // List B: 2 -> 4 -> 7 -> 9
        ListNode headB = new ListNode(2);
        headB.next = new ListNode(4);
        headB.next.next = common;

        ListNode intersection = getIntersectionNode(headA, headB);
        if (intersection != null) {
            System.out.println("Intersection at node with value: " + intersection.val);
        } else {
            System.out.println("No intersection.");
        }
    }
}
```

---

## Explanation:

* When a pointer reaches the end of a list, it switches to the head of the other list.
* This equalizes the path length for both pointers.
* If there is an intersection, they will meet at the intersection node.
* If no intersection, both will become null.

---

## Time Complexity:

* O(N + M), where N and M are the lengths of the two lists.

## Space Complexity:

* O(1) — constant extra space.

---

### 🔹 **36–45: Stack & Queue**

## 36. Implement stack using queue (and vice versa).

Implementing one data structure using another is a classic exercise to test your understanding of fundamental data structures.

---

# 1. **Implement Stack using Queues**

---

## Problem:

Implement a **stack** (LIFO) using **queues** (FIFO).

---

### Approaches:

* Use **two queues** or
* Use **one queue** with a trick.

---

### Method 1: Using Two Queues

* Push operation: enqueue element in queue1.
* Pop operation: dequeue from queue1 except the last element, enqueue these dequeued elements to queue2; the last dequeued element is the popped element.
* Swap queue1 and queue2.

---

### Method 2: Using One Queue

* Push operation: enqueue element, then dequeue and enqueue all previous elements behind it to maintain LIFO order.

---

### Code for Stack using One Queue:

```java
import java.util.LinkedList;
import java.util.Queue;

public class StackUsingQueue {
    Queue<Integer> queue;

    public StackUsingQueue() {
        queue = new LinkedList<>();
    }

    // Push operation - O(n)
    public void push(int x) {
        queue.add(x);
        int size = queue.size();
        // Move all elements behind the newly added element
        for (int i = 0; i < size - 1; i++) {
            int val = queue.remove();
            queue.add(val);
        }
    }

    // Pop operation - O(1)
    public int pop() {
        if (queue.isEmpty()) throw new RuntimeException("Stack is empty");
        return queue.remove();
    }

    // Top operation - O(1)
    public int top() {
        if (queue.isEmpty()) throw new RuntimeException("Stack is empty");
        return queue.peek();
    }

    // Check if empty
    public boolean empty() {
        return queue.isEmpty();
    }

    public static void main(String[] args) {
        StackUsingQueue stack = new StackUsingQueue();

        stack.push(10);
        stack.push(20);
        stack.push(30);

        System.out.println(stack.top()); // 30
        System.out.println(stack.pop()); // 30
        System.out.println(stack.pop()); // 20
        System.out.println(stack.empty()); // false
    }
}
```

---

# 2. **Implement Queue using Stacks**

---

## Problem:

Implement a **queue** (FIFO) using **stacks** (LIFO).

---

### Approaches:

* Use **two stacks**:

    * `stackPush` for enqueue operation.
    * `stackPop` for dequeue operation.

---

### How it works:

* Enqueue: push element onto `stackPush`.
* Dequeue: if `stackPop` is empty, pop all elements from `stackPush` and push to `stackPop` (reverses order), then pop from `stackPop`.

---

### Code for Queue using Two Stacks:

```java
import java.util.Stack;

public class QueueUsingStacks {
    Stack<Integer> stackPush;
    Stack<Integer> stackPop;

    public QueueUsingStacks() {
        stackPush = new Stack<>();
        stackPop = new Stack<>();
    }

    // Enqueue - O(1)
    public void enqueue(int x) {
        stackPush.push(x);
    }

    // Dequeue - Amortized O(1)
    public int dequeue() {
        if (stackPop.isEmpty()) {
            while (!stackPush.isEmpty()) {
                stackPop.push(stackPush.pop());
            }
        }
        if (stackPop.isEmpty()) {
            throw new RuntimeException("Queue is empty");
        }
        return stackPop.pop();
    }

    // Peek front element
    public int peek() {
        if (stackPop.isEmpty()) {
            while (!stackPush.isEmpty()) {
                stackPop.push(stackPush.pop());
            }
        }
        if (stackPop.isEmpty()) {
            throw new RuntimeException("Queue is empty");
        }
        return stackPop.peek();
    }

    // Check if empty
    public boolean empty() {
        return stackPush.isEmpty() && stackPop.isEmpty();
    }

    public static void main(String[] args) {
        QueueUsingStacks queue = new QueueUsingStacks();

        queue.enqueue(10);
        queue.enqueue(20);
        queue.enqueue(30);

        System.out.println(queue.peek()); // 10
        System.out.println(queue.dequeue()); // 10
        System.out.println(queue.dequeue()); // 20
        System.out.println(queue.empty()); // false
    }
}
```

---

## Summary:

| Implement          | Data structure used   | Time Complexity (Push/Enqueue) | Time Complexity (Pop/Dequeue) |
| ------------------ | --------------------- | ------------------------------ | ----------------------------- |
| Stack using Queue  | Queue (1 or 2 queues) | O(n)                           | O(1)                          |
| Queue using Stacks | Stack (2 stacks)      | O(1)                           | Amortized O(1)                |

---

## 37. Valid parentheses.

The **Valid Parentheses** problem is a classic stack-related problem.

---

## Problem Statement:

Given a string containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['`, and `']'`, determine if the input string is **valid**.

A string is valid if:

* Open brackets are closed by the same type of brackets.
* Open brackets are closed in the correct order.

---

### Example:

| Input      | Output  |
| ---------- | ------- |
| `"()"`     | `true`  |
| `"()[]{}"` | `true`  |
| `"(]"`     | `false` |
| `"([)]"`   | `false` |
| `"{[]}"`   | `true`  |

---

## Approach:

* Use a **stack** to keep track of opening brackets.
* Traverse the string:

    * If the character is an opening bracket, push it onto the stack.
    * If it’s a closing bracket, check the top of the stack:

        * If the stack is empty or the top does not match the corresponding opening bracket, return false.
        * Otherwise, pop the stack.
* At the end, if the stack is empty, return true; else false.

---

## Java Code:

```java
import java.util.Stack;

public class ValidParentheses {

    public static boolean isValid(String s) {
        Stack<Character> stack = new Stack<>();

        for (char c : s.toCharArray()) {
            if (c == '(' || c == '{' || c == '[') {
                stack.push(c);
            } else {
                if (stack.isEmpty()) return false;

                char top = stack.pop();
                if (!matches(top, c)) {
                    return false;
                }
            }
        }

        return stack.isEmpty();
    }

    private static boolean matches(char open, char close) {
        return (open == '(' && close == ')') ||
               (open == '{' && close == '}') ||
               (open == '[' && close == ']');
    }

    public static void main(String[] args) {
        String[] tests = {"()", "()[]{}", "(]", "([)]", "{[]}"};

        for (String test : tests) {
            System.out.println(test + " : " + isValid(test));
        }
    }
}
```

---

## Explanation:

* Each time we encounter an opening bracket, we push it.
* For closing brackets, we check if the top of the stack matches.
* If not matched or stack empty, invalid.
* If stack empty after complete traversal, the string is valid.

---

## Time Complexity:

* O(N), N = length of string.

## Space Complexity:

* O(N) in worst case (all opening brackets).

---

Want me to cover **valid parentheses with other constraints** or **explain stack usage in more detail**?

---

## 38. Next greater element.

Great! The **Next Greater Element (NGE)** problem is a classic stack problem often asked in interviews.

---

## Problem Statement:

Given an array `nums`, for each element, find the **next greater element** to its right in the array. If there is no greater element, return `-1` for that element.

---

### Example:

Input: `[4, 5, 2, 25]`
Output: `[5, 25, 25, -1]`

Explanation:

* Next greater element for 4 is 5.
* Next greater element for 5 is 25.
* Next greater element for 2 is 25.
* Next greater element for 25 is -1 (no greater element).

---

## Approach: Using Stack (Efficient)

1. Use a stack to keep indices or elements for which we haven't found the next greater element yet.
2. Traverse the array from left to right.
3. For the current element:

    * While the stack is not empty and current element > element at top of the stack:

        * Pop from stack and assign current element as next greater for that popped element.
    * Push the current element (or its index) onto the stack.
4. After traversal, elements still in the stack have no next greater element → assign `-1` for them.

---

## Java Code:

```java
import java.util.Stack;
import java.util.Arrays;

public class NextGreaterElement {

    public static int[] nextGreaterElement(int[] nums) {
        int n = nums.length;
        int[] result = new int[n];
        Stack<Integer> stack = new Stack<>();

        for (int i = 0; i < n; i++) {
            // While current number is greater than stack's top element's number,
            // pop from stack and update result for that index.
            while (!stack.isEmpty() && nums[i] > nums[stack.peek()]) {
                int index = stack.pop();
                result[index] = nums[i];
            }
            stack.push(i);
        }

        // For remaining elements in stack, no next greater element found
        while (!stack.isEmpty()) {
            result[stack.pop()] = -1;
        }

        return result;
    }

    public static void main(String[] args) {
        int[] nums = {4, 5, 2, 25};
        int[] nge = nextGreaterElement(nums);
        System.out.println(Arrays.toString(nge));  // Output: [5, 25, 25, -1]
    }
}
```

---

## Explanation:

* Stack stores indices of elements waiting for next greater element.
* When a bigger number appears, it resolves next greater elements for smaller numbers in stack.
* Finally, unfulfilled elements get `-1`.

---

## Time Complexity:

* O(N) — Each element pushed and popped at most once.

## Space Complexity:

* O(N) — For the stack and output array.

---

## 39. Min stack (getMin in O(1)).

The **Min Stack** problem is a classic one where you design a stack that, in addition to `push` and `pop`, can return the **minimum element in O(1) time**.

---

## Problem Statement:

Implement a stack that supports the following operations **in constant time**:

* `push(x)` — push element x onto stack.
* `pop()` — remove the element on top of the stack.
* `top()` — get the top element.
* `getMin()` — retrieve the minimum element in the stack.

---

## Challenge:

How to maintain the minimum element efficiently?

---

## Approach 1: Using Two Stacks

* **Main stack:** stores all the elements.
* **Min stack:** stores the minimum element at each state.

**How?**

* When pushing, compare the new element with the current min (top of min stack).
* Push the new element on the main stack.
* Push the new element on the min stack if it's smaller or equal to the current min.
* When popping, pop from main stack.
* If popped element equals top of min stack, also pop from min stack.

---

## Java Code:

```java
import java.util.Stack;

public class MinStack {
    private Stack<Integer> stack;
    private Stack<Integer> minStack;

    public MinStack() {
        stack = new Stack<>();
        minStack = new Stack<>();
    }

    // Push element
    public void push(int x) {
        stack.push(x);
        if (minStack.isEmpty() || x <= minStack.peek()) {
            minStack.push(x);
        }
    }

    // Pop element
    public void pop() {
        if (stack.isEmpty()) throw new RuntimeException("Stack is empty");

        int popped = stack.pop();
        if (popped == minStack.peek()) {
            minStack.pop();
        }
    }

    // Top element
    public int top() {
        if (stack.isEmpty()) throw new RuntimeException("Stack is empty");
        return stack.peek();
    }

    // Get minimum element
    public int getMin() {
        if (minStack.isEmpty()) throw new RuntimeException("Stack is empty");
        return minStack.peek();
    }

    public static void main(String[] args) {
        MinStack minStack = new MinStack();

        minStack.push(5);
        minStack.push(3);
        minStack.push(7);
        minStack.push(3);

        System.out.println("Min: " + minStack.getMin()); // 3
        minStack.pop();
        System.out.println("Min: " + minStack.getMin()); // 3
        minStack.pop();
        System.out.println("Min: " + minStack.getMin()); // 3
        minStack.pop();
        System.out.println("Min: " + minStack.getMin()); // 5
    }
}
```

---

## Explanation:

* The `minStack` always keeps track of the minimum at the current stack state.
* When a smaller or equal element is pushed, it also goes to `minStack`.
* When popping, if the popped element is the current minimum, it is also popped from `minStack`.
* `getMin()` just returns the top of `minStack` → O(1).

---

## Time Complexity:

* All operations (`push`, `pop`, `top`, `getMin`) are **O(1)**.

## Space Complexity:

* O(N) for two stacks.

---

## 40. Evaluate postfix/infix expressions.

Evaluating **infix** and **postfix** expressions is a common and important problem involving stacks.

---

# 1. Evaluating **Postfix** Expression (Reverse Polish Notation)

---

## Problem:

Given a postfix expression (e.g., `"231*+9-"`), evaluate it.

### How Postfix works:

* Operands appear before operators.
* No need for parentheses.
* Example: `"231*+9-"` means:

    * Push 2, push 3, push 1
    * Pop 1 and 3 → multiply → 3 \* 1 = 3, push 3
    * Pop 3 and 2 → add → 2 + 3 = 5, push 5
    * Push 9
    * Pop 9 and 5 → subtract → 5 - 9 = -4

---

## Approach:

* Use a **stack**.
* Traverse tokens:

    * If token is operand, push it.
    * If token is operator, pop two operands, apply operator, push result.
* At end, top of stack is result.

---

## Java Code:

```java
import java.util.Stack;

public class PostfixEvaluation {

    public static int evaluatePostfix(String expr) {
        Stack<Integer> stack = new Stack<>();

        for (char c : expr.toCharArray()) {
            if (Character.isDigit(c)) {
                stack.push(c - '0');  // convert char to int
            } else {
                int b = stack.pop();
                int a = stack.pop();

                switch (c) {
                    case '+': stack.push(a + b); break;
                    case '-': stack.push(a - b); break;
                    case '*': stack.push(a * b); break;
                    case '/': stack.push(a / b); break;
                }
            }
        }
        return stack.pop();
    }

    public static void main(String[] args) {
        String expr = "231*+9-";
        System.out.println("Result: " + evaluatePostfix(expr));  // Output: -4
    }
}
```

---

# 2. Evaluating **Infix** Expression

---

## Problem:

Given an infix expression (e.g., `"2 + 3 * 1 - 9"`), evaluate it.

---

## Approach:

* Use **two stacks**: one for operands, one for operators.
* Rules:

    1. If token is number → push to operand stack.
    2. If token is operator:

        * While top of operator stack has higher or equal precedence, apply it.
        * Push current operator.
    3. If token is `(` → push to operator stack.
    4. If token is `)` → pop operators and apply until `(` is found.

---

## Java Code (Basic version supporting +, -, \*, / and parentheses):

```java
import java.util.Stack;

public class InfixEvaluation {

    public static int precedence(char op) {
        if (op == '+' || op == '-') return 1;
        if (op == '*' || op == '/') return 2;
        return 0;
    }

    public static int applyOp(int a, int b, char op) {
        switch(op) {
            case '+': return a + b;
            case '-': return a - b;
            case '*': return a * b;
            case '/': return a / b;
        }
        return 0;
    }

    public static int evaluateInfix(String expression) {
        Stack<Integer> values = new Stack<>();
        Stack<Character> ops = new Stack<>();

        for (int i = 0; i < expression.length(); i++) {
            char c = expression.charAt(i);

            if (Character.isWhitespace(c)) continue;

            if (Character.isDigit(c)) {
                int val = 0;
                // handle multi-digit numbers
                while (i < expression.length() && Character.isDigit(expression.charAt(i))) {
                    val = val * 10 + (expression.charAt(i) - '0');
                    i++;
                }
                i--; // adjust for the outer loop increment
                values.push(val);
            }
            else if (c == '(') {
                ops.push(c);
            }
            else if (c == ')') {
                while (ops.peek() != '(') {
                    int b = values.pop();
                    int a = values.pop();
                    char op = ops.pop();
                    values.push(applyOp(a, b, op));
                }
                ops.pop(); // remove '('
            }
            else { // operator
                while (!ops.isEmpty() && precedence(ops.peek()) >= precedence(c)) {
                    int b = values.pop();
                    int a = values.pop();
                    char op = ops.pop();
                    values.push(applyOp(a, b, op));
                }
                ops.push(c);
            }
        }

        while (!ops.isEmpty()) {
            int b = values.pop();
            int a = values.pop();
            char op = ops.pop();
            values.push(applyOp(a, b, op));
        }

        return values.pop();
    }

    public static void main(String[] args) {
        String expr = "2 + 3 * 1 - 9";
        System.out.println("Result: " + evaluateInfix(expr));  // Output: -4
    }
}
```

---

## Summary:

| Expression Type | Method                                  | Data Structure Used | Time Complexity |
| --------------- | --------------------------------------- | ------------------- | --------------- |
| Postfix         | Stack (push operands, pop for operator) | Single stack        | O(N)            |
| Infix           | Two stacks (operands & operators)       | Two stacks          | O(N)            |

---

## 41. Sliding window maximum.

Sliding Window Maximum is a classic and important problem for arrays that’s often asked in interviews.

---

## Problem Statement:

Given an array `nums` and a sliding window size `k`, find the maximum value in each sliding window as it moves from the beginning to the end of the array.

---

### Example:

Input:
`nums = [1,3,-1,-3,5,3,6,7]`, `k = 3`

Output:
`[3,3,5,5,6,7]`

Explanation:
Windows and their maximums are:

* `[1, 3, -1]` → 3
* `[3, -1, -3]` → 3
* `[-1, -3, 5]` → 5
* `[-3, 5, 3]` → 5
* `[5, 3, 6]` → 6
* `[3, 6, 7]` → 7

---

## Approach: Using Deque (Double-ended Queue)

* We want to keep track of useful elements (potential maximum candidates) in the current window.
* Use a deque to store **indices** of elements in decreasing order of their values.
* The front of the deque always contains the index of the maximum element for the current window.
* Steps:

    1. Remove indices which are out of this window's range (`i - k`).
    2. Remove all indices from the back whose corresponding values are less than the current element (they cannot be maximum if current is bigger).
    3. Add current element’s index to the back.
    4. The front of deque gives max for current window after `i >= k - 1`.

---

## Java Code:

```java
import java.util.*;

public class SlidingWindowMaximum {

    public static int[] maxSlidingWindow(int[] nums, int k) {
        if (nums == null || k <= 0) return new int[0];

        int n = nums.length;
        int[] result = new int[n - k + 1];
        Deque<Integer> deque = new LinkedList<>();

        for (int i = 0; i < n; i++) {
            // Remove indices out of window
            while (!deque.isEmpty() && deque.peekFirst() < i - k + 1) {
                deque.pollFirst();
            }

            // Remove smaller values from back
            while (!deque.isEmpty() && nums[deque.peekLast()] < nums[i]) {
                deque.pollLast();
            }

            // Add current index
            deque.offerLast(i);

            // Start recording max when first window is completed
            if (i >= k - 1) {
                result[i - k + 1] = nums[deque.peekFirst()];
            }
        }

        return result;
    }

    public static void main(String[] args) {
        int[] nums = {1,3,-1,-3,5,3,6,7};
        int k = 3;
        int[] maxWindows = maxSlidingWindow(nums, k);

        System.out.println(Arrays.toString(maxWindows));  // Output: [3, 3, 5, 5, 6, 7]
    }
}
```

---

## Explanation:

* The deque stores indices of elements in descending order of values.
* The maximum element in the current window is always at the front of the deque.
* Elements smaller than the current one are removed from the back because they can’t be maximum if current is bigger.

---

## Time Complexity:

* O(N), because each element is pushed and popped from deque at most once.

## Space Complexity:

* O(k), for the deque storing indices in a window.

---

## 42. Design a circular queue.

Designing a **circular queue** is a classic data structure problem often asked in interviews. It helps efficiently use fixed-size storage by treating the queue like a circle, wrapping around when it reaches the end.

---

## What is a Circular Queue?

A **circular queue** is a linear data structure that follows FIFO (First In First Out) but connects the end back to the front, forming a circle. This allows efficient use of space, especially when implementing with an array.

---

## Why Circular?

* In a normal queue implemented with an array, after some dequeue operations, front index moves ahead, and even if there is free space at the beginning, you can't enqueue new elements without shifting.
* Circular queue overcomes this by wrapping indices to the beginning once you reach the end.

---

## Core Operations:

* `enqueue(x)` — add element to the rear.
* `dequeue()` — remove element from the front.
* `front()` — get front element.
* `rear()` — get rear element.
* `isEmpty()` — check if queue is empty.
* `isFull()` — check if queue is full.

---

## Implementation details:

* Use an array `arr` of fixed size `capacity`.
* Maintain two pointers:

    * `front` — points to the current front element.
    * `rear` — points to the last element.
* Both initialized as `-1` indicating empty queue.
* Use modulo `% capacity` to wrap around.

---

## Java Code:

```java
public class CircularQueue {
    private int[] arr;
    private int front;
    private int rear;
    private int capacity;
    private int size;

    public CircularQueue(int capacity) {
        this.capacity = capacity;
        arr = new int[capacity];
        front = -1;
        rear = -1;
        size = 0;
    }

    public boolean isEmpty() {
        return size == 0;
    }

    public boolean isFull() {
        return size == capacity;
    }

    public boolean enqueue(int value) {
        if (isFull()) {
            System.out.println("Queue is full. Cannot enqueue " + value);
            return false;
        }

        if (isEmpty()) {
            front = 0;
        }
        rear = (rear + 1) % capacity;
        arr[rear] = value;
        size++;
        return true;
    }

    public int dequeue() {
        if (isEmpty()) {
            System.out.println("Queue is empty. Cannot dequeue.");
            return -1; // or throw exception
        }

        int result = arr[front];
        front = (front + 1) % capacity;
        size--;

        // Reset pointers if queue is empty after dequeue
        if (size == 0) {
            front = -1;
            rear = -1;
        }

        return result;
    }

    public int getFront() {
        if (isEmpty()) {
            System.out.println("Queue is empty.");
            return -1;
        }
        return arr[front];
    }

    public int getRear() {
        if (isEmpty()) {
            System.out.println("Queue is empty.");
            return -1;
        }
        return arr[rear];
    }

    // For debugging: print queue elements in order
    public void printQueue() {
        if (isEmpty()) {
            System.out.println("Queue is empty.");
            return;
        }

        System.out.print("Queue elements: ");
        for (int i = 0; i < size; i++) {
            int index = (front + i) % capacity;
            System.out.print(arr[index] + " ");
        }
        System.out.println();
    }

    public static void main(String[] args) {
        CircularQueue queue = new CircularQueue(5);

        queue.enqueue(10);
        queue.enqueue(20);
        queue.enqueue(30);
        queue.enqueue(40);

        queue.printQueue(); // 10 20 30 40

        System.out.println("Dequeued: " + queue.dequeue()); // 10
        queue.printQueue(); // 20 30 40

        queue.enqueue(50);
        queue.enqueue(60);
        queue.printQueue(); // 20 30 40 50 60

        System.out.println("Is full? " + queue.isFull()); // true

        System.out.println("Rear element: " + queue.getRear()); // 60
        System.out.println("Front element: " + queue.getFront()); // 20

        // Try enqueue when full
        queue.enqueue(70); // Queue is full

        // Dequeue all elements
        while (!queue.isEmpty()) {
            System.out.println("Dequeued: " + queue.dequeue());
        }
        queue.printQueue(); // Queue is empty
    }
}
```

---

## Explanation:

* `front` and `rear` track positions of the first and last elements.
* When enqueueing, we increment `rear` modulo capacity to wrap around.
* When dequeuing, increment `front` modulo capacity.
* Size helps track whether queue is empty or full to distinguish between those cases.

---

## Time Complexity:

* All operations: **O(1)**

---

## 43. Implement LRU Cache.

Implementing an **LRU (Least Recently Used) Cache** is a very popular interview question combining hashing and doubly linked lists for O(1) operations.

---

## Problem:

Design a data structure that supports these operations in **O(1)** time:

* `get(key)`: Return the value of the key if it exists, else return -1.
* `put(key, value)`: Insert or update the value of the key. If the cache is full, remove the least recently used item before inserting.

---

## Core Idea:

* Use a **HashMap** to achieve O(1) access to cache entries by key.
* Use a **Doubly Linked List** to maintain usage order (most recently used at the front, least at the back).
* On access or insertion, move the node to the front.
* When capacity is reached, remove the tail (least recently used).

---

## Step-by-step:

1. **HashMap** maps key → Node (which contains key, value, prev, next).
2. **Doubly Linked List** maintains usage order.
3. When `get`:

    * If key exists, move node to front, return value.
    * Else return -1.
4. When `put`:

    * If key exists, update value, move node to front.
    * Else add new node at front.
    * If capacity exceeded, remove node at tail.

---

## Java Code:

```java
import java.util.HashMap;

public class LRUCache {

    class Node {
        int key, value;
        Node prev, next;

        Node(int k, int v) {
            key = k;
            value = v;
        }
    }

    private int capacity;
    private HashMap<Integer, Node> map;
    private Node head, tail;

    public LRUCache(int capacity) {
        this.capacity = capacity;
        map = new HashMap<>();

        head = new Node(0, 0); // dummy head
        tail = new Node(0, 0); // dummy tail

        head.next = tail;
        tail.prev = head;
    }

    public int get(int key) {
        if (!map.containsKey(key)) return -1;

        Node node = map.get(key);
        remove(node);
        insertAtFront(node);
        return node.value;
    }

    public void put(int key, int value) {
        if (map.containsKey(key)) {
            Node node = map.get(key);
            node.value = value;
            remove(node);
            insertAtFront(node);
        } else {
            if (map.size() == capacity) {
                Node lru = tail.prev;
                remove(lru);
                map.remove(lru.key);
            }
            Node newNode = new Node(key, value);
            insertAtFront(newNode);
            map.put(key, newNode);
        }
    }

    private void remove(Node node) {
        node.prev.next = node.next;
        node.next.prev = node.prev;
    }

    private void insertAtFront(Node node) {
        node.next = head.next;
        node.prev = head;

        head.next.prev = node;
        head.next = node;
    }

    public static void main(String[] args) {
        LRUCache cache = new LRUCache(2);

        cache.put(1, 1);
        cache.put(2, 2);
        System.out.println(cache.get(1)); // returns 1

        cache.put(3, 3); // evicts key 2
        System.out.println(cache.get(2)); // returns -1 (not found)

        cache.put(4, 4); // evicts key 1
        System.out.println(cache.get(1)); // returns -1 (not found)
        System.out.println(cache.get(3)); // returns 3
        System.out.println(cache.get(4)); // returns 4
    }
}
```

---

## Explanation:

* Dummy head and tail simplify insert/delete logic.
* `remove(node)` disconnects node from list.
* `insertAtFront(node)` adds node right after head.
* The map ensures O(1) access to nodes.
* The doubly linked list maintains order of usage.

---

## Time Complexity:

* `get` and `put`: **O(1)**

---

## 44. Largest rectangle in a histogram.

The **Largest Rectangle in Histogram** is a classic and challenging problem often asked in technical interviews. It requires understanding of stacks and how to efficiently compute areas in a histogram.

---

## Problem Statement:

Given an array representing the heights of bars in a histogram, find the area of the largest rectangle that can be formed within the histogram.

---

### Example:

Input:
`heights = [2, 1, 5, 6, 2, 3]`

Output:
`10`

Explanation:
The largest rectangle is formed by bars with heights 5 and 6 (width 2), so area = 5 \* 2 = 10.

---

## Intuition:

* For each bar, we want to find how far it can extend to the left and right without encountering a bar shorter than itself.
* Using a **stack** helps efficiently find these bounds.

---

## Approach (Using Stack):

1. Use a stack to store indices of bars in ascending height order.
2. Iterate over the bars:

    * While current bar’s height is less than the bar at stack’s top, pop from stack and calculate area for popped bar as the smallest bar.
    * The width for this popped bar is:

        * If stack is empty after popping, width = current index
        * Else width = current index - index at new stack top - 1
3. Push current bar’s index to the stack.
4. After processing all bars, pop remaining bars from stack and calculate area similarly.

---

## Java Code:

```java
import java.util.Stack;

public class LargestRectangleHistogram {
    public static int largestRectangleArea(int[] heights) {
        Stack<Integer> stack = new Stack<>();
        int maxArea = 0;
        int n = heights.length;

        for (int i = 0; i <= n; i++) {
            // Use 0 height for last iteration to clear stack
            int currentHeight = (i == n) ? 0 : heights[i];

            while (!stack.isEmpty() && currentHeight < heights[stack.peek()]) {
                int height = heights[stack.pop()];
                int width;
                if (stack.isEmpty()) {
                    width = i;
                } else {
                    width = i - stack.peek() - 1;
                }
                int area = height * width;
                maxArea = Math.max(maxArea, area);
            }
            stack.push(i);
        }

        return maxArea;
    }

    public static void main(String[] args) {
        int[] histogram = {2, 1, 5, 6, 2, 3};
        System.out.println("Largest Rectangle Area: " + largestRectangleArea(histogram)); // Output: 10
    }
}
```

---

## Explanation:

* The stack stores indices of bars with increasing heights.
* When a lower height bar is found, it means the bars in stack can’t extend beyond this point.
* We pop bars from stack and calculate area with the popped bar as the smallest height.
* The width is calculated using current index and new top of stack.

---

## Time Complexity:

* O(N), because each element is pushed and popped at most once.

## Space Complexity:

* O(N), for the stack.

---

## 45. Daily Temperatures problem.

The **Daily Temperatures** problem is a classic stack-based problem related to finding the next greater element to the right.

---

## Problem Statement:

Given an array `temperatures` representing daily temperatures, return an array `answer` such that for each day in the input, `answer[i]` is the number of days you have to wait until a warmer temperature. If there is no future day for which this is possible, put `0` instead.

---

### Example:

Input:
`temperatures = [73, 74, 75, 71, 69, 72, 76, 73]`

Output:
`[1, 1, 4, 2, 1, 1, 0, 0]`

Explanation:

* On day 0 (73°F), next warmer day is day 1 (74°F), so answer\[0] = 1.
* On day 1 (74°F), next warmer day is day 2 (75°F), so answer\[1] = 1.
* On day 2 (75°F), next warmer day is day 6 (76°F), so answer\[2] = 4.
* Days 6 and 7 have no warmer future days, so answer is 0.

---

## Approach: Using Stack

* Use a stack to keep indices of days with unresolved temperatures.
* Iterate through the array:

    * While the stack is not empty **and** current temperature is warmer than temperature at stack's top index:

        * Pop the index from stack.
        * Calculate the difference in indices and store in answer for that popped day.
    * Push current index onto stack.
* Remaining indices in stack have no warmer future days, so their answer is 0.

---

## Java Code:

```java
import java.util.Arrays;
import java.util.Stack;

public class DailyTemperatures {

    public static int[] dailyTemperatures(int[] temperatures) {
        int n = temperatures.length;
        int[] answer = new int[n];
        Stack<Integer> stack = new Stack<>(); // store indices

        for (int i = 0; i < n; i++) {
            while (!stack.isEmpty() && temperatures[i] > temperatures[stack.peek()]) {
                int prevIndex = stack.pop();
                answer[prevIndex] = i - prevIndex;
            }
            stack.push(i);
        }

        // Remaining indices in stack have 0 in answer by default
        return answer;
    }

    public static void main(String[] args) {
        int[] temps = {73, 74, 75, 71, 69, 72, 76, 73};
        System.out.println(Arrays.toString(dailyTemperatures(temps))); // [1, 1, 4, 2, 1, 1, 0, 0]
    }
}
```

---

## Explanation:

* Stack stores indices of days where we have not yet found a warmer day.
* When we find a warmer temperature, we update answer for all colder days in stack that this warmer day satisfies.
* Indices left in stack mean no warmer day exists ahead.

---

## Time Complexity:

* O(N), each index is pushed and popped at most once.

## Space Complexity:

* O(N), for the stack and output array.

---

### 🔹 **46–60: Trees & Binary Search Tree (BST)**

## 46. Inorder, Preorder, Postorder Traversal (recursive & iterative).

Tree traversals are fundamental in understanding binary trees, and knowing both recursive and iterative methods is important for interviews.

---

# Binary Tree Traversals:

Given a binary tree, the three common types of depth-first traversals are:

| Traversal Type | Visit Order                         |
| -------------- | ----------------------------------- |
| **Inorder**    | Left subtree → Node → Right subtree |
| **Preorder**   | Node → Left subtree → Right subtree |
| **Postorder**  | Left subtree → Right subtree → Node |

---

## 1. Recursive Traversals

### (a) Inorder (Left, Root, Right)

```java
void inorder(TreeNode root) {
    if (root == null) return;
    inorder(root.left);
    System.out.print(root.val + " ");
    inorder(root.right);
}
```

### (b) Preorder (Root, Left, Right)

```java
void preorder(TreeNode root) {
    if (root == null) return;
    System.out.print(root.val + " ");
    preorder(root.left);
    preorder(root.right);
}
```

### (c) Postorder (Left, Right, Root)

```java
void postorder(TreeNode root) {
    if (root == null) return;
    postorder(root.left);
    postorder(root.right);
    System.out.print(root.val + " ");
}
```

---

## 2. Iterative Traversals

---

### (a) Iterative Inorder Traversal

* Use a stack.
* Push all left children until null.
* Pop from stack, process node, then move to right child.

```java
import java.util.*;

void inorderIterative(TreeNode root) {
    Stack<TreeNode> stack = new Stack<>();
    TreeNode curr = root;

    while (curr != null || !stack.isEmpty()) {
        while (curr != null) {
            stack.push(curr);
            curr = curr.left;
        }
        curr = stack.pop();
        System.out.print(curr.val + " ");
        curr = curr.right;
    }
}
```

---

### (b) Iterative Preorder Traversal

* Use a stack.
* Process node, push right child first, then left child.

```java
void preorderIterative(TreeNode root) {
    if (root == null) return;

    Stack<TreeNode> stack = new Stack<>();
    stack.push(root);

    while (!stack.isEmpty()) {
        TreeNode curr = stack.pop();
        System.out.print(curr.val + " ");

        if (curr.right != null) stack.push(curr.right);
        if (curr.left != null) stack.push(curr.left);
    }
}
```

---

### (c) Iterative Postorder Traversal

* More tricky.
* One common approach uses two stacks or a single stack with a pointer to track processed nodes.

#### Using two stacks:

```java
void postorderIterative(TreeNode root) {
    if (root == null) return;

    Stack<TreeNode> stack1 = new Stack<>();
    Stack<TreeNode> stack2 = new Stack<>();

    stack1.push(root);

    while (!stack1.isEmpty()) {
        TreeNode curr = stack1.pop();
        stack2.push(curr);

        if (curr.left != null) stack1.push(curr.left);
        if (curr.right != null) stack1.push(curr.right);
    }

    while (!stack2.isEmpty()) {
        System.out.print(stack2.pop().val + " ");
    }
}
```

---

## Summary Table:

| Traversal | Recursive             | Iterative                           |
| --------- | --------------------- | ----------------------------------- |
| Inorder   | `left → root → right` | Stack with left pushes              |
| Preorder  | `root → left → right` | Stack with right then left          |
| Postorder | `left → right → root` | Two stacks or modified single stack |

---

## TreeNode class (for reference)

```java
class TreeNode {
    int val;
    TreeNode left, right;

    TreeNode(int val) {
        this.val = val;
    }
}
```

---

## 47. Level-order traversal (BFS).

**Level-order traversal** of a binary tree is also known as **Breadth-First Search (BFS)** on trees. It visits nodes level by level from left to right.

---

## Problem:

Traverse the tree level by level and print or return nodes at each level.

---

## Approach:

* Use a **Queue** to keep track of nodes at the current level.
* Start by adding the root to the queue.
* While the queue is not empty:

    * Remove the front node.
    * Process the node (e.g., print or add to result).
    * Add the node’s left and right children to the queue (if they exist).
* This naturally processes nodes level-by-level.

---

## Java Code (Level-order Traversal):

```java
import java.util.*;

public class LevelOrderTraversal {

    static class TreeNode {
        int val;
        TreeNode left, right;

        TreeNode(int val) { this.val = val; }
    }

    public static List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> result = new ArrayList<>();
        if (root == null) return result;

        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);

        while (!queue.isEmpty()) {
            int levelSize = queue.size(); // Number of nodes at current level
            List<Integer> currentLevel = new ArrayList<>();

            for (int i = 0; i < levelSize; i++) {
                TreeNode node = queue.poll();
                currentLevel.add(node.val);

                if (node.left != null) queue.offer(node.left);
                if (node.right != null) queue.offer(node.right);
            }

            result.add(currentLevel);
        }

        return result;
    }

    public static void main(String[] args) {
        // Construct binary tree
        /*
              1
             / \
            2   3
           / \   \
          4   5   6
        */
        TreeNode root = new TreeNode(1);
        root.left = new TreeNode(2);
        root.right = new TreeNode(3);
        root.left.left = new TreeNode(4);
        root.left.right = new TreeNode(5);
        root.right.right = new TreeNode(6);

        List<List<Integer>> levels = levelOrder(root);
        System.out.println(levels);
        // Output: [[1], [2, 3], [4, 5, 6]]
    }
}
```

---

## Explanation:

* We use a queue to keep track of nodes.
* `levelSize` lets us separate nodes level-by-level.
* For each level, we process exactly `levelSize` nodes.
* Add their children to the queue for the next level.

---

## Time Complexity:

* O(N), where N is the number of nodes, as each node is visited once.

## Space Complexity:

* O(N), for the queue and output list in the worst case (last level).

---

## 48. Height of a binary tree.

Finding the **height of a binary tree** is a fundamental tree problem.

---

## Definition:

* The **height** of a binary tree is the number of edges on the longest path from the root node down to the farthest leaf node.

* Sometimes it is defined as the number of nodes on the longest path from the root to a leaf, in which case height = edges + 1.

* Here, we'll consider **height as the number of edges**.

* If the tree is empty, height = -1 (no edges).

* A single node tree (only root) has height = 0.

---

## Approach:

* Recursively compute the height of left and right subtrees.
* Height of the tree = `1 + max(height of left subtree, height of right subtree)`

---

## Java Code (Recursive):

```java
class TreeNode {
    int val;
    TreeNode left, right;

    TreeNode(int val) {
        this.val = val;
    }
}

public class BinaryTreeHeight {

    public static int height(TreeNode root) {
        if (root == null) {
            return -1; // no edges in empty tree
        }

        int leftHeight = height(root.left);
        int rightHeight = height(root.right);

        return 1 + Math.max(leftHeight, rightHeight);
    }

    public static void main(String[] args) {
        // Example tree:
        /*
              1
             / \
            2   3
           / 
          4
        */

        TreeNode root = new TreeNode(1);
        root.left = new TreeNode(2);
        root.right = new TreeNode(3);
        root.left.left = new TreeNode(4);

        System.out.println("Height of tree: " + height(root)); // Output: 2
    }
}
```

---

## Explanation:

* Base case: height of null node = -1.
* For each node, find height of left and right subtree recursively.
* Return 1 + max(leftHeight, rightHeight).
* The height is measured in edges, so a leaf node’s children are null with height -1, so leaf node height is 0.

---

## Time Complexity:

* O(N), visits every node once.

## Space Complexity:

* O(H), H = height of tree (recursive call stack).

---

## 49. Validate a binary search tree.

Validating a **Binary Search Tree (BST)** is a common interview question.

---

## Problem:

Given the root of a binary tree, determine if it is a valid BST.

---

## BST Property:

* For every node:

    * All nodes in its left subtree are **less** than the node’s value.
    * All nodes in its right subtree are **greater** than the node’s value.
* This must hold **recursively** for every subtree.

---

## Approach 1: Recursion with min/max bounds

* Keep track of allowed value range for each node.
* Initially, root can have any value (`-∞` to `+∞`).
* For left child, upper bound is parent node's value.
* For right child, lower bound is parent node's value.
* If a node violates the bound, return false.

---

## Java Code:

```java
class TreeNode {
    int val;
    TreeNode left, right;

    TreeNode(int val) { this.val = val; }
}

public class ValidateBST {

    public static boolean isValidBST(TreeNode root) {
        return helper(root, null, null);
    }

    private static boolean helper(TreeNode node, Integer lower, Integer upper) {
        if (node == null) return true;

        int val = node.val;

        if (lower != null && val <= lower) return false;
        if (upper != null && val >= upper) return false;

        // Left subtree must be < val
        if (!helper(node.left, lower, val)) return false;
        // Right subtree must be > val
        if (!helper(node.right, val, upper)) return false;

        return true;
    }

    public static void main(String[] args) {
        /*
              5
             / \
            1   7
        */
        TreeNode root = new TreeNode(5);
        root.left = new TreeNode(1);
        root.right = new TreeNode(7);

        System.out.println(isValidBST(root));  // true

        // Invalid BST
        root.right.left = new TreeNode(4);
        System.out.println(isValidBST(root));  // false
    }
}
```

---

## Explanation:

* `lower` and `upper` keep track of value constraints for nodes.
* If a node's value does not lie within `(lower, upper)` range, return false.
* Recursively check left and right subtrees with updated bounds.

---

## Approach 2: Inorder traversal

* Inorder traversal of a BST gives a sorted sequence.
* Traverse inorder and check if current node's value is **greater** than previous node’s value.
* If not, it's not a BST.

---

## 50. Lowest Common Ancestor (LCA) in a BST.

Finding the **Lowest Common Ancestor (LCA)** in a Binary Search Tree (BST) is a classic problem.

---

## Problem:

Given a BST and two nodes `p` and `q`, find their lowest common ancestor (LCA).

**LCA** is the lowest (deepest) node in the tree that has both `p` and `q` as descendants (where we allow a node to be a descendant of itself).

---

## Why BST helps?

* BST property: Left subtree nodes < node < Right subtree nodes.
* So if both `p` and `q` are less than current node, LCA lies in left subtree.
* If both are greater, LCA lies in right subtree.
* Otherwise, current node is the LCA.

---

## Approach (Iterative / Recursive):

* Start at root.
* If both `p.val` and `q.val` are smaller than root’s val, go left.
* If both are greater, go right.
* Else, root is LCA.

---

## Java Code (Recursive):

```java
class TreeNode {
    int val;
    TreeNode left, right;

    TreeNode(int val) { this.val = val; }
}

public class LCABST {

    public static TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root == null) return null;

        if (p.val < root.val && q.val < root.val) {
            return lowestCommonAncestor(root.left, p, q);
        } else if (p.val > root.val && q.val > root.val) {
            return lowestCommonAncestor(root.right, p, q);
        } else {
            return root;  // This is the split point and hence LCA
        }
    }

    public static void main(String[] args) {
        /*
               6
              / \
             2   8
            / \ / \
           0  4 7  9
             / \
            3   5
        */
        TreeNode root = new TreeNode(6);
        root.left = new TreeNode(2);
        root.right = new TreeNode(8);
        root.left.left = new TreeNode(0);
        root.left.right = new TreeNode(4);
        root.left.right.left = new TreeNode(3);
        root.left.right.right = new TreeNode(5);
        root.right.left = new TreeNode(7);
        root.right.right = new TreeNode(9);

        TreeNode p = root.left;       // Node 2
        TreeNode q = root.left.right; // Node 4

        TreeNode lca = lowestCommonAncestor(root, p, q);
        System.out.println("LCA: " + lca.val);  // Output: 2
    }
}
```

---

## Explanation:

* When both `p` and `q` are on the same side (left/right), we go down that subtree.
* When they split, current node is the LCA.

---

## Time Complexity:

* O(H), where H is height of the BST.
tive version or LCA in a normal binary tree (not BST)?

---

## 51. Convert sorted array to BST.

Converting a **sorted array** into a **height-balanced Binary Search Tree (BST)** is a classic problem.

---

## Problem:

Given a sorted (ascending) array, convert it to a height-balanced BST, meaning the depth of the two subtrees of every node never differs by more than 1.

---

## Intuition:

* The middle element of the array becomes the root (to balance left and right).
* Recursively apply this to the left half for left subtree.
* Recursively apply this to the right half for right subtree.

---

## Approach (Divide & Conquer):

1. Find middle element index `mid = (start + end) / 2`.
2. Create a new node with `arr[mid]`.
3. Recursively do the same for subarray `start` to `mid - 1` for left subtree.
4. Recursively do the same for subarray `mid + 1` to `end` for right subtree.
5. Return the node.

---

## Java Code:

```java
class TreeNode {
    int val;
    TreeNode left, right;

    TreeNode(int val) { this.val = val; }
}

public class SortedArrayToBST {

    public static TreeNode sortedArrayToBST(int[] nums) {
        if (nums == null || nums.length == 0) return null;
        return helper(nums, 0, nums.length - 1);
    }

    private static TreeNode helper(int[] nums, int start, int end) {
        if (start > end) return null;

        int mid = start + (end - start) / 2;
        TreeNode node = new TreeNode(nums[mid]);

        node.left = helper(nums, start, mid - 1);
        node.right = helper(nums, mid + 1, end);

        return node;
    }

    // Utility to print inorder traversal (for verification)
    public static void inorder(TreeNode root) {
        if (root == null) return;
        inorder(root.left);
        System.out.print(root.val + " ");
        inorder(root.right);
    }

    public static void main(String[] args) {
        int[] sortedArr = {-10, -3, 0, 5, 9};
        TreeNode root = sortedArrayToBST(sortedArr);

        System.out.print("Inorder traversal of constructed BST: ");
        inorder(root);
        // Output: -10 -3 0 5 9
    }
}
```

---

## Explanation:

* We pick the middle element as root to keep tree balanced.
* Left subarray builds left subtree; right subarray builds right subtree.
* Inorder traversal of this BST will give back the original sorted array.

---

## Time Complexity:

* O(N), where N is number of elements (each element is processed once).

## Space Complexity:

* O(log N) due to recursion stack for balanced tree.

---

## 52. Check if two trees are identical.

Checking if two binary trees are **identical** means verifying that they have the same structure and node values.

---

## Problem:

Given two binary trees, determine if they are exactly the same (both structure and values).

---

## Approach (Recursion):

* If both nodes are `null`, they are identical (base case).
* If one is `null` and the other isn't, trees differ.
* If both nodes are non-null, check:

    * Current node values are equal.
    * Left subtrees are identical.
    * Right subtrees are identical.

---

## Java Code:

```java
class TreeNode {
    int val;
    TreeNode left, right;

    TreeNode(int val) { this.val = val; }
}

public class IdenticalTrees {

    public static boolean isIdentical(TreeNode root1, TreeNode root2) {
        if (root1 == null && root2 == null) return true;

        if (root1 == null || root2 == null) return false;

        if (root1.val != root2.val) return false;

        return isIdentical(root1.left, root2.left) && isIdentical(root1.right, root2.right);
    }

    public static void main(String[] args) {
        TreeNode tree1 = new TreeNode(1);
        tree1.left = new TreeNode(2);
        tree1.right = new TreeNode(3);

        TreeNode tree2 = new TreeNode(1);
        tree2.left = new TreeNode(2);
        tree2.right = new TreeNode(3);

        System.out.println(isIdentical(tree1, tree2));  // Output: true

        tree2.right.val = 4;

        System.out.println(isIdentical(tree1, tree2));  // Output: false
    }
}
```

---

## Explanation:

* Both trees are traversed simultaneously.
* If any mismatch in values or structure occurs, return false.
* If all nodes match, return true.

---

## Time Complexity:

* O(min(N, M)) where N and M are nodes in the two trees (because both trees are traversed).

---

## 53. Symmetric tree.

Checking if a **binary tree is symmetric** is another common and important problem, especially in interviews.

---

## Problem:

Given the root of a binary tree, check whether it is a **mirror of itself** (i.e., symmetric around its center).

---

## Symmetric Tree – Definition:

A tree is symmetric if the left subtree is a **mirror reflection** of the right subtree.

---

## Visual Example:

```
    1
   / \
  2   2
 / \ / \
3  4 4  3   ← Symmetric

But this is not:

    1
   / \
  2   2
   \   \
   3    3   ← Not symmetric
```

---

## Approach: Recursive Mirror Check

Write a helper function `isMirror(TreeNode t1, TreeNode t2)` that checks:

* Both nodes are null → symmetric
* Only one is null → not symmetric
* Values match, and:

    * `t1.left` is a mirror of `t2.right`
    * `t1.right` is a mirror of `t2.left`

---

## Java Code:

```java
class TreeNode {
    int val;
    TreeNode left, right;

    TreeNode(int val) { this.val = val; }
}

public class SymmetricTree {

    public static boolean isSymmetric(TreeNode root) {
        if (root == null) return true;
        return isMirror(root.left, root.right);
    }

    private static boolean isMirror(TreeNode t1, TreeNode t2) {
        if (t1 == null && t2 == null) return true;
        if (t1 == null || t2 == null) return false;

        return (t1.val == t2.val)
            && isMirror(t1.left, t2.right)
            && isMirror(t1.right, t2.left);
    }

    public static void main(String[] args) {
        // Symmetric tree
        TreeNode root = new TreeNode(1);
        root.left = new TreeNode(2);
        root.right = new TreeNode(2);
        root.left.left = new TreeNode(3);
        root.left.right = new TreeNode(4);
        root.right.left = new TreeNode(4);
        root.right.right = new TreeNode(3);

        System.out.println("Is symmetric: " + isSymmetric(root)); // true
    }
}
```

---

## Time Complexity:

* O(N), where N = number of nodes in the tree.

## Space Complexity:

* O(H), where H = height of the tree (for recursion stack).

---

## 54. Diameter of a binary tree.

The **Diameter of a Binary Tree** is a very popular and frequently asked tree problem in coding interviews.

---

## 🔍 Problem:

Given the root of a binary tree, return the **diameter** of the tree.

**Diameter** is the length of the longest path between any two nodes in the tree. This path **may or may not** pass through the root.

> **Note**: Length is counted as the **number of edges** between the two nodes.

---

## 💡 Intuition:

The longest path between two nodes might:

* Pass through the current root (left height + right height).
* Be entirely in the left subtree.
* Be entirely in the right subtree.

We want the **maximum** of all these paths.

---

## ✅ Approach:

Use **post-order traversal** (DFS):

1. Recursively calculate the height of left and right subtrees.
2. Update the diameter as `leftHeight + rightHeight`.
3. Return height as `1 + max(leftHeight, rightHeight)`.

---

## ✅ Java Code:

```java
class TreeNode {
    int val;
    TreeNode left, right;
    TreeNode(int val) { this.val = val; }
}

public class DiameterOfBinaryTree {
    static int diameter = 0;

    public static int diameterOfBinaryTree(TreeNode root) {
        diameter = 0;
        height(root);
        return diameter;
    }

    private static int height(TreeNode node) {
        if (node == null) return 0;

        int left = height(node.left);
        int right = height(node.right);

        // Update diameter at this node
        diameter = Math.max(diameter, left + right);

        // Return height to parent
        return 1 + Math.max(left, right);
    }

    public static void main(String[] args) {
        /*
               1
              / \
             2   3
            / \
           4   5
        */
        TreeNode root = new TreeNode(1);
        root.left = new TreeNode(2);
        root.right = new TreeNode(3);
        root.left.left = new TreeNode(4);
        root.left.right = new TreeNode(5);

        System.out.println("Diameter: " + diameterOfBinaryTree(root)); // Output: 3 (Path: 4 → 2 → 5 or 4 → 2 → 1 → 3)
    }
}
```

---

## 🧠 Explanation:

* At node 2: left = 1 (from 4), right = 1 (from 5) → diameter = 2
* At node 1: left = 2 (from 2), right = 1 (from 3) → diameter = 3 (updated)

---

## ⏱️ Time Complexity:

* **O(N)** where N is number of nodes — each node is visited once.

## 📦 Space Complexity:

* **O(H)** recursion stack — H is height of tree.

---

## 55. Zigzag level order traversal.

### ✅ Problem: Zigzag Level Order Traversal of Binary Tree

You are given the root of a binary tree. Return its **zigzag level order traversal** — where the traversal alternates between **left-to-right** and **right-to-left** at each level.

---

### 📘 Example:

For this tree:

```
        1
       / \
      2   3
     / \   \
    4   5   6
```

Zigzag level order traversal is:

```
[
 [1],
 [3, 2],
 [4, 5, 6]
]
```

---

### 🔍 Intuition:

This is a level order traversal (BFS), but with a twist:

* On **even levels** (0, 2, …) traverse **left to right**
* On **odd levels** (1, 3, …) traverse **right to left**

---

### ✅ Approach (Using Queue + Deque):

1. Use a **Queue** for BFS traversal.
2. Use a **Deque/List** to build each level’s result.

    * If it’s an even level → add elements **at end**.
    * If it’s an odd level → add elements **at beginning**.

---

### ✅ Java Code:

```java
import java.util.*;

class TreeNode {
    int val;
    TreeNode left, right;

    TreeNode(int val) { this.val = val; }
}

public class ZigzagTraversal {

    public static List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        List<List<Integer>> result = new ArrayList<>();
        if (root == null) return result;

        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        boolean leftToRight = true;

        while (!queue.isEmpty()) {
            int size = queue.size();
            LinkedList<Integer> level = new LinkedList<>();

            for (int i = 0; i < size; i++) {
                TreeNode node = queue.poll();

                if (leftToRight)
                    level.addLast(node.val);
                else
                    level.addFirst(node.val);

                if (node.left != null) queue.offer(node.left);
                if (node.right != null) queue.offer(node.right);
            }

            result.add(level);
            leftToRight = !leftToRight; // flip direction
        }

        return result;
    }

    public static void main(String[] args) {
        /*
                1
               / \
              2   3
             / \   \
            4   5   6
        */
        TreeNode root = new TreeNode(1);
        root.left = new TreeNode(2);
        root.right = new TreeNode(3);
        root.left.left = new TreeNode(4);
        root.left.right = new TreeNode(5);
        root.right.right = new TreeNode(6);

        List<List<Integer>> result = zigzagLevelOrder(root);
        System.out.println(result);
        // Output: [[1], [3, 2], [4, 5, 6]]
    }
}
```

---

### ⏱️ Time Complexity:

* **O(N)** — each node is visited once.

### 📦 Space Complexity:

* **O(N)** — for queue and result list.

---

## 56. Boundary traversal of binary tree.

### ✅ Problem: Boundary Traversal of a Binary Tree

**Goal**: Traverse the boundary of a binary tree **anti-clockwise**, starting from the root. The boundary includes:

1. **Left boundary** (excluding leaf nodes),
2. **Leaf nodes** (from left to right),
3. **Right boundary** (excluding leaf nodes, **reversed**).

---

### 📘 Example:

For the tree:

```
         1
       /   \
      2     3
     / \   / \
    4   5 6   7
           \
            8
```

The boundary traversal is:

```
[1, 2, 4, 5, 8, 7, 3]
```

---

### 🔍 Strategy:

We break the problem into 3 parts:

1. **Left Boundary**:

    * Traverse left from root.left until you hit a leaf.
    * Skip leaves (they'll be included later).

2. **Leaf Nodes**:

    * Use DFS to collect all leaf nodes.

3. **Right Boundary**:

    * Traverse right from root.right until you hit a leaf.
    * Skip leaves.
    * Store in a stack or list and reverse before adding to result.

---

### ✅ Java Code:

```java
import java.util.*;

class TreeNode {
    int val;
    TreeNode left, right;
    TreeNode(int val) { this.val = val; }
}

public class BoundaryTraversal {

    public static List<Integer> boundaryOfBinaryTree(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        if (root == null) return result;
        if (!isLeaf(root)) result.add(root.val);

        addLeftBoundary(root.left, result);
        addLeaves(root, result);
        addRightBoundary(root.right, result);

        return result;
    }

    private static void addLeftBoundary(TreeNode node, List<Integer> result) {
        while (node != null) {
            if (!isLeaf(node)) result.add(node.val);
            node = (node.left != null) ? node.left : node.right;
        }
    }

    private static void addRightBoundary(TreeNode node, List<Integer> result) {
        Stack<Integer> stack = new Stack<>();
        while (node != null) {
            if (!isLeaf(node)) stack.push(node.val);
            node = (node.right != null) ? node.right : node.left;
        }
        while (!stack.isEmpty()) {
            result.add(stack.pop());
        }
    }

    private static void addLeaves(TreeNode node, List<Integer> result) {
        if (node == null) return;
        if (isLeaf(node)) {
            result.add(node.val);
            return;
        }
        addLeaves(node.left, result);
        addLeaves(node.right, result);
    }

    private static boolean isLeaf(TreeNode node) {
        return (node.left == null && node.right == null);
    }

    public static void main(String[] args) {
        /*
                 1
               /   \
              2     3
             / \   / \
            4   5 6   7
                   \
                    8
        */
        TreeNode root = new TreeNode(1);
        root.left = new TreeNode(2);
        root.right = new TreeNode(3);
        root.left.left = new TreeNode(4);
        root.left.right = new TreeNode(5);
        root.right.left = new TreeNode(6);
        root.right.right = new TreeNode(7);
        root.right.left.right = new TreeNode(8);

        List<Integer> boundary = boundaryOfBinaryTree(root);
        System.out.println("Boundary traversal: " + boundary);
        // Output: [1, 2, 4, 5, 8, 7, 3]
    }
}
```

---

### ⏱️ Time Complexity:

* **O(N)**: All nodes are visited once.

### 📦 Space Complexity:

* **O(H)** for recursion (H = height), and up to O(N) for final list.

---

## 57. Vertical order traversal.

### ✅ Problem: Vertical Order Traversal of a Binary Tree

**Goal**: Given the root of a binary tree, return its vertical order traversal — where nodes are grouped **column by column**, from **leftmost** to **rightmost**.

---

### 📘 Example:

For the tree:

```
        1
       / \
      2   3
     / \ / \
    4  5 6  7
```

Vertical Order Traversal is:

```
[
 [4],
 [2],
 [1, 5, 6],
 [3],
 [7]
]
```

---

### 🔍 How It Works:

We perform **BFS traversal** and track:

* **Vertical (column) index**:

    * `column - 1` for left child
    * `column + 1` for right child
* Use a **TreeMap** to maintain column order.
* Use a **Queue** to perform level-order traversal while keeping track of column numbers.

---

### ✅ Java Code (BFS Approach):

```java
import java.util.*;

class TreeNode {
    int val;
    TreeNode left, right;

    TreeNode(int val) { this.val = val; }
}

public class VerticalOrderTraversal {

    public static List<List<Integer>> verticalOrder(TreeNode root) {
        List<List<Integer>> result = new ArrayList<>();
        if (root == null) return result;

        // Map: column -> list of nodes
        TreeMap<Integer, List<Integer>> map = new TreeMap<>();
        // Queue for BFS: stores node + its column index
        Queue<Pair> queue = new LinkedList<>();
        queue.offer(new Pair(root, 0));

        while (!queue.isEmpty()) {
            Pair curr = queue.poll();
            TreeNode node = curr.node;
            int col = curr.col;

            map.putIfAbsent(col, new ArrayList<>());
            map.get(col).add(node.val);

            if (node.left != null)
                queue.offer(new Pair(node.left, col - 1));
            if (node.right != null)
                queue.offer(new Pair(node.right, col + 1));
        }

        // Assemble result from TreeMap
        for (List<Integer> colNodes : map.values()) {
            result.add(colNodes);
        }

        return result;
    }

    static class Pair {
        TreeNode node;
        int col;

        Pair(TreeNode n, int c) {
            node = n;
            col = c;
        }
    }

    public static void main(String[] args) {
        /*
                1
               / \
              2   3
             / \ / \
            4  5 6  7
        */
        TreeNode root = new TreeNode(1);
        root.left = new TreeNode(2);
        root.right = new TreeNode(3);
        root.left.left = new TreeNode(4);
        root.left.right = new TreeNode(5);
        root.right.left = new TreeNode(6);
        root.right.right = new TreeNode(7);

        List<List<Integer>> vertical = verticalOrder(root);
        System.out.println("Vertical Order: " + vertical);
        // Output: [[4], [2], [1, 5, 6], [3], [7]]
    }
}
```

---

### ⏱️ Time Complexity:

* **O(N)**: Each node is visited once.
* **O(N log N)**: Because of `TreeMap` insertion.

### 📦 Space Complexity:

* **O(N)**: For queue and column map.

---

## 58. Bottom view / top view of binary tree.

Let's cover both the **Top View** and **Bottom View** of a Binary Tree — popular and commonly asked problems in system design and interviews.

---

## ✅ Problem 1: **Top View of a Binary Tree**

> **Top view** includes the first node at each **vertical column** when viewed from the **top**.

### 📘 Example:

For this tree:

```
        1
       / \
      2   3
     / \   \
    4   5   6
         \
          7
```

**Top View**: `[4, 2, 1, 3, 6]`

---

## ✅ Problem 2: **Bottom View of a Binary Tree**

> **Bottom view** includes the **last node** at each vertical column when viewed from the **bottom**.

**Bottom View** of the same tree: `[4, 2, 7, 3, 6]`

---

## 🔍 Strategy for Both

* Do a **level-order traversal** (BFS).
* Track each node’s **horizontal distance (HD)** from the root:

    * Left child: `HD - 1`
    * Right child: `HD + 1`
* Use a **Map\<Integer, Integer>** to store the first (for top view) or last (for bottom view) node at each horizontal distance.

---

## ✅ Java Code (Both Top and Bottom View)

```java
import java.util.*;

class TreeNode {
    int val;
    TreeNode left, right;
    TreeNode(int val) { this.val = val; }
}

class Pair {
    TreeNode node;
    int hd; // horizontal distance

    Pair(TreeNode node, int hd) {
        this.node = node;
        this.hd = hd;
    }
}

public class TreeViews {

    public static List<Integer> topView(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        if (root == null) return result;

        Map<Integer, Integer> map = new TreeMap<>();
        Queue<Pair> queue = new LinkedList<>();

        queue.offer(new Pair(root, 0));

        while (!queue.isEmpty()) {
            Pair curr = queue.poll();
            TreeNode node = curr.node;
            int hd = curr.hd;

            // Only add first node at this horizontal distance
            map.putIfAbsent(hd, node.val);

            if (node.left != null) queue.offer(new Pair(node.left, hd - 1));
            if (node.right != null) queue.offer(new Pair(node.right, hd + 1));
        }

        result.addAll(map.values());
        return result;
    }

    public static List<Integer> bottomView(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        if (root == null) return result;

        Map<Integer, Integer> map = new TreeMap<>();
        Queue<Pair> queue = new LinkedList<>();

        queue.offer(new Pair(root, 0));

        while (!queue.isEmpty()) {
            Pair curr = queue.poll();
            TreeNode node = curr.node;
            int hd = curr.hd;

            // Always overwrite, we want the last (bottom) node at this HD
            map.put(hd, node.val);

            if (node.left != null) queue.offer(new Pair(node.left, hd - 1));
            if (node.right != null) queue.offer(new Pair(node.right, hd + 1));
        }

        result.addAll(map.values());
        return result;
    }

    public static void main(String[] args) {
        /*
                 1
               /   \
              2     3
             / \     \
            4   5     6
                 \
                  7
        */
        TreeNode root = new TreeNode(1);
        root.left = new TreeNode(2);
        root.right = new TreeNode(3);
        root.left.left = new TreeNode(4);
        root.left.right = new TreeNode(5);
        root.right.right = new TreeNode(6);
        root.left.right.right = new TreeNode(7);

        System.out.println("Top View: " + topView(root));       // Output: [4, 2, 1, 3, 6]
        System.out.println("Bottom View: " + bottomView(root)); // Output: [4, 2, 7, 3, 6]
    }
}
```

---

## ⏱️ Time & Space Complexity:

* **Time**: O(N) — Visit every node once.
* **Space**: O(N) — Queue and map can hold all nodes in the worst case.

---

## 59. Maximum path sum in binary tree.

### ✅ Problem: **Maximum Path Sum in a Binary Tree**

> **Goal**: Find the **maximum sum of any path** in a binary tree.
> A path may start and end at **any node**, but it must follow **parent-child connections** (no cycles or jumps).

---

### 🔍 Path Definition:

* A path can go from a node to **any descendant**, or even **split** at a node and go through both left and right children.
* But a path **cannot revisit nodes**.
* The **maximum path sum** is the maximum of all such valid paths.

---

### 📘 Example:

For the tree:

```
        -10
        /  \
       9   20
          /  \
         15   7
```

Valid paths:

* `15` → `20` → `7` = **42** (This is the max!)
* `9` alone = 9
* `20` → `15` = 35
* etc.

**Output**: `42`

---

### 🧠 Key Insight:

At each node, you can:

1. Continue the path **down one side** (`max(left, right) + node.val`) — for recursion.
2. Consider a new path **splitting through** that node (`left + node.val + right`) — for max tracking.

---

### ✅ Java Code:

```java
class TreeNode {
    int val;
    TreeNode left, right;
    TreeNode(int x) { val = x; }
}

public class MaxPathSum {
    private static int maxSum;

    public static int maxPathSum(TreeNode root) {
        maxSum = Integer.MIN_VALUE;
        findMaxPath(root);
        return maxSum;
    }

    private static int findMaxPath(TreeNode node) {
        if (node == null) return 0;

        // Max path sum going left or right, ignore if negative
        int left = Math.max(0, findMaxPath(node.left));
        int right = Math.max(0, findMaxPath(node.right));

        // Max path including both left and right through current node
        int localMax = node.val + left + right;

        // Update global max
        maxSum = Math.max(maxSum, localMax);

        // Return the max one-side path sum for recursion
        return node.val + Math.max(left, right);
    }

    public static void main(String[] args) {
        /*
                -10
                /  \
               9   20
                  /  \
                 15   7
        */
        TreeNode root = new TreeNode(-10);
        root.left = new TreeNode(9);
        root.right = new TreeNode(20);
        root.right.left = new TreeNode(15);
        root.right.right = new TreeNode(7);

        System.out.println("Maximum Path Sum: " + maxPathSum(root)); // Output: 42
    }
}
```

---

### ⏱️ Time Complexity:

* **O(N)** – We visit every node once.

### 📦 Space Complexity:

* **O(H)** – Recursion stack height (H = height of the tree).

---

### 🔄 Example Path Breakdown:

At node `20`:

* Left = 15
* Right = 7
* Local path sum = 15 + 20 + 7 = 42 ✅
* Return to parent: `20 + max(15, 7) = 35`

---

## 60. Flatten binary tree to linked list.

### ✅ Problem: Flatten Binary Tree to Linked List

> Given a binary tree, flatten it to a **linked list in-place** (using the right child pointers) **in the same order as a preorder traversal**.

---

### 🔍 Example:

Input Tree:

```
      1
     / \
    2   5
   / \   \
  3   4   6
```

Output (flattened):

```
1
 \
  2
   \
    3
     \
      4
       \
        5
         \
          6
```

Each node’s left child should be `null`, and the right child points to the next node in preorder.

---

## ✅ Approach 1: Reverse Preorder (Right → Left → Root)

* We do **postorder traversal**, but visit **right first**, then left.
* Keep a reference to the previously visited node.
* Update each node's `right` to the previously visited node, and `left = null`.

---

### ✅ Java Code (Recursive Reverse Preorder):

```java
class TreeNode {
    int val;
    TreeNode left, right;
    TreeNode(int x) { val = x; }
}

public class FlattenBinaryTree {
    private static TreeNode prev = null;

    public static void flatten(TreeNode root) {
        if (root == null) return;

        flatten(root.right);
        flatten(root.left);

        root.right = prev;
        root.left = null;
        prev = root;
    }

    // Helper to print the flattened list
    public static void printFlattened(TreeNode root) {
        while (root != null) {
            System.out.print(root.val + " -> ");
            root = root.right;
        }
        System.out.println("null");
    }

    public static void main(String[] args) {
        /*
              1
             / \
            2   5
           / \   \
          3   4   6
        */
        TreeNode root = new TreeNode(1);
        root.left = new TreeNode(2);
        root.right = new TreeNode(5);
        root.left.left = new TreeNode(3);
        root.left.right = new TreeNode(4);
        root.right.right = new TreeNode(6);

        flatten(root);
        printFlattened(root); // Output: 1 -> 2 -> 3 -> 4 -> 5 -> 6 -> null
    }
}
```

---

## ✅ Approach 2: Morris Traversal (No Recursion or Stack)

* Time: O(N)
* Space: O(1) (true in-place)
* For each node with a left child:

    * Find the **rightmost node** in the left subtree (predecessor).
    * Connect that node's `right` to current node’s `right`.
    * Move left subtree to the right.
    * Set left = null.

---

### 🔄 Morris Flatten Java Code:

```java
public static void flatten(TreeNode root) {
    TreeNode curr = root;

    while (curr != null) {
        if (curr.left != null) {
            // Find rightmost in left subtree
            TreeNode prev = curr.left;
            while (prev.right != null) {
                prev = prev.right;
            }

            // Rewire connections
            prev.right = curr.right;
            curr.right = curr.left;
            curr.left = null;
        }
        curr = curr.right;
    }
}
```

---

## ⏱️ Time & Space Complexity:

| Approach          | Time | Space |
| ----------------- | ---- | ----- |
| Recursive         | O(N) | O(H)  |
| Morris (In-place) | O(N) | O(1)  |

---

### 🔹 **61–70: Recursion & Backtracking**

## 61. Subsets / Power set.

### ✅ Problem: Subsets / Power Set

> Given a set of integers `nums`, return **all possible subsets (the power set)**.

---

### 🔍 Example:

```text
Input: nums = [1, 2, 3]

Output:
[
  [],          // empty set
  [1],
  [2],
  [3],
  [1, 2],
  [1, 3],
  [2, 3],
  [1, 2, 3]
]
```

---

## ✅ Approach 1: Backtracking (DFS)

We explore every element by either:

* **Including** it in the current subset
* **Excluding** it

### 🔁 Recursive Tree (Decision at each index):

For `nums = [1, 2]`:

```
           []
         /    \
       [1]     []
      /   \      \
 [1,2]   [1]     [2]
```

---

### ✅ Java Code (Backtracking):

```java
import java.util.*;

public class PowerSet {
    public static List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        backtrack(nums, 0, new ArrayList<>(), result);
        return result;
    }

    private static void backtrack(int[] nums, int index, List<Integer> current, List<List<Integer>> result) {
        result.add(new ArrayList<>(current)); // Add current subset

        for (int i = index; i < nums.length; i++) {
            current.add(nums[i]);                  // Include nums[i]
            backtrack(nums, i + 1, current, result); // Recurse
            current.remove(current.size() - 1);    // Backtrack
        }
    }

    public static void main(String[] args) {
        int[] nums = {1, 2, 3};
        List<List<Integer>> subsets = subsets(nums);
        for (List<Integer> subset : subsets) {
            System.out.println(subset);
        }
    }
}
```

---

## ✅ Approach 2: Iterative (BFS-style Expansion)

Start with: `[]`
For each number in `nums`, add it to all existing subsets.

### Example (nums = \[1, 2]):

Start with: `[[]]`
Process `1`: `[[], [1]]`
Process `2`: `[[], [1], [2], [1,2]]`

---

### 🔁 Java Code (Iterative):

```java
public static List<List<Integer>> subsets(int[] nums) {
    List<List<Integer>> result = new ArrayList<>();
    result.add(new ArrayList<>());

    for (int num : nums) {
        int n = result.size();
        for (int i = 0; i < n; i++) {
            List<Integer> subset = new ArrayList<>(result.get(i));
            subset.add(num);
            result.add(subset);
        }
    }
    return result;
}
```

---

## ✅ Approach 3: Bit Manipulation (Best when set size ≤ 20)

For `n` elements, total subsets = `2^n`.
Each subset corresponds to a binary number of length `n`.

For example, nums = `[a, b, c]`
000 → \[]
001 → \[c]
010 → \[b]
011 → \[b, c]
...

---

### 🔁 Java Code (Bitmasking):

```java
public static List<List<Integer>> subsets(int[] nums) {
    int n = nums.length;
    List<List<Integer>> result = new ArrayList<>();

    for (int i = 0; i < (1 << n); i++) {
        List<Integer> subset = new ArrayList<>();
        for (int j = 0; j < n; j++) {
            if ((i & (1 << j)) != 0) {
                subset.add(nums[j]);
            }
        }
        result.add(subset);
    }

    return result;
}
```

---

## 🧠 Time & Space Complexity:

* **Time**: O(2^n \* n) — for generating and copying each subset
* **Space**: O(2^n \* n) — total number of subsets

---

## 62. Permutations of a string/array.

### ✅ Problem: Permutations of a String or Array

> Given a string or array `nums`, generate all possible **permutations** (order matters, no duplicates unless handled explicitly).

---

### 🔍 Example 1: For array `[1, 2, 3]`

**Output**:

```
[1, 2, 3]  
[1, 3, 2]  
[2, 1, 3]  
[2, 3, 1]  
[3, 1, 2]  
[3, 2, 1]
```

---

### 🔍 Example 2: For string `"abc"`

**Output**:

```
abc  
acb  
bac  
bca  
cab  
cba
```

---

## ✅ Approach: Backtracking (Swap-based or Visited array)

We generate all permutations by:

* Swapping elements in the array.
* Or by maintaining a `visited[]` boolean array and building the current permutation list recursively.

---

### ✅ Java Code (Array Input - Swap Based)

```java
import java.util.*;

public class Permutations {

    public static List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        backtrack(nums, 0, result);
        return result;
    }

    private static void backtrack(int[] nums, int index, List<List<Integer>> result) {
        if (index == nums.length) {
            List<Integer> permutation = new ArrayList<>();
            for (int num : nums) permutation.add(num);
            result.add(permutation);
            return;
        }

        for (int i = index; i < nums.length; i++) {
            swap(nums, i, index);  // fix one element
            backtrack(nums, index + 1, result);
            swap(nums, i, index);  // backtrack
        }
    }

    private static void swap(int[] nums, int i, int j) {
        int temp = nums[i]; nums[i] = nums[j]; nums[j] = temp;
    }

    public static void main(String[] args) {
        int[] nums = {1, 2, 3};
        List<List<Integer>> res = permute(nums);
        for (List<Integer> p : res) {
            System.out.println(p);
        }
    }
}
```

---

### ✅ Java Code (String Input - Character Array)

```java
public class StringPermutations {
    public static void permute(char[] chars, int index) {
        if (index == chars.length) {
            System.out.println(String.valueOf(chars));
            return;
        }

        for (int i = index; i < chars.length; i++) {
            swap(chars, i, index);
            permute(chars, index + 1);
            swap(chars, i, index); // backtrack
        }
    }

    private static void swap(char[] a, int i, int j) {
        char temp = a[i]; a[i] = a[j]; a[j] = temp;
    }

    public static void main(String[] args) {
        String s = "abc";
        permute(s.toCharArray(), 0);
    }
}
```

---

### ⏱ Time & Space Complexity

| Metric      | Value          |
| ----------- | -------------- |
| Time        | O(N!)          |
| Space       | O(N) recursion |
| Output Size | O(N! × N)      |

---

### ✅ Handling Duplicates (Like `[1, 1, 2]`)

Use **HashSet** to skip duplicates at each level:

```java
Set<Integer> seen = new HashSet<>();
if (seen.contains(nums[i])) continue;
```

Or sort input first and skip duplicates smartly:

```java
if (i != index && nums[i] == nums[index]) continue;
```

---

## 63. Combination Sum I & II.

Here's a detailed explanation of **Combination Sum I & II** problems along with Java solutions.

---

## ✅ Combination Sum I

### Problem:

Given an array of **distinct positive integers** `candidates` and a target number `target`, find all unique combinations where the candidate numbers sum to `target`.
You can use **an unlimited number of times** for each candidate.

### Example:

```
Input: candidates = [2,3,6,7], target = 7
Output:
[
  [7],
  [2,2,3]
]
```

---

### Approach:

* Use **backtracking**.
* At each step, you can **reuse the same candidate**.
* When the sum exceeds target, backtrack.
* Stop when sum == target and add combination to results.

---

### Java Code:

```java
import java.util.*;

public class CombinationSumI {
    public static List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> result = new ArrayList<>();
        backtrack(candidates, target, 0, new ArrayList<>(), result);
        return result;
    }

    private static void backtrack(int[] candidates, int target, int start, 
                                  List<Integer> current, List<List<Integer>> result) {
        if (target == 0) {
            result.add(new ArrayList<>(current));
            return;
        }
        if (target < 0) return;

        for (int i = start; i < candidates.length; i++) {
            current.add(candidates[i]);
            // Reuse same element by passing i (not i+1)
            backtrack(candidates, target - candidates[i], i, current, result);
            current.remove(current.size() - 1);
        }
    }

    public static void main(String[] args) {
        int[] candidates = {2,3,6,7};
        int target = 7;
        List<List<Integer>> res = combinationSum(candidates, target);
        for (List<Integer> comb : res) {
            System.out.println(comb);
        }
    }
}
```

---

## ✅ Combination Sum II

### Problem:

Given an array of **candidates (can have duplicates)** and a target, find all unique combinations where the candidate numbers sum to `target`.
Each candidate **may only be used once** in the combination.

### Example:

```
Input: candidates = [10,1,2,7,6,1,5], target = 8
Output:
[
  [1,1,6],
  [1,2,5],
  [1,7],
  [2,6]
]
```

---

### Approach:

* Sort the array to handle duplicates.
* Use backtracking with **index moving forward**.
* Skip duplicates at the same recursion level to avoid repeated combinations.

---

### Java Code:

```java
import java.util.*;

public class CombinationSumII {
    public static List<List<Integer>> combinationSum2(int[] candidates, int target) {
        List<List<Integer>> result = new ArrayList<>();
        Arrays.sort(candidates);  // Sort to handle duplicates
        backtrack(candidates, target, 0, new ArrayList<>(), result);
        return result;
    }

    private static void backtrack(int[] candidates, int target, int start, 
                                  List<Integer> current, List<List<Integer>> result) {
        if (target == 0) {
            result.add(new ArrayList<>(current));
            return;
        }
        if (target < 0) return;

        for (int i = start; i < candidates.length; i++) {
            // Skip duplicates at same recursion level
            if (i > start && candidates[i] == candidates[i - 1]) continue;

            current.add(candidates[i]);
            backtrack(candidates, target - candidates[i], i + 1, current, result);
            current.remove(current.size() - 1);
        }
    }

    public static void main(String[] args) {
        int[] candidates = {10,1,2,7,6,1,5};
        int target = 8;
        List<List<Integer>> res = combinationSum2(candidates, target);
        for (List<Integer> comb : res) {
            System.out.println(comb);
        }
    }
}
```

---

## 🧠 Time Complexity:

* Both problems are **exponential** in worst case:
  roughly **O(2^N)** where N is the number of candidates, due to exploring combinations.

---

## 64. N-Queens Problem.

### ✅ Problem: N-Queens

> Place **N queens** on an N×N chessboard so that no two queens threaten each other.
> Return **all distinct solutions**, where each solution is a board configuration with queens placed safely.

---

### 🔍 Example (N=4):

Solutions:

```
[
 [".Q..",
  "...Q",
  "Q...",
  "..Q."],

 ["..Q.",
  "Q...",
  "...Q",
  ".Q.."]
]
```

---

## ✅ Problem Explanation:

* No two queens share the same:

    * Row
    * Column
    * Diagonal (both main and anti-diagonal)

---

## ✅ Approach: Backtracking

* Place queens row by row.
* For each row, try all columns.
* Check if placing queen is **safe** (no conflict).
* If safe, place and move to next row.
* If not safe, try next column.
* When all rows filled, record solution.

---

### How to check diagonals efficiently:

* Use sets or boolean arrays to track:

    * Columns occupied
    * Main diagonals occupied: `row - col`
    * Anti diagonals occupied: `row + col`

---

### ✅ Java Code:

```java
import java.util.*;

public class NQueens {
    public static List<List<String>> solveNQueens(int n) {
        List<List<String>> solutions = new ArrayList<>();

        boolean[] cols = new boolean[n];
        boolean[] diag1 = new boolean[2 * n]; // row - col + n
        boolean[] diag2 = new boolean[2 * n]; // row + col

        char[][] board = new char[n][n];
        for (char[] row : board)
            Arrays.fill(row, '.');

        backtrack(0, n, board, cols, diag1, diag2, solutions);
        return solutions;
    }

    private static void backtrack(int row, int n, char[][] board,
                                  boolean[] cols, boolean[] diag1, boolean[] diag2,
                                  List<List<String>> solutions) {
        if (row == n) {
            solutions.add(construct(board));
            return;
        }

        for (int col = 0; col < n; col++) {
            int d1 = row - col + n;
            int d2 = row + col;
            if (cols[col] || diag1[d1] || diag2[d2]) continue;

            board[row][col] = 'Q';
            cols[col] = true; diag1[d1] = true; diag2[d2] = true;

            backtrack(row + 1, n, board, cols, diag1, diag2, solutions);

            // Backtrack
            board[row][col] = '.';
            cols[col] = false; diag1[d1] = false; diag2[d2] = false;
        }
    }

    private static List<String> construct(char[][] board) {
        List<String> res = new ArrayList<>();
        for (char[] row : board)
            res.add(new String(row));
        return res;
    }

    public static void main(String[] args) {
        int n = 4;
        List<List<String>> solutions = solveNQueens(n);
        for (List<String> sol : solutions) {
            for (String row : sol) System.out.println(row);
            System.out.println();
        }
    }
}
```

---

## ⏱ Time Complexity:

* Worst case: O(N!) because at each row you try all columns.
* Pruning by checking columns and diagonals speeds this up a lot.

---

## 65. Word search in a grid.

### ✅ Problem: Word Search in a Grid

> Given a 2D grid of characters and a word, check if the word exists in the grid.
> The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring.
> The same cell cannot be used more than once.

---

### 🔍 Example:

```
Board:
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]

Word = "ABCCED"  -> true  
Word = "SEE"     -> true  
Word = "ABCB"    -> false
```

---

## ✅ Approach: Backtracking (DFS)

* For each cell, if first char matches word\[0], start DFS.
* Explore neighbors (up, down, left, right) recursively for next char.
* Mark visited cells temporarily to avoid reuse.
* Backtrack after exploring neighbors.

---

### ✅ Java Code:

```java
public class WordSearch {

    public static boolean exist(char[][] board, String word) {
        int rows = board.length;
        int cols = board[0].length;

        for (int r = 0; r < rows; r++) {
            for (int c = 0; c < cols; c++) {
                if (dfs(board, word, r, c, 0)) return true;
            }
        }
        return false;
    }

    private static boolean dfs(char[][] board, String word, int r, int c, int index) {
        if (index == word.length()) return true;  // found whole word

        // Check boundaries and char match
        if (r < 0 || c < 0 || r >= board.length || c >= board[0].length || board[r][c] != word.charAt(index))
            return false;

        char temp = board[r][c];
        board[r][c] = '#';  // mark visited

        // Explore neighbors: up, down, left, right
        boolean found = dfs(board, word, r + 1, c, index + 1)
                     || dfs(board, word, r - 1, c, index + 1)
                     || dfs(board, word, r, c + 1, index + 1)
                     || dfs(board, word, r, c - 1, index + 1);

        board[r][c] = temp;  // backtrack

        return found;
    }

    public static void main(String[] args) {
        char[][] board = {
            {'A','B','C','E'},
            {'S','F','C','S'},
            {'A','D','E','E'}
        };
        System.out.println(exist(board, "ABCCED"));  // true
        System.out.println(exist(board, "SEE"));     // true
        System.out.println(exist(board, "ABCB"));    // false
    }
}
```

---

## ⏱ Time Complexity:

* O(M \* N \* 4^L), where M×N is board size and L is word length.
* At each step, 4 directions possible.

---

## 66. Sudoku solver.

### ✅ Problem: Sudoku Solver

> Given a partially filled 9x9 Sudoku board, fill the empty cells so that the board is a valid Sudoku solution.
> Each row, column, and 3x3 sub-box must contain digits 1 to 9 without repetition.

---

### 🔍 Example:

**Input board:**

```
5 3 . | . 7 . | . . .
6 . . | 1 9 5 | . . .
. 9 8 | . . . | . 6 .
------+-------+------
8 . . | . 6 . | . . 3
4 . . | 8 . 3 | . . 1
7 . . | . 2 . | . . 6
------+-------+------
. 6 . | . . . | 2 8 .
. . . | 4 1 9 | . . 5
. . . | . 8 . | . 7 9
```

**Output:**

Completed board that satisfies all Sudoku rules.

---

## ✅ Approach: Backtracking

* Find the first empty cell ('.' or 0).
* Try digits 1-9 in that cell.
* Check if placing the digit is valid (no conflict in row, column, 3x3 box).
* If valid, place digit and recursively try to solve the next cell.
* If no valid digit leads to solution, backtrack.

---

### ✅ Java Code:

```java
public class SudokuSolver {
    public static void solveSudoku(char[][] board) {
        backtrack(board);
    }

    private static boolean backtrack(char[][] board) {
        for (int row = 0; row < 9; row++) {
            for (int col = 0; col < 9; col++) {
                if (board[row][col] == '.') {
                    for (char c = '1'; c <= '9'; c++) {
                        if (isValid(board, row, col, c)) {
                            board[row][col] = c;

                            if (backtrack(board)) return true;

                            board[row][col] = '.'; // backtrack
                        }
                    }
                    return false; // no valid digit found
                }
            }
        }
        return true; // no empty cell left => solved
    }

    private static boolean isValid(char[][] board, int row, int col, char c) {
        for (int i = 0; i < 9; i++) {
            // check row
            if (board[row][i] == c) return false;
            // check column
            if (board[i][col] == c) return false;
            // check 3x3 box
            int boxRow = 3 * (row / 3) + i / 3;
            int boxCol = 3 * (col / 3) + i % 3;
            if (board[boxRow][boxCol] == c) return false;
        }
        return true;
    }

    public static void printBoard(char[][] board) {
        for (int i = 0; i < 9; i++) {
            if (i % 3 == 0 && i != 0) System.out.println("------+-------+------");
            for (int j = 0; j < 9; j++) {
                if (j % 3 == 0 && j != 0) System.out.print("| ");
                System.out.print(board[i][j] + " ");
            }
            System.out.println();
        }
    }

    public static void main(String[] args) {
        char[][] board = {
            {'5','3','.','.','7','.','.','.','.'},
            {'6','.','.','1','9','5','.','.','.'},
            {'.','9','8','.','.','.','.','6','.'},
            {'8','.','.','.','6','.','.','.','3'},
            {'4','.','.','8','.','3','.','.','1'},
            {'7','.','.','.','2','.','.','.','6'},
            {'.','6','.','.','.','.','2','8','.'},
            {'.','.','.','4','1','9','.','.','5'},
            {'.','.','.','.','8','.','.','7','9'}
        };
        
        solveSudoku(board);
        printBoard(board);
    }
}
```

---

## ⏱ Time Complexity:

* Exponential in worst case (backtracking over empty cells).
* Usually fast due to pruning via validity checks.

---

## 67. Rat in a maze.

### ✅ Problem: Rat in a Maze

> Given a N×N maze represented by a grid with 1s (open path) and 0s (blocked path), find a path from the top-left corner (0,0) to the bottom-right corner (N-1,N-1).
> You can move **only right or down** at any point. Return any valid path if exists.

---

### 🔍 Example:

```
Maze:
1 0 0 0
1 1 0 1
0 1 0 0
1 1 1 1

Output: A path such as (0,0) → (1,0) → (1,1) → (2,1) → (3,1) → (3,2) → (3,3)
```

---

## ✅ Approach: Backtracking

* Start at (0,0).
* If cell is open (1), mark as part of path.
* Move **right** or **down** recursively.
* If reach destination, return true.
* Else backtrack.

---

### ✅ Java Code:

```java
import java.util.*;

public class RatInMaze {

    public static List<int[]> findPath(int[][] maze) {
        int n = maze.length;
        List<int[]> path = new ArrayList<>();
        if (solveMaze(maze, 0, 0, path)) {
            return path;
        }
        return Collections.emptyList(); // no path found
    }

    private static boolean solveMaze(int[][] maze, int row, int col, List<int[]> path) {
        int n = maze.length;

        // Check if current cell is valid
        if (row < 0 || col < 0 || row >= n || col >= n || maze[row][col] == 0) {
            return false;
        }

        // Add current cell to path
        path.add(new int[]{row, col});

        // If destination reached
        if (row == n - 1 && col == n - 1) {
            return true;
        }

        // Move right
        if (solveMaze(maze, row, col + 1, path)) {
            return true;
        }

        // Move down
        if (solveMaze(maze, row + 1, col, path)) {
            return true;
        }

        // Backtrack
        path.remove(path.size() - 1);
        return false;
    }

    public static void main(String[] args) {
        int[][] maze = {
            {1,0,0,0},
            {1,1,0,1},
            {0,1,0,0},
            {1,1,1,1}
        };

        List<int[]> path = findPath(maze);
        if (path.isEmpty()) {
            System.out.println("No path found");
        } else {
            System.out.println("Path:");
            for (int[] cell : path) {
                System.out.print(Arrays.toString(cell) + " ");
            }
        }
    }
}
```

---

## ⏱ Time Complexity:

* Worst case: O(2^(N\*N)) because each cell can lead to two directions.
* Pruning blocked cells and boundaries helps reduce search.

---

## 68. Knight’s tour.

### ✅ Problem: Knight’s Tour

> Given an `N x N` chessboard, find a sequence of moves for a knight such that the knight visits every square exactly once.
> The knight moves in an "L" shape: 2 squares in one direction and 1 in perpendicular.

---

### 🔍 Explanation:

* Start from a given position (usually `(0,0)`).
* Move the knight to an unvisited valid position.
* Continue until all squares are visited.
* Backtrack if stuck.

---

### ✅ Approach: Backtracking

* Maintain a `board` to track the move number for each cell.
* Try all 8 possible knight moves.
* Mark visited cells with move count.
* Backtrack if no moves possible.

---

### ✅ Java Code:

```java
public class KnightsTour {
    private static final int[] rowMoves = {-2, -1, 1, 2, 2, 1, -1, -2};
    private static final int[] colMoves = {1, 2, 2, 1, -1, -2, -2, -1};

    public static boolean solveKT(int N) {
        int[][] board = new int[N][N];
        for (int i = 0; i < N; i++)
            for (int j = 0; j < N; j++)
                board[i][j] = -1;

        board[0][0] = 0; // starting position

        if (!solveKTUtil(0, 0, 1, board, N)) {
            System.out.println("No solution exists");
            return false;
        } else {
            printBoard(board, N);
            return true;
        }
    }

    private static boolean solveKTUtil(int row, int col, int moveCount, int[][] board, int N) {
        if (moveCount == N * N)
            return true;

        for (int i = 0; i < 8; i++) {
            int nextRow = row + rowMoves[i];
            int nextCol = col + colMoves[i];

            if (isSafe(nextRow, nextCol, board, N)) {
                board[nextRow][nextCol] = moveCount;

                if (solveKTUtil(nextRow, nextCol, moveCount + 1, board, N))
                    return true;
                else
                    board[nextRow][nextCol] = -1; // backtrack
            }
        }
        return false;
    }

    private static boolean isSafe(int row, int col, int[][] board, int N) {
        return (row >= 0 && col >= 0 && row < N && col < N && board[row][col] == -1);
    }

    private static void printBoard(int[][] board, int N) {
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                System.out.printf("%2d ", board[i][j]);
            }
            System.out.println();
        }
    }

    public static void main(String[] args) {
        int N = 8;
        solveKT(N);
    }
}
```

---

### ⏱ Time Complexity:

* Worst case is very high (exponential) due to many moves.
* Backtracking tries all possibilities.

---

If you want:

* Explanation of Warnsdorff's heuristic for optimization
* Variants like closed knight's tour
* Visualizations of moves

Just ask!

---

## 69. Generate balanced parentheses.

### ✅ Problem: Generate Balanced Parentheses

> Given `n`, generate all combinations of well-formed parentheses consisting of `n` pairs.

---

### 🔍 Example:

Input: `n = 3`
Output:

```
[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
```

---

## ✅ Approach: Backtracking

* Keep track of the count of open and close parentheses added so far.
* You can add `'('` if open count < n.
* You can add `')'` if close count < open count (to maintain balance).
* When the length of the current string is `2 * n`, add it to results.

---

### ✅ Java Code:

```java
import java.util.*;

public class GenerateParentheses {
    
    public static List<String> generateParenthesis(int n) {
        List<String> result = new ArrayList<>();
        backtrack(result, "", 0, 0, n);
        return result;
    }

    private static void backtrack(List<String> result, String current, int open, int close, int max) {
        if (current.length() == max * 2) {
            result.add(current);
            return;
        }

        if (open < max) {
            backtrack(result, current + "(", open + 1, close, max);
        }
        if (close < open) {
            backtrack(result, current + ")", open, close + 1, max);
        }
    }

    public static void main(String[] args) {
        int n = 3;
        List<String> parentheses = generateParenthesis(n);
        System.out.println(parentheses);
    }
}
```

---

### ⏱ Time Complexity:

* Exponential, roughly **O(4^n / sqrt(n))** (Catalan number growth).

---

## 70. Palindrome partitioning.

### ✅ Problem: Palindrome Partitioning

> Given a string `s`, partition `s` such that every substring of the partition is a palindrome.
> Return all possible palindrome partitioning of `s`.

---

### 🔍 Example:

Input: `"aab"`
Output:

```
[
  ["a", "a", "b"],
  ["aa", "b"]
]
```

---

## ✅ Approach: Backtracking + Palindrome Checking

* Use backtracking to try all partitions starting from index 0.
* For each substring `s[start:end]`, check if it's palindrome.
* If yes, add substring to current path and recurse from `end`.
* If `start` reaches string length, add path to results.

---

### ✅ Java Code:

```java
import java.util.*;

public class PalindromePartitioning {

    public static List<List<String>> partition(String s) {
        List<List<String>> result = new ArrayList<>();
        backtrack(s, 0, new ArrayList<>(), result);
        return result;
    }

    private static void backtrack(String s, int start, List<String> path, List<List<String>> result) {
        if (start == s.length()) {
            result.add(new ArrayList<>(path));
            return;
        }

        for (int end = start; end < s.length(); end++) {
            if (isPalindrome(s, start, end)) {
                path.add(s.substring(start, end + 1));
                backtrack(s, end + 1, path, result);
                path.remove(path.size() - 1);
            }
        }
    }

    private static boolean isPalindrome(String s, int low, int high) {
        while (low < high) {
            if (s.charAt(low++) != s.charAt(high--)) return false;
        }
        return true;
    }

    public static void main(String[] args) {
        String s = "aab";
        List<List<String>> partitions = partition(s);
        System.out.println(partitions);
    }
}
```

---

### ⏱ Time Complexity:

* Exponential, since we try all partitions.
* Palindrome checks take O(n) each, but can be optimized with DP.

---

### 🔹 **71–80: Dynamic Programming (DP)**

## 71. Fibonacci (Memoization & Tabulation).

Let's cover Fibonacci sequence calculation with **Memoization** and **Tabulation** approaches in Java, both of which are dynamic programming techniques.

---

## ✅ Problem: Fibonacci Numbers

Calculate the nth Fibonacci number where:

* `fib(0) = 0`
* `fib(1) = 1`
* `fib(n) = fib(n-1) + fib(n-2)` for `n > 1`

---

## 1️⃣ Memoization (Top-Down DP)

* Recursively calculate Fibonacci.
* Store computed results in a cache (array) to avoid recomputation.
* Reduces exponential time to linear.

### Java Code (Memoization):

```java
public class FibonacciMemo {
    public static int fib(int n, int[] memo) {
        if (n <= 1) return n;
        if (memo[n] != -1) return memo[n];

        memo[n] = fib(n - 1, memo) + fib(n - 2, memo);
        return memo[n];
    }

    public static void main(String[] args) {
        int n = 10;
        int[] memo = new int[n + 1];
        Arrays.fill(memo, -1);
        System.out.println("Fib(" + n + ") = " + fib(n, memo));
    }
}
```

---

## 2️⃣ Tabulation (Bottom-Up DP)

* Iteratively build up from base cases.
* Use an array to store Fibonacci values from 0 to n.
* Avoid recursion completely.

### Java Code (Tabulation):

```java
public class FibonacciTabulation {
    public static int fib(int n) {
        if (n <= 1) return n;

        int[] dp = new int[n + 1];
        dp[0] = 0;
        dp[1] = 1;

        for (int i = 2; i <= n; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }

        return dp[n];
    }

    public static void main(String[] args) {
        int n = 10;
        System.out.println("Fib(" + n + ") = " + fib(n));
    }
}
```

---

## ⏱ Time Complexity:

* Both approaches run in **O(n)** time.
* Space complexity is **O(n)** due to memo/table arrays.

---

## Bonus: Space-Optimized Tabulation

You only need the last two Fibonacci numbers at any point:

```java
public static int fibSpaceOptimized(int n) {
    if (n <= 1) return n;

    int a = 0, b = 1, c = 0;
    for (int i = 2; i <= n; i++) {
        c = a + b;
        a = b;
        b = c;
    }
    return c;
}
```

---

## 72. Longest Common Subsequence (LCS).

### ✅ Problem: Longest Common Subsequence (LCS)

> Given two strings `text1` and `text2`, find the length of their longest common subsequence.
> A subsequence is a sequence that appears in the same relative order but not necessarily contiguous.

---

### 🔍 Example:

```
Input: text1 = "ABCBDAB", text2 = "BDCABA"
Output: 4
Explanation: The LCS is "BCAB" or "BDAB"
```

---

## ✅ Approach: Dynamic Programming (Tabulation)

* Use a 2D `dp` array of size `(m+1) x (n+1)` where `m = text1.length()`, `n = text2.length()`.
* `dp[i][j]` represents the length of LCS of `text1[0..i-1]` and `text2[0..j-1]`.
* If characters match (`text1[i-1] == text2[j-1]`), then `dp[i][j] = dp[i-1][j-1] + 1`.
* Else, `dp[i][j] = max(dp[i-1][j], dp[i][j-1])`.

---

### ✅ Java Code:

```java
public class LongestCommonSubsequence {

    public static int lcs(String text1, String text2) {
        int m = text1.length();
        int n = text2.length();

        int[][] dp = new int[m + 1][n + 1];

        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (text1.charAt(i - 1) == text2.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1] + 1;
                } else {
                    dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
                }
            }
        }

        return dp[m][n];
    }

    public static void main(String[] args) {
        String text1 = "ABCBDAB";
        String text2 = "BDCABA";

        System.out.println("Length of LCS: " + lcs(text1, text2));
    }
}
```

---

## Optional: Print the LCS string

To reconstruct the LCS string, you can backtrack through the `dp` array from `dp[m][n]`.

---

## ⏱ Time & Space Complexity:

* Time: **O(m \* n)**
* Space: **O(m \* n)**

---

## 73. Longest Increasing Subsequence.

### ✅ Problem: Longest Increasing Subsequence (LIS)

> Given an integer array `nums`, find the length of the longest strictly increasing subsequence.

---

### 🔍 Example:

Input: `nums = [10, 9, 2, 5, 3, 7, 101, 18]`
Output: `4`
Explanation: The LIS is `[2, 3, 7, 101]`

---

## ✅ Approach 1: Dynamic Programming (O(n²))

* For each element, check all previous elements smaller than it.
* `dp[i]` stores length of LIS ending at index `i`.
* Update `dp[i] = max(dp[i], dp[j] + 1)` where `j < i` and `nums[j] < nums[i]`.

### Java Code:

```java
public class LongestIncreasingSubsequence {
    public static int lengthOfLIS(int[] nums) {
        int n = nums.length;
        int[] dp = new int[n];
        Arrays.fill(dp, 1);  // minimum LIS is 1 for each element

        int maxLen = 1;
        for (int i = 1; i < n; i++) {
            for (int j = 0; j < i; j++) {
                if (nums[j] < nums[i]) {
                    dp[i] = Math.max(dp[i], dp[j] + 1);
                }
            }
            maxLen = Math.max(maxLen, dp[i]);
        }

        return maxLen;
    }

    public static void main(String[] args) {
        int[] nums = {10, 9, 2, 5, 3, 7, 101, 18};
        System.out.println("Length of LIS: " + lengthOfLIS(nums));
    }
}
```

---

## ✅ Approach 2: Binary Search (Patience Sorting) — O(n log n)

* Maintain an array `tails` where `tails[i]` is the smallest tail of an increasing subsequence of length `i+1`.
* For each element, use binary search on `tails` to find the position to update.
* Length of `tails` is length of LIS.

### Java Code:

```java
import java.util.*;

public class LongestIncreasingSubsequence {
    public static int lengthOfLIS(int[] nums) {
        List<Integer> tails = new ArrayList<>();

        for (int num : nums) {
            int index = Collections.binarySearch(tails, num);
            if (index < 0) index = -(index + 1);

            if (index == tails.size()) {
                tails.add(num);
            } else {
                tails.set(index, num);
            }
        }

        return tails.size();
    }

    public static void main(String[] args) {
        int[] nums = {10, 9, 2, 5, 3, 7, 101, 18};
        System.out.println("Length of LIS: " + lengthOfLIS(nums));
    }
}
```

---

### ⏱ Complexity:

| Approach               | Time Complexity | Space Complexity |
| ---------------------- | --------------- | ---------------- |
| DP (nested loops)      | O(n²)           | O(n)             |
| Binary Search Patience | O(n log n)      | O(n)             |

---

## 74. 0/1 Knapsack Problem.

### ✅ Problem: 0/1 Knapsack

> Given weights and values of `n` items, and a maximum capacity `W`, find the maximum total value you can get by selecting items such that the total weight is at most `W`.
> Each item can be chosen **at most once** (hence 0/1 knapsack).

---

### 🔍 Example:

```
Weights = [1, 3, 4, 5]
Values =  [1, 4, 5, 7]
W = 7
Output: 9  (Choose items with weights 3 and 4 => 4 + 5 = 9)
```

---

## ✅ Approach: Dynamic Programming (Bottom-Up)

* Use a 2D `dp` array where `dp[i][w]` represents max value using first `i` items with capacity `w`.
* If item `i`'s weight > `w`, skip it: `dp[i][w] = dp[i-1][w]`.
* Else, max of skipping or taking the item:
  `dp[i][w] = max(dp[i-1][w], values[i-1] + dp[i-1][w - weights[i-1]])`.

---

### ✅ Java Code:

```java
public class Knapsack01 {

    public static int knapsack(int[] weights, int[] values, int W) {
        int n = weights.length;
        int[][] dp = new int[n + 1][W + 1];

        for (int i = 1; i <= n; i++) {
            for (int w = 1; w <= W; w++) {
                if (weights[i - 1] > w) {
                    dp[i][w] = dp[i - 1][w];
                } else {
                    dp[i][w] = Math.max(dp[i - 1][w],
                                        values[i - 1] + dp[i - 1][w - weights[i - 1]]);
                }
            }
        }

        return dp[n][W];
    }

    public static void main(String[] args) {
        int[] weights = {1, 3, 4, 5};
        int[] values = {1, 4, 5, 7};
        int W = 7;
        System.out.println("Max value: " + knapsack(weights, values, W));
    }
}
```

---

## ⏱ Time & Space Complexity:

* Time: **O(n \* W)**
* Space: **O(n \* W)**

---

## Optional: Space Optimization (Using 1D array)

You can optimize space by using a 1D array `dp[w]` and iterating weights in reverse order:

```java
public static int knapsackOptimized(int[] weights, int[] values, int W) {
    int n = weights.length;
    int[] dp = new int[W + 1];

    for (int i = 0; i < n; i++) {
        for (int w = W; w >= weights[i]; w--) {
            dp[w] = Math.max(dp[w], values[i] + dp[w - weights[i]]);
        }
    }

    return dp[W];
}
```

---

## 75. Coin Change Problem.

### ✅ Problem: Coin Change (Minimum Number of Coins)

> Given an array of coin denominations `coins` and an amount `amount`, find the **minimum number of coins** needed to make up that amount.
> Return -1 if it’s not possible.

---

### 🔍 Example:

```
coins = [1, 2, 5], amount = 11
Output: 3
Explanation: 11 = 5 + 5 + 1
```

---

## ✅ Approach: Dynamic Programming (Bottom-Up)

* Use a 1D `dp` array of size `amount + 1` where `dp[i]` is min coins to make amount `i`.
* Initialize `dp[0] = 0` (0 coins needed for amount 0).
* Initialize others as a large value (`amount + 1`).
* For each coin, update dp for amounts from coin value to amount.
* For each `i`, `dp[i] = min(dp[i], dp[i - coin] + 1)`.

---

### ✅ Java Code:

```java
import java.util.*;

public class CoinChange {

    public static int coinChange(int[] coins, int amount) {
        int max = amount + 1;
        int[] dp = new int[amount + 1];
        Arrays.fill(dp, max);
        dp[0] = 0;

        for (int coin : coins) {
            for (int i = coin; i <= amount; i++) {
                dp[i] = Math.min(dp[i], dp[i - coin] + 1);
            }
        }

        return dp[amount] > amount ? -1 : dp[amount];
    }

    public static void main(String[] args) {
        int[] coins = {1, 2, 5};
        int amount = 11;
        System.out.println("Minimum coins needed: " + coinChange(coins, amount));
    }
}
```

---

## ⏱ Time & Space Complexity:

* Time: **O(n \* amount)** where n = number of coins.
* Space: **O(amount)**

---

## Variants you might want to explore:

* Count total ways to make amount (Coin Change II)
* Print combination of coins used
* Recursive + memoization approach

---

## 76. Edit Distance.

### ✅ Problem: Edit Distance (Levenshtein Distance)

> Given two strings `word1` and `word2`, find the minimum number of operations required to convert `word1` into `word2`.
> Allowed operations:
>
> * Insert a character
> * Delete a character
> * Replace a character

---

### 🔍 Example:

```
Input: word1 = "horse", word2 = "ros"
Output: 3

Explanation:
horse -> rorse (replace 'h' with 'r')
rorse -> rose  (remove 'r')
rose  -> ros   (remove 'e')
```

---

## ✅ Approach: Dynamic Programming (Bottom-Up)

* Use a 2D `dp` array where `dp[i][j]` is the minimum edit distance between `word1[0..i-1]` and `word2[0..j-1]`.
* Initialization:
  `dp[0][j] = j` (convert empty string to first j chars by inserting)
  `dp[i][0] = i` (convert first i chars to empty string by deleting)
* Transition:
  If characters match:
  `dp[i][j] = dp[i-1][j-1]`
  Else:
  `dp[i][j] = 1 + min( dp[i-1][j] (delete), dp[i][j-1] (insert), dp[i-1][j-1] (replace) )`

---

### ✅ Java Code:

```java
public class EditDistance {

    public static int minDistance(String word1, String word2) {
        int m = word1.length();
        int n = word2.length();

        int[][] dp = new int[m + 1][n + 1];

        // Initialize base cases
        for (int i = 0; i <= m; i++) dp[i][0] = i;
        for (int j = 0; j <= n; j++) dp[0][j] = j;

        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (word1.charAt(i - 1) == word2.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1];
                } else {
                    dp[i][j] = 1 + Math.min(
                        dp[i - 1][j],    // delete
                        Math.min(
                            dp[i][j - 1],    // insert
                            dp[i - 1][j - 1] // replace
                        )
                    );
                }
            }
        }

        return dp[m][n];
    }

    public static void main(String[] args) {
        String word1 = "horse";
        String word2 = "ros";

        System.out.println("Minimum edit distance: " + minDistance(word1, word2));
    }
}
```

---

## ⏱ Time & Space Complexity:

* Time: **O(m \* n)**
* Space: **O(m \* n)**

---

## Optional:

* Space optimization using 2 rows since `dp[i][j]` depends only on `dp[i-1][..]`.
* Print the actual sequence of operations.

---

## 77. Subset sum problem.

### ✅ Problem: Subset Sum Problem

> Given an array of positive integers `nums` and a target sum `S`, determine if there is a subset of `nums` whose sum equals `S`.
> Return `true` if such a subset exists, otherwise `false`.

---

### 🔍 Example:

```
Input: nums = [3, 34, 4, 12, 5, 2], S = 9
Output: true
Explanation: There is a subset (4, 5) with sum 9.
```

---

## ✅ Approach: Dynamic Programming (Bottom-Up)

* Use a 2D boolean DP array `dp[n+1][S+1]` where `dp[i][j]` is `true` if a subset of the first `i` elements has sum `j`.
* Initialization:

    * `dp[0][0] = true` (empty subset sums to 0)
    * `dp[0][j] = false` for `j > 0` (no subset possible with 0 elements)
* Transition:
  For each element `nums[i-1]` and sum `j`:

    * If we exclude current element: `dp[i-1][j]`
    * If we include current element (only if `nums[i-1] <= j`): `dp[i-1][j - nums[i-1]]`
      Then:

  ```
  dp[i][j] = dp[i-1][j] || dp[i-1][j - nums[i-1]]
  ```

---

### ✅ Java Code:

```java
public class SubsetSum {

    public static boolean isSubsetSum(int[] nums, int S) {
        int n = nums.length;
        boolean[][] dp = new boolean[n + 1][S + 1];

        for (int i = 0; i <= n; i++) {
            dp[i][0] = true; // sum 0 possible with empty subset
        }

        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= S; j++) {
                if (nums[i - 1] > j) {
                    dp[i][j] = dp[i - 1][j]; // exclude element
                } else {
                    dp[i][j] = dp[i - 1][j] || dp[i - 1][j - nums[i - 1]]; // exclude or include
                }
            }
        }

        return dp[n][S];
    }

    public static void main(String[] args) {
        int[] nums = {3, 34, 4, 12, 5, 2};
        int S = 9;

        System.out.println("Subset with sum " + S + " exists? " + isSubsetSum(nums, S));
    }
}
```

---

## ⏱ Time & Space Complexity:

* Time: **O(n \* S)**
* Space: **O(n \* S)**

---

## Optional:

* Space optimization using 1D DP (iterate sums in reverse order)
* Print the subset itself (backtracking from `dp` table)

---

## 78. Minimum path sum in a grid.

### ✅ Problem: Minimum Path Sum in a Grid

> Given a `m x n` grid filled with non-negative numbers, find a path from the top-left corner to the bottom-right corner which minimizes the sum of all numbers along its path.
> You can only move either **down** or **right** at any point.

---

### 🔍 Example:

```
Input:
[
  [1, 3, 1],
  [1, 5, 1],
  [4, 2, 1]
]

Output: 7

Explanation: The path 1 → 3 → 1 → 1 → 1 minimizes the sum.
```

---

## ✅ Approach: Dynamic Programming (Bottom-Up)

* Use a 2D `dp` array of the same size as the grid.
* `dp[i][j]` represents minimum sum to reach cell `(i, j)`.
* Initialization:

    * `dp[0][0] = grid[0][0]`
    * First row: `dp[0][j] = dp[0][j-1] + grid[0][j]`
    * First column: `dp[i][0] = dp[i-1][0] + grid[i][0]`
* Transition:

    * For other cells:
      `dp[i][j] = grid[i][j] + min(dp[i-1][j], dp[i][j-1])`

---

### ✅ Java Code:

```java
public class MinPathSum {

    public static int minPathSum(int[][] grid) {
        int m = grid.length;
        int n = grid[0].length;

        int[][] dp = new int[m][n];
        dp[0][0] = grid[0][0];

        // Initialize first row
        for (int j = 1; j < n; j++) {
            dp[0][j] = dp[0][j - 1] + grid[0][j];
        }

        // Initialize first column
        for (int i = 1; i < m; i++) {
            dp[i][0] = dp[i - 1][0] + grid[i][0];
        }

        // Fill the dp array
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                dp[i][j] = grid[i][j] + Math.min(dp[i - 1][j], dp[i][j - 1]);
            }
        }

        return dp[m - 1][n - 1];
    }

    public static void main(String[] args) {
        int[][] grid = {
            {1, 3, 1},
            {1, 5, 1},
            {4, 2, 1}
        };

        System.out.println("Minimum path sum: " + minPathSum(grid));
    }
}
```

---

## ⏱ Time & Space Complexity:

* Time: **O(m \* n)**
* Space: **O(m \* n)**

---

## Optional: Space Optimization

* Since `dp[i][j]` depends only on `dp[i-1][j]` and `dp[i][j-1]`, we can optimize space using a 1D array.

---

## 79. Palindromic Substrings / Longest Palindromic Substring.

Let’s discuss **Palindromic Substrings** and **Longest Palindromic Substring** with explanations and examples.

---

### 1️⃣ Palindromic Substrings (Count total palindromic substrings)

> Given a string, count how many substrings are palindromes.

---

### Approach: Expand Around Center

* Every palindrome can be expanded from its center.
* There are `2n - 1` centers in a string of length `n`:

    * `n` odd-length centers (each character itself)
    * `n-1` even-length centers (between characters)
* For each center, expand outwards while the substring is a palindrome.

---

### Java Code to Count Palindromic Substrings:

```java
public class PalindromicSubstrings {

    public static int countPalindromicSubstrings(String s) {
        int count = 0;
        int n = s.length();

        for (int center = 0; center < 2 * n - 1; center++) {
            int left = center / 2;
            int right = left + center % 2;

            while (left >= 0 && right < n && s.charAt(left) == s.charAt(right)) {
                count++;
                left--;
                right++;
            }
        }

        return count;
    }

    public static void main(String[] args) {
        String s = "aaa";
        System.out.println("Total palindromic substrings: " + countPalindromicSubstrings(s));
    }
}
```

**Example:** For `"aaa"`
Palindromic substrings are: `"a", "a", "a", "aa", "aa", "aaa"` (6 total)

---

### 2️⃣ Longest Palindromic Substring

> Given a string, find the longest substring that is a palindrome.

---

### Approach: Expand Around Center (Similar to above)

* For each center, expand outwards and keep track of the longest palindrome found.

---

### Java Code for Longest Palindromic Substring:

```java
public class LongestPalindromicSubstring {

    public static String longestPalindrome(String s) {
        if (s == null || s.length() < 1) return "";

        int start = 0, end = 0;
        int n = s.length();

        for (int center = 0; center < 2 * n - 1; center++) {
            int left = center / 2;
            int right = left + center % 2;

            while (left >= 0 && right < n && s.charAt(left) == s.charAt(right)) {
                left--;
                right++;
            }

            int length = right - left - 1;  // length of palindrome
            if (length > end - start) {
                start = left + 1;
                end = right - 1;
            }
        }

        return s.substring(start, end + 1);
    }

    public static void main(String[] args) {
        String s = "babad";
        System.out.println("Longest palindromic substring: " + longestPalindrome(s));
    }
}
```

**Example:** For `"babad"`
Longest palindrome is `"bab"` or `"aba"` (both valid)

---

### ⏱ Time Complexity:

* Both methods run in **O(n²)** time.
* Space complexity is **O(1)** (not counting input and output strings).

---

## 80. Matrix Chain Multiplication.

### ✅ Problem: Matrix Chain Multiplication

> Given a sequence of matrices, find the most efficient way to multiply these matrices together.
> The goal is to minimize the total number of scalar multiplications.
> You are **not** actually performing the multiplications, only deciding the order.

---

### 🔍 Problem Details:

* Suppose you have `n` matrices: A1, A2, ..., An.
* Dimensions of Ai is `p[i-1] x p[i]` for i=1 to n.
* Input: an array `p` of length `n+1` where matrix `Ai` has dimensions `p[i-1] x p[i]`.
* Output: minimum number of scalar multiplications needed.

---

### Example:

```
p = [40, 20, 30, 10, 30]

This means matrices:
A1 = 40x20
A2 = 20x30
A3 = 30x10
A4 = 10x30

Minimum cost of multiplication = 26000
```

---

## ✅ Approach: Dynamic Programming (Bottom-Up)

* Let `dp[i][j]` = minimum number of multiplications needed to multiply matrices `Ai` through `Aj`.
* Base case: `dp[i][i] = 0` (multiplying one matrix costs 0).
* For chain length `l` from 2 to n:

    * For each `i` from 1 to `n-l+1`:

        * Set `j = i + l - 1`
        * Try all possible splits `k` between `i` and `j-1`:

          ```
          cost = dp[i][k] + dp[k+1][j] + p[i-1]*p[k]*p[j]
          ```
        * Choose minimum cost among all splits.

---

### ✅ Java Code:

```java
public class MatrixChainMultiplication {

    public static int matrixChainOrder(int[] p) {
        int n = p.length - 1; // number of matrices
        int[][] dp = new int[n + 1][n + 1];

        // cost is zero when multiplying one matrix
        for (int i = 1; i <= n; i++) {
            dp[i][i] = 0;
        }

        for (int length = 2; length <= n; length++) { // length of the chain
            for (int i = 1; i <= n - length + 1; i++) {
                int j = i + length - 1;
                dp[i][j] = Integer.MAX_VALUE;

                for (int k = i; k < j; k++) {
                    int cost = dp[i][k] + dp[k + 1][j] + p[i - 1] * p[k] * p[j];
                    if (cost < dp[i][j]) {
                        dp[i][j] = cost;
                    }
                }
            }
        }

        return dp[1][n];
    }

    public static void main(String[] args) {
        int[] p = {40, 20, 30, 10, 30};
        System.out.println("Minimum number of multiplications is " + matrixChainOrder(p));
    }
}
```

---

## ⏱ Time & Space Complexity:

* Time: **O(n³)** (three nested loops)
* Space: **O(n²)** (dp table)

---

## Optional:

* Recover the optimal parenthesization by storing the split points.
* Recursive + memoization version.

---

### 🔹 **81–85: Searching & Sorting**

## 81. Binary Search and variants (first/last occurrence).

Let’s dive into **Binary Search** and its important variants: **first occurrence** and **last occurrence** in a sorted array.

---

## 1️⃣ Classic Binary Search

**Goal:** Find the index of a target value in a sorted array. If not found, return `-1`.

---

### Algorithm:

* Use two pointers `low = 0`, `high = n-1`.
* Calculate `mid = low + (high - low)/2`.
* If `arr[mid] == target` return `mid`.
* If `arr[mid] < target` search in the right half (`low = mid + 1`).
* Else search in the left half (`high = mid - 1`).

---

### Code (Java):

```java
public static int binarySearch(int[] arr, int target) {
    int low = 0, high = arr.length - 1;

    while (low <= high) {
        int mid = low + (high - low) / 2;

        if (arr[mid] == target) {
            return mid;
        } else if (arr[mid] < target) {
            low = mid + 1;
        } else {
            high = mid - 1;
        }
    }
    return -1; // target not found
}
```

---

## 2️⃣ First Occurrence of Target

**Goal:** Find the **first (leftmost)** index where `target` occurs in the sorted array (with duplicates).

---

### Modification:

* When `arr[mid] == target`, **do not stop**.
* Record `mid` as a candidate answer, then continue searching **left half** (`high = mid - 1`).

---

### Code (Java):

```java
public static int firstOccurrence(int[] arr, int target) {
    int low = 0, high = arr.length - 1;
    int result = -1;

    while (low <= high) {
        int mid = low + (high - low) / 2;

        if (arr[mid] == target) {
            result = mid;     // record potential answer
            high = mid - 1;   // search left half for earlier occurrence
        } else if (arr[mid] < target) {
            low = mid + 1;
        } else {
            high = mid - 1;
        }
    }
    return result;
}
```

---

## 3️⃣ Last Occurrence of Target

**Goal:** Find the **last (rightmost)** index where `target` occurs.

---

### Modification:

* When `arr[mid] == target`, record `mid`, then search **right half** (`low = mid + 1`).

---

### Code (Java):

```java
public static int lastOccurrence(int[] arr, int target) {
    int low = 0, high = arr.length - 1;
    int result = -1;

    while (low <= high) {
        int mid = low + (high - low) / 2;

        if (arr[mid] == target) {
            result = mid;     // record potential answer
            low = mid + 1;    // search right half for later occurrence
        } else if (arr[mid] < target) {
            low = mid + 1;
        } else {
            high = mid - 1;
        }
    }
    return result;
}
```

---

## 🔎 Example:

```java
int[] arr = {1, 2, 2, 2, 3, 4, 5};
int target = 2;

System.out.println(binarySearch(arr, target));        // Might print 1, 2 or 3 (any occurrence)
System.out.println(firstOccurrence(arr, target));     // Prints 1
System.out.println(lastOccurrence(arr, target));      // Prints 3
```

---

## 🕒 Complexity:

* Time: **O(log n)** for all variants.
* Space: **O(1)**.

---

## 82. Search in 2D matrix.

Let's talk about **Search in a 2D Matrix** problem with detailed explanation and code.

---

### Problem:

You are given an `m x n` matrix with the following properties:

* Integers in each row are sorted in ascending order from left to right.
* The first integer of each row is greater than the last integer of the previous row.

**Goal:** Given a target value, determine if it exists in the matrix.

---

### Example:

```
Matrix:
[
  [1, 3, 5, 7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]

Target = 3

Output: true
```

---

## Approach 1: Treat the 2D matrix as a 1D sorted array and apply binary search

Since the matrix is sorted row-wise and the first element of each row is greater than the last element of the previous row, the entire matrix can be viewed as a sorted list.

* Number of elements = `m * n`.
* Map the 1D index `mid` to 2D indices as:

    * `row = mid / n`
    * `col = mid % n`
* Use binary search over the range `[0, m*n - 1]`.

---

### Code (Java):

```java
public class Search2DMatrix {

    public static boolean searchMatrix(int[][] matrix, int target) {
        if (matrix == null || matrix.length == 0) return false;

        int m = matrix.length;
        int n = matrix[0].length;

        int low = 0, high = m * n - 1;

        while (low <= high) {
            int mid = low + (high - low) / 2;
            int midValue = matrix[mid / n][mid % n];

            if (midValue == target) {
                return true;
            } else if (midValue < target) {
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }

        return false;
    }

    public static void main(String[] args) {
        int[][] matrix = {
            {1, 3, 5, 7},
            {10, 11, 16, 20},
            {23, 30, 34, 50}
        };
        int target = 3;

        System.out.println(searchMatrix(matrix, target)); // Output: true
    }
}
```

---

## Approach 2 (if rows and columns are sorted individually, but no global order):

This problem is a variation where each row and each column is sorted independently but no global row-to-row order exists. For that, you can start searching from the top-right corner and move left/down accordingly (also called Staircase Search).

---

### Time Complexity:

* **Approach 1:** O(log(m\*n)) = O(log m + log n)
* **Approach 2 (if applicable):** O(m + n)

---

## 83. Merge Sort.

Let’s go through **Merge Sort**, a classic and important sorting algorithm often asked in interviews.

---

## What is Merge Sort?

* **Divide and Conquer** sorting algorithm.
* Recursively divides the array into two halves, sorts each half, then merges the sorted halves.
* Stable sort and works in **O(n log n)** time.

---

## How Merge Sort Works?

1. **Divide:** Split the array into two halves.
2. **Conquer:** Recursively sort each half.
3. **Combine:** Merge the two sorted halves into a sorted array.

---

## Example:

```
Input: [38, 27, 43, 3, 9, 82, 10]

Divide until single elements:
[38, 27, 43, 3] and [9, 82, 10]
[38, 27] and [43, 3]
[38] and [27]
[43] and [3]

Merge step:
[27, 38], [3, 43]
[3, 27, 38, 43], etc.

Final sorted array:
[3, 9, 10, 27, 38, 43, 82]
```

---

## Java Code for Merge Sort:

```java
public class MergeSort {

    // Merge two sorted subarrays arr[l..m] and arr[m+1..r]
    private static void merge(int[] arr, int l, int m, int r) {
        int n1 = m - l + 1;
        int n2 = r - m;

        int[] left = new int[n1];
        int[] right = new int[n2];

        for (int i = 0; i < n1; i++)
            left[i] = arr[l + i];
        for (int j = 0; j < n2; j++)
            right[j] = arr[m + 1 + j];

        int i = 0, j = 0, k = l;

        // Merge left and right arrays
        while (i < n1 && j < n2) {
            if (left[i] <= right[j]) {
                arr[k++] = left[i++];
            } else {
                arr[k++] = right[j++];
            }
        }

        // Copy remaining elements, if any
        while (i < n1) {
            arr[k++] = left[i++];
        }
        while (j < n2) {
            arr[k++] = right[j++];
        }
    }

    // Recursive merge sort function
    public static void mergeSort(int[] arr, int l, int r) {
        if (l < r) {
            int m = l + (r - l) / 2;

            // Sort first half
            mergeSort(arr, l, m);

            // Sort second half
            mergeSort(arr, m + 1, r);

            // Merge sorted halves
            merge(arr, l, m, r);
        }
    }

    public static void main(String[] args) {
        int[] arr = {38, 27, 43, 3, 9, 82, 10};
        mergeSort(arr, 0, arr.length - 1);

        System.out.println("Sorted array:");
        for (int num : arr) {
            System.out.print(num + " ");
        }
    }
}
```

---

## Complexity:

| Aspect      | Complexity     |
| ----------- | -------------- |
| Time        | O(n log n)     |
| Space       | O(n) auxiliary |
| Stable sort | Yes            |

---

## Key Points:

* Merge Sort is a **stable** sorting algorithm.
* It requires extra space proportional to the array size.
* Very efficient for large datasets, especially linked lists.

---

## 84. Quick Sort.

Here's a detailed explanation of **Quick Sort**, another fundamental sorting algorithm often asked in interviews.

---

## What is Quick Sort?

* **Divide and Conquer** sorting algorithm.
* Picks a **pivot** element, partitions the array around the pivot so that elements less than the pivot come before it, and elements greater come after.
* Recursively applies the same process to the left and right subarrays.
* Average time complexity: **O(n log n)**, worst-case: **O(n²)**.
* In-place sort (uses very little extra memory).
* Not stable by default.

---

## How Quick Sort Works?

1. **Choose a pivot** (commonly last element or random).
2. **Partition** the array: rearrange so all elements smaller than pivot are on left, larger on right.
3. **Recursively** quicksort the left and right subarrays.

---

### Example:

```
Array: [10, 7, 8, 9, 1, 5]

Pivot = 5 (last element)

Partitioning:

Elements < 5: [1]
Elements > 5: [10, 7, 8, 9]

After partition: [1, 5, 10, 7, 8, 9]

Recursively apply quicksort on [1] and [10, 7, 8, 9]
```

---

## Java Code for Quick Sort:

```java
public class QuickSort {

    // Partition function to place pivot at correct position
    // and place smaller elements to left and bigger to right
    private static int partition(int[] arr, int low, int high) {
        int pivot = arr[high]; // pivot element
        int i = low - 1;       // index of smaller element

        for (int j = low; j < high; j++) {
            if (arr[j] <= pivot) {
                i++;
                // swap arr[i] and arr[j]
                int temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }

        // swap arr[i+1] and pivot
        int temp = arr[i + 1];
        arr[i + 1] = arr[high];
        arr[high] = temp;

        return i + 1; // return pivot index
    }

    // Recursive QuickSort function
    public static void quickSort(int[] arr, int low, int high) {
        if (low < high) {
            // Partition the array
            int pi = partition(arr, low, high);

            // Sort elements before and after partition
            quickSort(arr, low, pi - 1);
            quickSort(arr, pi + 1, high);
        }
    }

    public static void main(String[] args) {
        int[] arr = {10, 7, 8, 9, 1, 5};
        quickSort(arr, 0, arr.length - 1);

        System.out.println("Sorted array:");
        for (int num : arr) {
            System.out.print(num + " ");
        }
    }
}
```

---

## Time Complexity:

| Case         | Time Complexity |
| ------------ | --------------- |
| Best/Average | O(n log n)      |
| Worst        | O(n²)           |

* Worst case happens when the pivot chosen is always the smallest or largest element (e.g., sorted array with last element pivot).
* Randomized pivot selection or median-of-three can help avoid worst case.

---

## Space Complexity:

* **O(log n)** due to recursion stack.
* In-place, no extra array needed.

---

## Key Points:

* Quick Sort is usually faster in practice than Merge Sort due to better locality of reference.
* Not stable, meaning equal elements may change relative order.
* Pivot selection strategy matters for performance.

---

## 85. Kth largest/smallest element (using heap or partition).

Finding the **Kth largest or smallest element** is a classic problem with two popular efficient approaches:

---

# Problem Statement:

Given an unsorted array, find the **Kth largest** or **Kth smallest** element.

---

# Approach 1: Using Heaps (Priority Queues)

---

## Finding Kth Largest Element with Min-Heap:

* Use a **min-heap** of size K.
* Insert elements one by one.
* When heap size exceeds K, remove the smallest element.
* At the end, the root of the min-heap is the Kth largest element.

### Why?

* Keeps track of the largest K elements seen so far.
* Min-heap root is the smallest among those K elements — which is the Kth largest overall.

---

### Code (Java):

```java
import java.util.PriorityQueue;

public class KthLargestElement {

    public static int findKthLargest(int[] nums, int k) {
        PriorityQueue<Integer> minHeap = new PriorityQueue<>(); // Min-heap by default

        for (int num : nums) {
            minHeap.offer(num);

            if (minHeap.size() > k) {
                minHeap.poll();  // Remove smallest element
            }
        }

        return minHeap.peek();
    }

    public static void main(String[] args) {
        int[] nums = {3, 2, 1, 5, 6, 4};
        int k = 2;

        System.out.println(findKthLargest(nums, k));  // Output: 5
    }
}
```

---

## Finding Kth Smallest Element with Max-Heap:

* Use a **max-heap** of size K.
* Insert elements and when heap size > K, remove the largest.
* Root of max-heap is Kth smallest.

---

# Approach 2: Using Quickselect (Partition-based)

---

Quickselect is a selection algorithm based on the partition method of QuickSort:

* Partition the array around a pivot.
* After partitioning, pivot is at its correct sorted position.
* If pivot position == k-1, pivot is the Kth smallest element.
* Else recursively search left or right part depending on pivot position.

---

### Quickselect for Kth smallest element (Java):

```java
public class QuickSelect {

    public static int quickSelect(int[] nums, int low, int high, int k) {
        if (low == high) return nums[low];

        int pivotIndex = partition(nums, low, high);

        if (pivotIndex == k) {
            return nums[pivotIndex];
        } else if (pivotIndex < k) {
            return quickSelect(nums, pivotIndex + 1, high, k);
        } else {
            return quickSelect(nums, low, pivotIndex - 1, k);
        }
    }

    private static int partition(int[] nums, int low, int high) {
        int pivot = nums[high];
        int i = low;

        for (int j = low; j < high; j++) {
            if (nums[j] <= pivot) {
                swap(nums, i, j);
                i++;
            }
        }
        swap(nums, i, high);
        return i;
    }

    private static void swap(int[] nums, int i, int j) {
        int tmp = nums[i];
        nums[i] = nums[j];
        nums[j] = tmp;
    }

    public static void main(String[] args) {
        int[] nums = {3, 2, 1, 5, 6, 4};
        int k = 2;  // Find 2nd smallest element (index 1)

        System.out.println(quickSelect(nums, 0, nums.length - 1, k - 1));  // Output: 2
    }
}
```

---

### To find **Kth largest** using Quickselect:

* Find the element with index `n - k` (0-based), because largest means counting from end.

Example:

```java
int n = nums.length;
int kthLargest = quickSelect(nums, 0, n - 1, n - k);
```

---

# Summary:

| Method      | Time Complexity | Space Complexity | Notes                |
| ----------- | --------------- | ---------------- | -------------------- |
| Heap        | O(n log k)      | O(k)             | Good if k is small   |
| Quickselect | Average O(n)    | O(1)             | Worst O(n²) but rare |

---

### 🔹 **86–90: Greedy Algorithms**

## 86. Activity selection problem.

Here's a detailed explanation of the **Activity Selection Problem**, a classic greedy algorithm problem often asked in interviews.

---

# Activity Selection Problem

---

### Problem Statement:

Given `n` activities with their **start** and **finish times**, select the maximum number of activities that don't overlap (i.e., no two activities should be running at the same time).

---

### Example:

```
Activities (start, finish):
(1, 3), (2, 5), (4, 7), (6, 9), (8, 10)

Max activities selected without overlap:
(1, 3), (4, 7), (8, 10)  -> 3 activities
```

---

# Approach: Greedy Algorithm

---

### Intuition:

* Always select the activity that **finishes earliest** first.
* This leaves maximum room for the rest of the activities.

---

### Steps:

1. Sort all activities by their finish time.
2. Select the first activity (which finishes earliest).
3. For each subsequent activity, select it **only if** its start time is greater or equal to the finish time of the previously selected activity.
4. Repeat until all activities are processed.

---

### Why Greedy Works?

* Choosing the earliest finishing activity leaves more time for other activities.
* Leads to an optimal solution by local choice at each step.

---

# Code (Java):

```java
import java.util.Arrays;
import java.util.Comparator;

public class ActivitySelection {

    // Activity class to store start and finish time
    static class Activity {
        int start, finish;

        Activity(int s, int f) {
            start = s;
            finish = f;
        }
    }

    public static int maxActivities(Activity[] activities) {
        // Sort activities by finish time
        Arrays.sort(activities, Comparator.comparingInt(a -> a.finish));

        int count = 1;  // Select first activity
        int lastFinish = activities[0].finish;

        for (int i = 1; i < activities.length; i++) {
            if (activities[i].start >= lastFinish) {
                count++;
                lastFinish = activities[i].finish;
            }
        }
        return count;
    }

    public static void main(String[] args) {
        Activity[] activities = {
            new Activity(1, 3),
            new Activity(2, 5),
            new Activity(4, 7),
            new Activity(6, 9),
            new Activity(8, 10)
        };

        System.out.println("Maximum number of activities selected: " + maxActivities(activities));
    }
}
```

---

# Complexity:

| Aspect | Complexity              |
| ------ | ----------------------- |
| Time   | O(n log n) (sorting)    |
| Space  | O(n) (activities array) |

---

# Summary:

* Sort by finish times.
* Iteratively pick activities that start after or when the last selected finished.
* Greedy algorithm guarantees maximum number of non-overlapping activities.

---

## 87. Fractional knapsack.

Here’s a detailed explanation of the **Fractional Knapsack Problem**, a classic greedy algorithm problem.

---

# Fractional Knapsack Problem

---

### Problem Statement:

Given `n` items, each with a **weight** and a **value**, and a knapsack with a maximum capacity `W`, your goal is to maximize the total value in the knapsack. Unlike the 0/1 knapsack, **you can take fractions of items**.

---

### Example:

| Item | Value | Weight |
| ---- | ----- | ------ |
| 1    | 60    | 10     |
| 2    | 100   | 20     |
| 3    | 120   | 30     |

Knapsack Capacity = 50

---

### Intuition:

* Since fractional items are allowed, the **best approach is to take items with the highest value per weight unit first**.
* Take as much as possible of the highest value/weight ratio item, then move to the next.

---

# Approach: Greedy Algorithm

---

### Steps:

1. Calculate **value/weight ratio** for each item.
2. Sort items by this ratio in descending order.
3. Start taking items from the highest ratio:

    * If the whole item fits, take it.
    * Otherwise, take the fraction that fits.
4. Stop when the knapsack is full.

---

# Code (Java):

```java
import java.util.Arrays;
import java.util.Comparator;

public class FractionalKnapsack {

    static class Item {
        int value, weight;

        Item(int v, int w) {
            value = v;
            weight = w;
        }
    }

    public static double fractionalKnapsack(int W, Item[] items) {
        // Sort items by value/weight ratio
        Arrays.sort(items, (a, b) -> {
            double r1 = (double) a.value / a.weight;
            double r2 = (double) b.value / b.weight;
            return Double.compare(r2, r1);
        });

        double totalValue = 0.0;
        int remainingWeight = W;

        for (Item item : items) {
            if (item.weight <= remainingWeight) {
                // Take whole item
                totalValue += item.value;
                remainingWeight -= item.weight;
            } else {
                // Take fractional part
                double fraction = (double) remainingWeight / item.weight;
                totalValue += item.value * fraction;
                break; // Knapsack full
            }
        }

        return totalValue;
    }

    public static void main(String[] args) {
        Item[] items = {
            new Item(60, 10),
            new Item(100, 20),
            new Item(120, 30)
        };

        int W = 50; // Knapsack capacity

        System.out.println("Maximum value in knapsack = " + fractionalKnapsack(W, items));
    }
}
```

---

# Output:

```
Maximum value in knapsack = 240.0
```

---

# Time Complexity:

* Sorting items by ratio: **O(n log n)**
* Single pass to pick items: **O(n)**
* Overall: **O(n log n)**

---

# Key Points:

* Works only when **fractions of items can be taken**.
* Greedy approach always gives optimal solution.
* Different from 0/1 Knapsack (which requires DP and is **NP-hard**).

---

## 88. Job sequencing with deadlines.

Here's a detailed explanation of the **Job Sequencing with Deadlines** problem, a classic greedy algorithm problem that often appears in interviews.

---

# Job Sequencing with Deadlines

---

### Problem Statement:

Given a set of `n` jobs where each job has:

* A **deadline** (by which it should be finished),
* A **profit** (earned if the job is completed by its deadline),

Schedule the jobs to **maximize the total profit**, assuming only one job can be scheduled at a time and each job takes exactly 1 unit of time.

---

### Example:

| Job | Deadline | Profit |
| --- | -------- | ------ |
| 1   | 2        | 100    |
| 2   | 1        | 19     |
| 3   | 2        | 27     |
| 4   | 1        | 25     |
| 5   | 3        | 15     |

---

### Goal:

Find the schedule of jobs that yields the **maximum profit** without missing deadlines.

---

# Approach: Greedy Algorithm

---

### Intuition:

* Always pick the job with the **highest profit first**.
* Schedule it on the latest available slot before its deadline.
* If no slot is free before the deadline, discard the job.

---

### Steps:

1. Sort all jobs in **descending order of profit**.
2. Initialize a result array to keep track of free time slots (size = max deadline).
3. Iterate over jobs and for each job:

    * Find a free slot before or on its deadline, starting from the last possible slot.
    * If a free slot is found, assign the job to that slot.
4. Calculate total profit and jobs scheduled.

---

# Code (Java):

```java
import java.util.Arrays;
import java.util.Comparator;

public class JobSequencing {

    static class Job {
        int id, deadline, profit;

        Job(int id, int deadline, int profit) {
            this.id = id;
            this.deadline = deadline;
            this.profit = profit;
        }
    }

    public static int[] jobScheduling(Job[] jobs) {
        // Sort jobs by profit in descending order
        Arrays.sort(jobs, (a, b) -> b.profit - a.profit);

        int maxDeadline = 0;
        for (Job job : jobs) {
            maxDeadline = Math.max(maxDeadline, job.deadline);
        }

        int[] result = new int[maxDeadline];  // stores job ids
        boolean[] slotOccupied = new boolean[maxDeadline];

        int countJobs = 0;
        int totalProfit = 0;

        for (Job job : jobs) {
            // Find a free slot from job.deadline - 1 down to 0
            for (int j = Math.min(maxDeadline, job.deadline) - 1; j >= 0; j--) {
                if (!slotOccupied[j]) {
                    slotOccupied[j] = true;
                    result[j] = job.id;
                    countJobs++;
                    totalProfit += job.profit;
                    break;
                }
            }
        }

        System.out.println("Total jobs scheduled: " + countJobs);
        System.out.println("Total profit: " + totalProfit);
        System.out.print("Jobs scheduled in order: ");
        for (int i = 0; i < maxDeadline; i++) {
            if (slotOccupied[i]) {
                System.out.print(result[i] + " ");
            }
        }
        System.out.println();

        return result;
    }

    public static void main(String[] args) {
        Job[] jobs = {
            new Job(1, 2, 100),
            new Job(2, 1, 19),
            new Job(3, 2, 27),
            new Job(4, 1, 25),
            new Job(5, 3, 15)
        };

        jobScheduling(jobs);
    }
}
```

---

# Output:

```
Total jobs scheduled: 3
Total profit: 142
Jobs scheduled in order: 4 1 5 
```

---

# Explanation:

* Jobs picked are Job 4 (profit 25, deadline 1), Job 1 (profit 100, deadline 2), and Job 5 (profit 15, deadline 3).
* They fit into their slots without conflict and maximize profit.

---

# Complexity:

| Aspect | Complexity           |
| ------ | -------------------- |
| Time   | O(n log n) (sorting) |
| Space  | O(maxDeadline)       |

---

# Summary:

* Sort jobs by profit.
* Greedily assign each job to the latest available slot before its deadline.
* Maximizes profit for single-unit-time jobs.

---

## 89. Huffman encoding.

Here’s a detailed explanation of **Huffman Encoding**, a fundamental greedy algorithm used in data compression.

---

# Huffman Encoding

---

### Problem Statement:

Given a set of characters along with their frequencies, encode these characters into binary strings such that:

* The **overall encoded length** of the data is minimized.
* No encoded string is a prefix of another (prefix-free property).

---

### Intuition:

* Characters with **higher frequency** should get **shorter codes**.
* Characters with **lower frequency** get **longer codes**.
* This minimizes the total weighted path length in the encoding tree.

---

# How Huffman Encoding Works:

1. Treat each character as a leaf node with weight = frequency.
2. Insert all nodes into a **min-heap** based on frequency.
3. While there is more than one node in the heap:

    * Extract the two nodes with the smallest frequencies.
    * Create a new internal node with these two nodes as children.
    * The new node’s frequency = sum of the two nodes’ frequencies.
    * Insert the new node back into the heap.
4. The remaining node in the heap is the **root of the Huffman tree**.
5. Assign codes by traversing the tree:

    * Left edge = 0
    * Right edge = 1
6. The path from root to leaf gives the code for that character.

---

### Example:

| Character | Frequency |
| --------- | --------- |
| A         | 5         |
| B         | 9         |
| C         | 12        |
| D         | 13        |
| E         | 16        |
| F         | 45        |

The Huffman codes might be:

| Character | Code |
| --------- | ---- |
| F         | 0    |
| C         | 100  |
| D         | 101  |
| A         | 1100 |
| B         | 1101 |
| E         | 111  |

---

# Code (Java):

```java
import java.util.PriorityQueue;

public class HuffmanEncoding {

    // Node class representing each character and its frequency
    static class Node implements Comparable<Node> {
        char ch;
        int freq;
        Node left, right;

        Node(char ch, int freq) {
            this.ch = ch;
            this.freq = freq;
        }

        Node(int freq, Node left, Node right) {
            this.ch = '-';  // internal node
            this.freq = freq;
            this.left = left;
            this.right = right;
        }

        // Comparison based on frequency for PriorityQueue
        @Override
        public int compareTo(Node other) {
            return this.freq - other.freq;
        }
    }

    // Recursive method to print Huffman codes
    public static void printCodes(Node root, String code) {
        if (root == null) return;

        // If leaf node, print code
        if (root.left == null && root.right == null) {
            System.out.println(root.ch + ": " + code);
        }

        printCodes(root.left, code + "0");
        printCodes(root.right, code + "1");
    }

    public static void buildHuffmanTree(char[] chars, int[] freq) {
        PriorityQueue<Node> pq = new PriorityQueue<>();

        // Step 1: Create leaf nodes for each character and add to PQ
        for (int i = 0; i < chars.length; i++) {
            pq.add(new Node(chars[i], freq[i]));
        }

        // Step 2 & 3: Build Huffman tree
        while (pq.size() > 1) {
            Node left = pq.poll();
            Node right = pq.poll();

            Node parent = new Node(left.freq + right.freq, left, right);
            pq.add(parent);
        }

        // Step 4: Remaining node is root of Huffman tree
        Node root = pq.poll();

        // Step 5: Print Huffman codes
        printCodes(root, "");
    }

    public static void main(String[] args) {
        char[] chars = {'A', 'B', 'C', 'D', 'E', 'F'};
        int[] freq = {5, 9, 12, 13, 16, 45};

        buildHuffmanTree(chars, freq);
    }
}
```

---

# Output:

```
A: 1100
B: 1101
C: 100
D: 101
E: 111
F: 0
```

---

# Complexity:

| Aspect | Complexity                                |
| ------ | ----------------------------------------- |
| Time   | O(n log n) (building tree using min heap) |
| Space  | O(n)                                      |

---

# Summary:

* Huffman encoding creates an optimal prefix-free code based on character frequencies.
* Uses a greedy approach of combining lowest frequency nodes.
* Widely used in compression algorithms like ZIP, JPEG, MP3.

---

## 90. Minimum number of platforms.

Here’s a detailed explanation for the classic **Minimum Number of Platforms** problem — a common DSA interview question related to intervals and scheduling.

---

# Minimum Number of Platforms

---

### Problem Statement:

Given arrival and departure times of trains at a station, find the **minimum number of platforms** required so that no train waits (i.e., no two trains occupy the same platform simultaneously).

---

### Example:

| Train | Arrival | Departure |
| ----- | ------- | --------- |
| 1     | 9:00    | 9:10      |
| 2     | 9:40    | 12:00     |
| 3     | 9:50    | 11:20     |
| 4     | 11:00   | 11:30     |
| 5     | 15:00   | 19:00     |
| 6     | 18:00   | 20:00     |

---

### Intuition:

* We need to find the **maximum number of trains at the station at the same time**.
* If many trains overlap, we need more platforms.
* If trains arrive after some have departed, those platforms free up.

---

# Approach: Sorting & Two Pointers

---

### Steps:

1. Sort **arrival** times.
2. Sort **departure** times.
3. Use two pointers `i` and `j` for arrivals and departures.
4. Traverse:

    * If `arrival[i] <= departure[j]`, we need a platform: increment platforms needed, move `i`.
    * Else, a train has left, free a platform: decrement platform needed, move `j`.
5. Keep track of the maximum platforms needed during traversal.

---

# Code (Java):

```java
import java.util.Arrays;

public class MinimumPlatforms {

    public static int findMinPlatforms(int[] arrival, int[] departure) {
        Arrays.sort(arrival);
        Arrays.sort(departure);

        int platformNeeded = 0, maxPlatforms = 0;
        int i = 0, j = 0;

        while (i < arrival.length && j < departure.length) {
            if (arrival[i] <= departure[j]) {
                platformNeeded++;
                maxPlatforms = Math.max(maxPlatforms, platformNeeded);
                i++;
            } else {
                platformNeeded--;
                j++;
            }
        }

        return maxPlatforms;
    }

    public static void main(String[] args) {
        int[] arrival = {900, 940, 950, 1100, 1500, 1800};
        int[] departure = {910, 1200, 1120, 1130, 1900, 2000};

        System.out.println("Minimum number of platforms required = " + findMinPlatforms(arrival, departure));
    }
}
```

---

# Output:

```
Minimum number of platforms required = 3
```

---

# Explanation:

* Trains 2, 3, and 4 overlap between 9:50 and 11:20, needing 3 platforms simultaneously.

---

# Complexity:

| Aspect | Complexity           |
| ------ | -------------------- |
| Time   | O(n log n) (sorting) |
| Space  | O(1)                 |

---

### Summary:

* Sort arrivals and departures separately.
* Use two pointers to simulate trains coming and going.
* Count maximum simultaneous trains to get platform count.

---

### 🔹 **91–95: Graph Algorithms**

## 91. BFS and DFS traversal.

Here’s a detailed explanation of **BFS (Breadth-First Search)** and **DFS (Depth-First Search)** traversals in graphs, both fundamental for many interview questions.

---

# BFS (Breadth-First Search) and DFS (Depth-First Search) Traversal

---

### What are they?

* **BFS**: Explores the graph level by level, visiting all neighbors before going deeper.
* **DFS**: Explores as far as possible along each branch before backtracking.

---

# BFS (Breadth-First Search)

---

### Intuition:

* Start at a source node.
* Visit all neighbors at the current level before moving to nodes at the next level.
* Uses a **queue** data structure.

---

### Use cases:

* Shortest path in unweighted graphs.
* Level order traversal.
* Finding connected components.

---

### Steps:

1. Initialize a queue and add the starting node.
2. Mark the starting node as visited.
3. While queue is not empty:

    * Remove front node.
    * Add all its unvisited neighbors to the queue and mark them visited.

---

### BFS Code (Java):

```java
import java.util.*;

public class GraphBFS {
    private int vertices;
    private LinkedList<Integer>[] adjList;

    public GraphBFS(int v) {
        vertices = v;
        adjList = new LinkedList[v];
        for (int i = 0; i < v; i++) {
            adjList[i] = new LinkedList<>();
        }
    }

    void addEdge(int src, int dest) {
        adjList[src].add(dest);
        adjList[dest].add(src);  // For undirected graph
    }

    void BFS(int start) {
        boolean[] visited = new boolean[vertices];
        Queue<Integer> queue = new LinkedList<>();

        visited[start] = true;
        queue.add(start);

        while (!queue.isEmpty()) {
            int node = queue.poll();
            System.out.print(node + " ");

            for (int neighbor : adjList[node]) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    queue.add(neighbor);
                }
            }
        }
    }

    public static void main(String[] args) {
        GraphBFS g = new GraphBFS(5);

        g.addEdge(0, 1);
        g.addEdge(0, 2);
        g.addEdge(1, 3);
        g.addEdge(1, 4);

        System.out.println("BFS traversal starting from node 0:");
        g.BFS(0);
    }
}
```

---

# DFS (Depth-First Search)

---

### Intuition:

* Start at a source node.
* Explore as far as possible along each branch before backtracking.
* Uses **recursion** or a **stack** data structure.

---

### Use cases:

* Detecting cycles.
* Topological sorting.
* Path finding.

---

### Steps (recursive):

1. Visit the starting node and mark it visited.
2. For each unvisited neighbor, recursively do DFS.

---

### DFS Code (Java, recursive):

```java
import java.util.*;

public class GraphDFS {
    private int vertices;
    private LinkedList<Integer>[] adjList;

    public GraphDFS(int v) {
        vertices = v;
        adjList = new LinkedList[v];
        for (int i = 0; i < v; i++) {
            adjList[i] = new LinkedList<>();
        }
    }

    void addEdge(int src, int dest) {
        adjList[src].add(dest);
        adjList[dest].add(src);  // For undirected graph
    }

    void DFS(int node, boolean[] visited) {
        visited[node] = true;
        System.out.print(node + " ");

        for (int neighbor : adjList[node]) {
            if (!visited[neighbor]) {
                DFS(neighbor, visited);
            }
        }
    }

    public static void main(String[] args) {
        GraphDFS g = new GraphDFS(5);

        g.addEdge(0, 1);
        g.addEdge(0, 2);
        g.addEdge(1, 3);
        g.addEdge(1, 4);

        boolean[] visited = new boolean[5];
        System.out.println("DFS traversal starting from node 0:");
        g.DFS(0, visited);
    }
}
```

---

### DFS using Stack (iterative):

```java
void DFSIterative(int start) {
    boolean[] visited = new boolean[vertices];
    Stack<Integer> stack = new Stack<>();
    stack.push(start);

    while (!stack.isEmpty()) {
        int node = stack.pop();

        if (!visited[node]) {
            System.out.print(node + " ");
            visited[node] = true;

            for (int neighbor : adjList[node]) {
                if (!visited[neighbor]) {
                    stack.push(neighbor);
                }
            }
        }
    }
}
```

---

# Summary

| Feature          | BFS                                     | DFS                               |
| ---------------- | --------------------------------------- | --------------------------------- |
| Data Structure   | Queue                                   | Stack or Recursion                |
| Traversal Order  | Level by level                          | Deep into branch first            |
| Use Cases        | Shortest path (unweighted), level order | Cycle detection, topological sort |
| Space Complexity | O(V)                                    | O(V)                              |

---

## 92. Detect cycle in directed/undirected graph.

Detecting cycles in graphs is a classic problem, and the approach differs depending on whether the graph is **directed** or **undirected**.

---

# Cycle Detection in Graphs

---

### 1. Detect Cycle in **Undirected** Graph

---

### Intuition:

* A cycle exists if during DFS, you reach a node that has already been visited **and** is **not the parent** of the current node.
* The "parent" check is important because in undirected graphs, edges are two-way, so coming back to the immediate parent is not a cycle.

---

### Approach (DFS):

* For each unvisited node, run DFS.
* Track the parent node.
* If you visit an already visited node that is **not the parent**, then a cycle exists.

---

### Code (Java):

```java
import java.util.*;

public class CycleUndirected {
    private int vertices;
    private LinkedList<Integer>[] adjList;

    public CycleUndirected(int v) {
        vertices = v;
        adjList = new LinkedList[v];
        for (int i = 0; i < v; i++) {
            adjList[i] = new LinkedList<>();
        }
    }

    void addEdge(int src, int dest) {
        adjList[src].add(dest);
        adjList[dest].add(src);
    }

    boolean isCyclicUtil(int node, boolean[] visited, int parent) {
        visited[node] = true;

        for (int neighbor : adjList[node]) {
            if (!visited[neighbor]) {
                if (isCyclicUtil(neighbor, visited, node))
                    return true;
            } else if (neighbor != parent) {
                return true; // cycle found
            }
        }

        return false;
    }

    boolean isCyclic() {
        boolean[] visited = new boolean[vertices];

        for (int i = 0; i < vertices; i++) {
            if (!visited[i]) {
                if (isCyclicUtil(i, visited, -1))
                    return true;
            }
        }
        return false;
    }

    public static void main(String[] args) {
        CycleUndirected graph = new CycleUndirected(4);
        graph.addEdge(0, 1);
        graph.addEdge(1, 2);
        graph.addEdge(2, 3);
        graph.addEdge(3, 0); // adding cycle

        System.out.println("Graph contains cycle: " + graph.isCyclic());
    }
}
```

---

### Output:

```
Graph contains cycle: true
```

---

### 2. Detect Cycle in **Directed** Graph

---

### Intuition:

* Use DFS with 3 states for nodes:

    * **Not visited** (0)
    * **Visiting** (1) — currently in recursion stack
    * **Visited** (2) — completely processed
* If during DFS you visit a node that is **already in "Visiting" state**, it means there's a cycle.

---

### Approach (DFS + recursion stack):

* Track recursion stack to detect back edges.
* If back edge found (visiting node visited again), cycle exists.

---

### Code (Java):

```java
import java.util.*;

public class CycleDirected {
    private int vertices;
    private LinkedList<Integer>[] adjList;

    public CycleDirected(int v) {
        vertices = v;
        adjList = new LinkedList[v];
        for (int i = 0; i < v; i++) {
            adjList[i] = new LinkedList<>();
        }
    }

    void addEdge(int src, int dest) {
        adjList[src].add(dest);
    }

    boolean isCyclicUtil(int node, int[] visited) {
        // 0 = not visited, 1 = visiting, 2 = visited
        if (visited[node] == 1) return true;   // cycle found
        if (visited[node] == 2) return false;  // already processed

        visited[node] = 1; // mark as visiting

        for (int neighbor : adjList[node]) {
            if (isCyclicUtil(neighbor, visited))
                return true;
        }

        visited[node] = 2; // mark as visited
        return false;
    }

    boolean isCyclic() {
        int[] visited = new int[vertices];

        for (int i = 0; i < vertices; i++) {
            if (visited[i] == 0) {
                if (isCyclicUtil(i, visited))
                    return true;
            }
        }

        return false;
    }

    public static void main(String[] args) {
        CycleDirected graph = new CycleDirected(4);
        graph.addEdge(0, 1);
        graph.addEdge(1, 2);
        graph.addEdge(2, 3);
        graph.addEdge(3, 1); // cycle 1->2->3->1

        System.out.println("Graph contains cycle: " + graph.isCyclic());
    }
}
```

---

### Output:

```
Graph contains cycle: true
```

---

# Summary:

| Graph Type | Cycle Detection Approach                         | Key Concept                                 |
| ---------- | ------------------------------------------------ | ------------------------------------------- |
| Undirected | DFS with parent check                            | Detect visited node that’s not parent       |
| Directed   | DFS with recursion stack (3-state visited array) | Detect back edges (node in recursion stack) |

---

## 93. Topological sort (Kahn’s algorithm).

Here’s a detailed explanation of **Topological Sort** using **Kahn’s Algorithm**, a classic BFS-based approach.

---

# Topological Sort using Kahn’s Algorithm

---

### What is Topological Sort?

* It’s a linear ordering of vertices of a **Directed Acyclic Graph (DAG)** such that for every directed edge `u -> v`, vertex `u` comes before `v` in the ordering.
* Used in scheduling tasks, build systems, course prerequisites, etc.

---

### When to use?

* Only on **Directed Acyclic Graphs (DAGs)**.
* If there’s a cycle, topological sort is impossible.

---

# Kahn’s Algorithm (BFS-based approach)

---

### Intuition:

* Keep track of **in-degree** (number of incoming edges) for each vertex.
* Start with all vertices having **in-degree 0** (no dependencies).
* Remove those vertices and decrease in-degree of their neighbors.
* When neighbors’ in-degree becomes 0, add them to the queue.
* Continue until all vertices are processed.

If not all vertices get processed (i.e., queue becomes empty before processing all), then the graph has a cycle.

---

### Steps:

1. Calculate in-degree for all vertices.
2. Initialize a queue and enqueue all vertices with in-degree 0.
3. While queue is not empty:

    * Dequeue a vertex and add it to the topological order.
    * For each neighbor, decrement its in-degree.
    * If any neighbor’s in-degree becomes 0, enqueue it.
4. If topological order includes all vertices, print it; else, the graph has a cycle.

---

### Code (Java):

```java
import java.util.*;

public class KahnTopologicalSort {
    private int vertices;
    private List<Integer>[] adjList;

    public KahnTopologicalSort(int v) {
        vertices = v;
        adjList = new List[v];
        for (int i = 0; i < v; i++) {
            adjList[i] = new ArrayList<>();
        }
    }

    void addEdge(int src, int dest) {
        adjList[src].add(dest);
    }

    void topologicalSort() {
        int[] inDegree = new int[vertices];

        // Calculate in-degree for each vertex
        for (int i = 0; i < vertices; i++) {
            for (int neighbor : adjList[i]) {
                inDegree[neighbor]++;
            }
        }

        Queue<Integer> queue = new LinkedList<>();

        // Enqueue vertices with in-degree 0
        for (int i = 0; i < vertices; i++) {
            if (inDegree[i] == 0) {
                queue.add(i);
            }
        }

        int count = 0; // Count of visited vertices
        List<Integer> topOrder = new ArrayList<>();

        while (!queue.isEmpty()) {
            int node = queue.poll();
            topOrder.add(node);

            for (int neighbor : adjList[node]) {
                inDegree[neighbor]--;
                if (inDegree[neighbor] == 0) {
                    queue.add(neighbor);
                }
            }
            count++;
        }

        // Check if there was a cycle
        if (count != vertices) {
            System.out.println("Graph contains a cycle. Topological sort not possible.");
        } else {
            System.out.println("Topological order: " + topOrder);
        }
    }

    public static void main(String[] args) {
        KahnTopologicalSort graph = new KahnTopologicalSort(6);

        graph.addEdge(5, 2);
        graph.addEdge(5, 0);
        graph.addEdge(4, 0);
        graph.addEdge(4, 1);
        graph.addEdge(2, 3);
        graph.addEdge(3, 1);

        graph.topologicalSort();
    }
}
```

---

### Output:

```
Topological order: [4, 5, 0, 2, 3, 1]
```

---

### Explanation:

* Vertices 4 and 5 have in-degree 0 initially, so they start.
* Removing them updates in-degrees of neighbors.
* When neighbors’ in-degree reaches 0, they get added to queue.
* The final ordering respects all edges’ directions.

---

### Complexity:

| Aspect | Complexity |
| ------ | ---------- |
| Time   | O(V + E)   |
| Space  | O(V + E)   |

* `V` = vertices, `E` = edges

---

## 94. Dijkstra’s shortest path.

Here's a detailed explanation of **Dijkstra’s Algorithm** for finding the shortest path from a source node to all other nodes in a weighted graph with **non-negative edge weights**.

---

# Dijkstra’s Algorithm (Shortest Path)

---

### What is it?

* It finds the shortest distance from a **single source vertex** to all other vertices in a weighted graph.
* Works only for **graphs with non-negative edge weights**.
* It’s a **greedy algorithm** that picks the nearest unvisited vertex at every step.

---

### How does it work?

* Initialize distances from source to all vertices as **infinity**, except the source itself (distance = 0).
* Use a **priority queue (min-heap)** to always pick the vertex with the smallest tentative distance.
* Update the distances of the picked vertex’s neighbors if a shorter path is found through it.
* Repeat until all vertices are processed.

---

### Step-by-step:

1. Initialize a distance array `dist[]` with infinity for all vertices except source, which is 0.
2. Use a min-priority queue to pick the vertex with the smallest distance that is not finalized yet.
3. For the picked vertex `u`, update distance for each neighbor `v`:

    * If `dist[u] + weight(u,v) < dist[v]`, update `dist[v]`.
4. Mark `u` as processed.
5. Repeat until all vertices are processed or the queue is empty.

---

### Example Graph:

```
    (0)
   /   \
  4     1
 /       \
(1)-----2-(2)
  \       /
   5     3
    \   /
     (3)
```

* Edges: 0->1(4), 0->2(1), 1->2(2), 1->3(5), 2->3(3)
* Source = 0

---

### Code (Java):

```java
import java.util.*;

public class DijkstraAlgorithm {
    static class Edge {
        int dest;
        int weight;
        Edge(int d, int w) {
            dest = d;
            weight = w;
        }
    }

    public static void dijkstra(List<Edge>[] graph, int source) {
        int V = graph.length;
        int[] dist = new int[V];
        boolean[] visited = new boolean[V];

        Arrays.fill(dist, Integer.MAX_VALUE);
        dist[source] = 0;

        PriorityQueue<int[]> pq = new PriorityQueue<>(Comparator.comparingInt(a -> a[1]));
        // Elements in pq: [vertex, distance]
        pq.offer(new int[]{source, 0});

        while (!pq.isEmpty()) {
            int[] current = pq.poll();
            int u = current[0];

            if (visited[u]) continue;
            visited[u] = true;

            for (Edge edge : graph[u]) {
                int v = edge.dest;
                int weight = edge.weight;

                if (!visited[v] && dist[u] + weight < dist[v]) {
                    dist[v] = dist[u] + weight;
                    pq.offer(new int[]{v, dist[v]});
                }
            }
        }

        // Print shortest distances
        System.out.println("Vertex \t Distance from Source " + source);
        for (int i = 0; i < V; i++) {
            System.out.println(i + "\t\t" + dist[i]);
        }
    }

    public static void main(String[] args) {
        int V = 4;
        List<Edge>[] graph = new ArrayList[V];
        for (int i = 0; i < V; i++) graph[i] = new ArrayList<>();

        graph[0].add(new Edge(1, 4));
        graph[0].add(new Edge(2, 1));
        graph[1].add(new Edge(2, 2));
        graph[1].add(new Edge(3, 5));
        graph[2].add(new Edge(3, 3));

        dijkstra(graph, 0);
    }
}
```

---

### Output:

```
Vertex 	 Distance from Source 0
0		 0
1		 3
2		 1
3		 4
```

---

### Explanation:

* Start at vertex 0: distance 0.
* Neighbors: 1 (distance 4), 2 (distance 1).
* Pick vertex 2 (distance 1) next, update vertex 3 distance to 4 (1 + 3).
* Pick vertex 1 (distance 3, updated through vertex 2: 0->2->1 = 1+2=3).
* Pick vertex 3 last.

---

### Complexity:

| Aspect | Complexity                            |
| ------ | ------------------------------------- |
| Time   | O((V + E) log V) using priority queue |
| Space  | O(V + E)                              |

* `V` = number of vertices
* `E` = number of edges

---

## 95. Union Find (Disjoint Set).

Here's a detailed explanation of the **Union-Find (Disjoint Set)** data structure, which is super useful in problems involving grouping, connectivity, and detecting cycles in undirected graphs.

---

# Union Find (Disjoint Set)

---

### What is Union Find?

* A data structure that **keeps track of a set of elements partitioned into disjoint (non-overlapping) subsets**.
* Supports two main operations efficiently:

    1. **Find:** Determine which subset a particular element belongs to. This can be used to check if two elements are in the same subset.
    2. **Union:** Merge two subsets into a single subset.

---

### Why use Union Find?

* Useful in scenarios where you need to **manage connectivity** and **check if two elements are connected**.
* Classic use cases:

    * Detect cycles in an undirected graph.
    * Kruskal’s algorithm for Minimum Spanning Tree (MST).
    * Network connectivity.
    * Grouping elements.

---

### Key Concepts

* **Parent array:** Each element points to a parent. Initially, every element is its own parent (each element is a separate set).
* **Rank/Size array (optional but recommended):** To keep tree shallow, track either size or rank of each set and attach smaller tree under larger one during union.
* **Path compression:** During Find operation, flatten the structure by making every node point directly to the root.

---

### Operations:

1. **Find(x):**
   Returns the representative (root parent) of the set that element `x` belongs to.

2. **Union(x, y):**
   Joins the sets containing `x` and `y`.

---

### Example:

Suppose we have elements: 1, 2, 3, 4, 5

Initially:

* Each element is in its own set: {1}, {2}, {3}, {4}, {5}

Union(1, 2):

* Now sets are {1, 2}, {3}, {4}, {5}

Union(3, 4):

* Sets: {1, 2}, {3, 4}, {5}

Union(2, 4):

* Sets: {1, 2, 3, 4}, {5}

Find(3) → root of 3 is 1 or 2 (depending on union implementation).
Find(5) → root of 5 is 5.

---

### Java Implementation (with Path Compression and Union by Rank):

```java
public class UnionFind {
    private int[] parent;
    private int[] rank;  // Rank can be used as an approximation of tree height

    // Initialize parent and rank arrays
    public UnionFind(int n) {
        parent = new int[n];
        rank = new int[n];
        for (int i = 0; i < n; i++) {
            parent[i] = i;  // Initially, each element is its own parent
            rank[i] = 0;    // Initial rank is 0
        }
    }

    // Find with path compression
    public int find(int x) {
        if (parent[x] != x) {
            parent[x] = find(parent[x]);  // Path compression step
        }
        return parent[x];
    }

    // Union by rank
    public void union(int x, int y) {
        int rootX = find(x);
        int rootY = find(y);

        if (rootX != rootY) {
            // Attach smaller rank tree under root of higher rank tree
            if (rank[rootX] < rank[rootY]) {
                parent[rootX] = rootY;
            } else if (rank[rootX] > rank[rootY]) {
                parent[rootY] = rootX;
            } else {
                parent[rootY] = rootX;
                rank[rootX]++;
            }
        }
    }

    // Check if two elements are in the same set
    public boolean connected(int x, int y) {
        return find(x) == find(y);
    }

    public static void main(String[] args) {
        UnionFind uf = new UnionFind(6);  // Elements: 0 to 5

        uf.union(1, 2);
        uf.union(2, 3);
        uf.union(4, 5);

        System.out.println(uf.connected(1, 3));  // true
        System.out.println(uf.connected(1, 4));  // false

        uf.union(3, 4);

        System.out.println(uf.connected(1, 5));  // true (because 3 and 4 got connected)
    }
}
```

---

### Explanation of the code:

* **Initialization:** Each element is its own parent.
* **Find:** Recursively finds root parent and performs path compression by making every node point to root directly.
* **Union:** Attach smaller tree under bigger tree to keep the forest shallow.
* **Connected:** Checks if two elements share the same root.

---

### Time Complexity:

* Almost **O(1)** (amortized) per operation due to path compression and union by rank.
* For `m` operations on `n` elements, total complexity is close to **O(m α(n))**, where **α(n)** is the inverse Ackermann function (very slow growing, practically constant).

---

### Use Cases in Interviews:

* Detect cycle in an undirected graph: If union operation tries to union two nodes already connected, a cycle exists.
* Kruskal's MST: Sort edges, union sets while adding edges.
* Connected components in a graph.
* Grouping similar objects.

---

### 🔹 **96–100: Miscellaneous / Advanced**

## 96. Sliding window maximum / minimum.

Let's dive deep into the **Sliding Window Maximum/Minimum** problem, which is a classic in arrays and data structures.

---

# Sliding Window Maximum / Minimum

---

### Problem Statement:

Given an array `nums` and a sliding window size `k`, find the **maximum (or minimum)** value in each sliding window as the window moves from the start to the end of the array.

---

### Example:

For example, with array:
`nums = [1, 3, -1, -3, 5, 3, 6, 7]`, and `k = 3`,
the sliding windows and their maximum values are:

| Window       | Maximum |
| ------------ | ------- |
| \[1, 3, -1]  | 3       |
| \[3, -1, -3] | 3       |
| \[-1, -3, 5] | 5       |
| \[-3, 5, 3]  | 5       |
| \[5, 3, 6]   | 6       |
| \[3, 6, 7]   | 7       |

Output: `[3, 3, 5, 5, 6, 7]`

---

### Naive Approach:

* For every window, scan all `k` elements and find max/min.
* Time complexity: **O(N\*k)**, which is inefficient for large arrays.

---

### Efficient Approach: Using Deque (Double-Ended Queue)

---

### Key Idea:

* Use a **deque** to store indices of elements.
* Maintain the deque such that:

    * Indices in deque are in **decreasing order of their values** (for max).
    * The front of the deque always holds the index of the max element for the current window.
* As you slide the window:

    * Remove elements out of the window from the front.
    * Remove smaller elements from the back (because they can't be the maximum if a bigger element comes after).
* This gives **O(N)** time complexity.

---

### Step-by-step explanation:

* Traverse the array once.
* For every element:

    1. Remove indices from the back whose values are smaller than or equal to the current element (for max).
    2. Add current element's index at the back.
    3. Remove the front element if it is out of the current window.
    4. Once we reach the window size `k`, the front of the deque is the max for that window.

---

### Java Code (Sliding Window Maximum):

```java
import java.util.*;

public class SlidingWindowMaximum {
    public static int[] maxSlidingWindow(int[] nums, int k) {
        if (nums == null || k <= 0) return new int[0];
        int n = nums.length;
        int[] result = new int[n - k + 1];
        Deque<Integer> deque = new LinkedList<>();  // stores indices
        
        for (int i = 0; i < n; i++) {
            // Remove indices out of current window
            while (!deque.isEmpty() && deque.peekFirst() < i - k + 1) {
                deque.pollFirst();
            }
            
            // Remove smaller values from the back
            while (!deque.isEmpty() && nums[deque.peekLast()] <= nums[i]) {
                deque.pollLast();
            }
            
            // Add current index
            deque.offerLast(i);
            
            // Starting to add results from i = k-1
            if (i >= k - 1) {
                result[i - k + 1] = nums[deque.peekFirst()];
            }
        }
        
        return result;
    }
    
    public static void main(String[] args) {
        int[] nums = {1, 3, -1, -3, 5, 3, 6, 7};
        int k = 3;
        int[] maxValues = maxSlidingWindow(nums, k);
        System.out.println(Arrays.toString(maxValues));  // Output: [3, 3, 5, 5, 6, 7]
    }
}
```

---

### To find **Sliding Window Minimum**:

* Change the comparison in step 2:

    * Remove indices from the back whose values are **greater than or equal** to the current element.
* The rest of the logic stays the same.

---

### Why is this O(N)?

* Each element is added to the deque once.
* Each element is removed at most once.
* So total operations = 2N = O(N).

---

### Summary:

| Approach    | Time Complexity | Space Complexity |
| ----------- | --------------- | ---------------- |
| Naive       | O(N\*k)         | O(1)             |
| Deque-based | O(N)            | O(k)             |

---

## 97. Trapping rainwater.

Here's a detailed explanation of the **Trapping Rain Water** problem, a classic and frequently asked interview question in Data Structures & Algorithms.

---

# Trapping Rain Water Problem

---

### Problem Statement:

Given an array of non-negative integers representing the elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.

---

### Example:

```
Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
```

Explanation:
The water trapped is 6 units between the bars as shown below:

```
|       |  
|   |~~~| |  
| | | |~| |  
|_|_|_|_|_|  
0 1 0 2 1 0 1 3 2 1 2 1
```

`~` represents trapped water.

---

### Intuition:

* Water trapped at any position depends on the **maximum height of bars to the left** and **maximum height of bars to the right**.
* Water trapped at `i` = `min(max_left[i], max_right[i]) - height[i]`
* We sum this up for all positions.

---

### Approaches:

---

### 1. Brute Force (O(N²)):

* For each element, find max height on left and right.
* Water trapped = `min(max_left, max_right) - height[i]`.
* Time: O(N²), Space: O(1).

---

### 2. Dynamic Programming (Prefix & Suffix arrays) (O(N)):

* Precompute:

    * `max_left[i]`: max height to the left of `i` (including `i`).
    * `max_right[i]`: max height to the right of `i` (including `i`).
* Calculate trapped water at each index using the formula above.
* Time: O(N), Space: O(N).

---

### 3. Two Pointer Approach (Optimal, O(N) time and O(1) space):

* Use two pointers `left` and `right`.
* Maintain variables `left_max` and `right_max`.
* Move pointers inward from both ends.
* At each step, calculate trapped water based on `left_max` and `right_max`.

---

### Detailed Explanation of Two Pointer Approach:

* Initialize `left = 0`, `right = n-1`.
* Initialize `left_max = 0`, `right_max = 0`, `water = 0`.
* While `left < right`:

    * If `height[left] < height[right]`:

        * If `height[left] >= left_max`, update `left_max = height[left]`.
        * Else, add `left_max - height[left]` to water.
        * Move `left++`.
    * Else:

        * If `height[right] >= right_max`, update `right_max = height[right]`.
        * Else, add `right_max - height[right]` to water.
        * Move `right--`.
* Return `water`.

---

### Java Code (Two Pointer approach):

```java
public class TrappingRainWater {
    public static int trap(int[] height) {
        int left = 0, right = height.length - 1;
        int left_max = 0, right_max = 0;
        int water = 0;

        while (left < right) {
            if (height[left] < height[right]) {
                if (height[left] >= left_max) {
                    left_max = height[left];
                } else {
                    water += left_max - height[left];
                }
                left++;
            } else {
                if (height[right] >= right_max) {
                    right_max = height[right];
                } else {
                    water += right_max - height[right];
                }
                right--;
            }
        }

        return water;
    }

    public static void main(String[] args) {
        int[] height = {0,1,0,2,1,0,1,3,2,1,2,1};
        System.out.println("Trapped water: " + trap(height));  // Output: 6
    }
}
```

---

### Explanation:

* We always move the pointer with the smaller height, because the trapped water depends on the smaller side.
* We keep track of the max height on both ends.
* When the current height is less than max height on that side, water can be trapped.

---

### Time & Space Complexity:

| Approach           | Time Complexity | Space Complexity |
| ------------------ | --------------- | ---------------- |
| Brute Force        | O(N²)           | O(1)             |
| DP (prefix/suffix) | O(N)            | O(N)             |
| Two Pointer        | O(N)            | O(1)             |

---

## 98. Largest rectangle of 1s in a matrix.

Let’s explore the **Largest Rectangle of 1s in a Binary Matrix** problem in detail, which is an important and common question combining arrays, stacks, and matrix concepts.

---

# Largest Rectangle of 1s in a Binary Matrix

---

### Problem Statement:

Given a 2D binary matrix filled with 0s and 1s, find the largest rectangle containing only 1s and return its area.

---

### Example:

```
Input:
[
  [1, 0, 1, 0, 0],
  [1, 0, 1, 1, 1],
  [1, 1, 1, 1, 1],
  [1, 0, 0, 1, 0]
]

Output: 6
```

Explanation:
The largest rectangle of 1s has area 6, formed by the 3rd row, columns 1 to 5 (1-indexed).

---

### Intuition:

* This problem is an extension of **Largest Rectangle in Histogram**.
* Each row in the matrix can be seen as a histogram of heights representing continuous 1s stacked vertically.
* We can convert each row into a histogram and then use the Largest Rectangle in Histogram solution on it.

---

### Step-by-step Approach:

1. **Convert each row into a histogram:**

    * For each cell `(i,j)` in the matrix, if `matrix[i][j] == 1`, then:

        * `heights[j] = heights[j] + 1` (increment height)
    * Else:

        * `heights[j] = 0`
2. **For each row histogram, calculate the largest rectangle area (using stack)**

    * Use the classic Largest Rectangle in Histogram algorithm.
3. **Keep track of the maximum area from all rows**

---

### Largest Rectangle in Histogram (Brief Recap):

* Use a stack to store indices of bars.
* Bars are kept in increasing order of heights.
* When a bar of smaller height comes, calculate areas with the bars popped from the stack.
* Calculate area for each popped bar as height \* width, where width is calculated using indices.
* Time complexity is O(N) for each histogram.

---

### Code Implementation (Java):

```java
import java.util.Stack;

public class LargestRectangle1s {
    // Function to calculate largest rectangle in histogram
    public static int largestRectangleArea(int[] heights) {
        Stack<Integer> stack = new Stack<>();
        int maxArea = 0;
        int n = heights.length;
        
        for (int i = 0; i <= n; i++) {
            int currentHeight = (i == n) ? 0 : heights[i];
            while (!stack.isEmpty() && currentHeight < heights[stack.peek()]) {
                int height = heights[stack.pop()];
                int width = stack.isEmpty() ? i : i - stack.peek() - 1;
                maxArea = Math.max(maxArea, height * width);
            }
            stack.push(i);
        }
        return maxArea;
    }

    // Main function to calculate max rectangle of 1s in matrix
    public static int maximalRectangle(int[][] matrix) {
        if (matrix.length == 0) return 0;

        int maxArea = 0;
        int[] heights = new int[matrix[0].length];
        
        for (int i = 0; i < matrix.length; i++) {
            // Build the histogram for this row
            for (int j = 0; j < matrix[0].length; j++) {
                if (matrix[i][j] == 1) {
                    heights[j] += 1;
                } else {
                    heights[j] = 0;
                }
            }
            // Calculate largest rectangle for this histogram
            maxArea = Math.max(maxArea, largestRectangleArea(heights));
        }
        
        return maxArea;
    }

    public static void main(String[] args) {
        int[][] matrix = {
            {1, 0, 1, 0, 0},
            {1, 0, 1, 1, 1},
            {1, 1, 1, 1, 1},
            {1, 0, 0, 1, 0}
        };

        System.out.println("Largest rectangle of 1s: " + maximalRectangle(matrix));  // Output: 6
    }
}
```

---

### Explanation:

* We treat each row as a histogram.
* For each row:

    * Update heights array.
    * Find largest rectangle in that histogram.
* Keep track of the max area found.

---

### Complexity:

| Operation                                | Time Complexity | Space Complexity |
| ---------------------------------------- | --------------- | ---------------- |
| Updating heights array                   | O(M \* N)       | O(N)             |
| Largest rectangle in histogram (per row) | O(M \* N)       | O(N)             |
| **Overall**                              | **O(M \* N)**   | **O(N)**         |

Where `M` = number of rows, `N` = number of columns.

---

## 99. Trie implementation (insert/search).

Let's dive into **Trie** (also called prefix tree) — a fundamental data structure especially useful for storing and searching strings efficiently, often used in autocomplete, spell-check, and prefix matching problems.

---

# Trie Implementation: Insert and Search

---

### What is a Trie?

* A Trie is a tree-like data structure used to store collections of strings.
* Each node represents a character.
* Paths from root to a node represent prefixes or complete words.
* Enables efficient prefix-based search.

---

### Basic Structure:

Each Trie node typically contains:

* An array (or map) of child nodes (for next characters).
* A boolean flag to mark the end of a valid word.

---

### Operations:

* **Insert:** Add a word to the trie.
* **Search:** Check if a word exists in the trie.

---

### Java Implementation:

```java
class TrieNode {
    TrieNode[] children;
    boolean isEndOfWord;

    public TrieNode() {
        children = new TrieNode[26];  // assuming only lowercase a-z
        isEndOfWord = false;
    }
}

public class Trie {
    private TrieNode root;

    public Trie() {
        root = new TrieNode();
    }

    // Insert a word into the Trie
    public void insert(String word) {
        TrieNode node = root;
        for (char c : word.toCharArray()) {
            int index = c - 'a';
            if (node.children[index] == null) {
                node.children[index] = new TrieNode();
            }
            node = node.children[index];
        }
        node.isEndOfWord = true;
    }

    // Search for a word in the Trie
    public boolean search(String word) {
        TrieNode node = root;
        for (char c : word.toCharArray()) {
            int index = c - 'a';
            if (node.children[index] == null) {
                return false;
            }
            node = node.children[index];
        }
        return node.isEndOfWord;
    }

    // Optional: Check if there is any word in the trie that starts with the given prefix
    public boolean startsWith(String prefix) {
        TrieNode node = root;
        for (char c : prefix.toCharArray()) {
            int index = c - 'a';
            if (node.children[index] == null) {
                return false;
            }
            node = node.children[index];
        }
        return true;
    }

    public static void main(String[] args) {
        Trie trie = new Trie();

        trie.insert("apple");
        System.out.println(trie.search("apple"));   // true
        System.out.println(trie.search("app"));     // false
        System.out.println(trie.startsWith("app")); // true

        trie.insert("app");
        System.out.println(trie.search("app"));     // true
    }
}
```

---

### Explanation:

* **Insert:**
  We iterate through each character of the word. For each character, we check if the corresponding child exists. If not, create a new node. Move down to the child node. After the last character, mark `isEndOfWord = true`.

* **Search:**
  Iterate through each character and traverse the Trie. If at any point child node is missing, word doesn't exist. After traversal, check if the node marks end of a word.

* **startsWith:** (Optional) Checks if any word in Trie starts with a given prefix.

---

### Complexity:

| Operation | Time Complexity | Explanation                                                 |
| --------- | --------------- | ----------------------------------------------------------- |
| Insert    | O(L)            | L = length of the word                                      |
| Search    | O(L)            | Same as above                                               |
| Space     | O(AL \* N)      | A = alphabet size, L = avg word length, N = number of words |

---

## 100. Bit manipulation tricks (check odd/even, swap bits, count set bits).

Bit manipulation is a powerful technique in programming that helps solve problems efficiently by directly working on bits. Here are some essential **bit manipulation tricks** with explanations and examples in Java.

---

# Bit Manipulation Tricks

---

### 1. Check if a number is **Odd or Even**

* **Odd number:** The least significant bit (LSB) is 1.
* **Even number:** The LSB is 0.

**How?**
Use bitwise AND (`&`) with `1`:

```java
boolean isOdd(int num) {
    return (num & 1) == 1;
}

boolean isEven(int num) {
    return (num & 1) == 0;
}
```

**Example:**

```java
int x = 7; // binary 0111
System.out.println(isOdd(x));  // true
System.out.println(isEven(x)); // false
```

---

### 2. Swap two numbers without using a temporary variable (using XOR)

**XOR trick:**

```java
void swap(int a, int b) {
    a = a ^ b;
    b = a ^ b;  // b = (a ^ b) ^ b = a
    a = a ^ b;  // a = (a ^ b) ^ a = b
    System.out.println("a = " + a + ", b = " + b);
}
```

**Explanation:**

* XORing a number twice with the same number restores the original number.
* So this sequence swaps values without extra space.

---

### 3. Count the number of set bits (1s) in an integer

There are multiple ways:

#### a. Simple method — check each bit (O(log n)):

```java
int countSetBits(int num) {
    int count = 0;
    while (num != 0) {
        count += (num & 1);
        num >>= 1;  // right shift by 1 bit
    }
    return count;
}
```

#### b. Brian Kernighan’s Algorithm (faster, O(set bits)):

```java
int countSetBits(int num) {
    int count = 0;
    while (num != 0) {
        num = num & (num - 1);  // drops the lowest set bit
        count++;
    }
    return count;
}
```

**Explanation:**
`num & (num-1)` clears the rightmost set bit, so the loop runs only as many times as there are set bits.

---

### 4. Other useful bit tricks:

* **Get the rightmost set bit:**

```java
int rightmostSetBit = num & (-num);
```

* **Check if a number is a power of two:**

```java
boolean isPowerOfTwo(int num) {
    return num > 0 && (num & (num - 1)) == 0;
}
```

* **Toggle a bit at position `pos`:**

```java
num = num ^ (1 << pos);
```

---

### Summary Table:

| Task                  | Bit Operation                       | Explanation                      |
| --------------------- | ----------------------------------- | -------------------------------- |
| Check odd/even        | `(num & 1)`                         | LSB 1 means odd                  |
| Swap two numbers      | `a ^= b; b ^= a; a ^= b;`           | XOR swapping                     |
| Count set bits        | Brian Kernighan's: `num &= (num-1)` | Clears rightmost set bit         |
| Get rightmost set bit | `num & (-num)`                      | Isolates lowest set bit          |
| Check power of two    | `(num & (num-1)) == 0`              | Only one bit set for powers of 2 |

---