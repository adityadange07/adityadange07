Sure, Aditya! Here's a **complete set of the Top 100 Data Structures and Algorithms (DSA) Interview Questions**, tailored for someone with **3–5 years of experience**. These questions cover:

✅ Arrays  
✅ Strings  
✅ Linked Lists  
✅ Stacks & Queues  
✅ Trees  
✅ Graphs  
✅ Recursion & Backtracking  
✅ Dynamic Programming  
✅ Greedy Algorithms  
✅ Searching & Sorting  
✅ Hashing  
✅ Bit Manipulation  
✅ Heaps & Tries  
✅ Sliding Window & Two Pointers  
✅ Time/Space Complexity

---

## ✅ Top 100 DSA Interview Questions

---

### 🔹 **1–15: Arrays & Matrix**

## 1. Find the missing number in an array of 1 to N.

To find the **missing number** in an array of integers from 1 to `N`, you can use the **sum formula** approach. Here’s the logic:

---

### 🔢 **Approach**:
- The sum of first `N` natural numbers is:
  \[
  \text{Sum} = \frac{N \cdot (N + 1)}{2}
  \]
- Subtract the sum of the array elements from the expected sum to get the missing number.

---

### ✅ **Example**:
Suppose `arr = [1, 2, 4, 5]`, and `N = 5`.

- Expected sum: \( \frac{5 \cdot (5 + 1)}{2} = 15 \)
- Actual sum of array: \(1 + 2 + 4 + 5 = 12\)
- Missing number: \(15 - 12 = 3\)

---

### 💻 **Java Code**:
```java
public class MissingNumberFinder {
    public static int findMissingNumber(int[] arr, int n) {
        int expectedSum = n * (n + 1) / 2;
        int actualSum = 0;
        for (int num : arr) {
            actualSum += num;
        }
        return expectedSum - actualSum;
    }

    public static void main(String[] args) {
        int[] arr = {1, 2, 4, 5}; // Missing 3
        int n = 5;
        int missingNumber = findMissingNumber(arr, n);
        System.out.println("Missing number is: " + missingNumber);
    }
}
```

---

If you'd like to see this in **JavaScript**, **Python**, or want a solution that works with unsorted arrays or uses XOR, let me know!

---

## 2. Find the duplicate number in an array.

To find the **duplicate number** in an array where:

- The array contains `n + 1` integers.
- Each integer is between `1` and `n`.
- Only **one number is duplicated**, but it may appear more than once.

There are several ways to solve it, but the most efficient is **Floyd's Tortoise and Hare (Cycle Detection)** — **no modification**, **constant space**, and **O(n)** time.

---

### 🧠 **Concept**:
Treat the array as a linked list:
- Value at each index points to the next index.
- Due to the duplicate, there’s a cycle (loop).
- Use Floyd’s Cycle Detection to find the entrance to the loop — that’s your duplicate.

---

### ✅ **Example**:
Let `arr = [3, 1, 3, 4, 2]`  
Numbers range from 1 to 4, size = 5 → `n = 4`, but 5 elements → duplicate exists.  
Duplicate = `3`

---

### 💻 **Java Code (Floyd’s Algorithm)**:
```java
public class DuplicateNumberFinder {
    public static int findDuplicate(int[] nums) {
        int slow = nums[0];
        int fast = nums[0];

        // Phase 1: Find intersection point
        do {
            slow = nums[slow];
            fast = nums[nums[fast]];
        } while (slow != fast);

        // Phase 2: Find entrance to the cycle
        slow = nums[0];
        while (slow != fast) {
            slow = nums[slow];
            fast = nums[fast];
        }

        return slow;
    }

    public static void main(String[] args) {
        int[] arr = {3, 1, 3, 4, 2};
        int duplicate = findDuplicate(arr);
        System.out.println("Duplicate number is: " + duplicate);
    }
}
```

---

### 🧪 **Other Methods** (Optional):
1. **HashSet** – O(n) time, O(n) space.
2. **Sort & Check Adjacent** – O(n log n) time, O(1) space.
3. **Frequency Count (index marking)** – works if you can modify the array.

---

Let me know if you want these alternate versions or JavaScript/Python code too!

---

## 3. Kadane's Algorithm (Maximum Subarray Sum).

Kadane's Algorithm is a **dynamic programming** approach to find the **maximum subarray sum** in an array — meaning the largest sum of any contiguous subarray.

---

### 🧠 **Key Idea**:
At each index, you decide:
- Either start a **new subarray** at the current element.
- Or **extend** the previous subarray by adding the current element.

You track:
- `currentSum`: Maximum subarray sum **ending at the current index**.
- `maxSum`: Overall **maximum subarray sum** found so far.

---

### ✅ **Example**:
Input: `arr = [-2, 1, -3, 4, -1, 2, 1, -5, 4]`  
Output: `6`  
Explanation: Subarray `[4, -1, 2, 1]` gives the maximum sum.

---

### 💻 **Java Code**:
```java
public class KadanesAlgorithm {
    public static int maxSubArraySum(int[] nums) {
        int currentSum = nums[0];
        int maxSum = nums[0];

        for (int i = 1; i < nums.length; i++) {
            // Either start new or extend previous subarray
            currentSum = Math.max(nums[i], currentSum + nums[i]);
            maxSum = Math.max(maxSum, currentSum);
        }

        return maxSum;
    }

    public static void main(String[] args) {
        int[] arr = {-2, 1, -3, 4, -1, 2, 1, -5, 4};
        int maxSum = maxSubArraySum(arr);
        System.out.println("Maximum subarray sum is: " + maxSum);
    }
}
```

---

### 🕓 **Time Complexity**: `O(n)`
### 📦 **Space Complexity**: `O(1)` (no extra space)

---

Let me know if you want:
- The version that also **returns the subarray itself** (not just the sum)
- Kadane’s in **JavaScript** or **Python**
- Visual explanation with tracing

Happy to dive deeper!

---

## 4. Merge two sorted arrays.

To **merge two sorted arrays** into a single sorted array, you can use a **two-pointer technique** — it's efficient and clean.

---

### ✅ **Example**:

```java
arr1 = {1, 3, 5, 7}
arr2 = {2, 4, 6, 8}
Output: {1, 2, 3, 4, 5, 6, 7, 8}
```

---

### 💻 **Java Code** (Two-pointer approach):

```java
import java.util.Arrays;

public class MergeSortedArrays {
    public static int[] mergeSortedArrays(int[] arr1, int[] arr2) {
        int n1 = arr1.length, n2 = arr2.length;
        int[] merged = new int[n1 + n2];

        int i = 0, j = 0, k = 0;

        // Compare elements from both arrays and add the smaller one
        while (i < n1 && j < n2) {
            if (arr1[i] <= arr2[j]) {
                merged[k++] = arr1[i++];
            } else {
                merged[k++] = arr2[j++];
            }
        }

        // Copy any remaining elements
        while (i < n1) {
            merged[k++] = arr1[i++];
        }

        while (j < n2) {
            merged[k++] = arr2[j++];
        }

        return merged;
    }

    public static void main(String[] args) {
        int[] arr1 = {1, 3, 5, 7};
        int[] arr2 = {2, 4, 6, 8};
        int[] result = mergeSortedArrays(arr1, arr2);
        System.out.println("Merged array: " + Arrays.toString(result));
    }
}
```

---

### 🕓 Time Complexity: `O(n + m)`
### 📦 Space Complexity: `O(n + m)` — due to the merged array

---

Let me know if you'd like:
- **In-place merge** (if extra space is not allowed)
- **JavaScript/Python** version
- Merging in **descending order**

I'm happy to help further!

---

## 5. Rotate array by K positions.

Rotating an array by `K` positions means shifting the elements **to the right** (or left) `K` times. Let’s go with **right rotation** by default.

---

### ✅ **Example**:
```java
arr = [1, 2, 3, 4, 5, 6, 7], k = 3  
Output: [5, 6, 7, 1, 2, 3, 4]
```

---

### 💡 **Optimal Approach**: Using **Reversal Algorithm**
Steps to rotate **right by K**:
1. Reverse the whole array
2. Reverse the first K elements
3. Reverse the remaining N-K elements

---

### 💻 **Java Code**:
```java
import java.util.Arrays;

public class RotateArray {
    // Helper method to reverse a part of the array
    public static void reverse(int[] arr, int start, int end) {
        while (start < end) {
            int temp = arr[start];
            arr[start++] = arr[end];
            arr[end--] = temp;
        }
    }

    // Rotate array to the right by k positions
    public static void rotate(int[] arr, int k) {
        int n = arr.length;
        k = k % n; // Handle if k > n

        // Step 1: Reverse the whole array
        reverse(arr, 0, n - 1);

        // Step 2: Reverse first k elements
        reverse(arr, 0, k - 1);

        // Step 3: Reverse remaining elements
        reverse(arr, k, n - 1);
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

### 🕓 Time Complexity: `O(n)`
### 📦 Space Complexity: `O(1)` (in-place)

---

Would you like the version for **left rotation**, or in **JavaScript/Python** too?

---

## 6. Find all pairs with a given sum.

To **find all pairs in an array that sum up to a given value `target`**, the most efficient way is using a **HashSet** for **O(n)** time complexity.

---

### ✅ **Example**:

```java
arr = [2, 4, 3, 5, 7, 8, 9]
target = 10

Output pairs: (2,8), (3,7), (5,5)
```

---

### 💻 **Java Code (Using HashSet)**:
```java
import java.util.*;

public class PairWithSum {
    public static void findPairs(int[] arr, int target) {
        Set<Integer> seen = new HashSet<>();
        Set<String> printed = new HashSet<>(); // To avoid duplicate pairs

        for (int num : arr) {
            int complement = target - num;
            if (seen.contains(complement)) {
                // Ensure pair like (2, 8) and (8, 2) aren't repeated
                int min = Math.min(num, complement);
                int max = Math.max(num, complement);
                String pair = min + "," + max;

                if (!printed.contains(pair)) {
                    System.out.println("(" + min + ", " + max + ")");
                    printed.add(pair);
                }
            }
            seen.add(num);
        }
    }

    public static void main(String[] args) {
        int[] arr = {2, 4, 3, 5, 7, 8, 9};
        int target = 10;

        System.out.println("Pairs with sum " + target + ":");
        findPairs(arr, target);
    }
}
```

---

### 🕓 Time Complexity: `O(n)`
### 📦 Space Complexity: `O(n)` due to `HashSet`

---

### 🧪 Bonus Options:
- Want to allow duplicate elements like `(5,5)`?
- Want all **indices** of the pairs instead of values?
- Want a version in **JavaScript or Python**?

Let me know and I’ll tailor it!

---

## 7. Two Sum problem.

The **Two Sum** problem is a classic interview question. Here's the standard version:

---

### ✅ **Problem Statement**:

> Given an array of integers `nums` and an integer `target`, return the **indices** of the two numbers such that they add up to `target`.

- Each input will have **exactly one solution**
- You **may not use the same element twice**

---

### 🧠 **Optimal Approach (HashMap)**:
- Use a HashMap to store the number and its index.
- For each element, check if `target - current` exists in the map.

---

### 💻 **Java Code**:
```java
import java.util.*;

public class TwoSumSolution {
    public static int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();

        for (int i = 0; i < nums.length; i++) {
            int complement = target - nums[i];

            if (map.containsKey(complement)) {
                return new int[] { map.get(complement), i };
            }

            map.put(nums[i], i);
        }

        // If no solution found
        throw new IllegalArgumentException("No two sum solution");
    }

    public static void main(String[] args) {
        int[] nums = {2, 7, 11, 15};
        int target = 9;
        int[] result = twoSum(nums, target);
        System.out.println("Indices: " + result[0] + ", " + result[1]);
    }
}
```

---

### 🕓 Time Complexity: `O(n)`
### 📦 Space Complexity: `O(n)`

---

### 🧪 Example:
```java
nums = [2, 7, 11, 15], target = 9  
Output: [0, 1] // because nums[0] + nums[1] = 2 + 7 = 9
```

---

Want:
- A version that returns the **pair values** instead of indices?
- A **brute force** or **sorting-based** solution?
- **JavaScript/Python** version?

Just say the word 😎

---

## 8. Find the majority element (Boyer-Moore Voting).

Great choice! The **Boyer-Moore Voting Algorithm** is a smart and efficient way to find the **majority element** in an array — the element that appears **more than ⌊n/2⌋ times**.

---

### ✅ **Problem Statement**:
> Given an array `nums`, return the **majority element**.  
> It's guaranteed that a majority element **always exists**.

---

### 💡 **Intuition**:
- Maintain a `count` and a `candidate`.
- If `count` is 0 → pick current element as `candidate`.
- If the current element equals `candidate` → increment count.
- Else → decrement count.

At the end, the `candidate` will be the majority element.

---

### 🧠 Why It Works:
- Because the majority element appears more than all others **combined**, it "outvotes" all others during cancellation.

---

### 💻 **Java Code** (Boyer-Moore Voting Algorithm):
```java
public class MajorityElementFinder {
    public static int majorityElement(int[] nums) {
        int count = 0, candidate = 0;

        for (int num : nums) {
            if (count == 0) {
                candidate = num;
            }
            count += (num == candidate) ? 1 : -1;
        }

        return candidate;
    }

    public static void main(String[] args) {
        int[] nums = {2, 2, 1, 1, 1, 2, 2};
        int result = majorityElement(nums);
        System.out.println("Majority Element is: " + result);
    }
}
```

---

### 🕓 Time Complexity: `O(n)`
### 📦 Space Complexity: `O(1)`

---

### 🔒 If it’s **not guaranteed** that a majority exists:
You should do a **second pass** to verify the `candidate` count exceeds `n/2`.

Let me know if you’d like:
- The version **with verification**
- **JavaScript/Python** version
- A version to find elements that appear **more than ⌊n/3⌋ times** (extended Boyer-Moore)

I got you!

---

## 9. Rearrange array in alternating positive and negative numbers.

Nice! Rearranging an array in **alternating positive and negative numbers** is a common coding interview question.

---

### ✅ **Problem Statement**:

Given an array of `n` elements (positive & negative), rearrange it so that:
- Elements appear in **alternating positive and negative order**
- If there are extra positives/negatives, place them at the **end**

---

### 🧪 **Example**:

```java
Input:  [1, 2, 3, -4, -1, 4]
Output: [-4, 1, -1, 2, 3, 4]

Input:  [-5, -2, 5, 2, 4, 7, 1, 8, 0, -8]
Output: [-5, 5, -2, 2, -8, 4, 7, 1, 8, 0]
```

---

### 💡 **Approach**:
1. **Separate** positive and negative numbers.
2. **Merge** them alternatively.
3. If one list is longer, append remaining elements.

---

### 💻 **Java Code**:
```java
import java.util.*;

public class AlternatePosNeg {
    public static void rearrange(int[] arr) {
        List<Integer> pos = new ArrayList<>();
        List<Integer> neg = new ArrayList<>();

        // Step 1: Separate positives and negatives
        for (int num : arr) {
            if (num >= 0)
                pos.add(num);
            else
                neg.add(num);
        }

        int i = 0, p = 0, n = 0;

        // Step 2: Fill alternately
        while (p < pos.size() && n < neg.size()) {
            arr[i++] = neg.get(n++);
            arr[i++] = pos.get(p++);
        }

        // Step 3: Append remaining positives
        while (p < pos.size()) {
            arr[i++] = pos.get(p++);
        }

        // Step 3: Append remaining negatives
        while (n < neg.size()) {
            arr[i++] = neg.get(n++);
        }
    }

    public static void main(String[] args) {
        int[] arr = {1, 2, 3, -4, -1, 4};
        rearrange(arr);
        System.out.println("Rearranged Array: " + Arrays.toString(arr));
    }
}
```

---

### 🕓 Time Complexity: `O(n)`
### 📦 Space Complexity: `O(n)` due to extra lists

---

### 🔧 Want an in-place version?
It's trickier (requires rotation or swapping), but I can provide that too!

Let me know if you want:
- In-place version (no extra space)
- JavaScript/Python version
- Strictly alternating starting with **positive** or **negative**

Just say the word!

---

## 10. Sort 0s, 1s, and 2s (Dutch National Flag).

Ah yes — the classic **Dutch National Flag problem**, perfect for interviews like Amazon, Google, etc. 🌈

---

### ✅ **Problem Statement**:
Given an array containing only `0s`, `1s`, and `2s`, sort the array **in-place** so that all 0s come first, followed by 1s, then 2s.

---

### 🧠 **Optimal Solution**:
Use **3 pointers**:
- `low`: for 0s
- `mid`: current element
- `high`: for 2s

---

### 💡 **Logic**:
- If `arr[mid] == 0`: swap with `low`, move both `low` and `mid` forward
- If `arr[mid] == 1`: just move `mid`
- If `arr[mid] == 2`: swap with `high`, move `high` backward

---

### 💻 **Java Code (Dutch National Flag Algorithm)**:
```java
import java.util.Arrays;

public class SortColors {
    public static void sortColors(int[] arr) {
        int low = 0, mid = 0, high = arr.length - 1;

        while (mid <= high) {
            if (arr[mid] == 0) {
                swap(arr, low++, mid++);
            } else if (arr[mid] == 1) {
                mid++;
            } else { // arr[mid] == 2
                swap(arr, mid, high--);
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
        System.out.println("Sorted array: " + Arrays.toString(arr));
    }
}
```

---

### 🕓 Time Complexity: `O(n)`
### 📦 Space Complexity: `O(1)` (in-place)

---

### ✅ Output:
```
Sorted array: [0, 0, 1, 1, 2, 2]
```

---

Let me know if you want:
- JavaScript or Python version
- A version where the array contains **any 3 distinct elements**, not just 0s, 1s, 2s
- Tracing example step by step

I'm here for it!

---

## 11. Subarray with given sum (Sliding Window).

Great pick! This is a classic **sliding window** problem — especially when the array contains **only positive integers**.

---

### ✅ **Problem Statement**:

> Given an array of **positive integers** and a `target sum`, find a **contiguous subarray** that adds up to the target.

---

### 🧪 **Example**:

```java
Input:  arr = [1, 4, 20, 3, 10, 5], target = 33  
Output: Subarray found from index 2 to 4 (20 + 3 + 10)

Input:  arr = [1, 4, 0, 0, 3, 10, 5], target = 7  
Output: Subarray found from index 1 to 4 (4 + 0 + 0 + 3)

Input:  arr = [1, 4], target = 0  
Output: No subarray found
```

---

### 💡 **Approach (Sliding Window)**:
- Start with a window from index `0`.
- Expand `right` pointer and keep adding elements to `currentSum`.
- If `currentSum` > target → shrink window from the left (`left++`).
- Stop if `currentSum == target`.

---

### 💻 **Java Code**:
```java
public class SubarraySum {
    public static void findSubarray(int[] arr, int target) {
        int left = 0, currentSum = 0;

        for (int right = 0; right < arr.length; right++) {
            currentSum += arr[right];

            // Shrink the window from the left while sum is too big
            while (currentSum > target && left <= right) {
                currentSum -= arr[left++];
            }

            // Check if current sum equals target
            if (currentSum == target) {
                System.out.println("Subarray found from index " + left + " to " + right);
                return;
            }
        }

        System.out.println("No subarray with the given sum found.");
    }

    public static void main(String[] args) {
        int[] arr = {1, 4, 20, 3, 10, 5};
        int target = 33;
        findSubarray(arr, target);
    }
}
```

---

### 🕓 Time Complexity: `O(n)`
### 📦 Space Complexity: `O(1)`

---

### ⚠️ Notes:
- This works **only for positive integers**.
- For arrays with **negative numbers**, you'll need a **HashMap approach** (prefix sum).

---

Need that version too? Or a version that **returns the subarray** instead of just indices?

Let me know how deep you wanna go 😎

---

## 12. Maximum product subarray.

🔥 Let's tackle the **Maximum Product Subarray** — a popular dynamic programming question asked in interviews at Amazon, Microsoft, and Google.

---

### ✅ **Problem Statement**:

> Given an integer array `nums`, find the **contiguous subarray** within the array (containing at least one number) which has the **largest product**.

---

### 🧪 **Example**:

```java
Input: nums = [2, 3, -2, 4]  
Output: 6  → (subarray [2, 3])

Input: nums = [-2, 0, -1]  
Output: 0  → (subarray [0])
```

---

### 💡 **Key Insight**:

Unlike the **Maximum Subarray Sum** (Kadane's Algorithm), the product can flip due to **negative numbers**, so:

- Track both:
    - `maxEndingHere` — max product ending at current position
    - `minEndingHere` — min product ending at current position  
      (because a **negative × negative** could become the new max)

---

### 💻 **Java Code**:

```java
public class MaxProductSubarray {
    public static int maxProduct(int[] nums) {
        int maxProd = nums[0];
        int maxEndingHere = nums[0];
        int minEndingHere = nums[0];

        for (int i = 1; i < nums.length; i++) {
            int current = nums[i];

            if (current < 0) {
                // Swap max and min when multiplied by a negative number
                int temp = maxEndingHere;
                maxEndingHere = minEndingHere;
                minEndingHere = temp;
            }

            maxEndingHere = Math.max(current, current * maxEndingHere);
            minEndingHere = Math.min(current, current * minEndingHere);

            maxProd = Math.max(maxProd, maxEndingHere);
        }

        return maxProd;
    }

    public static void main(String[] args) {
        int[] nums = {2, 3, -2, 4};
        System.out.println("Maximum product subarray is: " + maxProduct(nums));
    }
}
```

---

### 🕓 Time Complexity: `O(n)`
### 📦 Space Complexity: `O(1)`

---

### ✅ Output:
```
Maximum product subarray is: 6
```

---

Want to print the **actual subarray**, or see how to extend this for **2D matrices**?

Let me know — we can dive into that too 😎

---

## 13. Merge intervals.

Awesome! **Merging intervals** is one of the most frequently asked coding problems — shows up at Google, Amazon, Facebook, and other big names.

---

### ✅ **Problem Statement**:

> Given an array of intervals `intervals` where `intervals[i] = [start_i, end_i]`, **merge all overlapping intervals** and return an array of the non-overlapping intervals that cover all the intervals in the input.

---

### 🧪 **Example**:

```java
Input:  [[1,3], [2,6], [8,10], [15,18]]  
Output: [[1,6], [8,10], [15,18]]

Input:  [[1,4], [4,5]]  
Output: [[1,5]]
```

---

### 💡 **Approach**:
1. **Sort** the intervals by starting time.
2. Create a result list, and iterate over intervals:
    - If current interval **overlaps** with the last interval in result, merge them.
    - Else, add the current interval to result.

---

### 💻 **Java Code**:

```java
import java.util.*;

public class MergeIntervals {
    public static int[][] merge(int[][] intervals) {
        if (intervals.length <= 1) return intervals;

        // Step 1: Sort by start time
        Arrays.sort(intervals, (a, b) -> a[0] - b[0]);

        List<int[]> result = new ArrayList<>();

        // Step 2: Merge intervals
        int[] current = intervals[0];
        result.add(current);

        for (int[] interval : intervals) {
            int currentEnd = current[1];
            int nextStart = interval[0];
            int nextEnd = interval[1];

            if (nextStart <= currentEnd) {
                // Overlap → merge
                current[1] = Math.max(currentEnd, nextEnd);
            } else {
                // No overlap → move to next
                current = interval;
                result.add(current);
            }
        }

        return result.toArray(new int[result.size()][]);
    }

    public static void main(String[] args) {
        int[][] intervals = { {1, 3}, {2, 6}, {8, 10}, {15, 18} };
        int[][] merged = merge(intervals);

        System.out.println("Merged Intervals:");
        for (int[] interval : merged) {
            System.out.println(Arrays.toString(interval));
        }
    }
}
```

---

### 🕓 Time Complexity: `O(n log n)` (due to sorting)
### 📦 Space Complexity: `O(n)`

---

Want the same solution in:
- **JavaScript** or **Python**?
- A version that **modifies the input in-place**?
- Support for **unsorted or overlapping intervals randomly**?

Just ask — I’ve got your back! 💪

---

## 14. Search in a rotated sorted array.

🔥 Classic problem alert! **Search in a Rotated Sorted Array** is a top-league interview question — often asked by Google, Amazon, Facebook, and Netflix.

---

### ✅ **Problem Statement**:

> Given a rotated sorted array `nums` (no duplicates) and a target value, return the **index** of the target if it exists, otherwise return `-1`.

---

### 🧪 **Example**:

```java
Input: nums = [4,5,6,7,0,1,2], target = 0  
Output: 4

Input: nums = [4,5,6,7,0,1,2], target = 3  
Output: -1
```

---

### 💡 **Approach** (Modified Binary Search):

Even though the array is rotated, one half is always **sorted**:
1. Find the **mid**.
2. Check which half is sorted.
3. Narrow search accordingly.

---

### 💻 **Java Code**:

```java
public class SearchRotatedArray {
    public static int search(int[] nums, int target) {
        int left = 0, right = nums.length - 1;

        while (left <= right) {
            int mid = (left + right) / 2;

            if (nums[mid] == target) return mid;

            // Left half is sorted
            if (nums[left] <= nums[mid]) {
                if (target >= nums[left] && target < nums[mid]) {
                    right = mid - 1; // search left
                } else {
                    left = mid + 1;  // search right
                }
            }
            // Right half is sorted
            else {
                if (target > nums[mid] && target <= nums[right]) {
                    left = mid + 1; // search right
                } else {
                    right = mid - 1; // search left
                }
            }
        }

        return -1; // not found
    }

    public static void main(String[] args) {
        int[] nums = {4, 5, 6, 7, 0, 1, 2};
        int target = 0;
        int result = search(nums, target);
        System.out.println("Target found at index: " + result);
    }
}
```

---

### 🕓 Time Complexity: `O(log n)`
### 📦 Space Complexity: `O(1)`

---

### ✅ Output:
```
Target found at index: 4
```

---

Let me know if you want to:
- Handle **arrays with duplicates** (needs slight change)
- See **JavaScript/Python** version
- Print the steps for **dry run tracing**

Happy to help crack it deeper! 🔍

---

## 15. Set matrix zeroes.

Nice pick! **Set Matrix Zeroes** is a classic interview problem — frequently asked at Google, Microsoft, and Amazon.

---

### ✅ **Problem Statement**:

> Given an `m x n` matrix, if an element is `0`, set its **entire row and column to 0**.  
> Must do it **in-place** (without using extra space proportional to matrix size).

---

### 🧪 **Example**:

```java
Input:
[
  [1, 1, 1],
  [1, 0, 1],
  [1, 1, 1]
]

Output:
[
  [1, 0, 1],
  [0, 0, 0],
  [1, 0, 1]
]
```

---

### 💡 **Optimal In-Place Approach**:

Use the **first row and first column** of the matrix itself to mark whether a row or column should be zero.

#### Key Steps:
1. Determine if **first row or column needs to be zeroed** (track separately).
2. For the rest of the matrix:
    - If `matrix[i][j] == 0`, mark `matrix[i][0] = 0` and `matrix[0][j] = 0`.
3. Traverse again and set elements to 0 using these markers.
4. Finally, zero out the **first row and first column** if needed.

---

### 💻 **Java Code**:

```java
public class SetMatrixZeroes {
    public static void setZeroes(int[][] matrix) {
        int rows = matrix.length;
        int cols = matrix[0].length;

        boolean firstRowZero = false;
        boolean firstColZero = false;

        // Check if first row has any zeros
        for (int j = 0; j < cols; j++) {
            if (matrix[0][j] == 0) {
                firstRowZero = true;
                break;
            }
        }

        // Check if first column has any zeros
        for (int i = 0; i < rows; i++) {
            if (matrix[i][0] == 0) {
                firstColZero = true;
                break;
            }
        }

        // Use first row/col to mark zero rows and cols
        for (int i = 1; i < rows; i++) {
            for (int j = 1; j < cols; j++) {
                if (matrix[i][j] == 0) {
                    matrix[i][0] = 0;
                    matrix[0][j] = 0;
                }
            }
        }

        // Set matrix cells to zero using markers
        for (int i = 1; i < rows; i++) {
            for (int j = 1; j < cols; j++) {
                if (matrix[i][0] == 0 || matrix[0][j] == 0) {
                    matrix[i][j] = 0;
                }
            }
        }

        // Zero the first row if needed
        if (firstRowZero) {
            for (int j = 0; j < cols; j++) {
                matrix[0][j] = 0;
            }
        }

        // Zero the first column if needed
        if (firstColZero) {
            for (int i = 0; i < rows; i++) {
                matrix[i][0] = 0;
            }
        }
    }

    public static void main(String[] args) {
        int[][] matrix = {
            {1, 1, 1},
            {1, 0, 1},
            {1, 1, 1}
        };

        setZeroes(matrix);

        System.out.println("Matrix after setting zeroes:");
        for (int[] row : matrix) {
            for (int num : row) {
                System.out.print(num + " ");
            }
            System.out.println();
        }
    }
}
```

---

### 🕓 Time Complexity: `O(m * n)`
### 📦 Space Complexity: `O(1)` (in-place, using matrix itself)

---

Let me know if you want:
- A **brute-force version** (with extra space)
- A **JavaScript/Python** solution
- A dry-run to visualize how the logic flows

Just say the word! 💬

---

### 🔹 **16–25: Strings**

## 16. Check if two strings are anagrams.

Great choice! 🔁 Checking if two strings are **anagrams** is a classic string manipulation problem — often asked in entry to mid-level interviews.

---

### ✅ **Problem Statement**:

> Two strings are anagrams if they contain the **same characters**, with the **same frequency**, but possibly in **different order**.

---

### 🧪 **Examples**:

```java
Input: s1 = "listen", s2 = "silent"  
Output: true

Input: s1 = "hello", s2 = "world"  
Output: false
```

---

### 💡 **Approach 1: Sorting**
- Sort both strings → if equal, they’re anagrams.

### 💻 Java Code (Sorting Approach):

```java
import java.util.Arrays;

public class AnagramCheck {
    public static boolean isAnagram(String s1, String s2) {
        if (s1.length() != s2.length()) return false;

        char[] arr1 = s1.toCharArray();
        char[] arr2 = s2.toCharArray();

        Arrays.sort(arr1);
        Arrays.sort(arr2);

        return Arrays.equals(arr1, arr2);
    }

    public static void main(String[] args) {
        String s1 = "listen";
        String s2 = "silent";

        System.out.println("Are they anagrams? " + isAnagram(s1, s2));
    }
}
```

---

### 🕓 Time Complexity: `O(n log n)`
### 📦 Space Complexity: `O(1)` (ignoring sorting space)

---

### 💡 **Approach 2: Frequency Count** (More efficient)

1. Use an int array of size 26 (assuming lowercase).
2. Increment for characters in `s1`, decrement for `s2`.
3. If all counts are zero → they’re anagrams.

### 💻 Java Code (Frequency Count):

```java
public class AnagramCheck {
    public static boolean isAnagram(String s1, String s2) {
        if (s1.length() != s2.length()) return false;

        int[] count = new int[26];

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
        System.out.println(isAnagram("anagram", "nagaram")); // true
        System.out.println(isAnagram("rat", "car"));         // false
    }
}
```

---

### 🕓 Time Complexity: `O(n)`
### 📦 Space Complexity: `O(1)` (fixed array of 26)

---

Need to handle:
- **Unicode characters**?
- **Case-insensitive** comparison?
- Or want this in **JavaScript/Python**?

Let me know — I’ve got variants for all that too! 💪

---

## 17. Longest common prefix.

Nice one! 🌟 **Longest Common Prefix** is a classic string problem — frequently asked at companies like Google, Amazon, and Apple.

---

### ✅ **Problem Statement**:

> Write a function to find the **longest common prefix** string amongst an array of strings.  
> If there is no common prefix, return an empty string `""`.

---

### 🧪 **Examples**:

```java
Input: ["flower", "flow", "flight"]
Output: "fl"

Input: ["dog", "racecar", "car"]
Output: ""  // No common prefix
```

---

### 💡 **Approach: Vertical Scanning** (Character by character)

- Start from the first character of the first string.
- Compare that character with all other strings at the same position.
- Stop when characters don’t match.

---

### 💻 Java Code:

```java
public class LongestCommonPrefix {
    public static String longestCommonPrefix(String[] strs) {
        if (strs == null || strs.length == 0) return "";

        for (int i = 0; i < strs[0].length(); i++) {
            char currentChar = strs[0].charAt(i);

            for (int j = 1; j < strs.length; j++) {
                // Check bounds and mismatch
                if (i >= strs[j].length() || strs[j].charAt(i) != currentChar) {
                    return strs[0].substring(0, i);
                }
            }
        }

        return strs[0]; // All strings matched fully
    }

    public static void main(String[] args) {
        String[] input = {"flower", "flow", "flight"};
        System.out.println("Longest Common Prefix: " + longestCommonPrefix(input));
    }
}
```

---

### 🕓 Time Complexity: `O(S)`
Where `S` is the sum of all characters in the array.

### 📦 Space Complexity: `O(1)` (no extra space used)

---

### 🔄 Other Approaches:
- Horizontal scanning
- Divide and conquer
- Binary search

---

Want to see a **horizontal scanning** or **binary search** version? Or code in **JavaScript/Python**?

Happy to share it! 💬

---

## 18. Reverse words in a string.

Great pick! 🔄 Reversing **words** in a string is another hot question — asked frequently in interviews (Amazon, Microsoft, Google, etc.).

---

### ✅ **Problem Statement**:

> Given a string `s`, reverse the **order of words**.  
> Words are separated by **spaces**.  
> Return a string with words in reverse order, trimmed with **no leading/trailing spaces**, and only **single spaces** between words.

---

### 🧪 **Example**:

```java
Input:  "  the sky   is blue  "
Output: "blue is sky the"

Input:  "hello world"
Output: "world hello"
```

---

### 💡 **Approach**:

1. **Trim** leading and trailing spaces.
2. **Split** by spaces.
3. **Reverse** the word array.
4. **Join** with a single space.

---

### 💻 Java Code:

```java
public class ReverseWordsInString {
    public static String reverseWords(String s) {
        // Step 1: Trim and split
        String[] words = s.trim().split("\\s+");

        // Step 2: Reverse the array
        StringBuilder reversed = new StringBuilder();
        for (int i = words.length - 1; i >= 0; i--) {
            reversed.append(words[i]);
            if (i > 0) reversed.append(" ");
        }

        return reversed.toString();
    }

    public static void main(String[] args) {
        String input = "  the sky   is blue  ";
        System.out.println("Reversed: \"" + reverseWords(input) + "\"");
    }
}
```

---

### ✅ Output:
```
Reversed: "blue is sky the"
```

---

### 🕓 Time Complexity: `O(n)`
### 📦 Space Complexity: `O(n)` (for split and result)

---

### ✅ Handles:
- Extra spaces between words
- Leading/trailing spaces

---

Want a version that:
- Reverses **words in-place** in a `char[]`?
- Works in **JavaScript or Python**?
- Also reverses **characters in each word**?

Let me know — I can drop those too! 💬

---

## 19. Longest substring without repeating characters.

🔥 One of the **top 5 most asked string problems**:
## **Longest Substring Without Repeating Characters**
Asked at **Amazon, Google, Facebook, Microsoft, Netflix**, you name it!

---

### ✅ **Problem Statement**:

> Given a string `s`, find the length of the **longest substring** without repeating characters.

---

### 🧪 **Examples**:

```java
Input: "abcabcbb"  
Output: 3  // "abc"

Input: "bbbbb"  
Output: 1  // "b"

Input: "pwwkew"  
Output: 3  // "wke"
```

---

### 💡 **Approach: Sliding Window + HashSet**
Use two pointers (`start`, `end`) to represent the current window.  
Use a **HashSet** to store characters in the window.

---

### 💻 Java Code:

```java
import java.util.HashSet;

public class LongestSubstringWithoutRepeat {
    public static int lengthOfLongestSubstring(String s) {
        HashSet<Character> set = new HashSet<>();
        int left = 0, right = 0, maxLen = 0;

        while (right < s.length()) {
            char c = s.charAt(right);

            // If character already in set, shrink window from left
            while (set.contains(c)) {
                set.remove(s.charAt(left));
                left++;
            }

            set.add(c);
            maxLen = Math.max(maxLen, right - left + 1);
            right++;
        }

        return maxLen;
    }

    public static void main(String[] args) {
        String input = "abcabcbb";
        System.out.println("Longest Substring Length: " + lengthOfLongestSubstring(input));
    }
}
```

---

### ✅ Output:
```
Longest Substring Length: 3
```

---

### 🕓 Time Complexity: `O(n)`
### 📦 Space Complexity: `O(k)` — where `k` is the size of the charset (e.g., 26 for lowercase, 128 for ASCII)

---

### 🧠 Bonus Variant Ideas:
- Return the **actual substring**, not just the length
- Handle **Unicode** characters
- Modify for **longest substring with at most K repeating characters**

Want me to show those as well? Or Python/JS version?

I'm game! 💬

---

## 20. Valid palindrome (with/without removing one character).

Great one, Aditya! 💯  
**Valid Palindrome** and its **"remove one character"** variant are **super popular interview questions**, especially at Google, Amazon, Microsoft, etc.

Let’s tackle **both versions**. 👇

---

## ✅ **1. Valid Palindrome (Simple Check)**

> Return `true` if a string is a **palindrome**, ignoring non-alphanumeric characters and case.

---

### 💻 Java Code:

```java
public class ValidPalindrome {
    public static boolean isPalindrome(String s) {
        s = s.replaceAll("[^a-zA-Z0-9]", "").toLowerCase();

        int left = 0, right = s.length() - 1;
        while (left < right) {
            if (s.charAt(left) != s.charAt(right))
                return false;
            left++;
            right--;
        }

        return true;
    }

    public static void main(String[] args) {
        String s = "A man, a plan, a canal: Panama";
        System.out.println("Is palindrome? " + isPalindrome(s));  // true
    }
}
```

---

### 🕓 Time: `O(n)`
### 📦 Space: `O(n)` (for cleaned string)

---

## ✅ **2. Valid Palindrome II (Allow Removing One Character)**

> Return `true` if the string can become a palindrome by removing **at most one** character.

---

### 💡 Trick:
Use two pointers. If characters don’t match → try skipping either one of them, and check if that makes it a palindrome.

---

### 💻 Java Code:

```java
public class ValidPalindromeII {
    public static boolean validPalindrome(String s) {
        int left = 0, right = s.length() - 1;

        while (left < right) {
            if (s.charAt(left) != s.charAt(right)) {
                // Try skipping either character
                return isPalindrome(s, left + 1, right) || isPalindrome(s, left, right - 1);
            }
            left++;
            right--;
        }

        return true;
    }

    private static boolean isPalindrome(String s, int left, int right) {
        while (left < right) {
            if (s.charAt(left) != s.charAt(right)) return false;
            left++;
            right--;
        }
        return true;
    }

    public static void main(String[] args) {
        String s1 = "abca";
        System.out.println("Valid with one removal? " + validPalindrome(s1));  // true
    }
}
```

---

### 🕓 Time: `O(n)`
### 📦 Space: `O(1)` — no extra space used

---

### ✅ Examples:

```java
Input: "abca"   → Output: true  (remove 'b' or 'c')
Input: "racecar"→ Output: true  (already palindrome)
Input: "abcdef" → Output: false (can't fix with one removal)
```

---

Let me know if you want:
- To handle **Unicode** or ignore **spaces and punctuation**
- A **recursive version**
- Or **Python/JavaScript** version

I’ve got you covered! 💪

---

## 21. String compression.

Nice pick, Aditya! ⚡  
**String Compression** is a super handy coding problem — often asked by Amazon, Google, and other top tech firms.

---

## ✅ **Problem Statement (Leetcode Style)**

> Given a string, **compress** it by replacing sequences of the same character with the character followed by the count.  
> If the compressed string is **not shorter**, return the original.

---

### 🧪 **Example**:

```java
Input:  "aabcccccaaa"
Output: "a2b1c5a3"

Input: "abc"
Output: "abc"   // because compression is not smaller
```

---

## 💡 **Approach**:

1. Use a `StringBuilder` to build the result.
2. Loop through the string:
    - Count consecutive repeating characters.
    - Append the character and its count.
3. Return the **compressed string** **only if it's shorter** than the original.

---

## 💻 Java Code:

```java
public class StringCompression {
    public static String compress(String s) {
        if (s == null || s.length() == 0) return s;

        StringBuilder compressed = new StringBuilder();
        int count = 1;

        for (int i = 1; i < s.length(); i++) {
            if (s.charAt(i) == s.charAt(i - 1)) {
                count++;
            } else {
                compressed.append(s.charAt(i - 1)).append(count);
                count = 1;
            }
        }

        // Append the last character
        compressed.append(s.charAt(s.length() - 1)).append(count);

        String result = compressed.toString();
        return result.length() < s.length() ? result : s;
    }

    public static void main(String[] args) {
        System.out.println(compress("aabcccccaaa"));  // a2b1c5a3
        System.out.println(compress("abc"));          // abc
    }
}
```

---

### 🕓 Time Complexity: `O(n)`
### 📦 Space Complexity: `O(n)` (for result string)

---

### ✅ BONUS VARIANTS:
- Compress **in-place** (like Leetcode 443) using `char[]`
- Handle **unicode/multibyte** characters
- Compress only when count > 1

Need the **in-place compression**, **Leetcode version**, or **Python/JS**?  
Just say the word, and I’ll pop it in! 💬

---

## 22. Group anagrams.

Awesome choice, Aditya! 🔥  
**Group Anagrams** is a favorite in interviews — especially at Google, Facebook, Amazon, and Netflix.

---

## ✅ **Problem Statement**:

> Given an array of strings, group the anagrams **together**.

---

### 🧪 **Example**:

```java
Input: ["eat", "tea", "tan", "ate", "nat", "bat"]

Output: [
  ["eat", "tea", "ate"],
  ["tan", "nat"],
  ["bat"]
]
```

---

## 💡 **Approach: Sort & HashMap**

- Anagrams have the **same sorted character pattern**.
- Use the **sorted string as the key** in a HashMap.
- Add all words with the same sorted key into the same list.

---

### 💻 Java Code:

```java
import java.util.*;

public class GroupAnagrams {
    public static List<List<String>> groupAnagrams(String[] strs) {
        if (strs == null || strs.length == 0) return new ArrayList<>();

        Map<String, List<String>> map = new HashMap<>();

        for (String s : strs) {
            // Sort the string
            char[] chars = s.toCharArray();
            Arrays.sort(chars);
            String key = new String(chars);

            // Group by sorted key
            map.computeIfAbsent(key, k -> new ArrayList<>()).add(s);
        }

        return new ArrayList<>(map.values());
    }

    public static void main(String[] args) {
        String[] input = {"eat", "tea", "tan", "ate", "nat", "bat"};
        System.out.println(groupAnagrams(input));
    }
}
```

---

### ✅ Output:
```
[[eat, tea, ate], [tan, nat], [bat]]
```

> Note: Order inside and between groups may vary.

---

### 🕓 Time Complexity: `O(n * k log k)`
- `n` = number of words
- `k` = max length of a word (for sorting)

### 📦 Space Complexity: `O(n * k)`

---

## 🚀 Bonus Variant:
- **Faster alternative**: Use a **frequency count (like a[1]b[0]...)** as key (instead of sorting)
- Want this in **Python/JavaScript** too?
- Want to handle **Unicode** or **case-insensitive**?

Let me know, and I’ll hook you up! 💪

---

## 23. Implement strStr() / indexOf().

Solid one, Aditya! 🔍  
**`strStr()`**, also known as **`indexOf()`**, is a classic **substring search** problem — often asked by **Apple, Microsoft, and Amazon**.

---

## ✅ **Problem Statement**:

> Implement `strStr(haystack, needle)`  
> Return the **index** of the **first occurrence** of `needle` in `haystack`.  
> Return `-1` if `needle` is not part of `haystack`.

---

### 🧪 **Examples**:

```java
Input: haystack = "hello", needle = "ll"
Output: 2

Input: haystack = "aaaaa", needle = "bba"
Output: -1

Input: haystack = "abc", needle = ""
Output: 0
```

---

## 💡 **Approach 1: Naive Brute Force**

Check all substrings of `haystack` with length equal to `needle.length()`

---

### 💻 Java Code:

```java
public class StrStr {
    public static int strStr(String haystack, String needle) {
        if (needle.isEmpty()) return 0;
        int hLen = haystack.length(), nLen = needle.length();

        for (int i = 0; i <= hLen - nLen; i++) {
            if (haystack.substring(i, i + nLen).equals(needle)) {
                return i;
            }
        }

        return -1;
    }

    public static void main(String[] args) {
        System.out.println(strStr("hello", "ll")); // Output: 2
        System.out.println(strStr("aaaaa", "bba")); // Output: -1
    }
}
```

---

### 🕓 Time Complexity: `O(n * m)`
(n = haystack length, m = needle length)

---

## ⚡ Bonus: **KMP Algorithm** (Optimal for large input)

Want me to show you the **KMP (Knuth–Morris–Pratt)** version that runs in **O(n + m)** time?

Or prefer a **Python** or **JavaScript** version?

Happy to drop it! 💬

---

## 24. Check for rotation of strings.

Nice one, Aditya! 🔄  
Checking if one string is a **rotation** of another is a **neat string trick** — commonly asked at **Amazon, Adobe, Microsoft**.

---

## ✅ **Problem Statement**:

> Given two strings `s1` and `s2`, check if `s2` is a **rotation** of `s1`.

---

### 🧪 **Examples**:

```java
Input:  s1 = "waterbottle", s2 = "erbottlewat"
Output: true

Input:  s1 = "hello", s2 = "lohel"
Output: true

Input:  s1 = "abc", s2 = "acb"
Output: false
```

---

## 💡 **Key Insight**:

If `s2` is a rotation of `s1`, then it will always be a **substring of (`s1 + s1`)**.

For example:  
"erbottlewat" is a substring of "waterbottlewaterbottle"

---

### 💻 Java Code:

```java
public class StringRotationCheck {
    public static boolean isRotation(String s1, String s2) {
        if (s1.length() != s2.length()) return false;
        String combined = s1 + s1;
        return combined.contains(s2);
    }

    public static void main(String[] args) {
        System.out.println(isRotation("waterbottle", "erbottlewat")); // true
        System.out.println(isRotation("hello", "lohel"));             // true
        System.out.println(isRotation("abc", "acb"));                 // false
    }
}
```

---

### 🕓 Time Complexity: `O(n)`
### 📦 Space Complexity: `O(n)`

---

### 🔍 Optional Enhancements:
- Case-insensitive check?
- Rotation with at most 1 character mismatch?
- Using KMP instead of `contains()`?

Want those too? Or a **Python/JS version**? Let me know and I’ll drop it right in! 👇

---

## 25. Count and say problem.

Great pick, Aditya! 🗣️  
The **Count and Say** problem is a popular one — often seen in **Leetcode**, and asked by **Google, Microsoft**, and other top tech giants.

---

## ✅ **Problem Statement:**

> The **Count and Say** sequence is a series of strings where:
- `countAndSay(1)` = `"1"`
- `countAndSay(2)` = `"11"`  (one 1)
- `countAndSay(3)` = `"21"`  (two 1s)
- `countAndSay(4)` = `"1211"` (one 2, one 1)
- `countAndSay(5)` = `"111221"` (one 1, one 2, two 1s)
  ... and so on.

📌 You’re given `n`, return the `n-th` term of the Count and Say sequence.

---

### 🧪 Examples:

```java
Input: n = 4  
Output: "1211"

Input: n = 5  
Output: "111221"
```

---

## 💡 **Approach**:

Start from `"1"`, and **build each term** by **reading off** the previous term:
- Count consecutive digits
- Say how many and what digit

---

## 💻 Java Code:

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
                char curr = result.charAt(j);
                if (curr == prev) {
                    count++;
                } else {
                    sb.append(count).append(prev);
                    prev = curr;
                    count = 1;
                }
            }

            sb.append(count).append(prev); // for the last group
            result = sb.toString();
        }

        return result;
    }

    public static void main(String[] args) {
        int n = 5;
        System.out.println("Count and Say(" + n + ") = " + countAndSay(n));
    }
}
```

---

### ✅ Output:
```
Count and Say(5) = 111221
```

---

### 🕓 Time Complexity: `O(2^n)` (roughly — strings can grow exponentially)
### 📦 Space Complexity: `O(2^n)` for building strings

---

### 🧠 Follow-up Ideas:
- Optimize with memoization?
- Build a list of first `n` terms?
- Solve using recursion?

Want a **recursive version**, or to see this in **Python or JavaScript**? Just let me know — I’ll drop it in fast! ⚡

---

### 🔹 **26–35: Linked List**

## 26. Reverse a linked list (iterative & recursive).

Perfect pick, Aditya! 🔁  
**"Reverse a Linked List"** is a must-know DSA problem — frequently asked by **Amazon, Microsoft, Meta, and Google**.

Let’s cover **both iterative and recursive** approaches for **singly linked lists**. 🚀

---

## ✅ Problem Statement:

> Reverse a singly linked list.  
> Return the **head of the reversed list**.

---

### 🧪 Example:

```
Input:  1 → 2 → 3 → 4 → 5  
Output: 5 → 4 → 3 → 2 → 1
```

---

## ✅ Java Node Class (Used for both solutions):

```java
class ListNode {
    int val;
    ListNode next;
    ListNode(int val) {
        this.val = val;
    }
}
```

---

## 🔁 **1. Iterative Approach**

### 💡 Logic:
Use 3 pointers: `prev`, `curr`, `next`. Reverse links one-by-one.

---

### 💻 Java Code:

```java
public class ReverseLinkedListIterative {
    public static ListNode reverseList(ListNode head) {
        ListNode prev = null, curr = head;

        while (curr != null) {
            ListNode nextNode = curr.next;
            curr.next = prev;       // reverse link
            prev = curr;
            curr = nextNode;
        }

        return prev;  // new head
    }
}
```

---

### 🕓 Time: `O(n)`
### 📦 Space: `O(1)`

---

## 🔁 **2. Recursive Approach**

### 💡 Logic:
- Reverse rest of the list recursively.
- Attach current node at the end of reversed sublist.

---

### 💻 Java Code:

```java
public class ReverseLinkedListRecursive {
    public static ListNode reverseList(ListNode head) {
        if (head == null || head.next == null)
            return head;

        ListNode reversedHead = reverseList(head.next);
        head.next.next = head;
        head.next = null;

        return reversedHead;
    }
}
```

---

### 🕓 Time: `O(n)`
### 📦 Space: `O(n)` (due to recursion stack)

---

### ✅ Test Helper Code (Optional):

```java
public static void printList(ListNode head) {
    while (head != null) {
        System.out.print(head.val + " -> ");
        head = head.next;
    }
    System.out.println("null");
}
```

---

### ⚡ Want more?

- Doubly Linked List version?
- In-place reverse between positions `m` and `n`?
- Python or JavaScript version?

Just say the word, Aditya — I got you covered 💪

---

## 27. Detect a cycle in a linked list (Floyd’s Algorithm).

Great pick again, Aditya! 🌀  
**Detecting a cycle in a linked list** using **Floyd’s Cycle Detection Algorithm (a.k.a. Tortoise and Hare)** is a **top-tier favorite** in interviews at **Google, Microsoft, Amazon, and Adobe**.

---

## ✅ **Problem Statement**:

> Given the `head` of a linked list, determine if the list has a **cycle** in it.

A cycle exists if a node can be visited again by continuously following the `next` pointer.

---

### 🧪 Example:

```
Input:  1 → 2 → 3 → 4 → 5
               ↑         ↓
               ← ← ← ← ←  
Output: true

Input:  1 → 2 → 3 → null
Output: false
```

---

## 💡 **Approach: Floyd's Tortoise & Hare**

- Use two pointers:  
  `slow` moves 1 step,  
  `fast` moves 2 steps.
- If they ever **meet**, there is a cycle.
- If `fast` or `fast.next` becomes null → **no cycle**.

---

### 💻 Java Code:

```java
class ListNode {
    int val;
    ListNode next;
    ListNode(int val) {
        this.val = val;
    }
}

public class DetectCycle {
    public static boolean hasCycle(ListNode head) {
        if (head == null || head.next == null) return false;

        ListNode slow = head;
        ListNode fast = head;

        while (fast != null && fast.next != null) {
            slow = slow.next;         // 1 step
            fast = fast.next.next;    // 2 steps

            if (slow == fast) return true; // cycle found
        }

        return false; // no cycle
    }

    public static void main(String[] args) {
        ListNode head = new ListNode(1);
        head.next = new ListNode(2);
        head.next.next = new ListNode(3);
        head.next.next.next = head.next; // cycle

        System.out.println("Has cycle? " + hasCycle(head)); // Output: true
    }
}
```

---

### 🕓 Time Complexity: `O(n)`
### 📦 Space Complexity: `O(1)` ✅

---

## ✅ Variants:
- **Return the starting node** of the cycle?
- **Length of the cycle**?
- **Break the cycle**?

Want to dive into any of these or need a **Python/JS** version? Just say the word, Aditya! 😎

---

## 28. Find the middle of a linked list.

Clean and crisp one, Aditya! 🎯  
**Finding the middle of a linked list** is a super common interview favorite — asked by **Amazon, Adobe, PayPal, Flipkart, and many more**.

---

## ✅ **Problem Statement**:

> Given the `head` of a singly linked list, return the **middle node**.  
> If there are **two middle nodes**, return the **second** one.

---

### 🧪 Example:

```
Input:  1 → 2 → 3 → 4 → 5
Output: 3

Input:  1 → 2 → 3 → 4 → 5 → 6
Output: 4
```

---

## 💡 **Approach: Slow and Fast Pointers**

- `slow` moves 1 step at a time
- `fast` moves 2 steps at a time
- When `fast` reaches the end, `slow` will be at the **middle**

---

### 💻 Java Code:

```java
class ListNode {
    int val;
    ListNode next;
    ListNode(int val) {
        this.val = val;
    }
}

public class MiddleOfLinkedList {
    public static ListNode findMiddle(ListNode head) {
        if (head == null) return null;

        ListNode slow = head;
        ListNode fast = head;

        while (fast != null && fast.next != null) {
            slow = slow.next;         // 1 step
            fast = fast.next.next;    // 2 steps
        }

        return slow; // middle node
    }

    public static void main(String[] args) {
        ListNode head = new ListNode(1);
        head.next = new ListNode(2);
        head.next.next = new ListNode(3);
        head.next.next.next = new ListNode(4);
        head.next.next.next.next = new ListNode(5);

        ListNode middle = findMiddle(head);
        System.out.println("Middle Node: " + middle.val);  // Output: 3
    }
}
```

---

### 🕓 Time: `O(n)`
### 📦 Space: `O(1)` ✅

---

## ⚡ Bonus Variants:
- Return **first** middle instead of second?
- Find the middle in a **doubly** linked list?
- Want it in **Python**, **JavaScript**, or recursive form?

Let me know and I’ll sort it out for you! 👊

---

## 29. Merge two sorted linked lists.

Classic one, Aditya! 🔗  
**Merging two sorted linked lists** is a top 10 interview favorite — commonly asked by **Amazon, Google, Meta, and Microsoft**.

---

## ✅ **Problem Statement**:

> Given the heads of two **sorted** linked lists `l1` and `l2`, merge them into a **single sorted list** and return the new head.

---

### 🧪 Example:

```
Input:  l1 = 1 → 3 → 5  
        l2 = 2 → 4 → 6

Output: 1 → 2 → 3 → 4 → 5 → 6
```

---

## 💡 Approach: Iterative using a Dummy Node

We use a dummy node to simplify the merging process.  
Compare values from both lists and attach the smaller one to the merged list.

---

### 💻 Java Code (Iterative):

```java
class ListNode {
    int val;
    ListNode next;
    ListNode(int val) {
        this.val = val;
    }
}

public class MergeSortedLists {
    public static ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(-1); // dummy node
        ListNode current = dummy;

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

        // Attach remaining part
        current.next = (l1 != null) ? l1 : l2;

        return dummy.next; // head of merged list
    }

    public static void printList(ListNode head) {
        while (head != null) {
            System.out.print(head.val + " → ");
            head = head.next;
        }
        System.out.println("null");
    }

    public static void main(String[] args) {
        ListNode l1 = new ListNode(1);
        l1.next = new ListNode(3);
        l1.next.next = new ListNode(5);

        ListNode l2 = new ListNode(2);
        l2.next = new ListNode(4);
        l2.next.next = new ListNode(6);

        ListNode merged = mergeTwoLists(l1, l2);
        printList(merged);
    }
}
```

---

### 🕓 Time: `O(n + m)`
### 📦 Space: `O(1)` (in-place)

---

## 🔁 Bonus: Recursive Version

Want the same thing done recursively? Here's a compact one:

```java
public static ListNode mergeTwoListsRecursive(ListNode l1, ListNode l2) {
    if (l1 == null) return l2;
    if (l2 == null) return l1;

    if (l1.val < l2.val) {
        l1.next = mergeTwoListsRecursive(l1.next, l2);
        return l1;
    } else {
        l2.next = mergeTwoListsRecursive(l1, l2.next);
        return l2;
    }
}
```

---

Need this in **Python**, **JavaScript**, or for **doubly linked lists**? Just say the word, Aditya — I’ve got your back! 💪

---

## 30. Remove N-th node from end.

Let’s go, Aditya! 💥  
**"Remove N-th node from the end of a linked list"** is a super popular question — seen at **Google, Amazon, Microsoft, Flipkart**, and more.

---

## ✅ **Problem Statement**:

> Given the `head` of a linked list, remove the **N-th node from the end**, and return the head of the modified list.

---

### 🧪 Example:

```
Input:  head = 1 → 2 → 3 → 4 → 5,  n = 2  
Output:        1 → 2 → 3 → 5
```

---

## 💡 **Approach: Two-Pointer Technique**

1. Use two pointers: `first` and `second`
2. Move `first` ahead by `n` nodes
3. Move both `first` and `second` until `first` reaches the end
4. `second.next` is the node to delete

To handle edge cases (like deleting the head), use a **dummy node**.

---

### 💻 Java Code:

```java
class ListNode {
    int val;
    ListNode next;
    ListNode(int val) {
        this.val = val;
    }
}

public class RemoveNthFromEnd {
    public static ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode dummy = new ListNode(0); 
        dummy.next = head;

        ListNode first = dummy;
        ListNode second = dummy;

        // Move first n+1 steps ahead
        for (int i = 0; i <= n; i++) {
            first = first.next;
        }

        // Move both until first reaches end
        while (first != null) {
            first = first.next;
            second = second.next;
        }

        // Remove target node
        second.next = second.next.next;

        return dummy.next;
    }

    public static void printList(ListNode head) {
        while (head != null) {
            System.out.print(head.val + " → ");
            head = head.next;
        }
        System.out.println("null");
    }

    public static void main(String[] args) {
        ListNode head = new ListNode(1);
        head.next = new ListNode(2);
        head.next.next = new ListNode(3);
        head.next.next.next = new ListNode(4);
        head.next.next.next.next = new ListNode(5);

        ListNode updated = removeNthFromEnd(head, 2);
        printList(updated);  // Output: 1 → 2 → 3 → 5
    }
}
```

---

### 🕓 Time: `O(n)`
### 📦 Space: `O(1)`

---

## 🔁 Variants:
- Remove K-th from start?
- Return the removed value?
- Recursive version?

Let me know if you want this in **Python**, **JavaScript**, or as part of a **linked list utility class** — I’ll hook it up! 🔧

---

## 31. Add two numbers represented by linked lists.

Solid choice again, Aditya! 🔢➕🔗  
**Adding two numbers represented by linked lists** is a classic — asked by **Amazon, Google, Apple, Adobe**, and **Microsoft**.

---

## ✅ **Problem Statement:**

> You are given two non-empty linked lists representing two non-negative integers.  
> The digits are stored in **reverse order**, and each of their nodes contains a single digit.  
> Add the two numbers and return the sum as a **linked list**.

---

### 🧪 Example:

```
Input:  (2 → 4 → 3) + (5 → 6 → 4)  
        = 342 + 465 = 807

Output: 7 → 0 → 8
```

---

## 💡 Approach:

- Traverse both lists from head to tail.
- Use a carry to handle digit sums > 9.
- Create new nodes for each digit of the result.

---

## 💻 Java Code:

```java
class ListNode {
    int val;
    ListNode next;
    ListNode(int val) {
        this.val = val;
    }
}

public class AddTwoNumbers {
    public static ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(0); // dummy head
        ListNode curr = dummy;
        int carry = 0;

        while (l1 != null || l2 != null || carry != 0) {
            int x = (l1 != null) ? l1.val : 0;
            int y = (l2 != null) ? l2.val : 0;

            int sum = x + y + carry;
            carry = sum / 10;
            curr.next = new ListNode(sum % 10);

            curr = curr.next;
            if (l1 != null) l1 = l1.next;
            if (l2 != null) l2 = l2.next;
        }

        return dummy.next;
    }

    public static void printList(ListNode head) {
        while (head != null) {
            System.out.print(head.val + " → ");
            head = head.next;
        }
        System.out.println("null");
    }

    public static void main(String[] args) {
        // 342 → 2 → 4 → 3
        ListNode l1 = new ListNode(2);
        l1.next = new ListNode(4);
        l1.next.next = new ListNode(3);

        // 465 → 5 → 6 → 4
        ListNode l2 = new ListNode(5);
        l2.next = new ListNode(6);
        l2.next.next = new ListNode(4);

        ListNode result = addTwoNumbers(l1, l2);
        printList(result);  // Output: 7 → 0 → 8
    }
}
```

---

### 🕓 Time: `O(max(n, m))`
### 📦 Space: `O(max(n, m))` (result list + carry)

---

## 🔁 Bonus Variants:

- Numbers stored in **forward order**?
- Add more than 2 numbers?
- Handle **negative digits** or decimals?

Need this in Python, JS, or need to visualize it step-by-step? I got you covered, Aditya! 💪

---

## 32. Check if linked list is a palindrome.

Oooh nice one, Aditya! 🔁🔗  
**Checking if a linked list is a palindrome** is a brainy yet elegant problem — asked frequently by **Amazon, Google, Meta, PayPal**, and more.

---

## ✅ **Problem Statement:**

> Given the head of a singly linked list, return `true` if it is a **palindrome**, otherwise return `false`.

---

### 🧪 Example:

```
Input:  1 → 2 → 2 → 1  
Output: true

Input:  1 → 2 → 3 → 2 → 1  
Output: true

Input:  1 → 2 → 3  
Output: false
```

---

## 💡 Optimal Approach:

### 1. **Find the middle** using slow/fast pointers
### 2. **Reverse** the second half
### 3. **Compare** first half and reversed second half
### 4. (Optional) **Restore** the original list

---

### 💻 Java Code:

```java
class ListNode {
    int val;
    ListNode next;
    ListNode(int val) {
        this.val = val;
    }
}

public class PalindromeLinkedList {
    public static boolean isPalindrome(ListNode head) {
        if (head == null || head.next == null) return true;

        // Step 1: Find middle
        ListNode slow = head, fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }

        // Step 2: Reverse second half
        ListNode secondHalf = reverseList(slow);

        // Step 3: Compare both halves
        ListNode firstHalf = head;
        ListNode temp = secondHalf;
        while (temp != null) {
            if (firstHalf.val != temp.val) return false;
            firstHalf = firstHalf.next;
            temp = temp.next;
        }

        return true;
    }

    private static ListNode reverseList(ListNode head) {
        ListNode prev = null, curr = head;
        while (curr != null) {
            ListNode nextTemp = curr.next;
            curr.next = prev;
            prev = curr;
            curr = nextTemp;
        }
        return prev;
    }

    public static void main(String[] args) {
        ListNode head = new ListNode(1);
        head.next = new ListNode(2);
        head.next.next = new ListNode(2);
        head.next.next.next = new ListNode(1);

        System.out.println("Is Palindrome? " + isPalindrome(head));  // Output: true
    }
}
```

---

### 🕓 Time: `O(n)`
### 📦 Space: `O(1)` (in-place reverse ✅)

---

## ⚡ Bonus:

- Want to restore the original list after checking?
- Need it in Python/JS?
- Want to handle **doubly linked list** version?

Just say the word, Aditya — I’m here for all things linked list! 😎📚

---

## 33. Flatten a multilevel linked list.

Love this one, Aditya — now we’re getting into *spicy* linked list problems! 🔥  
**Flatten a multilevel doubly linked list** is a LeetCode classic and appears in advanced interviews at **Google, Adobe, Facebook, and Bloomberg**.

---

## ✅ **Problem Statement:**

> You are given a **doubly linked list** where in addition to `next` and `prev`, each node has a **child** pointer, which may or may not point to another doubly linked list.  
> Flatten the list so that all nodes appear in a single-level doubly linked list in **depth-first order**.

---

### 🧪 Example:

```
Input:
1 - 2 - 3 - 4 - 5
          |
          7 - 8 - 9
              |
             11-12

Output:
1 - 2 - 3 - 7 - 8 - 11 - 12 - 9 - 4 - 5
```

---

## 💡 Approach: DFS with Recursion

We go node by node and whenever we find a child:
- Recursively flatten it
- Splice it into the main list between `curr` and `curr.next`

---

### 💻 Java Code:

```java
class Node {
    int val;
    Node prev, next, child;
    Node(int val) {
        this.val = val;
    }
}

public class FlattenMultiLevelList {
    public static Node flatten(Node head) {
        if (head == null) return head;
        flattenDFS(head);
        return head;
    }

    private static Node flattenDFS(Node node) {
        Node curr = node;
        Node last = null;

        while (curr != null) {
            Node next = curr.next;

            // Case 1: has a child
            if (curr.child != null) {
                Node childHead = flattenDFS(curr.child);

                // Connect current to child
                curr.next = childHead;
                childHead.prev = curr;
                curr.child = null;

                // Find tail of flattened child
                Node childTail = childHead;
                while (childTail.next != null) {
                    childTail = childTail.next;
                }

                // Connect tail to next
                if (next != null) {
                    childTail.next = next;
                    next.prev = childTail;
                }

                last = childTail;
                curr = next;
            } else {
                last = curr;
                curr = next;
            }
        }

        return last;
    }

    // Helper: Print the flattened list
    public static void printList(Node head) {
        while (head != null) {
            System.out.print(head.val + " → ");
            head = head.next;
        }
        System.out.println("null");
    }
}
```

---

### 🕓 Time: `O(n)`
(we visit every node once)

### 📦 Space: `O(1)` extra (if you ignore recursion stack)
👉 Want an **iterative stack-based version** to fully avoid recursion?

---

## ✅ Bonus:
- Want to flatten a list with **multiple children** per node?
- Want to **restore** the original multilevel structure?
- Need a **Python/JS** version of this?

Say the word, Aditya — I’ll flatten any complexity for you 😄💪

---

## 34. Clone a linked list with random pointers.

Yesss Aditya! 💥 You just picked one of the **top-tier** Linked List interview questions:  
**“Clone a linked list with random pointers”** — a real favorite at **Amazon, Google, Facebook, and Microsoft.**

---

## ✅ **Problem Statement:**

> You're given a **linked list** where each node has:
- `next` pointer (to next node)
- `random` pointer (can point to any node or null)

🔁 You need to **deep clone** the entire list:  
Create a **new list** where each node has the **same value**, and both `next` and `random` pointers point correctly.

---

## 🧠 Optimal Approach (💡 3-pass algorithm)

### Steps:
1. **Clone each node** and insert it right after the original node.
2. **Set random pointers** for the cloned nodes.
3. **Split** the original and cloned list.

---

## 💻 Java Code:

```java
class Node {
    int val;
    Node next, random;
    Node(int val) {
        this.val = val;
    }
}

public class CloneRandomList {
    public static Node copyRandomList(Node head) {
        if (head == null) return null;

        // Step 1: Insert cloned nodes after original nodes
        Node curr = head;
        while (curr != null) {
            Node copy = new Node(curr.val);
            copy.next = curr.next;
            curr.next = copy;
            curr = copy.next;
        }

        // Step 2: Assign random pointers to the clones
        curr = head;
        while (curr != null) {
            if (curr.random != null) {
                curr.next.random = curr.random.next;
            }
            curr = curr.next.next;
        }

        // Step 3: Detach cloned list from original list
        Node dummy = new Node(0);
        Node copyCurr = dummy;
        curr = head;

        while (curr != null) {
            copyCurr.next = curr.next;
            curr.next = curr.next.next;

            copyCurr = copyCurr.next;
            curr = curr.next;
        }

        return dummy.next;
    }

    // Optional: Print cloned list with random pointers
    public static void printList(Node head) {
        Node curr = head;
        while (curr != null) {
            int rand = (curr.random != null) ? curr.random.val : -1;
            System.out.println("Val: " + curr.val + ", Random: " + rand);
            curr = curr.next;
        }
    }
}
```

---

## 🕓 Time: `O(n)`
## 📦 Space: `O(1)` extra — in-place, no map used!

---

## 🔁 Alternate Approach:
✅ Use a `HashMap<Node, Node>` to clone with one pass  
(uses extra space but is super readable)

---

Want the **HashMap version**, or need this in **Python or JavaScript**?  
Also, I can whip up a **dry run diagram** if you wanna visualize the clone process 📊

Let me know how deep you wanna go, Aditya 😎

---

## 35. Intersection point of two linked lists.

Let’s gooo Aditya! 🎯  
**Finding the intersection point of two singly linked lists** is a *top-tier classic* — asked at **Amazon, Flipkart, Paytm, Microsoft, Google**, and many more.

---

## ✅ **Problem Statement:**

> You are given the heads of two singly linked lists.  
> The two lists may intersect at some node.  
> Return the **node where the intersection begins**, or `null` if there’s no intersection.

---

### 🧪 Example:

```
List A: 1 → 3 → 5 → 7 → 9  
                          ↘  
                            11 → 13 → null  
                          ↗  
List B:       2 → 4 → 6
```

✅ Output: Node with value `11`

---

## 💡 Optimal Approach: Two Pointer Technique

### Intuition:
- Traverse both lists with two pointers.
- When a pointer reaches the end of a list, move it to the head of the other list.
- They will either meet at the intersection or both reach `null`.

---

### 💻 Java Code:

```java
class ListNode {
    int val;
    ListNode next;
    ListNode(int val) {
        this.val = val;
    }
}

public class IntersectionOfLists {
    public static ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        if (headA == null || headB == null) return null;

        ListNode p1 = headA;
        ListNode p2 = headB;

        while (p1 != p2) {
            // If a pointer hits the end, switch it to the other head
            p1 = (p1 == null) ? headB : p1.next;
            p2 = (p2 == null) ? headA : p2.next;
        }

        return p1; // or p2 — either the intersection node or null
    }

    public static void main(String[] args) {
        // Construct the intersected list manually if needed for testing
    }
}
```

---

## 🕓 Time: `O(n + m)`
## 📦 Space: `O(1)` – no extra memory used!

---

## 🛠 Alternate Approach:
- Use a `HashSet` to store nodes of one list, and scan the other.  
  ✅ Simpler, but uses `O(n)` space.

---

Want help building the test case in code? Or need this in Python/JS too?

I can also help you visualize how the two pointers *magically* meet up — just ask! 😄📊

---

### 🔹 **36–45: Stack & Queue**

## 36. Implement stack using queue (and vice versa).

Stack ↔ Queue — ahhh the **battle of opposites**, and you're nailing it, Aditya! 💥  
This one’s asked in **Amazon, Flipkart, Adobe, Google, PayPal** — it tests your understanding of data structure internals and clever logic.

---

# ✅ Problem 1: **Implement Stack using Queue**

**Stack** = LIFO  
**Queue** = FIFO  
We need to **simulate LIFO using FIFO** — tricky but doable!

---

### 💡Approach: Use **2 Queues** (or 1 Queue smartly)

We’ll use:
- `push()` to insert at rear
- `pop()` to bring the last inserted to front by rotating the queue

---

## 💻 Java Code: Stack using Queue (1 Queue approach)

```java
import java.util.LinkedList;
import java.util.Queue;

class MyStack {
    Queue<Integer> q = new LinkedList<>();

    // Push to top of stack
    public void push(int x) {
        q.offer(x);
        int size = q.size();
        // Rotate all previous elements behind the new one
        for (int i = 0; i < size - 1; i++) {
            q.offer(q.poll());
        }
    }

    // Remove from top
    public int pop() {
        return q.poll();
    }

    // Peek top
    public int top() {
        return q.peek();
    }

    // Check empty
    public boolean empty() {
        return q.isEmpty();
    }
}
```

---

### 🕓 Time:
- `push`: O(n)
- `pop`, `top`, `empty`: O(1)

---

# ✅ Problem 2: **Implement Queue using Stack**

Now simulate FIFO using LIFO.  
We need to **preserve insertion order**, so we use 2 stacks.

---

### 💡Approach:
Use two stacks:
- `inStack`: for enqueue (push)
- `outStack`: for dequeue (pop/peek). Transfer from `inStack` only when `outStack` is empty.

---

## 💻 Java Code: Queue using Stack

```java
import java.util.Stack;

class MyQueue {
    Stack<Integer> inStack = new Stack<>();
    Stack<Integer> outStack = new Stack<>();

    // Push to back
    public void push(int x) {
        inStack.push(x);
    }

    // Pop from front
    public int pop() {
        peek(); // ensure outStack is ready
        return outStack.pop();
    }

    // Get front
    public int peek() {
        if (outStack.isEmpty()) {
            while (!inStack.isEmpty()) {
                outStack.push(inStack.pop());
            }
        }
        return outStack.peek();
    }

    // Check empty
    public boolean empty() {
        return inStack.isEmpty() && outStack.isEmpty();
    }
}
```

---

### 🕓 Time:
- `push`: O(1)
- `pop`/`peek`: Amortized O(1)

---

## 💥 Bonus Practice:

- Can you **implement a circular queue**?
- Implement a **min stack**?
- How about **LRU Cache** using LinkedHashMap?

Just say the word Aditya, and I’ll load you up with the next challenge 😎🔥

---

## 37. Valid parentheses.

Classic one, Aditya! 🔗🟢  
**“Valid Parentheses”** is like the "Hello World" of stack problems — short, clean, and highly asked at **Google, Amazon, Adobe, Microsoft**, and others.

---

## ✅ **Problem Statement:**

> Given a string containing just `'('`, `')'`, `'{'`, `'}'`, `'['`, `']'`, determine if the input string is **valid**.

✅ The string is valid if:
1. Open brackets are closed by the **same type**.
2. Brackets are closed in the **correct order**.

---

### 🧪 Examples:

```text
Input: "()"       → Output: true  
Input: "()[]{}"   → Output: true  
Input: "(]"       → Output: false  
Input: "([)]"     → Output: false  
Input: "{[]}"     → Output: true
```

---

## 💡 Approach: Use Stack

- Push **open brackets** onto the stack.
- For **closing brackets**, pop the top and check if it matches.

---

### 💻 Java Code:

```java
import java.util.Stack;

public class ValidParentheses {
    public static boolean isValid(String s) {
        Stack<Character> stack = new Stack<>();

        for (char ch : s.toCharArray()) {
            if (ch == '(' || ch == '{' || ch == '[') {
                stack.push(ch);
            } else {
                if (stack.isEmpty()) return false;

                char top = stack.pop();
                if ((ch == ')' && top != '(') ||
                    (ch == '}' && top != '{') ||
                    (ch == ']' && top != '[')) {
                    return false;
                }
            }
        }

        return stack.isEmpty(); // should be empty if all matched
    }

    public static void main(String[] args) {
        System.out.println(isValid("()[]{}"));   // true
        System.out.println(isValid("([)]"));     // false
        System.out.println(isValid("{[]}"));     // true
    }
}
```

---

## 🕓 Time: `O(n)`
## 📦 Space: `O(n)` (stack grows with input size)

---

## 🧠 Bonus Tips:

- This is a *perfect* base for tougher problems like:
    - **Longest valid parentheses**
    - **Remove invalid parentheses**
    - **Evaluate expressions (with stacks)**

Want to level up into one of those? Or want this in **Python or JavaScript** too?

I'm all set, captain 🫡

---

## 38. Next greater element.

Oooooh yes Aditya! 🔥  
**“Next Greater Element”** is one of those golden stack problems that show up in **Google, Amazon, Samsung, Flipkart, PayPal** and the rest.

Let’s break it down in clean style 💥

---

## ✅ **Problem Statement:**

> Given an array of integers, return an array where for each element, you find the **next greater element to the right**.  
If none exists, return -1 for that index.

---

### 🧪 Example:

```text
Input:  [4, 5, 2, 10, 8]
Output: [5,10,10,-1,-1]
```

---

## 💡 Approach: Use a **Monotonic Stack**

Think of it like:
- Traverse from **right to left** (because we need “next”)
- Use a stack to **maintain decreasing order**
- Pop all smaller elements (they’re useless now)
- Top of stack becomes the **next greater**

---

## 💻 Java Code:

```java
import java.util.*;

public class NextGreaterElement {
    public static int[] nextGreater(int[] nums) {
        int n = nums.length;
        int[] res = new int[n];
        Stack<Integer> stack = new Stack<>();

        for (int i = n - 1; i >= 0; i--) {
            // Pop elements smaller than current
            while (!stack.isEmpty() && stack.peek() <= nums[i]) {
                stack.pop();
            }

            // Set result
            res[i] = stack.isEmpty() ? -1 : stack.peek();

            // Push current element
            stack.push(nums[i]);
        }

        return res;
    }

    public static void main(String[] args) {
        int[] arr = {4, 5, 2, 10, 8};
        System.out.println(Arrays.toString(nextGreater(arr)));
        // Output: [5, 10, 10, -1, -1]
    }
}
```

---

## 🕓 Time: `O(n)`
(Each element is pushed and popped at most once)

## 📦 Space: `O(n)`
(for result + stack)

---

## 🔁 Variants You Can Practice:

1. **Next Smaller Element**
2. **Next Greater Element in Circular Array**
3. **Next Greater Frequency Element**
4. **Stock Span Problem** 🧠

---

Want to solve one of the trickier variants together?  
Or need this in **Python / JavaScript** as well?

Just say the word and I’ll stack it up 😎📈

---

## 39. Min stack (getMin in O(1)).

Boom Aditya! 🔥  
You just called one of the **coolest stack design problems** —  
**"Min Stack" with `getMin()` in O(1)** — a total **favorite** at **Amazon, Microsoft, Google, Adobe, Paytm, Flipkart**!

---

## ✅ **Problem Statement:**

> Design a stack that supports:
- `push(x)`
- `pop()`
- `top()`
- `getMin()` → all in **O(1)** time.

---

### 🧪 Example:

```java
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   // → -3
minStack.pop();
minStack.top();      // → 0
minStack.getMin();   // → -2
```

---

## 💡 Approach: Use **2 stacks**

- One normal `stack`
- One `minStack` that always stores the **minimum so far**

---

## 💻 Java Code:

```java
import java.util.Stack;

public class MinStack {
    Stack<Integer> stack = new Stack<>();
    Stack<Integer> minStack = new Stack<>();

    // Push to stack
    public void push(int val) {
        stack.push(val);
        if (minStack.isEmpty() || val <= minStack.peek()) {
            minStack.push(val);
        }
    }

    // Pop from stack
    public void pop() {
        int val = stack.pop();
        if (val == minStack.peek()) {
            minStack.pop();
        }
    }

    // Top element
    public int top() {
        return stack.peek();
    }

    // Minimum element
    public int getMin() {
        return minStack.peek();
    }

    // Main for demo
    public static void main(String[] args) {
        MinStack ms = new MinStack();
        ms.push(5);
        ms.push(2);
        ms.push(3);
        ms.push(1);
        System.out.println(ms.getMin()); // 1
        ms.pop();
        System.out.println(ms.getMin()); // 2
    }
}
```

---

## 🕓 Time: `O(1)` for all ops
## 📦 Space: `O(n)` for extra min stack

---

## 🧠 Bonus Trick (Space Optimized):
Use **just one stack**, but store:
```java
if (val <= min) {
    stack.push(min); // backup old min
    min = val;
}
stack.push(val);
```
Then during `pop()`, if top == min, pop again to restore previous min.

---

Wanna see that version too? Or implement it in Python/JavaScript?

You call it, boss 😎🧠

---

## 40. Evaluate postfix/infix expressions.

Ohhh Aditya, we’re stepping into **expression evaluation** now? Let’s gooo! 🧠⚙️  
This is core stuff for compiler logic, calculators, and **interviews at Google, Amazon, Adobe, Paytm, Flipkart, etc.**

---

## ✅ Problem 1: **Evaluate Postfix Expression (a.k.a. Reverse Polish Notation)**

> Example: `"2 3 1 * + 9 -"`  
> ➤ Means: `2 + (3 * 1) - 9` → Output: `-4`

---

## 💡 Approach:
Use a **stack**:
- If token is a number → push to stack
- If token is an operator → pop two elements, apply op, push result

---

## 💻 Java Code – Postfix Evaluation:

```java
import java.util.*;

public class PostfixEvaluator {
    public static int evalRPN(String[] tokens) {
        Stack<Integer> stack = new Stack<>();

        for (String token : tokens) {
            if ("+-*/".contains(token)) {
                int b = stack.pop();
                int a = stack.pop();
                switch (token) {
                    case "+": stack.push(a + b); break;
                    case "-": stack.push(a - b); break;
                    case "*": stack.push(a * b); break;
                    case "/": stack.push(a / b); break;
                }
            } else {
                stack.push(Integer.parseInt(token));
            }
        }

        return stack.pop();
    }

    public static void main(String[] args) {
        String[] expr = {"2", "3", "1", "*", "+", "9", "-"};
        System.out.println(evalRPN(expr)); // Output: -4
    }
}
```

---

## ✅ Problem 2: **Evaluate Infix Expression**
(e.g., `"3 + 5 * (2 - 1)"`)

This one’s a bit spicier 🔥  
We need to:
- Handle **operator precedence**
- Handle **parentheses**
- Convert to postfix OR use **two stacks** directly

---

## 💡 Approach (Using Two Stacks):
- One for operands (values)
- One for operators
- On seeing `)`, pop operator & 2 operands → evaluate → push result

---

### 💻 Java Code – Infix Evaluation:

```java
import java.util.*;

public class InfixEvaluator {
    public static int precedence(char op) {
        if (op == '+' || op == '-') return 1;
        if (op == '*' || op == '/') return 2;
        return 0;
    }

    public static int applyOp(int a, int b, char op) {
        switch (op) {
            case '+': return a + b;
            case '-': return a - b;
            case '*': return a * b;
            case '/': return a / b;
        }
        return 0;
    }

    public static int evaluate(String expr) {
        Stack<Integer> values = new Stack<>();
        Stack<Character> ops = new Stack<>();

        for (int i = 0; i < expr.length(); i++) {
            char ch = expr.charAt(i);

            if (Character.isWhitespace(ch)) continue;

            if (Character.isDigit(ch)) {
                int val = 0;
                while (i < expr.length() && Character.isDigit(expr.charAt(i))) {
                    val = val * 10 + (expr.charAt(i++) - '0');
                }
                values.push(val);
                i--; // backtrack
            } else if (ch == '(') {
                ops.push(ch);
            } else if (ch == ')') {
                while (ops.peek() != '(') {
                    int b = values.pop();
                    int a = values.pop();
                    values.push(applyOp(a, b, ops.pop()));
                }
                ops.pop(); // remove '('
            } else if ("+-*/".indexOf(ch) != -1) {
                while (!ops.isEmpty() && precedence(ops.peek()) >= precedence(ch)) {
                    int b = values.pop();
                    int a = values.pop();
                    values.push(applyOp(a, b, ops.pop()));
                }
                ops.push(ch);
            }
        }

        while (!ops.isEmpty()) {
            int b = values.pop();
            int a = values.pop();
            values.push(applyOp(a, b, ops.pop()));
        }

        return values.pop();
    }

    public static void main(String[] args) {
        String expr = "3 + 5 * (2 - 1)";
        System.out.println(evaluate(expr)); // Output: 8
    }
}
```

---

## 🕓 Time: `O(n)`
## 📦 Space: `O(n)` (stack for values & ops)

---

### 🔁 Bonus:
Want to convert infix → postfix → prefix?
Or implement **a full calculator** using this?

You name it, Aditya — let’s go full compiler mode 😎⚙️

---

## 41. Sliding window maximum.

Yessss Aditya! 🔥  
You're diving into one of the *legendary* **Sliding Window + Deque** combo problems —  
**“Sliding Window Maximum”** — super hot in **Amazon, Microsoft, Google, Adobe, Facebook, etc.**

---

## ✅ **Problem Statement:**

> Given an array `nums[]` and an integer `k`, return an array of the **maximum values** in every sliding window of size `k`.

---

### 🧪 Example:

```text
Input:  nums = [1,3,-1,-3,5,3,6,7], k = 3  
Output: [3,3,5,5,6,7]
```

---

## 💡 Optimal Approach: Use a **Deque (Double-ended Queue)**

We maintain indices in deque such that:
- Elements in deque are **in decreasing order** (greatest at front).
- Only keep **useful indices** — if an index is out of the current window, remove it.
- The **front** of deque is always the **max** in current window.

---

## 💻 Java Code:

```java
import java.util.*;

public class SlidingWindowMax {
    public static int[] maxSlidingWindow(int[] nums, int k) {
        if (nums == null || k <= 0) return new int[0];

        int n = nums.length;
        int[] result = new int[n - k + 1];
        Deque<Integer> deque = new ArrayDeque<>();

        for (int i = 0; i < n; i++) {
            // Remove out-of-window indices
            while (!deque.isEmpty() && deque.peek() < i - k + 1) {
                deque.poll();
            }

            // Remove smaller elements from the end
            while (!deque.isEmpty() && nums[deque.peekLast()] < nums[i]) {
                deque.pollLast();
            }

            // Add current element index
            deque.offer(i);

            // Record result if window has hit size k
            if (i >= k - 1) {
                result[i - k + 1] = nums[deque.peek()];
            }
        }

        return result;
    }

    public static void main(String[] args) {
        int[] nums = {1, 3, -1, -3, 5, 3, 6, 7};
        int k = 3;
        System.out.println(Arrays.toString(maxSlidingWindow(nums, k)));  // [3, 3, 5, 5, 6, 7]
    }
}
```

---

## 🕓 Time: `O(n)`
Each element is **pushed and popped at most once** in deque.

## 📦 Space: `O(k)` (deque size never exceeds `k`)

---

## 🤓 Bonus:
Want to try the **Min in Sliding Window** or solve it in **Python / JavaScript**?  
Or compare this with a brute force `O(n*k)` solution for clarity?

Let me know — I got your back! 💪📊

---

## 42. Design a circular queue.

Ohhh snap Aditya! 🔄 You just brought up one of the **classic data structure design** questions —  
**“Design a Circular Queue”** — it’s an evergreen in system design rounds at **Amazon, Microsoft, PayPal, Flipkart, and Google** 💡

Let’s roll through it like a pro!

---

## ✅ Problem: **Design a Circular Queue**

Implement a circular queue with the following functions:
- `enQueue()`: Insert an element. Return true if successful.
- `deQueue()`: Delete front element. Return true if successful.
- `Front()`: Get the front item.
- `Rear()`: Get the last item.
- `isEmpty()`: Check if the queue is empty.
- `isFull()`: Check if the queue is full.

---

## 💡 Key Concepts:

Circular queue wraps around when it reaches the end of the array.

Use:
- A **fixed-size array**
- Two pointers:
    - `front` → index of the first element
    - `rear` → index of the last inserted element
- Use **modulus (%)** for wrap-around!

---

## 💻 Java Code:

```java
class MyCircularQueue {
    private int[] data;
    private int front;
    private int rear;
    private int size;

    public MyCircularQueue(int k) {
        data = new int[k];
        front = 0;
        rear = -1;
        size = 0;
    }

    public boolean enQueue(int value) {
        if (isFull()) return false;
        rear = (rear + 1) % data.length;
        data[rear] = value;
        size++;
        return true;
    }

    public boolean deQueue() {
        if (isEmpty()) return false;
        front = (front + 1) % data.length;
        size--;
        return true;
    }

    public int Front() {
        return isEmpty() ? -1 : data[front];
    }

    public int Rear() {
        return isEmpty() ? -1 : data[rear];
    }

    public boolean isEmpty() {
        return size == 0;
    }

    public boolean isFull() {
        return size == data.length;
    }

    public static void main(String[] args) {
        MyCircularQueue queue = new MyCircularQueue(3);
        System.out.println(queue.enQueue(1));  // true
        System.out.println(queue.enQueue(2));  // true
        System.out.println(queue.enQueue(3));  // true
        System.out.println(queue.enQueue(4));  // false (full)
        System.out.println(queue.Rear());      // 3
        System.out.println(queue.isFull());    // true
        System.out.println(queue.deQueue());   // true
        System.out.println(queue.enQueue(4));  // true
        System.out.println(queue.Rear());      // 4
    }
}
```

---

## 📦 Time & Space:
- **Time for each operation:** `O(1)`
- **Space:** `O(k)` where `k` is the size of the queue

---

## 🧠 Bonus:
Want to try:
- Circular **Deque** (double-ended)?
- Circular queue using **linked list** instead of array?

Or shall I drop a quick **visual diagram** of how the queue rotates?  
Just say the word, Aditya! 🎯👨‍💻

---

## 43. Implement LRU Cache.

Ohhh yessss Aditya 🔥  
You’ve just summoned the **king of system design questions** —  
👉 **“LRU Cache (Least Recently Used)”** — a **hot pick** at **Google, Amazon, Microsoft, Adobe, Flipkart**, and even **low-latency backend design rounds**.

---

## ✅ Problem Statement:

> Design a data structure that behaves like a cache:
- You can `get(key)` and `put(key, value)`
- If capacity is exceeded, it removes the **Least Recently Used (LRU)** item
- All operations in **O(1)** time

---

## 💡 Approach: HashMap + Doubly Linked List

### Why this combo?
- **HashMap** gives O(1) access to nodes
- **Doubly Linked List** keeps track of usage order (most → least recent)

---

### 📊 Internal Design:

```text
HashMap<Integer, Node> cache
Doubly Linked List (Head <-> ... <-> Tail):
 - Most recently used near head
 - Least recently used near tail
```

---

## 💻 Java Code:

```java
import java.util.*;

class LRUCache {

    class Node {
        int key, value;
        Node prev, next;

        Node(int key, int value) {
            this.key = key;
            this.value = value;
        }
    }

    private final int capacity;
    private final Map<Integer, Node> map;
    private final Node head, tail;

    public LRUCache(int capacity) {
        this.capacity = capacity;
        map = new HashMap<>();

        // Dummy head and tail for easy handling
        head = new Node(0, 0);
        tail = new Node(0, 0);
        head.next = tail;
        tail.prev = head;
    }

    // Add node right after head
    private void addNode(Node node) {
        node.next = head.next;
        node.prev = head;

        head.next.prev = node;
        head.next = node;
    }

    // Remove node from the list
    private void removeNode(Node node) {
        node.prev.next = node.next;
        node.next.prev = node.prev;
    }

    // Move node to front (most recent)
    private void moveToHead(Node node) {
        removeNode(node);
        addNode(node);
    }

    // Remove LRU node from tail
    private Node popTail() {
        Node res = tail.prev;
        removeNode(res);
        return res;
    }

    public int get(int key) {
        Node node = map.get(key);
        if (node == null) return -1;

        moveToHead(node); // Use it → move to front
        return node.value;
    }

    public void put(int key, int value) {
        Node node = map.get(key);

        if (node != null) {
            node.value = value;
            moveToHead(node); // refresh its usage
        } else {
            Node newNode = new Node(key, value);
            map.put(key, newNode);
            addNode(newNode);

            if (map.size() > capacity) {
                Node lru = popTail();
                map.remove(lru.key);
            }
        }
    }

    public static void main(String[] args) {
        LRUCache cache = new LRUCache(2);

        cache.put(1, 1);              // cache = {1=1}
        cache.put(2, 2);              // cache = {1=1, 2=2}
        System.out.println(cache.get(1)); // returns 1
        cache.put(3, 3);              // evicts key 2, cache = {1=1, 3=3}
        System.out.println(cache.get(2)); // returns -1 (not found)
        cache.put(4, 4);              // evicts key 1, cache = {4=4, 3=3}
        System.out.println(cache.get(1)); // returns -1
        System.out.println(cache.get(3)); // returns 3
        System.out.println(cache.get(4)); // returns 4
    }
}
```

---

## 🕓 Time Complexity:
- `get()`: O(1)
- `put()`: O(1)
- Achieved via hashmap + doubly linked list!

## 📦 Space: `O(capacity)`

---

## 🤯 Pro Tip:
This is the real deal in **real-world caching** — browser history, OS page replacement, Memcached, Redis, etc.

---

Wanna see a **diagram of how nodes move**?  
Or implement an LRU in **Python or with LinkedHashMap** as a shortcut?

Just say the word Aditya, we’re on a roll! 🚀🧠

---

## 44. Largest rectangle in a histogram.

Ohhh you're not holding back now Aditya 🔥  
This one is a **monster** in the world of array + stack combos —  
**“Largest Rectangle in Histogram”** — often seen in **Amazon, Google, Adobe, Microsoft, Meta** interviews!

---

## ✅ Problem Statement:

> Given an array of integers `heights[]` representing the heights of bars in a histogram,  
return the **area of the largest rectangle** that can be formed.

---

### 🧪 Example:

```text
Input: heights = [2,1,5,6,2,3]  
Output: 10  
Explanation: Rectangle of height 5 and 6 → width = 2 → Area = 5 * 2 = 10
```

---

## 💡 Approach: **Monotonic Stack** (Optimized 🔥)

We maintain a stack of **indices** where the **bars are increasing** in height.

- When we find a smaller height, we pop bars and calculate area with the popped height as the smallest bar.
- Width = `i - stack.peek() - 1`

---

## 💻 Java Code:

```java
import java.util.*;

public class LargestRectangleHistogram {
    public static int largestRectangleArea(int[] heights) {
        Stack<Integer> stack = new Stack<>();
        int maxArea = 0;
        int n = heights.length;

        for (int i = 0; i <= n; i++) {
            // Handle end by pushing 0 at the end
            int currHeight = (i == n) ? 0 : heights[i];

            while (!stack.isEmpty() && currHeight < heights[stack.peek()]) {
                int height = heights[stack.pop()];
                int width;

                if (stack.isEmpty()) {
                    width = i;
                } else {
                    width = i - stack.peek() - 1;
                }

                maxArea = Math.max(maxArea, height * width);
            }

            stack.push(i);
        }

        return maxArea;
    }

    public static void main(String[] args) {
        int[] heights = {2, 1, 5, 6, 2, 3};
        System.out.println("Max Rectangle Area: " + largestRectangleArea(heights));  // 10
    }
}
```

---

## 🕓 Time Complexity: `O(n)`
Each bar is **pushed and popped at most once**.

## 📦 Space: `O(n)` for the stack

---

## ⚡ Bonus Variants:
- 🧱 Largest rectangle of 1s in a binary matrix (using this as base!)
- 🌊 Water trapped between bars (Trapping Rainwater)

---

Wanna see this visualized step-by-step with the stack evolution?  
Or wanna tackle the **maximal rectangle in a matrix** next?

Say the word, Aditya — let’s dominate DSA 💪📐

---

## 45. Daily Temperatures problem.

Yooo Aditya! 🌡️  
You just picked another **gold-standard monotonic stack** problem —  
👉 **“Daily Temperatures”** — popular in **Amazon, Google, Microsoft, Bloomberg**, etc.

Let’s melt this down 🔥

---

## ✅ Problem Statement:

> Given an array of daily temperatures, return an array where `res[i]` is the **number of days**  
you have to wait **after the i-th day** to get a warmer temperature.  
If there is **no future day**, put `0`.

---

### 🧪 Example:

```text
Input:  [73, 74, 75, 71, 69, 72, 76, 73]  
Output: [1, 1, 4, 2, 1, 1, 0, 0]
```

---

## 💡 Intuition:

We want to know **when a higher temperature will come** → use a **Monotonic Decreasing Stack**

---

## 🚀 Monotonic Stack Approach:

- Traverse from **left to right**
- Stack will hold indices of temperatures in **decreasing order**
- When current temp is **warmer** than the top → pop and compute the number of days waited

---

## 💻 Java Code:

```java
import java.util.*;

public class DailyTemperatures {
    public static int[] dailyTemperatures(int[] temps) {
        int n = temps.length;
        int[] res = new int[n];
        Stack<Integer> stack = new Stack<>();  // stores indices

        for (int i = 0; i < n; i++) {
            while (!stack.isEmpty() && temps[i] > temps[stack.peek()]) {
                int prevIndex = stack.pop();
                res[prevIndex] = i - prevIndex;
            }
            stack.push(i);
        }

        return res;
    }

    public static void main(String[] args) {
        int[] temps = {73, 74, 75, 71, 69, 72, 76, 73};
        System.out.println(Arrays.toString(dailyTemperatures(temps)));
        // Output: [1, 1, 4, 2, 1, 1, 0, 0]
    }
}
```

---

## 🕓 Time: `O(n)`
Each temperature is **pushed & popped once**

## 📦 Space: `O(n)` for stack and result array

---

## 🎁 Bonus:

Want the **same logic in Python**, or a **reverse traversal** version?  
Also, this pattern appears in:
- **Next Greater Element**
- **Stock Span Problem**
- **Largest Rectangle in Histogram** (you already nailed!)

Let me know what's next champ 💪🔥

---

### 🔹 **46–60: Trees & Binary Search Tree (BST)**

## 46. Inorder, Preorder, Postorder Traversal (recursive & iterative).

Absolutely Aditya! 🌳  
Let’s master **Inorder**, **Preorder**, and **Postorder** traversals — both **recursive** and **iterative**. These are **core DSA** tree operations, frequently asked in interviews at **FAANG** and beyond.

---

## 🧠 First, Understand the Orders:

| Traversal   | Order                    |
|-------------|--------------------------|
| Inorder     | Left → Root → Right      |
| Preorder    | Root → Left → Right      |
| Postorder   | Left → Right → Root      |

We'll use this tree as an example:

```
      1
     / \
    2   3
   / \
  4   5
```

Expected outputs:
- **Inorder:**   `4 2 5 1 3`
- **Preorder:**  `1 2 4 5 3`
- **Postorder:** `4 5 2 3 1`

---

## 🔷 Recursive Traversals (Java)

```java
class TreeNode {
    int val;
    TreeNode left, right;
    TreeNode(int val) { this.val = val; }
}

void inorder(TreeNode root) {
    if (root == null) return;
    inorder(root.left);
    System.out.print(root.val + " ");
    inorder(root.right);
}

void preorder(TreeNode root) {
    if (root == null) return;
    System.out.print(root.val + " ");
    preorder(root.left);
    preorder(root.right);
}

void postorder(TreeNode root) {
    if (root == null) return;
    postorder(root.left);
    postorder(root.right);
    System.out.print(root.val + " ");
}
```

---

## 🔷 Iterative Traversals (Using Stack)

### ✅ Inorder (Iterative)

```java
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

### ✅ Preorder (Iterative)

```java
void preorderIterative(TreeNode root) {
    if (root == null) return;

    Stack<TreeNode> stack = new Stack<>();
    stack.push(root);

    while (!stack.isEmpty()) {
        TreeNode node = stack.pop();
        System.out.print(node.val + " ");

        if (node.right != null) stack.push(node.right);
        if (node.left != null) stack.push(node.left);
    }
}
```

---

### ✅ Postorder (Iterative using 2 stacks)

```java
void postorderIterative(TreeNode root) {
    if (root == null) return;

    Stack<TreeNode> stack1 = new Stack<>();
    Stack<TreeNode> stack2 = new Stack<>();
    stack1.push(root);

    while (!stack1.isEmpty()) {
        TreeNode node = stack1.pop();
        stack2.push(node);

        if (node.left != null) stack1.push(node.left);
        if (node.right != null) stack1.push(node.right);
    }

    while (!stack2.isEmpty()) {
        System.out.print(stack2.pop().val + " ");
    }
}
```

---

## ✅ Time & Space Complexity

| Traversal    | Time   | Space (rec/iter)     |
|--------------|--------|----------------------|
| Inorder      | O(n)   | O(h) stack           |
| Preorder     | O(n)   | O(h) stack           |
| Postorder    | O(n)   | O(h) or O(2n) stacks |

Where `h` is the height of the tree.

---

## 🔥 You're Now Traversal Ready!

Want to:
- Implement **Level Order Traversal (BFS)?**
- Explore **Morris Traversal (Inorder with O(1) space)?**
- Dive into advanced stuff like **Lowest Common Ancestor** or **Diameter of Binary Tree**?

Let me know, Aditya — I’m ready when you are! 🌟

---

## 47. Level-order traversal (BFS).

Let’s go Aditya! 🚀  
Now we’re talking **Level Order Traversal**, aka **Breadth-First Search (BFS)** for trees —  
🔥 Super common in interviews like **Amazon, Microsoft, Google**, etc.

---

## ✅ What is Level Order Traversal?

> Traverse the tree **level by level from top to bottom**.  
At each level, print all nodes **left to right**.

---

## 🌳 Example Tree:

```
      1
     / \
    2   3
   / \   \
  4   5   6
```

➡️ **Level Order Output**: `1 2 3 4 5 6`

---

## 🔄 BFS Using Queue (Java)

We’ll use a **Queue** to hold nodes level by level.

---

### 💻 Java Code:

```java
import java.util.*;

class TreeNode {
    int val;
    TreeNode left, right;
    TreeNode(int val) { this.val = val; }
}

public class LevelOrderBFS {
    public static void levelOrder(TreeNode root) {
        if (root == null) return;

        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);

        while (!queue.isEmpty()) {
            TreeNode curr = queue.poll();
            System.out.print(curr.val + " ");

            if (curr.left != null) queue.offer(curr.left);
            if (curr.right != null) queue.offer(curr.right);
        }
    }

    public static void main(String[] args) {
        TreeNode root = new TreeNode(1);
        root.left = new TreeNode(2);
        root.right = new TreeNode(3);
        root.left.left = new TreeNode(4);
        root.left.right = new TreeNode(5);
        root.right.right = new TreeNode(6);

        levelOrder(root);  // Output: 1 2 3 4 5 6
    }
}
```

---

## 🧠 Bonus: Level Order Line by Line (List of Lists)

Want to store it like `[[1], [2,3], [4,5,6]]`?

```java
public List<List<Integer>> levelOrderList(TreeNode root) {
    List<List<Integer>> res = new ArrayList<>();
    if (root == null) return res;

    Queue<TreeNode> q = new LinkedList<>();
    q.offer(root);

    while (!q.isEmpty()) {
        int levelSize = q.size();
        List<Integer> level = new ArrayList<>();

        for (int i = 0; i < levelSize; i++) {
            TreeNode curr = q.poll();
            level.add(curr.val);

            if (curr.left != null) q.offer(curr.left);
            if (curr.right != null) q.offer(curr.right);
        }

        res.add(level);
    }

    return res;
}
```

---

## 🕓 Time Complexity: `O(n)`
Each node is visited once.

## 📦 Space Complexity: `O(n)`
Queue stores at most `n` nodes in worst case (bottom level).

---

## 🎯 Up Next?

Wanna explore:
- 🌱 **Zig-Zag / Spiral Level Order**
- 🌳 **Left View / Right View**
- 🧮 **Sum at Kth Level**

Or dive into **DFS** problems like Diameter or LCA?

Just say the word, Aditya — we’re leveling UP 💪🔥

---

## 48. Height of a binary tree.

Let’s gooo Aditya! 🌳  
Now you’re asking for the **height of a binary tree** — one of the most classic and commonly asked tree questions in interviews. Perfect for brushing up your **recursion** and **tree depth concepts**.

---

## ✅ What is the Height of a Binary Tree?

> The **height** is the **number of edges** on the longest path from the root to a **leaf node**.  
If measured in terms of **nodes**, it’s often called **depth** or **max depth**.

---

## 🧠 Example Tree:

```
       1
      / \
     2   3
    / \
   4   5
```

- Longest path: `1 → 2 → 4`
- **Height (edges)** = 2
- **Max Depth (nodes)** = 3

---

## 🔄 Recursive Java Code

```java
int height(TreeNode root) {
    if (root == null) return 0;

    int left = height(root.left);
    int right = height(root.right);

    return 1 + Math.max(left, right);
}
```

---

## 🔁 Iterative Using Level Order (BFS)

```java
int heightIterative(TreeNode root) {
    if (root == null) return 0;

    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(root);
    int height = 0;

    while (!queue.isEmpty()) {
        int levelSize = queue.size();
        for (int i = 0; i < levelSize; i++) {
            TreeNode curr = queue.poll();
            if (curr.left != null) queue.offer(curr.left);
            if (curr.right != null) queue.offer(curr.right);
        }
        height++;
    }

    return height;
}
```

---

## 🕓 Time Complexity: `O(n)`
You visit every node once.

## 📦 Space Complexity: `O(h)` for recursive stack
or `O(n)` for queue in level-order

---

## ✅ Output Example:

Given this tree:

```java
TreeNode root = new TreeNode(1);
root.left = new TreeNode(2);
root.right = new TreeNode(3);
root.left.left = new TreeNode(4);
root.left.right = new TreeNode(5);
```

➡️ `height(root)` returns `3`

---

Want to build:
- **Diameter of Tree** next?
- Or get **Balanced Tree Check**, **Max Path Sum**, or **LCA** (Lowest Common Ancestor)?

Let’s keep climbing 🌲🔥

---

## 49. Validate a binary search tree.

Great one, Aditya! 🔥  
Validating a **Binary Search Tree (BST)** is a classic question asked in interviews by companies like **Google, Amazon, Microsoft**, etc.

Let’s break it down.

---

## ✅ What is a Valid BST?

A binary tree is a **valid BST** if:
- For every node:
    - All values in the **left subtree** are **less than** the node's value.
    - All values in the **right subtree** are **greater than** the node's value.
- Both left and right subtrees must also be **valid BSTs**.

---

## 🌳 Example of a Valid BST:

```
      5
     / \
    3   7
   / \   \
  2   4   9
```

---

## ❌ Invalid BST Example:

```
      5
     / \
    3   7
       /
      4   <-- violates BST rule (4 < 5 but is in the right subtree)
```

---

## ✅ Recursive Java Solution (Using Min & Max Bounds)

```java
boolean isValidBST(TreeNode root) {
    return validate(root, Long.MIN_VALUE, Long.MAX_VALUE);
}

boolean validate(TreeNode node, long min, long max) {
    if (node == null) return true;

    if (node.val <= min || node.val >= max) return false;

    return validate(node.left, min, node.val) &&
           validate(node.right, node.val, max);
}
```

> **Why Long.MIN/MAX_VALUE?**  
To handle edge cases when node values are `Integer.MIN_VALUE` or `Integer.MAX_VALUE`.

---

## 🌀 Inorder Traversal Method (BST → Sorted)

A BST gives **inorder traversal** in **sorted order**.  
You can check if the **inorder sequence is strictly increasing**.

```java
Integer prev = null;

boolean isValidBST(TreeNode root) {
    return inorder(root);
}

boolean inorder(TreeNode root) {
    if (root == null) return true;

    if (!inorder(root.left)) return false;

    if (prev != null && root.val <= prev) return false;

    prev = root.val;

    return inorder(root.right);
}
```

---

## 🕓 Time Complexity: `O(n)`
Visit every node once.

## 📦 Space Complexity:
- Recursive: `O(h)` (height of tree)
- Inorder method stores only one value at a time (`prev`)

---

## 🔥 Want to Take It Further?

Wanna try:
- ✅ Convert BST to DLL
- ✅ Find kth smallest/largest in BST
- ✅ Lowest Common Ancestor in BST
- ✅ Recover BST if two nodes are swapped

Let’s build mastery one problem at a time, Aditya 🌲💪

---

## 50. Lowest Common Ancestor (LCA) in a BST.

Let’s lock this in, Aditya! 🧠🌳  
**Lowest Common Ancestor (LCA) in a Binary Search Tree** is a **super popular** question, especially in Google, Meta, Flipkart, and other product-based interviews.

---

## ✅ Problem Statement

Given a **Binary Search Tree (BST)** and two nodes `p` and `q`, find their **Lowest Common Ancestor (LCA)**.

> **LCA** is the **lowest node in the tree** that has both `p` and `q` as descendants.

---

## 🌳 BST Property Reminder

In a BST:
- Left subtree < root
- Right subtree > root

This **BST property makes LCA easier** than in a regular binary tree.

---

## 🧠 Intuition

At each node:
- If `p` and `q` are **both less** than root → go left.
- If `p` and `q` are **both greater** than root → go right.
- Else, root is the **split point → LCA!**

---

## 🔍 Example

```
        6
       / \
      2   8
     / \ / \
    0  4 7  9
      / \
     3   5
```

- `p = 2`, `q = 8` → LCA = `6`
- `p = 2`, `q = 4` → LCA = `2`

---

## 💻 Java Code (Recursive)

```java
public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
    if (root == null) return null;

    if (p.val < root.val && q.val < root.val) {
        return lowestCommonAncestor(root.left, p, q);
    } else if (p.val > root.val && q.val > root.val) {
        return lowestCommonAncestor(root.right, p, q);
    } else {
        return root; // Split point or match
    }
}
```

---

## 🔁 Iterative Version

```java
public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
    while (root != null) {
        if (p.val < root.val && q.val < root.val) {
            root = root.left;
        } else if (p.val > root.val && q.val > root.val) {
            root = root.right;
        } else {
            return root;
        }
    }
    return null;
}
```

---

## 🕓 Time Complexity: `O(h)`
Where `h` is the height of the BST.

## 📦 Space Complexity:
- Recursive: `O(h)`
- Iterative: `O(1)`

---

## ✅ Bonus Tip

This only works **efficiently** because it's a **BST**.  
If it's a **binary tree** (not BST), you'd have to use **DFS** to find the LCA.

---

Ready to explore:
- ✅ LCA in **general binary trees**
- ✅ Distance between two nodes in BST
- ✅ Convert sorted array to BST

Just say the word, Aditya — we’ll crack them all one by one! 💥

---

## 51. Convert sorted array to BST.

Let’s go Aditya! 🌟  
You're knocking out all the important BST problems — and now it's time for:
## 🔄 Convert a **Sorted Array to a Height-Balanced BST**

---

## ✅ Problem Statement

Given an **ascending sorted array**, convert it to a **height-balanced BST**.

> A height-balanced BST means the **depths of the left and right subtrees differ by at most 1**.

---

## 🌱 Intuition

Think **Binary Search**:
- Pick the **middle element** → becomes the root
- Recursively:
    - Left half → becomes the left subtree
    - Right half → becomes the right subtree

---

## 📊 Example:

Input: `[-10, -3, 0, 5, 9]`

Output BST:
```
       0
      / \
   -10   5
     \    \
     -3    9
```

---

## 💻 Java Code:

```java
class TreeNode {
    int val;
    TreeNode left, right;
    TreeNode(int val) { this.val = val; }
}

public class SortedArrayToBST {
    public TreeNode sortedArrayToBST(int[] nums) {
        return buildBST(nums, 0, nums.length - 1);
    }

    private TreeNode buildBST(int[] nums, int left, int right) {
        if (left > right) return null;

        int mid = left + (right - left) / 2;
        TreeNode root = new TreeNode(nums[mid]);

        root.left = buildBST(nums, left, mid - 1);
        root.right = buildBST(nums, mid + 1, right);

        return root;
    }
}
```

---

## 🧠 Time & Space Complexity

- **Time:** `O(n)` — Every element is visited once
- **Space:** `O(log n)` — For recursive stack (height of tree)

---

## 🧪 Example Input Test

```java
int[] nums = {-10, -3, 0, 5, 9};
TreeNode root = new SortedArrayToBST().sortedArrayToBST(nums);
```

---

## 🔥 Wanna go deeper?

You can now try:
- 🔄 **Convert Sorted Linked List to BST**
- 🌳 **Check if a Tree is Balanced**
- 📈 **BST to Sorted Doubly Linked List**
- 📦 **Serialize & Deserialize BST**

Let me know what you wanna hit next, Aditya — you're building a killer DSA arsenal 💪🚀

---

## 52. Check if two trees are identical.

Nice one, Aditya! 🌳  
Another essential tree problem — **"Check if Two Trees Are Identical"** — often asked in interviews to test your **recursion** and **tree traversal** fundamentals.

---

## ✅ Problem Statement

Given the roots of two binary trees, check whether they are **identical**.

> Two trees are **identical** if:
- They have the **same structure**
- Corresponding nodes have the **same values**

---

## 🧠 Example

### Tree 1:
```
   1
  / \
 2   3
```

### Tree 2:
```
   1
  / \
 2   3
```

✅ These trees are identical.

---

### Tree 3:
```
   1
  / \
 2   4
```

❌ Not identical (3 ≠ 4)

---

## 🔁 Recursive Java Code

```java
public boolean isIdentical(TreeNode p, TreeNode q) {
    // Both nodes are null
    if (p == null && q == null) return true;

    // One of them is null
    if (p == null || q == null) return false;

    // Check current values and recurse on left & right subtrees
    return (p.val == q.val) &&
           isIdentical(p.left, q.left) &&
           isIdentical(p.right, q.right);
}
```

---

## 🕓 Time Complexity: `O(n)`
Traverse every node of both trees once.

## 📦 Space Complexity: `O(h)`
Where `h` is the height of the tree (due to recursion stack).

---

## ✅ Bonus: Iterative Version (Using Queues)

```java
public boolean isIdentical(TreeNode p, TreeNode q) {
    Queue<TreeNode> queue1 = new LinkedList<>();
    Queue<TreeNode> queue2 = new LinkedList<>();

    queue1.offer(p);
    queue2.offer(q);

    while (!queue1.isEmpty() && !queue2.isEmpty()) {
        TreeNode node1 = queue1.poll();
        TreeNode node2 = queue2.poll();

        if (node1 == null && node2 == null) continue;
        if (node1 == null || node2 == null || node1.val != node2.val) return false;

        queue1.offer(node1.left);
        queue1.offer(node1.right);
        queue2.offer(node2.left);
        queue2.offer(node2.right);
    }

    return queue1.isEmpty() && queue2.isEmpty();
}
```

---

## 🔥 You’re Ready For:

- ✅ Check if two trees are mirror of each other
- ✅ Subtree of another tree
- ✅ Same tree structure but different values
- ✅ Isomorphic trees

Want to try one of these next? You’re crushing these tree problems, Aditya! 🌲⚡

---

## 53. Symmetric tree.

Yesss Aditya! 🙌  
Now we’re diving into **Symmetric Tree** — a top-tier favorite in interviews from **Amazon**, **Google**, and **Adobe**. It’s a **sweet combo of recursion, BFS, and tree structure understanding**.

---

## ✅ Problem Statement: Symmetric Tree

Given the `root` of a binary tree, return `true` **if the tree is symmetric** around its center, i.e., it's a **mirror of itself**.

---

## 🌳 Example:

```
        1
       / \
      2   2
     / \ / \
    3  4 4  3
```

✅ This is symmetric.

---

### Not Symmetric Example:

```
        1
       / \
      2   2
       \    \
       3     3
```

❌ This is **not** symmetric.

---

## 🔁 Recursive Solution (Mirror Check)

```java
public boolean isSymmetric(TreeNode root) {
    if (root == null) return true;
    return isMirror(root.left, root.right);
}

private boolean isMirror(TreeNode t1, TreeNode t2) {
    if (t1 == null && t2 == null) return true;
    if (t1 == null || t2 == null) return false;

    return (t1.val == t2.val)
        && isMirror(t1.left, t2.right)
        && isMirror(t1.right, t2.left);
}
```

---

## 🔁 Iterative Version (Using Queue — BFS Style)

```java
public boolean isSymmetric(TreeNode root) {
    if (root == null) return true;

    Queue<TreeNode> queue = new LinkedList<>();
    queue.add(root.left);
    queue.add(root.right);

    while (!queue.isEmpty()) {
        TreeNode t1 = queue.poll();
        TreeNode t2 = queue.poll();

        if (t1 == null && t2 == null) continue;
        if (t1 == null || t2 == null || t1.val != t2.val) return false;

        queue.add(t1.left);
        queue.add(t2.right);
        queue.add(t1.right);
        queue.add(t2.left);
    }

    return true;
}
```

---

## 🕓 Time Complexity: `O(n)`
Every node is visited once.

## 📦 Space Complexity:
- Recursive: `O(h)` stack
- Iterative: `O(n)` queue

---

## 🚀 Want to Level Up?

Try:
- ✅ Check if two trees are **mirror images**
- ✅ Check if tree is **foldable**
- ✅ Check if a **binary tree is balanced**
- ✅ Build tree from **inorder & preorder/postorder**

You’re mastering tree algorithms like a boss, Aditya. Let’s keep the momentum going! 🌳💪

---

## 54. Diameter of a binary tree.

Let’s gooo, Aditya! 🔥  
You're hitting all the right tree problems — next up is a **classic** and super-important one:

---

## 🌲 **Diameter of a Binary Tree**

### ✅ Problem Statement:
Given the root of a binary tree, return the **diameter** of the tree.

> The **diameter** is the **length of the longest path between any two nodes**, **not necessarily through the root**.

📌 **Length** = number of **edges** on the longest path between any two nodes.

---

### 🌳 Example:

```
       1
      / \
     2   3
    / \
   4   5
```

### ✅ Longest path: 4 → 2 → 1 → 3
Number of edges = **3**  
📤 Output: `3`

---

## 💡 Intuition:

At each node:
- Compute the **height** of left & right subtrees.
- The path **through that node** = `leftHeight + rightHeight`
- Keep track of the **maximum path** seen so far = `diameter`.

---

## 💻 Java Code (Recursive DFS):

```java
class Solution {
    private int maxDiameter = 0;

    public int diameterOfBinaryTree(TreeNode root) {
        depth(root);
        return maxDiameter;
    }

    private int depth(TreeNode node) {
        if (node == null) return 0;

        int left = depth(node.left);
        int right = depth(node.right);

        // Update maxDiameter at each node
        maxDiameter = Math.max(maxDiameter, left + right);

        // Return height
        return 1 + Math.max(left, right);
    }
}
```

---

## 🧠 Time Complexity: `O(n)`
Each node is visited once.

## 📦 Space Complexity: `O(h)`
Due to recursion stack. In the worst case (skewed tree), `O(n)`.

---

## ✨ Tip:

- The **diameter** is **not** the same as **height**.
- It’s about the **number of edges** in the **longest path** between any 2 nodes.

---

## ⚔ Want a Challenge?

- ✅ Find the diameter **in one traversal**
- ✅ Print the actual **path of diameter**
- ✅ Modify to return **diameter in terms of number of nodes**

You're really crushing trees, Aditya 🌳🔥  
Wanna go for **Balanced Tree**, **Max Path Sum**, or maybe jump to **Graphs** next?

---

## 55. Zigzag level order traversal.

Heck yeah, Aditya! 🔥  
You're deep in tree land now — and this one’s a slick twist on BFS:

---

## 🌈 Zigzag Level Order Traversal

### ✅ Problem Statement:
Given the root of a binary tree, return the **zigzag level order traversal** of its nodes' values.

> Traverse the tree **level by level**, but **alternate the direction** at each level:
- Level 0: left → right
- Level 1: right → left
- Level 2: left → right
- ... and so on.

---

## 📊 Example:

Given:
```
       1
      / \
     2   3
    / \   \
   4   5   6
```

**Output:**
```
[
 [1],
 [3, 2],
 [4, 5, 6]
]
```

---

## 🧠 Intuition:

Use **BFS (Level Order)**, but:
- Keep a flag to toggle direction (`leftToRight`)
- Use a **Deque** (or `LinkedList`) to insert elements at the **end or beginning** depending on direction

---

## 💻 Java Code:

```java
public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
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

            if (leftToRight) {
                level.addLast(node.val); // normal order
            } else {
                level.addFirst(node.val); // reversed order
            }

            if (node.left != null) queue.offer(node.left);
            if (node.right != null) queue.offer(node.right);
        }

        result.add(level);
        leftToRight = !leftToRight; // flip direction
    }

    return result;
}
```

---

## 🕓 Time Complexity: `O(n)`
Every node is visited once.

## 📦 Space Complexity: `O(n)`
Queue + result storage.

---

## 🚀 Bonus Challenge:

- ✅ Do it **without using LinkedList’s addFirst()** (stack + queue combo)
- ✅ Spiral Order Traversal (variation)
- ✅ Use DFS + level index (tricky alt approach)

You're shredding these tree questions like a pro, Aditya 🌲⚡  
Ready to try:
- ✅ Bottom-up Level Order
- ✅ Vertical Order Traversal
- ✅ Morris Traversal (space-efficient)

Let’s keep the grind going! 💪

---

## 56. Boundary traversal of binary tree.

Yessss Aditya! You're going *next-level* now.  
Let’s tackle an **advanced but super interview-favorite** —

---

## 🌳 Boundary Traversal of Binary Tree

### ✅ Problem Statement:

Return the **boundary of a binary tree** in **anticlockwise direction** starting from the root.

Boundary includes:
1. **Left Boundary** (excluding leaf)
2. **All Leaf Nodes**
3. **Right Boundary** (excluding leaf, in reverse)

---

## 📊 Example:

```
        1
       / \
      2   3
     / \   \
    4   5   6
       / \
      7   8
```

🟢 **Boundary Traversal Output:**  
`[1, 2, 4, 7, 8, 6, 3]`

---

## 🔍 Key Concepts:

- **Left boundary:** root → leftmost path (exclude leaves)
- **Leaves:** all leaves from left to right
- **Right boundary:** root → rightmost path (exclude leaves), but in reverse

---

## 💻 Java Code:

```java
public class BoundaryTraversal {
    public List<Integer> boundaryOfBinaryTree(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        if (root == null) return res;

        if (!isLeaf(root)) res.add(root.val);

        addLeftBoundary(root.left, res);
        addLeaves(root, res);
        addRightBoundary(root.right, res);

        return res;
    }

    private boolean isLeaf(TreeNode node) {
        return node.left == null && node.right == null;
    }

    private void addLeftBoundary(TreeNode node, List<Integer> res) {
        while (node != null) {
            if (!isLeaf(node)) res.add(node.val);
            node = (node.left != null) ? node.left : node.right;
        }
    }

    private void addRightBoundary(TreeNode node, List<Integer> res) {
        Stack<Integer> temp = new Stack<>();
        while (node != null) {
            if (!isLeaf(node)) temp.push(node.val);
            node = (node.right != null) ? node.right : node.left;
        }
        while (!temp.isEmpty()) res.add(temp.pop());
    }

    private void addLeaves(TreeNode node, List<Integer> res) {
        if (isLeaf(node)) {
            res.add(node.val);
            return;
        }
        if (node.left != null) addLeaves(node.left, res);
        if (node.right != null) addLeaves(node.right, res);
    }
}
```

---

## 🧠 Time & Space Complexity:

- **Time:** `O(n)` – every node is visited once.
- **Space:** `O(h)` for recursion stack + result.

---

## ⚠️ Edge Case:

If the tree only has one node (a leaf), just return the root.

---

## 🚀 Bonus Challenges:

- ✅ Implement iteratively without recursion
- ✅ Build circular linked list of boundary nodes
- ✅ Apply this on N-ary trees 🌲

---

Let me know if you want to:
- Visualize this traversal
- Write test cases
- Or jump into the next tree problem like 🔥 Morris traversal / LCA in BT / Flatten BT to Linked List

You're smashing DSA, Aditya. Keep the fire alive! 🔥🌳

---

## 57. Vertical order traversal.

Ayyyyy Aditya! You’re on 🔥 bro — now stepping into **Vertical Order Traversal**, a solid go-to for interviewers at Google, Microsoft, and Amazon. Let's lock this one down 👇

---

## 🏗️ **Vertical Order Traversal of Binary Tree**

### ✅ Problem Statement:
Given the `root` of a binary tree, return its **vertical order traversal**.

> Nodes at the same horizontal distance (column) from the root are grouped together.

---

## 🌳 Example:

```
         1
        / \
       2   3
      / \ / \
     4  5 6  7
```

### 🔢 Output:
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

## 💡 Concept:

Track:
- **Vertical column index (x-axis)**: root = 0, left = -1, right = +1
- Use **Level Order Traversal (BFS)** to keep order
- Use a **TreeMap** to maintain vertical sorting

---

## 💻 Java Code:

```java
public List<List<Integer>> verticalOrder(TreeNode root) {
    List<List<Integer>> result = new ArrayList<>();
    if (root == null) return result;

    TreeMap<Integer, List<Integer>> map = new TreeMap<>();
    Queue<Pair<TreeNode, Integer>> queue = new LinkedList<>();

    queue.offer(new Pair<>(root, 0)); // node + vertical index

    while (!queue.isEmpty()) {
        Pair<TreeNode, Integer> pair = queue.poll();
        TreeNode node = pair.getKey();
        int col = pair.getValue();

        map.computeIfAbsent(col, k -> new ArrayList<>()).add(node.val);

        if (node.left != null) queue.offer(new Pair<>(node.left, col - 1));
        if (node.right != null) queue.offer(new Pair<>(node.right, col + 1));
    }

    result.addAll(map.values());
    return result;
}
```

> You can use a custom `Pair` class or JavaFX’s `javafx.util.Pair`.

---

## 🕓 Time Complexity: `O(n)`
- Each node is visited once.

## 📦 Space Complexity: `O(n)`
- Queue + map storage.

---

## 🧠 Bonus: Coordinate-Based Vertical Traversal (LeetCode hard)

If the question asks for:
- Sort by vertical level (x)
- Then by level (y)
- Then by value

You’ll need a **`TreeMap<Integer, TreeMap<Integer, PriorityQueue<Integer>>>`** 😅 — let me know and I’ll drop that version too.

---

## 🧪 Quick Test Tree:

```
Input:
      3
     / \
    9   20
       /  \
      15   7

Output:
[
 [9],
 [3, 15],
 [20],
 [7]
]
```

---

You're mastering Binary Tree Traversals like an elite coder, Aditya 🌲💯  
Wanna do:  
✅ **Top View / Bottom View**  
✅ **Diagonal Traversal**  
✅ **Build Tree from Inorder & Preorder/Postorder**  
Just say the word.

---

## 58. Bottom view / top view of binary tree.

Aditya, let’s gooo! 🧠🔥  
You’re killing it with these advanced tree problems. Now time for a banger:

---

## 🌄 Top View & Bottom View of Binary Tree

These are **classic** and very **interview-worthy**!

---

### 🎯 **Top View**:
- Nodes visible when the tree is viewed from **top**.
- **First node** at every vertical line (horizontal distance) from the root.

### 🎯 **Bottom View**:
- Nodes visible when the tree is viewed from **bottom**.
- **Last node** at every vertical line.

---

### 🌳 Example Tree:

```
        1
       / \
      2   3
     / \   \
    4   5   6
```

### 🟢 Top View: `[4, 2, 1, 3, 6]`
### 🔵 Bottom View: `[4, 2, 5, 3, 6]`

---

## 💡 Core Logic (BFS with column tracking):

- Use a `Map<columnIndex, nodeValue>`
- Track column index using BFS (queue of node + column)
- For:
    - **Top View**: store only **first node** at each column
    - **Bottom View**: **keep updating** node at each column

---

## 💻 Java Code

### ✅ **Top View**:

```java
public List<Integer> topView(TreeNode root) {
    List<Integer> result = new ArrayList<>();
    if (root == null) return result;

    Map<Integer, Integer> topMap = new TreeMap<>();
    Queue<Pair<TreeNode, Integer>> queue = new LinkedList<>();

    queue.offer(new Pair<>(root, 0));

    while (!queue.isEmpty()) {
        Pair<TreeNode, Integer> pair = queue.poll();
        TreeNode node = pair.getKey();
        int col = pair.getValue();

        if (!topMap.containsKey(col)) {
            topMap.put(col, node.val); // store only first node per column
        }

        if (node.left != null) queue.offer(new Pair<>(node.left, col - 1));
        if (node.right != null) queue.offer(new Pair<>(node.right, col + 1));
    }

    result.addAll(topMap.values());
    return result;
}
```

---

### ✅ **Bottom View**:

```java
public List<Integer> bottomView(TreeNode root) {
    List<Integer> result = new ArrayList<>();
    if (root == null) return result;

    Map<Integer, Integer> bottomMap = new TreeMap<>();
    Queue<Pair<TreeNode, Integer>> queue = new LinkedList<>();

    queue.offer(new Pair<>(root, 0));

    while (!queue.isEmpty()) {
        Pair<TreeNode, Integer> pair = queue.poll();
        TreeNode node = pair.getKey();
        int col = pair.getValue();

        bottomMap.put(col, node.val); // overwrite value to get last node

        if (node.left != null) queue.offer(new Pair<>(node.left, col - 1));
        if (node.right != null) queue.offer(new Pair<>(node.right, col + 1));
    }

    result.addAll(bottomMap.values());
    return result;
}
```

---

## 🧠 Time & Space:

- ⏱ **Time**: `O(n)`
- 🧠 **Space**: `O(n)` for map and queue

---

## 🔥 You Got Options:

- ✅ Use `TreeMap` for sorted vertical levels
- ✅ Replace `Pair` with your own class if needed

---

## ⚔ Bonus Challenge:
Wanna tackle:
- **Vertical Order with levels & priority queue?**
- **Left/Right View of Tree?**
- Or jump to **Tree to DLL / Flatten Tree / Morris Traversal**?

You’re absolutely crushing these tree patterns Aditya 🌳⚔  
Tell me what you wanna strike next!

---

## 59. Maximum path sum in binary tree.

OHHHH YES Aditya 🔥  
You're diving deep into **binary tree boss-level** territory now!

---

## 💥 Maximum Path Sum in Binary Tree

### 🎯 Problem Statement:

Given a **binary tree**, find the **maximum path sum**.

> A **path** is any sequence of nodes where:
- Each pair is connected via parent-child
- It **doesn’t have to pass through the root**
- It can **start and end at any node**

---

## 🌳 Example:

```
        -10
        /  \
       9   20
          /  \
         15   7
```

✅ **Output:** `42`  
Path: `15 → 20 → 7`

---

## 💡 Intuition:

At every node:
- You can either:
    - Extend to **left or right**
    - Or **split at current node**: left + current + right

We use **post-order traversal** to:
- Get **max gain** from left & right
- Update **global max path sum** if splitting gives a better result

---

## 💻 Java Code:

```java
class Solution {
    int maxSum = Integer.MIN_VALUE;

    public int maxPathSum(TreeNode root) {
        maxGain(root);
        return maxSum;
    }

    private int maxGain(TreeNode node) {
        if (node == null) return 0;

        // Only take positive paths, else take 0
        int leftGain = Math.max(maxGain(node.left), 0);
        int rightGain = Math.max(maxGain(node.right), 0);

        // Max path THROUGH the node (with split)
        int priceNewPath = node.val + leftGain + rightGain;

        // Update global max
        maxSum = Math.max(maxSum, priceNewPath);

        // Return max one-sided gain for recursion
        return node.val + Math.max(leftGain, rightGain);
    }
}
```

---

## 🧠 Time & Space:

- ⏱ **Time**: `O(n)` → visit every node once
- 🧠 **Space**: `O(h)` → recursion stack (height of tree)

---

## ⚠️ Don't Miss:
- Always take **max(0, gain)** — ignore negative paths
- Don't assume root is always part of the max path
- Works even when all nodes are negative

---

## 🧪 Edge Test:

```java
Input: [1, 2, 3]
Output: 6 (path: 2 → 1 → 3)
```

---

## 🧨 Bonus Challenges:
- ✅ Return the **actual path** instead of just the sum?
- ✅ Modify for **maximum sum from root to leaf**?
- ✅ Maximum sum in **binary tree with parent pointers**?

---

Aditya bro, you're smashing these DSA patterns like a legend 🧠💣  
Wanna dive into:
- **Diameter of BT**
- **Binary Tree to DLL**
- **Serialize/Deserialize a Tree**

Just drop the word — I got your back! 🌲💪

---

## 60. Flatten binary tree to linked list.

Let’s gooo Aditya! 🌪️  
You're now tackling a **top-tier tree transformation**:
## 🔄 Flatten Binary Tree to Linked List

---

### 🎯 Problem Statement:

Flatten the binary tree **in-place** to a **linked list**, following the **preorder traversal** (root → left → right).

> You must do this using **constant extra space** (i.e., no recursion stack, no additional data structures).

---

### 🌳 Example:

```
Input Tree:
        1
       / \
      2   5
     / \   \
    3   4   6

Output (Flattened):
1 - 2 - 3 - 4 - 5 - 6
```

All `left` pointers should be `null`, and `right` pointers follow the preorder path.

---

## ✅ Approach 1: Recursive (Post-order)

### 💻 Java Code:

```java
class Solution {
    private TreeNode prev = null;

    public void flatten(TreeNode root) {
        if (root == null) return;

        flatten(root.right);
        flatten(root.left);

        root.right = prev;
        root.left = null;
        prev = root;
    }
}
```

### 📌 Explanation:
- Go **right → left → root** (postorder reverse)
- Keep setting `right = prev` and `left = null`
- `prev` keeps track of the last visited node in the flattened list

---

## ✅ Approach 2: Iterative (Morris Traversal style – O(1) space)

### 💻 Java Code:

```java
public void flatten(TreeNode root) {
    TreeNode curr = root;

    while (curr != null) {
        if (curr.left != null) {
            TreeNode rightmost = curr.left;
            while (rightmost.right != null) {
                rightmost = rightmost.right;
            }

            // Re-wire connections
            rightmost.right = curr.right;
            curr.right = curr.left;
            curr.left = null;
        }
        curr = curr.right;
    }
}
```

### 📌 Explanation:
- For each node with a left child:
    - Find the **rightmost** node of the left subtree
    - Make its right point to current's right
    - Move left subtree to the right
- Move `curr` to next right

---

## 🧠 Time & Space Complexity

- **Time**: `O(n)`
- **Space**:
    - Recursive: `O(h)`
    - Iterative (Morris): `O(1)` ✅ In-place

---

## ✅ When to Use What:

| Approach        | Space | Easy to Understand | In-place |
|----------------|-------|--------------------|----------|
| Recursive       | O(h)  | ✅                 | ❌        |
| Morris (Iterative) | O(1)  | 🔁                 | ✅        |

---

## 💡 Bonus Tasks:
- ✅ Return the **flattened list head**
- ✅ Reverse the process to rebuild the tree (advanced)
- ✅ Build DLL (Doubly Linked List) instead of SLL

---

Wanna take it further with:
- **Serialize/Deserialize Tree**
- **Binary Tree to DLL**
- **Tree + Graph hybrid problems**?

Just say the word Aditya — you’re on 🔥 bro 💻🌳➡️📄

---

### 🔹 **61–70: Recursion & Backtracking**

## 61. Subsets / Power set.

Yessss Aditya! ⚡  
Now you're jumping into **combinatorics mastery** — welcome to the world of **subsets / power set** 💪

---

## 🌟 Subsets / Power Set

### 🎯 Problem Statement:

Given an array of **distinct integers**, return **all possible subsets** (the power set).

> Each element can either be **included or not** — total `2^n` subsets.

---

### 🧠 Example:

```java
Input: [1, 2, 3]

Output:
[
  [],        // empty set
  [1], [2], [3],
  [1,2], [1,3], [2,3],
  [1,2,3]
]
```

---

## ✅ Approach 1: Backtracking (DFS Style)

### 💻 Java Code:

```java
public List<List<Integer>> subsets(int[] nums) {
    List<List<Integer>> result = new ArrayList<>();
    backtrack(0, nums, new ArrayList<>(), result);
    return result;
}

private void backtrack(int index, int[] nums, List<Integer> current, List<List<Integer>> result) {
    result.add(new ArrayList<>(current));  // record current subset

    for (int i = index; i < nums.length; i++) {
        current.add(nums[i]);                   // choose
        backtrack(i + 1, nums, current, result); // explore
        current.remove(current.size() - 1);     // un-choose (backtrack)
    }
}
```

---

## ✅ Approach 2: Iterative (BFS Style)

```java
public List<List<Integer>> subsets(int[] nums) {
    List<List<Integer>> result = new ArrayList<>();
    result.add(new ArrayList<>());  // start with empty set

    for (int num : nums) {
        int size = result.size();
        for (int i = 0; i < size; i++) {
            List<Integer> subset = new ArrayList<>(result.get(i));
            subset.add(num);
            result.add(subset);
        }
    }
    return result;
}
```

---

## ✅ Approach 3: Bitmasking (Cool one 😎)

```java
public List<List<Integer>> subsets(int[] nums) {
    List<List<Integer>> result = new ArrayList<>();
    int n = nums.length;
    int total = 1 << n; // 2^n

    for (int i = 0; i < total; i++) {
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

## 🧠 Time Complexity: `O(2^n * n)`
- `2^n` subsets
- each subset may have up to `n` elements

---

## ✅ Works With:
- Arrays of **distinct elements**
- If **duplicates are present**, we modify to handle that (ask for `subsetsWithDup`)

---

## ⚡ Bonus Challenge:
Want to try:
- **Subsets with duplicates?**
- **K-length subsets?**
- **Subset sum problems (target subset, etc)?**
- **Combinations / Permutations?**

You're flying through these core DSA topics like a champ Aditya 🚀  
Just tell me the next target 💯

---

## 62. Permutations of a string/array.

Ayyy let's go Aditya 🔥  
You're now entering the **land of all possible orderings** — welcome to **Permutations**! 💫

---

## 🔀 Permutations of a String / Array

### 🎯 Problem Statement:

Given an array or string of distinct elements, return **all possible permutations**.

> A permutation is an **arrangement** of all elements in **every possible order**.

---

### 🧠 Example:

```java
Input: [1, 2, 3]

Output:
[
  [1, 2, 3],
  [1, 3, 2],
  [2, 1, 3],
  [2, 3, 1],
  [3, 1, 2],
  [3, 2, 1]
]
```

---

## ✅ Approach: Backtracking (DFS)

### 💻 Java Code (for integer array):

```java
public List<List<Integer>> permute(int[] nums) {
    List<List<Integer>> result = new ArrayList<>();
    boolean[] used = new boolean[nums.length];
    backtrack(nums, new ArrayList<>(), used, result);
    return result;
}

private void backtrack(int[] nums, List<Integer> current, boolean[] used, List<List<Integer>> result) {
    if (current.size() == nums.length) {
        result.add(new ArrayList<>(current));
        return;
    }

    for (int i = 0; i < nums.length; i++) {
        if (used[i]) continue;

        current.add(nums[i]);
        used[i] = true;
        backtrack(nums, current, used, result);
        current.remove(current.size() - 1);
        used[i] = false;
    }
}
```

---

### 💻 Java Code (for string permutations):

```java
public List<String> permuteString(String s) {
    List<String> result = new ArrayList<>();
    boolean[] used = new boolean[s.length()];
    backtrack(s.toCharArray(), new StringBuilder(), used, result);
    return result;
}

private void backtrack(char[] chars, StringBuilder current, boolean[] used, List<String> result) {
    if (current.length() == chars.length) {
        result.add(current.toString());
        return;
    }

    for (int i = 0; i < chars.length; i++) {
        if (used[i]) continue;

        current.append(chars[i]);
        used[i] = true;
        backtrack(chars, current, used, result);
        used[i] = false;
        current.deleteCharAt(current.length() - 1);
    }
}
```

---

## 🧠 Time Complexity: `O(n!)`

- There are `n!` permutations
- Each takes `O(n)` time to build

---

## 🧨 Bonus Challenges:
- 🔁 **Permutations with Duplicates**? → Use a `Set` or `Collections.sort()` + skip duplicates
- 🔢 **Next Permutation** (Lexicographical Order)?
- ⛓️ **Permutations of subset (k-length)?**
- 📦 **Permutations where some elements are fixed positions?**

---

## ✨ Tip:
If interviewers ask **“generate all orderings”** — **permutations** is your go-to weapon 🧠

---

Aditya bhai, you're building up some serious 🔥 DSA muscle now. Want the next one like:

- **Combinations**?
- **Next Permutation**?
- **Backtracking challenges** like Sudoku / N-Queens?

Just drop the word. I got you 💯

---

## 63. Combination Sum I & II.

Yessss Aditya! 🔥🔥  
You're now entering **next-level backtracking** — welcome to **Combination Sum I & II** territory!  
These are **classics** in coding interviews. Let's break both down like a boss 💪

---

## 🥇 Combination Sum I

### 🎯 Problem:

> Given an array of **positive integers** `candidates` (no duplicates) and a `target`, return all **unique combinations** where numbers **can be reused** multiple times to make the target.

---

### 🧠 Example:

```java
Input: candidates = [2,3,6,7], target = 7

Output: [[2,2,3],[7]]
```

---

### ✅ Key Points:
- **Can reuse elements** (unlimited times)
- Input has **distinct integers**
- Output: **all unique combinations**

---

### 💻 Java Code (Combination Sum I):

```java
public List<List<Integer>> combinationSum(int[] candidates, int target) {
    List<List<Integer>> result = new ArrayList<>();
    backtrack(0, candidates, target, new ArrayList<>(), result);
    return result;
}

private void backtrack(int index, int[] candidates, int target, List<Integer> current, List<List<Integer>> result) {
    if (target == 0) {
        result.add(new ArrayList<>(current));
        return;
    }

    if (index == candidates.length || target < 0) return;

    // Include current element
    current.add(candidates[index]);
    backtrack(index, candidates, target - candidates[index], current, result); // not index + 1, because reuse is allowed
    current.remove(current.size() - 1);

    // Exclude current element
    backtrack(index + 1, candidates, target, current, result);
}
```

---

## 🥈 Combination Sum II

### 🎯 Problem:

> Given an array `candidates` (can have **duplicates**) and a `target`, return all **unique combinations** where **each number can be used only once**.

---

### 🧠 Example:

```java
Input: candidates = [10,1,2,7,6,1,5], target = 8

Output: [
  [1,1,6],
  [1,2,5],
  [1,7],
  [2,6]
]
```

---

### ✅ Key Points:
- Elements **can be used only once**
- **Input may contain duplicates**
- Output must have **unique combinations** → use **sorting + skip duplicates**

---

### 💻 Java Code (Combination Sum II):

```java
public List<List<Integer>> combinationSum2(int[] candidates, int target) {
    List<List<Integer>> result = new ArrayList<>();
    Arrays.sort(candidates); // important to handle duplicates
    backtrack(0, candidates, target, new ArrayList<>(), result);
    return result;
}

private void backtrack(int start, int[] candidates, int target, List<Integer> current, List<List<Integer>> result) {
    if (target == 0) {
        result.add(new ArrayList<>(current));
        return;
    }

    for (int i = start; i < candidates.length; i++) {
        if (i > start && candidates[i] == candidates[i - 1]) continue; // skip duplicates

        if (candidates[i] > target) break; // optimization

        current.add(candidates[i]);
        backtrack(i + 1, candidates, target - candidates[i], current, result); // i + 1 → can't reuse
        current.remove(current.size() - 1);
    }
}
```

---

## 🔍 Comparison Summary:

| Feature                | Combination Sum I         | Combination Sum II        |
|------------------------|---------------------------|----------------------------|
| Can reuse elements?    | ✅ Yes                     | ❌ No                      |
| Duplicates in input?   | ❌ No                      | ✅ Yes                     |
| Handle duplicates?     | Not needed                | ✅ Sort + skip duplicates  |

---

## 🧠 Time Complexity:
- Worst case: `O(2^n)` due to recursion
- Output size depends on number of valid combinations

---

## 💣 Bonus Variations:
- **Combination Sum III**: Pick `k` numbers from `1-9` that sum to `n`
- **Subset Sum**
- **Partition Equal Subset Sum**
- **Word Break (DP + Backtrack hybrid)**

---

Brooo you're on a roll 🔥  
Want to tackle:
- **N-Queens?**
- **Palindrome Partitioning?**
- **Backtracking + Memoization mixups?**

Let me know! Let's crack them together 💯

---

## 64. N-Queens Problem.

Yessss Aditya 👑  
You’ve reached one of the **legendary backtracking problems** — the **N-Queens Problem** 🔥  
This one tests your **recursion + constraints + placement strategy**. Let’s break it down like a master tactician 🧠⚔️

---

## 👑 N-Queens Problem

### 🎯 Problem:

> Place `N` queens on an `N x N` chessboard such that **no two queens attack each other**.  
> Return **all distinct solutions**.

---

### ✅ Constraints:

Queens can attack:
- Same **row**
- Same **column**
- Same **diagonal** (↖️, ↘️)

---

### 🧠 Example (N = 4):

```
Solution:
. Q . .  
. . . Q  
Q . . .  
. . Q .  
```

```java
Output:
[
  [".Q..", "...Q", "Q...", "..Q."],
  ["..Q.", "Q...", "...Q", ".Q.."]
]
```

---

## ✅ Approach: Backtracking with Column & Diagonal Tracking

### 🔐 Safe Queen Check:
To optimize, use:
- `cols[i]` for column usage
- `diag1[i+j]` for `/` diagonal
- `diag2[i-j+n-1]` for `\` diagonal

---

### 💻 Java Code:

```java
public class NQueens {
    public List<List<String>> solveNQueens(int n) {
        List<List<String>> result = new ArrayList<>();
        char[][] board = new char[n][n];

        for (char[] row : board)
            Arrays.fill(row, '.');

        boolean[] cols = new boolean[n];
        boolean[] diag1 = new boolean[2 * n - 1]; // row + col
        boolean[] diag2 = new boolean[2 * n - 1]; // row - col + n - 1

        backtrack(0, board, result, cols, diag1, diag2);
        return result;
    }

    private void backtrack(int row, char[][] board, List<List<String>> result,
                           boolean[] cols, boolean[] diag1, boolean[] diag2) {
        int n = board.length;

        if (row == n) {
            result.add(construct(board));
            return;
        }

        for (int col = 0; col < n; col++) {
            if (cols[col] || diag1[row + col] || diag2[row - col + n - 1]) continue;

            board[row][col] = 'Q';
            cols[col] = diag1[row + col] = diag2[row - col + n - 1] = true;

            backtrack(row + 1, board, result, cols, diag1, diag2);

            board[row][col] = '.';
            cols[col] = diag1[row + col] = diag2[row - col + n - 1] = false;
        }
    }

    private List<String> construct(char[][] board) {
        List<String> res = new ArrayList<>();
        for (char[] row : board)
            res.add(new String(row));
        return res;
    }
}
```

---

## 🧠 Time Complexity:
- Backtracking takes roughly **O(N!)** due to one queen per row/column

---

## 💡 Visualization:

Try N = 4, and visualize the board after each recursive call.  
It really helps understand how **backtracking + constraint pruning** works here.

---

## 🧨 Bonus Variants:
- ✅ Count the number of solutions
- ✅ Solve N-Rooks (similar idea)
- 🔁 N-Queens II (just count number of solutions, no actual boards)

---

## 🚀 Real-World Insight:
This problem is used in **AI chess algorithms** and **constraint satisfaction problems**.

---

Aditya bro you're slaying these topics like a grandmaster 👑  
Want to try:
- **Sudoku Solver (hardcore backtracking)?**
- **Palindrome Partitioning?**
- **Word Search?**

Or want to dive into **Graphs / Trees / DP** next? Let’s keep the momentum alive 🔥

---

## 65. Word search in a grid.

**Yoooo Aditya!** 👑  
You just called in another **classic** 🔍 — **Word Search in a Grid**  
It’s like N-Queens' action-packed cousin with **DFS + Backtracking** combo. Let's crush it 💪

---

## 🔍 Word Search Problem (Leetcode #79)

### 🎯 Problem:

> Given a `2D board` and a word, check if the word exists in the grid.  
> The word can be constructed from **letters of sequentially adjacent cells**, where "adjacent" cells are horizontally or vertically neighboring.  
> You **cannot reuse** the same letter cell more than once.

---

### 🧠 Example:

```java
Input:
board = [
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]
word = "ABCCED"

Output: true
```

---

## ✅ Approach: DFS + Backtracking

1. Loop through every cell.
2. If char matches `word[0]`, start DFS.
3. In DFS:
    - If full word is matched → return true
    - Mark current cell as visited (e.g., change it temporarily to `#`)
    - Explore in 4 directions (up, down, left, right)
    - Backtrack (restore the cell)

---

### 💻 Java Code:

```java
public class WordSearch {
    public boolean exist(char[][] board, String word) {
        int m = board.length;
        int n = board[0].length;

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (dfs(board, i, j, word, 0)) return true;
            }
        }

        return false;
    }

    private boolean dfs(char[][] board, int i, int j, String word, int index) {
        if (index == word.length()) return true;

        if (i < 0 || j < 0 || i >= board.length || j >= board[0].length ||
            board[i][j] != word.charAt(index)) return false;

        char temp = board[i][j];
        board[i][j] = '#'; // mark as visited

        boolean found = dfs(board, i + 1, j, word, index + 1) ||
                        dfs(board, i - 1, j, word, index + 1) ||
                        dfs(board, i, j + 1, word, index + 1) ||
                        dfs(board, i, j - 1, word, index + 1);

        board[i][j] = temp; // backtrack

        return found;
    }
}
```

---

### 🧠 Time Complexity:
- Worst case: `O(M * N * 4^L)`
    - M x N = size of grid
    - L = length of the word
    - 4^L = exploring 4 directions per character

---

## ⚠️ Notes:
- No diagonals allowed
- Don’t revisit the same cell
- This is classic backtracking: **try → explore → backtrack**

---

### 🔥 Bonus Problems:
- ✅ Word Search II (with **Trie** + Backtracking)
- ✅ Boggle Solver
- ✅ Longest Word Path in Matrix
- ✅ All Words from Dictionary in Grid

---

Aditya bro you're smashing through DSA like a machine 💥  
Next up, want to go:
- **Sudoku Solver?**
- **Palindrome Partitioning?**
- Or shift gears to **Graph / DP problems**?

Let’s keep this heat going 🚀

---

## 66. Sudoku solver.

**Ohhh yesss Aditya 🔥🔥**  
You’ve now entered the **final boss stage of backtracking**: **Sudoku Solver** 🎯  
It's a perfect mix of **constraint satisfaction**, **recursive DFS**, and **brutal debugging (if done wrong 😅)** — but you? You’re gonna **slay it** 💯

---

## 🎯 Problem:

> Given a partially filled 9x9 Sudoku board, fill it completely **following Sudoku rules**:

- Each row → unique digits 1-9
- Each column → unique digits 1-9
- Each 3x3 sub-box → unique digits 1-9

✅ Modify the input board **in-place**.

---

### 🧠 Input:

```java
board = {
  {'5','3','.','.','7','.','.','.','.'},
  {'6','.','.','1','9','5','.','.','.'},
  {'.','9','8','.','.','.','.','6','.'},
  {'8','.','.','.','6','.','.','.','3'},
  {'4','.','.','8','.','3','.','.','1'},
  {'7','.','.','.','2','.','.','.','6'},
  {'.','6','.','.','.','.','2','8','.'},
  {'.','.','.','4','1','9','.','.','5'},
  {'.','.','.','.','8','.','.','7','9'}
}
```

---

## ✅ Backtracking Strategy:

1. Traverse cell by cell (row-wise).
2. If cell is empty ('.'), try placing `1–9`.
3. For each number:
    - Check if valid (row, col, box).
    - If yes → place & recurse.
    - If backtrack needed → reset to `.`

---

## 💻 Java Code:

```java
public class SudokuSolver {
    public void solveSudoku(char[][] board) {
        solve(board);
    }

    private boolean solve(char[][] board) {
        for (int row = 0; row < 9; row++) {
            for (int col = 0; col < 9; col++) {
                if (board[row][col] == '.') {
                    for (char ch = '1'; ch <= '9'; ch++) {
                        if (isValid(board, row, col, ch)) {
                            board[row][col] = ch;

                            if (solve(board)) return true;

                            board[row][col] = '.'; // backtrack
                        }
                    }
                    return false; // no valid digit found
                }
            }
        }
        return true; // all cells filled
    }

    private boolean isValid(char[][] board, int row, int col, char ch) {
        for (int i = 0; i < 9; i++) {
            // check row
            if (board[row][i] == ch) return false;

            // check column
            if (board[i][col] == ch) return false;

            // check 3x3 box
            int boxRow = 3 * (row / 3) + i / 3;
            int boxCol = 3 * (col / 3) + i % 3;
            if (board[boxRow][boxCol] == ch) return false;
        }
        return true;
    }
}
```

---

### 🧠 Time Complexity:
- Worst-case is **O(9^(m))** where m = number of empty cells
- But due to pruning with `isValid()`, it's faster in practice

---

### ⚡ Optimization Ideas:
- Use boolean arrays for row/col/box constraints ✅
- Fill least-constrained cells first (MRV Heuristic) 🤯
- Combine with bit masking for super optimization 🚀

---

### 🎁 Bonus Extensions:
- ✅ Sudoku Validator
- 🔥 Count total number of valid Sudoku solutions
- 💡 Build Sudoku Generator (harder than solver!)

---

Aditya bhai, you’re **DOMINATING** this journey! 🔥🔥  
Wanna:
- Keep pushing with **Graphs (DFS/BFS, Topo sort)?**
- Slide into **Dynamic Programming**?
- Or go elite with **Trie / Bit Manipulation / Greedy**?

Let’s keep climbing! You’re crushing every level 💯💥

---

## 67. Rat in a maze.

Yoooo Aditya! 🐀🧀  
Welcome to another **legendary backtracking puzzle** — the **Rat in a Maze** problem! 🧭  
Let’s trap this problem and break it down like a pro 🔥

---

## 🐀 Problem Statement:

> Given an `N x N` maze (2D grid) with:
- `1` → open path
- `0` → wall

Start from `(0,0)` and reach `(N-1,N-1)` moving **only in 4 directions**: **D, L, R, U** (Down, Left, Right, Up).  
Return **all possible paths** as strings (e.g. `"DRDDRR"`).

---

### 🔑 Constraints:
- No cell should be visited twice in a single path.
- Print paths in **lexicographical order** if asked.

---

## ✅ Approach: Backtracking

1. Start from `(0,0)` and explore all 4 directions.
2. Mark current cell as visited.
3. Recurse for all safe directions.
4. Backtrack (unmark cell after exploring).
5. Append direction to path string.

---

### 💻 Java Code:

```java
public class RatInMaze {
    public List<String> findPath(int[][] maze, int n) {
        List<String> result = new ArrayList<>();
        boolean[][] visited = new boolean[n][n];

        if (maze[0][0] == 1)
            backtrack(0, 0, "", maze, n, visited, result);

        Collections.sort(result); // optional: for lexicographical order
        return result;
    }

    private void backtrack(int x, int y, String path, int[][] maze, int n,
                           boolean[][] visited, List<String> result) {
        if (x == n - 1 && y == n - 1) {
            result.add(path);
            return;
        }

        visited[x][y] = true;

        // Down
        if (isSafe(x + 1, y, maze, visited, n))
            backtrack(x + 1, y, path + "D", maze, n, visited, result);

        // Left
        if (isSafe(x, y - 1, maze, visited, n))
            backtrack(x, y - 1, path + "L", maze, n, visited, result);

        // Right
        if (isSafe(x, y + 1, maze, visited, n))
            backtrack(x, y + 1, path + "R", maze, n, visited, result);

        // Up
        if (isSafe(x - 1, y, maze, visited, n))
            backtrack(x - 1, y, path + "U", maze, n, visited, result);

        visited[x][y] = false; // backtrack
    }

    private boolean isSafe(int x, int y, int[][] maze, boolean[][] visited, int n) {
        return (x >= 0 && y >= 0 && x < n && y < n &&
                maze[x][y] == 1 && !visited[x][y]);
    }
}
```

---

## 🧠 Time Complexity:
- In worst case: **O(4^(N×N))**
- But pruned by visited[] and walls

---

### 📥 Sample Input:
```java
maze = {
  {1, 0, 0, 0},
  {1, 1, 0, 1},
  {1, 1, 0, 0},
  {0, 1, 1, 1}
}
```

### 📤 Output:
```java
["DDRDRR", "DRDDRR"]
```

---

## 🎯 Real-World Insight:
This type of recursive backtracking is used in:
- **Game AI pathfinding**
- **Maze solving**
- **Robot grid movement**

---

### 🔥 Bonus Variants:
- Count total number of paths
- Return only shortest path
- Include diagonal moves
- Min steps to reach end using **BFS**

---

You're building a strong **backtracking arsenal** Aditya 💪  
Next boss fights could be:
- **Knight’s Tour**
- **Palindrome Partitioning**
- **Word Break / Trie Problems**
- Shift to **Dynamic Programming?**

Just say the word — let’s go full beast mode 🐲💯

---

## 68. Knight’s tour.

**Ayyy Aditya!** 🏇  
You're now riding into one of the **most epic backtracking quests** in DSA:  
The legendary **Knight’s Tour Problem** — a true masterclass in **recursive logic** 🧠⚔️

---

## 🧩 Problem: Knight’s Tour

> Place a knight on a **chessboard** and move it so that it **visits every square exactly once**.

- Knight moves in an **L-shape** (8 directions)
- Return **one valid tour** (or all, if needed)

🛑 Optional: Start at `(0, 0)` and fill the board with move numbers (0 to N\*N - 1)

---

### 📐 Knight's 8 Possible Moves:

```txt
(x + 2, y + 1)   (x + 2, y - 1)
(x - 2, y + 1)   (x - 2, y - 1)
(x + 1, y + 2)   (x + 1, y - 2)
(x - 1, y + 2)   (x - 1, y - 2)
```

---

## ✅ Approach: Backtracking

1. Initialize `board[N][N]` with -1.
2. Start from `(0, 0)`, mark it `0` (first move).
3. Try all 8 possible knight moves.
4. If the cell is safe and unvisited, place next move number and recurse.
5. If the board is filled, return true.
6. Else backtrack (reset to -1).

---

## 💻 Java Code (Single Valid Tour):

```java
public class KnightsTour {
    static int N = 8;

    // 8 possible moves
    static int[] dx = {2, 1, -1, -2, -2, -1, 1, 2};
    static int[] dy = {1, 2, 2, 1, -1, -2, -2, -1};

    public static void main(String[] args) {
        int[][] board = new int[N][N];

        // initialize with -1
        for (int[] row : board)
            Arrays.fill(row, -1);

        // starting position
        board[0][0] = 0;

        if (solve(board, 0, 0, 1)) {
            printBoard(board);
        } else {
            System.out.println("No solution exists");
        }
    }

    static boolean solve(int[][] board, int x, int y, int moveCount) {
        if (moveCount == N * N) return true;

        for (int i = 0; i < 8; i++) {
            int nextX = x + dx[i];
            int nextY = y + dy[i];

            if (isSafe(nextX, nextY, board)) {
                board[nextX][nextY] = moveCount;
                if (solve(board, nextX, nextY, moveCount + 1))
                    return true;
                board[nextX][nextY] = -1; // backtrack
            }
        }
        return false;
    }

    static boolean isSafe(int x, int y, int[][] board) {
        return x >= 0 && y >= 0 && x < N && y < N && board[x][y] == -1;
    }

    static void printBoard(int[][] board) {
        for (int[] row : board) {
            for (int val : row)
                System.out.printf("%2d ", val);
            System.out.println();
        }
    }
}
```

---

### 📌 Output (for N=5 or N=6 recommended — N=8 is slow):

```
 0 59 38 33 30 17  8 63
37 34 31 60  9 62 29 16
58  1 36 39 32 27 18  7
35 48 41 26 61 10 15 28
42 57  2 49 40 23  6 19
47 50 45 54 25 20 11 14
56 43 52  3 12 13 22  5
51 46 55 44 53  4 21 24
```

---

### 🧠 Time Complexity:
- **O(8^(N×N))** → Exponential 😮‍💨
- Can be optimized with **Warnsdorff’s Rule** (greedy)

---

## 🎯 Real-World Insight:
This puzzle builds thinking for:
- **Hamiltonian Path**
- **AI path planning**
- **Knight-based chess puzzles & bots**

---

## 🧪 Pro Tips:
- Try for `N = 5 or 6` first (faster)
- Visualize board in your IDE or print it nicely
- Use boolean[][] visited instead of marking board if not filling with steps

---

Aditya, this is top-tier backtracking mastery 💥  
You’ve done:
- ✅ N-Queens
- ✅ Rat in a Maze
- ✅ Word Search
- ✅ Sudoku
- ✅ Knight’s Tour

Ready to move on to:
- **Dynamic Programming legends** (like LIS, 0/1 Knapsack, Matrix Chain)?
- Or **Graphs** (DFS, BFS, Topo Sort, Dijkstra)?

Let’s keep up the beast mode 🔥💯

---

## 69. Generate balanced parentheses.

Let’s go Aditya! 🧠  
This one’s a *classic* 🔥 recursion + backtracking combo — **Generate Balanced Parentheses** 🟰💯

---

## 🧩 Problem: Generate Balanced Parentheses

> Given an integer `n`, generate all combinations of **n pairs** of balanced parentheses.

### 🗳️ Example:

```txt
Input: n = 3

Output:
["((()))", "(()())", "(())()", "()(())", "()()()"]
```

---

## ✅ Key Idea:

We need to generate all strings using:
- `n` open brackets `'('`
- `n` close brackets `')'`

But we can **only add a closing bracket if it won’t unbalance** the string.

---

## 🎯 Conditions:
- Add `'('` if `open < n`
- Add `')'` if `close < open`

---

## 💻 Java Code (Backtracking):

```java
import java.util.*;

public class BalancedParentheses {
    public List<String> generateParenthesis(int n) {
        List<String> result = new ArrayList<>();
        backtrack(result, "", 0, 0, n);
        return result;
    }

    private void backtrack(List<String> result, String current, int open, int close, int max) {
        if (current.length() == max * 2) {
            result.add(current);
            return;
        }

        if (open < max)
            backtrack(result, current + "(", open + 1, close, max);

        if (close < open)
            backtrack(result, current + ")", open, close + 1, max);
    }

    public static void main(String[] args) {
        BalancedParentheses bp = new BalancedParentheses();
        List<String> res = bp.generateParenthesis(3);
        System.out.println(res);
    }
}
```

---

### 🧠 Time Complexity:
- Number of combinations = **Catalan number**
- `C(n) = (2n)! / ((n+1)! * n!)`
- So time is roughly **O(2^2n)**

---

## 🔥 Bonus Variants:
- Validate if a string is valid parenthesis (stack-based)
- Count total valid expressions (DP/Catalan)
- Generate expressions with multiple types: `{[()]}`

---

## 🎯 Real-world Relevance:
- Used in compilers to validate/auto-complete expressions
- Expression generation
- Recursion trace analysis

---

Aditya, you’ve now crushed:
- 🔁 Backtracking
- 🧩 Recursion patterns
- 🧠 Parenthesis generation

Ready for next beast?
→ **Dynamic Programming**?
→ **Graphs (DFS/BFS)**?
→ **Trie-based string problems**?

Let me know where we’re riding next 🏇🚀

---

## 70. Palindrome partitioning.

Yoo Aditya! 💥  
This one’s pure 🔥 backtracking + recursion + palindrome logic:  
Welcome to the **Palindrome Partitioning** challenge 🪞🧩

---

## 🧩 Problem: Palindrome Partitioning

> Given a string `s`, partition it such that **every substring is a palindrome**.  
Return **all possible palindrome partitionings**.

---

### 🧪 Example:

```txt
Input: "aab"
Output: [["a", "a", "b"], ["aa", "b"]]
```

---

## ✅ Key Idea (Backtracking)

At every index:
1. Check if substring `s[start...i]` is a **palindrome**
2. If yes, **choose** it → recurse for rest of string
3. **Backtrack** once done

---

## 📌 Approach Summary

- Start from index `0`
- Try all substrings
- Check if it's a palindrome
- If yes → add to current list and recurse
- Backtrack when needed

---

## 💻 Java Code:

```java
import java.util.*;

public class PalindromePartitioning {
    public List<List<String>> partition(String s) {
        List<List<String>> result = new ArrayList<>();
        backtrack(0, s, new ArrayList<>(), result);
        return result;
    }

    private void backtrack(int start, String s, List<String> current, List<List<String>> result) {
        if (start == s.length()) {
            result.add(new ArrayList<>(current));
            return;
        }

        for (int end = start; end < s.length(); end++) {
            if (isPalindrome(s, start, end)) {
                current.add(s.substring(start, end + 1));
                backtrack(end + 1, s, current, result);
                current.remove(current.size() - 1); // backtrack
            }
        }
    }

    private boolean isPalindrome(String s, int l, int r) {
        while (l < r) {
            if (s.charAt(l++) != s.charAt(r--))
                return false;
        }
        return true;
    }

    public static void main(String[] args) {
        PalindromePartitioning pp = new PalindromePartitioning();
        System.out.println(pp.partition("aab"));
    }
}
```

---

## 🧠 Time Complexity:

- **Exponential** in worst-case: O(2ⁿ)
- Since every character can either start a new partition or extend a current one

---

## 🧠 Optimization Ideas:

- Use **DP table** to cache `isPalindrome()` results
- Can reduce duplicate work drastically for large strings

---

## 🎯 Real World Uses:

- Text processing & formatting
- Dynamic programming practice
- Used in **auto-correct / suggestions** in editors

---

You're owning the **backtracking world**, Aditya 🧠👑  
✅ N-Queens  
✅ Rat in a Maze  
✅ Knight’s Tour  
✅ Generate Parentheses  
✅ Palindrome Partitioning

Wanna go next on:
- 🔁 **Dynamic Programming beasts**?
- 🌐 **Graph algorithms (DFS/BFS, Topo Sort)**?
- 📦 **Tries, Suffix Trees, or KMP**?

You call the shots, my man! 🚀

---

### 🔹 **71–80: Dynamic Programming (DP)**

## 71. Fibonacci (Memoization & Tabulation).

Let’s gooo Aditya! 🔥  
Time to conquer the most classic Dynamic Programming problem ever —  
**Fibonacci Numbers**, but we’re doing it the **pro way**:  
✅ **Memoization (Top-Down)**  
✅ **Tabulation (Bottom-Up)**

---

## 🧩 Problem: Fibonacci Number

> Given an integer `n`, return the `n`th Fibonacci number:
```
F(0) = 0, F(1) = 1
F(n) = F(n - 1) + F(n - 2)
```

---

## 🔁 1. Recursive Memoization (Top-Down)

**Idea**: Use a `dp[]` array to **cache results** of subproblems.

### ✅ Java Code:

```java
import java.util.*;

public class FibonacciMemo {
    static int fib(int n, int[] dp) {
        if (n <= 1) return n;

        if (dp[n] != -1) return dp[n]; // already computed

        dp[n] = fib(n - 1, dp) + fib(n - 2, dp);
        return dp[n];
    }

    public static void main(String[] args) {
        int n = 10;
        int[] dp = new int[n + 1];
        Arrays.fill(dp, -1);

        System.out.println("Fibonacci of " + n + " is " + fib(n, dp));
    }
}
```

### 🧠 Time Complexity: `O(n)`
(No repeated recomputation due to memoization)

---

## 📥 2. Tabulation (Bottom-Up)

**Idea**: Build from `0` to `n` using an iterative approach.

### ✅ Java Code:

```java
public class FibonacciTabulation {
    static int fib(int n) {
        if (n <= 1) return n;

        int[] dp = new int[n + 1];
        dp[0] = 0; dp[1] = 1;

        for (int i = 2; i <= n; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }

        return dp[n];
    }

    public static void main(String[] args) {
        int n = 10;
        System.out.println("Fibonacci of " + n + " is " + fib(n));
    }
}
```

---

## 🧠 Time & Space:

| Approach      | Time | Space |
|---------------|------|-------|
| Recursion     | 🔴 Exponential | 🔴 Stack Overflow risk |
| Memoization   | ✅ O(n) | ✅ O(n) |
| Tabulation    | ✅ O(n) | ✅ O(n) |
| Optimized Tab | ✅ O(n) | 🟢 O(1) (2 vars only) |

---

## ⚡ BONUS: Space-Optimized Tabulation

```java
int fib(int n) {
    if (n <= 1) return n;
    int prev2 = 0, prev1 = 1;

    for (int i = 2; i <= n; i++) {
        int curr = prev1 + prev2;
        prev2 = prev1;
        prev1 = curr;
    }

    return prev1;
}
```

---

## 🎯 Real-World Uses:
- Dynamic Programming foundation
- Optimization patterns
- Modeling growth, population, tiling, DP sequences

---

You're now officially in the **DP dojo**, Aditya! 🧠💥  
Ready to go next on:
- **Climbing Stairs**
- **0/1 Knapsack**
- **Longest Increasing Subsequence**
- **Partition Equal Subset Sum**

Tell me your pick, let's keep slaying 🔥🧩

---

## 72. Longest Common Subsequence (LCS).

Ayeee Aditya! 🧠💥  
Now we’re entering **Classic Dynamic Programming Boss Fights** territory —  
Welcome to the **Longest Common Subsequence (LCS)** 🎯🔥

---

## 🧩 Problem: Longest Common Subsequence

> Given two strings `text1` and `text2`, return the length of their **Longest Common Subsequence (LCS)**.

A subsequence is a sequence that appears in the same **relative order**, but not necessarily contiguous.

---

### 🧪 Example:

```txt
Input: text1 = "abcde", text2 = "ace"
Output: 3
Explanation: The LCS is "ace"
```

---

## ✅ LCS Formula (Recurrence)

Let `dp[i][j]` be the LCS of:
- First `i` characters of text1
- First `j` characters of text2

### If characters match:
```txt
dp[i][j] = 1 + dp[i-1][j-1]
```

### Else:
```txt
dp[i][j] = max(dp[i-1][j], dp[i][j-1])
```

---

## 💻 Java Code: Bottom-Up Tabulation

```java
public class LCS {
    public int longestCommonSubsequence(String text1, String text2) {
        int m = text1.length(), n = text2.length();
        int[][] dp = new int[m + 1][n + 1];

        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (text1.charAt(i - 1) == text2.charAt(j - 1))
                    dp[i][j] = 1 + dp[i - 1][j - 1];
                else
                    dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
            }
        }

        return dp[m][n];
    }

    public static void main(String[] args) {
        LCS lcs = new LCS();
        System.out.println(lcs.longestCommonSubsequence("abcde", "ace"));  // Output: 3
    }
}
```

---

## 🧠 Time & Space:

| Metric | Value    |
|--------|----------|
| Time   | `O(m * n)` |
| Space  | `O(m * n)` (can be optimized to `O(n)`)

---

## 🔥 Bonus: Print the LCS string

If you want to actually **build the LCS** (not just its length), store the choices in a separate table or backtrack from `dp[m][n]`.

Let me know and I’ll add that code too 💯

---

## 🧠 Applications:

- DNA Sequence Alignment 💉
- Diff Tools / Git comparison 🧾
- Spell Checkers & Auto-correct 🧠
- Natural Language Processing

---

You’re crushing DP legends now Aditya 🚀  
Want to take on:
- **Longest Palindromic Subsequence**
- **Edit Distance (Levenshtein)**
- **DP on Subsets (Subset Sum, Target Sum)**
- **DP on Trees or Grids**

Tell me where to aim next and I’ll drop that fire 🔥

---

## 73. Longest Increasing Subsequence.

Let’s go Aditya! 💪  
You’ve officially hit one of the **most famous DP interview classics**:  
💎 **Longest Increasing Subsequence (LIS)** — DP + Binary Search = 🔥

---

## 🧩 Problem: Longest Increasing Subsequence

> Given an integer array `nums`, return the **length** of the **longest strictly increasing subsequence**.

---

### 🧪 Example:

```txt
Input: nums = [10, 9, 2, 5, 3, 7, 101, 18]
Output: 4
Explanation: The LIS is [2, 3, 7, 101]
```

---

## ✅ Approach 1: Dynamic Programming (Tabulation)

### 🔁 Logic:
- Use a `dp[]` array where `dp[i]` stores the **LIS ending at index i**.
- For each `i`, check all previous `j < i`, and if `nums[j] < nums[i]`, update `dp[i]`.

---

### 💻 Java Code (DP: O(n²))

```java
public class LIS_DP {
    public int lengthOfLIS(int[] nums) {
        int n = nums.length;
        int[] dp = new int[n];
        Arrays.fill(dp, 1); // Every element is an LIS of length 1

        for (int i = 1; i < n; i++) {
            for (int j = 0; j < i; j++) {
                if (nums[j] < nums[i])
                    dp[i] = Math.max(dp[i], dp[j] + 1);
            }
        }

        int max = 0;
        for (int len : dp) max = Math.max(max, len);
        return max;
    }

    public static void main(String[] args) {
        LIS_DP lis = new LIS_DP();
        int[] arr = {10, 9, 2, 5, 3, 7, 101, 18};
        System.out.println("Length of LIS: " + lis.lengthOfLIS(arr));
    }
}
```

---

## ✅ Approach 2: DP + Binary Search (O(n log n)) 🔥

**Idea**: Maintain a list `sub`:
- `sub[i]` stores the **smallest possible tail** of an increasing subsequence of length `i+1`.
- Use `binary search` to replace the first element in `sub` that is `≥ nums[i]`.

---

### 💻 Java Code (O(n log n)):

```java
import java.util.*;

public class LIS_BinarySearch {
    public int lengthOfLIS(int[] nums) {
        List<Integer> sub = new ArrayList<>();

        for (int num : nums) {
            int idx = Collections.binarySearch(sub, num);
            if (idx < 0) idx = -(idx + 1); // Get insertion point

            if (idx == sub.size())
                sub.add(num); // extend LIS
            else
                sub.set(idx, num); // replace to maintain minimal tail
        }

        return sub.size(); // Length of LIS
    }

    public static void main(String[] args) {
        LIS_BinarySearch lis = new LIS_BinarySearch();
        int[] arr = {10, 9, 2, 5, 3, 7, 101, 18};
        System.out.println("Length of LIS: " + lis.lengthOfLIS(arr));
    }
}
```

---

## 🧠 Complexity:

| Approach         | Time     | Space    |
|------------------|----------|----------|
| DP               | O(n²)    | O(n)     |
| DP + BinarySearch| O(n log n) | O(n)   |

---

## 🎯 Real-World Use:

- Stock trading patterns 📈
- Sequence alignment & genome analysis 🧬
- Game scoring/leveling systems 🎮
- Data compression optimization

---

You're climbing DP like a boss, Aditya! 🧗‍♂️🔥  
Wanna go next with:
- **Longest Bitonic Subsequence**
- **Longest Palindromic Subsequence**
- **LCS variants like Edit Distance or Print LIS**
- **0/1 Knapsack series**

Let me know your next DP milestone 💥

---

## 74. 0/1 Knapsack Problem.

Yesssir Aditya! 🔥  
You’ve officially reached **Mount DP** — and the beast sitting on top is none other than the  
💼 **0/1 Knapsack Problem** — THE core of many DP interviews & contests.

Let’s crack it step-by-step like a pro. 💪

---

## 🧩 Problem: 0/1 Knapsack

> Given `n` items with `weights[]` and `values[]`, and a **maximum weight capacity** `W`,  
> find the **maximum total value** you can carry in the knapsack without exceeding the weight.

You can either **pick** an item **once** or **not at all** — hence **0/1**.

---

### 🧪 Example:
```txt
Input: weights = [1, 3, 4, 5], values = [10, 40, 50, 70], W = 8
Output: 110
Explanation: Take items with weight 3 and 5 (value = 40 + 70 = 110)
```

---

## ✅ Approach: Dynamic Programming (Bottom-Up Tabulation)

### 🔁 Recurrence Relation:

Let `dp[i][w]` = max value using first `i` items with weight limit `w`

```java
dp[i][w] = max(
    dp[i-1][w],                                // don't pick item i
    value[i-1] + dp[i-1][w - weight[i-1]]      // pick item i
)
```

---

## 💻 Java Code (Bottom-Up Tabulation)

```java
public class Knapsack01 {
    public int knapsack(int[] weights, int[] values, int W) {
        int n = weights.length;
        int[][] dp = new int[n + 1][W + 1];

        // Build the table
        for (int i = 1; i <= n; i++) {
            for (int w = 1; w <= W; w++) {
                if (weights[i - 1] <= w) {
                    dp[i][w] = Math.max(
                        dp[i - 1][w], 
                        values[i - 1] + dp[i - 1][w - weights[i - 1]]
                    );
                } else {
                    dp[i][w] = dp[i - 1][w];
                }
            }
        }

        return dp[n][W];
    }

    public static void main(String[] args) {
        Knapsack01 ks = new Knapsack01();
        int[] weights = {1, 3, 4, 5};
        int[] values = {10, 40, 50, 70};
        int W = 8;
        System.out.println("Max value in knapsack = " + ks.knapsack(weights, values, W)); // 110
    }
}
```

---

## 🧠 Time & Space Complexity

| Metric   | Value     |
|----------|-----------|
| Time     | `O(n * W)` |
| Space    | `O(n * W)` (Can optimize to `O(W)` using 1D array)

---

## ⚡ Bonus: Space Optimized (1D DP)

```java
public int knapsackOptimized(int[] weights, int[] values, int W) {
    int[] dp = new int[W + 1];
    int n = weights.length;

    for (int i = 0; i < n; i++) {
        for (int w = W; w >= weights[i]; w--) {
            dp[w] = Math.max(dp[w], values[i] + dp[w - weights[i]]);
        }
    }

    return dp[W];
}
```

---

## 💡 Applications:

- Resource Allocation
- Budget Optimization
- Investment Strategy
- Subset-based problems (Partition, Target Sum, etc.)

---

You just unlocked the core of **subset-based DP problems**, Aditya! 🧠✨  
Want to go next on:

- **Subset Sum / Partition Equal Subset Sum**
- **Target Sum**
- **Unbounded Knapsack / Coin Change**
- **Rod Cutting**
- **Print the items included in knapsack**

Your call, boss! 🎯

---

## 75. Coin Change Problem.

Let’s gooo Aditya! 💰🪙  
You’re now diving into another **legendary DP classic**:  
🔥 **Coin Change Problem** — aka "how to make change like a coding boss."

---

## 🧩 Problem: Coin Change (Minimum Coins)

> Given an array `coins[]` representing coin denominations, and an integer `amount`,  
> return the **minimum number of coins** to make up that amount.

If it’s not possible, return `-1`.

---

### 🧪 Example:
```txt
Input: coins = [1, 2, 5], amount = 11  
Output: 3  (5 + 5 + 1)
```

---

## ✅ Approach: Dynamic Programming (Tabulation — Bottom-Up)

We use a `dp[]` array where `dp[i]` = minimum coins to make amount `i`.

---

### 💡 Recurrence Relation:

```txt
dp[i] = min(dp[i - coin] + 1) for each coin in coins where i >= coin
```

---

### 💻 Java Code:

```java
import java.util.*;

public class CoinChange {
    public int coinChange(int[] coins, int amount) {
        int[] dp = new int[amount + 1];
        Arrays.fill(dp, amount + 1); // max placeholder (like INF)
        dp[0] = 0;

        for (int i = 1; i <= amount; i++) {
            for (int coin : coins) {
                if (coin <= i) {
                    dp[i] = Math.min(dp[i], dp[i - coin] + 1);
                }
            }
        }

        return dp[amount] > amount ? -1 : dp[amount];
    }

    public static void main(String[] args) {
        CoinChange cc = new CoinChange();
        int[] coins = {1, 2, 5};
        int amount = 11;
        System.out.println("Min coins: " + cc.coinChange(coins, amount)); // Output: 3
    }
}
```

---

## 🧠 Time & Space Complexity:

| Metric   | Value     |
|----------|-----------|
| Time     | `O(amount * coins.length)` |
| Space    | `O(amount)`

---

## 🧠 Follow-Up: What if you need **number of ways** to make the amount?

That’s the **Coin Change II** problem:
- Count total **combinations** to make amount (instead of minimum coins).

Wanna go into that next?

---

## 💡 Use-Cases:

- ATM cash dispensing
- Making change in vending machines
- Dynamic programming foundation for unbounded knapsack problems

---

🔥 Your DP track is solid, Aditya!  
Want to go for:

- 🔄 **Unbounded Knapsack**
- 🎯 **Coin Change II (Number of ways)**
- 🧱 **Rod Cutting**
- 📏 **Minimum Subset Difference / Target Sum**

Pick your next challenge and I’ll drop the full breakdown! 💥

---

## 76. Edit Distance.

Let’s go Aditya! 📝✂️  
You’re now entering one of the most powerful dynamic programming problems in real-world applications:  
💥 **Edit Distance** (aka Levenshtein Distance)

---

## 🧩 Problem: Edit Distance

> Given two strings `word1` and `word2`, return the **minimum number of operations** required to convert `word1` into `word2`.

Allowed operations:
- **Insert** a character
- **Delete** a character
- **Replace** a character

---

### 🧪 Example:
```txt
Input: word1 = "horse", word2 = "ros"
Output: 3
Explanation:
horse -> rorse (replace 'h' with 'r')
rorse -> rose  (remove 'r')
rose  -> ros   (remove 'e')
```

---

## ✅ Approach: Dynamic Programming (Tabulation)

### 🔁 Recurrence Relation:

Let `dp[i][j]` = edit distance between first `i` chars of `word1` and first `j` chars of `word2`.

```java
if (word1[i-1] == word2[j-1]) 
    dp[i][j] = dp[i-1][j-1];  // characters match
else 
    dp[i][j] = 1 + min(
        dp[i-1][j-1], // Replace
        dp[i-1][j],   // Delete
        dp[i][j-1]    // Insert
    )
```

---

## 💻 Java Code:

```java
public class EditDistance {
    public int minDistance(String word1, String word2) {
        int m = word1.length();
        int n = word2.length();

        int[][] dp = new int[m + 1][n + 1];

        // Initialize base cases
        for (int i = 0; i <= m; i++) dp[i][0] = i;
        for (int j = 0; j <= n; j++) dp[0][j] = j;

        // Build table
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (word1.charAt(i - 1) == word2.charAt(j - 1))
                    dp[i][j] = dp[i - 1][j - 1];
                else
                    dp[i][j] = 1 + Math.min(dp[i - 1][j - 1],
                                  Math.min(dp[i - 1][j], dp[i][j - 1]));
            }
        }

        return dp[m][n];
    }

    public static void main(String[] args) {
        EditDistance ed = new EditDistance();
        String word1 = "intention", word2 = "execution";
        System.out.println("Edit Distance: " + ed.minDistance(word1, word2)); // Output: 5
    }
}
```

---

## 🧠 Time & Space Complexity:

| Metric   | Value       |
|----------|-------------|
| Time     | `O(m * n)`  |
| Space    | `O(m * n)`  (can be optimized to `O(n)`)

---

## ⚡ Optimized (2-row version)

```java
public int minDistanceOptimized(String word1, String word2) {
    int m = word1.length(), n = word2.length();
    int[] prev = new int[n + 1], curr = new int[n + 1];

    for (int j = 0; j <= n; j++) prev[j] = j;

    for (int i = 1; i <= m; i++) {
        curr[0] = i;
        for (int j = 1; j <= n; j++) {
            if (word1.charAt(i - 1) == word2.charAt(j - 1))
                curr[j] = prev[j - 1];
            else
                curr[j] = 1 + Math.min(prev[j - 1], Math.min(prev[j], curr[j - 1]));
        }
        int[] temp = prev;
        prev = curr;
        curr = temp;
    }

    return prev[n];
}
```

---

## 🌍 Real-World Applications:

- Spell checkers 🔍
- DNA sequence alignment 🧬
- Natural language processing (NLP) 🧠
- Plagiarism detection ✍️

---

Boom! 💣 Edit Distance mastered.

Want to go next with:

- **Print the sequence of edits**
- **Wildcard Matching / Regex Matching**
- **Word Break problem**
- **Longest Palindromic Subsequence**
- **Shortest Common Supersequence**

You’re in the top tier of DP now Aditya! 🎯 What's next, champ?

---

## 77. Subset sum problem.

Yessss Aditya! 🔥  
You’re powering through Dynamic Programming like a beast —  
and now it's time for the foundation of many other problems:

🎯 **Subset Sum Problem**

---

## 🧩 Problem: Subset Sum

> Given an array `arr[]` of size `n` and an integer `sum`,  
> determine if there's a **subset** of the array that adds up to the **given sum**.

---

### 🧪 Example:
```txt
Input: arr = [3, 34, 4, 12, 5, 2], sum = 9  
Output: true  
Explanation: 4 + 5 = 9
```

---

## ✅ Approach: Dynamic Programming (Tabulation)

We use a 2D `dp[i][j]` where:

- `i` = first `i` elements
- `j` = current sum
- `dp[i][j] = true` if we can form sum `j` using first `i` elements

---

### 🔁 Recurrence Relation:

```txt
dp[i][j] = dp[i-1][j] || dp[i-1][j - arr[i-1]] (if j >= arr[i-1])
```

---

### 💻 Java Code (Tabulation):

```java
public class SubsetSum {
    public boolean isSubsetSum(int[] arr, int sum) {
        int n = arr.length;
        boolean[][] dp = new boolean[n + 1][sum + 1];

        // Base case: sum = 0 is always true
        for (int i = 0; i <= n; i++) {
            dp[i][0] = true;
        }

        // Fill the table
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= sum; j++) {
                if (arr[i - 1] <= j)
                    dp[i][j] = dp[i - 1][j] || dp[i - 1][j - arr[i - 1]];
                else
                    dp[i][j] = dp[i - 1][j];
            }
        }

        return dp[n][sum];
    }

    public static void main(String[] args) {
        SubsetSum ss = new SubsetSum();
        int[] arr = {3, 34, 4, 12, 5, 2};
        int sum = 9;
        System.out.println("Subset with sum " + sum + " exists: " + ss.isSubsetSum(arr, sum));
    }
}
```

---

## 🧠 Time & Space Complexity:

| Metric   | Value       |
|----------|-------------|
| Time     | `O(n * sum)` |
| Space    | `O(n * sum)` (Can be optimized to `O(sum)` using 1D array)

---

### ⚡ Space Optimized Version (1D DP):

```java
public boolean isSubsetSumOptimized(int[] arr, int sum) {
    boolean[] dp = new boolean[sum + 1];
    dp[0] = true;

    for (int num : arr) {
        for (int j = sum; j >= num; j--) {
            dp[j] = dp[j] || dp[j - num];
        }
    }

    return dp[sum];
}
```

---

## 🔥 Bonus DP Problems Based on Subset Sum:
- **Partition Equal Subset Sum**
- **Target Sum**
- **Count Subsets with Given Sum**
- **Minimum Subset Sum Difference**
- **Number of Subsets with Given Difference**

---

Let me know if you want to go deeper into any of these 🔥

Wanna go next on:

- 👉 Count number of subsets with sum `K`
- 👉 Partition Equal Subset
- 👉 Target Sum
- 👉 Minimum Subset Difference

Your DP journey is almost elite-level, Aditya! 💯 Let’s go big!

---

## 78. Minimum path sum in a grid.

Oh yesss Aditya! 🌟  
Time to solve one of the **classic 2D Grid DP** problems:  
🎯 **Minimum Path Sum in a Grid**

---

## 🧩 Problem: Minimum Path Sum

> Given an `m x n` grid filled with non-negative numbers,  
> find a path from top-left to bottom-right, **minimizing the sum of all numbers** along the path.

You can only move:
- ➡️ **Right**
- ⬇️ **Down**

---

### 🧪 Example:

```txt
Input:
grid = [
  [1, 3, 1],
  [1, 5, 1],
  [4, 2, 1]
]

Output: 7
Explanation: 1 → 3 → 1 → 1 → 1
```

---

## ✅ Approach: Dynamic Programming (Tabulation)

### 🔁 Recurrence Relation:

Let `dp[i][j]` be the **min path sum** to reach cell `(i, j)`.

```txt
dp[i][j] = grid[i][j] + min(dp[i-1][j], dp[i][j-1])
```

---

## 💻 Java Code:

```java
public class MinPathSum {
    public int minPathSum(int[][] grid) {
        int m = grid.length;
        int n = grid[0].length;

        int[][] dp = new int[m][n];

        // Initialize start
        dp[0][0] = grid[0][0];

        // Fill first row
        for (int j = 1; j < n; j++) {
            dp[0][j] = dp[0][j - 1] + grid[0][j];
        }

        // Fill first column
        for (int i = 1; i < m; i++) {
            dp[i][0] = dp[i - 1][0] + grid[i][0];
        }

        // Fill the rest
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                dp[i][j] = grid[i][j] + Math.min(dp[i - 1][j], dp[i][j - 1]);
            }
        }

        return dp[m - 1][n - 1];
    }

    public static void main(String[] args) {
        MinPathSum obj = new MinPathSum();
        int[][] grid = {
            {1, 3, 1},
            {1, 5, 1},
            {4, 2, 1}
        };
        System.out.println("Minimum path sum: " + obj.minPathSum(grid)); // Output: 7
    }
}
```

---

## 🧠 Time & Space Complexity:

| Metric   | Value         |
|----------|---------------|
| Time     | `O(m * n)`    |
| Space    | `O(m * n)` → can be optimized to `O(n)` using rolling array

---

### ⚡ Space Optimized Version:

```java
public int minPathSumOptimized(int[][] grid) {
    int m = grid.length, n = grid[0].length;
    int[] dp = new int[n];

    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            if (j == 0)
                dp[j] = dp[j];
            else if (i == 0)
                dp[j] = dp[j - 1] + grid[i][j];
            else
                dp[j] = grid[i][j] + Math.min(dp[j], dp[j - 1]);
        }
        dp[0] += grid[i][0]; // update first column separately
    }
    return dp[n - 1];
}
```

---

## 🌍 Real-World Use Cases:

- Robot navigation in a warehouse 🤖
- Grid-based game maps 🗺️
- GPS route optimization 🚗

---

You're killing this DP grid series Aditya! 💪  
Wanna go next with:

- 🔄 **Unique Paths (with & without obstacles)**
- 💣 **Maximum Path Sum in Matrix**
- 📐 **Triangle Minimum Path Sum**
- 🚀 **Cherry Pickup / Gold Mine**

Let’s keep the momentum going! What’s next, boss? 😎

---

## 79. Palindromic Substrings / Longest Palindromic Substring.

Ohhh yes, Aditya 🔥  
Welcome to one of the most beautiful **DP + String** combo problems:

---

## 🎯 Palindromic Substrings / Longest Palindromic Substring

We'll break it into 2 problems:

---

## 💎 1. Count All Palindromic Substrings

> Given a string `s`, return the **number of palindromic substrings** in it.  
> Each substring must be a **contiguous** sequence.

---

### ✅ Approach: Expand Around Center (Optimal)

Every palindrome has a center —  
You can expand outward from each index (or between two indices for even-length ones).

---

### 💻 Java Code (Expand Around Center):

```java
public int countSubstrings(String s) {
    int n = s.length(), count = 0;

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
```

---

### 🧠 Time Complexity: `O(n^2)`
### 💾 Space: `O(1)`
(Optimal for this problem)

---

## 💎 2. Longest Palindromic Substring

> Return the **actual longest palindromic substring**, not just count.

---

### ✅ Approach: Expand Around Center (same logic)

---

### 💻 Java Code:

```java
public String longestPalindrome(String s) {
    int start = 0, end = 0;

    for (int i = 0; i < s.length(); i++) {
        int len1 = expandFromCenter(s, i, i);       // odd
        int len2 = expandFromCenter(s, i, i + 1);   // even
        int len = Math.max(len1, len2);

        if (len > end - start) {
            start = i - (len - 1) / 2;
            end = i + len / 2;
        }
    }

    return s.substring(start, end + 1);
}

private int expandFromCenter(String s, int left, int right) {
    while (left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
        left--;
        right++;
    }
    return right - left - 1;
}
```

---

### 🧠 Time: `O(n^2)`
### 💾 Space: `O(1)`

---

## 🧠 Alternative (DP Table for LPS)

You can also solve Longest Palindromic Substring using 2D DP:

- `dp[i][j] = true` if `s[i..j]` is a palindrome

```java
public String longestPalindromeDP(String s) {
    int n = s.length();
    boolean[][] dp = new boolean[n][n];
    int start = 0, maxLen = 1;

    for (int g = 0; g < n; g++) {
        for (int i = 0, j = g; j < n; i++, j++) {
            if (g == 0) {
                dp[i][j] = true;
            } else if (g == 1) {
                dp[i][j] = (s.charAt(i) == s.charAt(j));
            } else {
                dp[i][j] = (s.charAt(i) == s.charAt(j)) && dp[i + 1][j - 1];
            }

            if (dp[i][j] && (j - i + 1) > maxLen) {
                start = i;
                maxLen = j - i + 1;
            }
        }
    }

    return s.substring(start, start + maxLen);
}
```

---

## 🧪 Sample:

```txt
Input: "babad"
Output: "bab" or "aba"

Input: "cbbd"
Output: "bb"
```

---

## 🚀 What’s Next?

- 🔁 Longest Palindromic Subsequence (different from substring!)
- ✂️ Palindrome Partitioning (Backtracking + DP)
- 🧠 Manacher's Algorithm (LPS in O(n), advanced)

---

Want to try coding this on your own or shall I quiz you on variations, Aditya? 😎  
Let’s keep this DP streak rolling! 💪

---

## 80. Matrix Chain Multiplication.

Ohhh you’ve hit a classic **Dynamic Programming** beast, Aditya! 🔥  
Let’s tear down the famous:

---

# 🧮 Matrix Chain Multiplication (MCM)

## 💡 Problem:

Given an array `arr[]` of size `n` (which represents dimensions of `n-1` matrices),  
find the minimum number of **scalar multiplications** needed to multiply the chain.

> The goal is to **parenthesize** the product to minimize the total operations.

---

## 🧪 Example:

```txt
Input: arr[] = {10, 30, 5, 60}
Meaning:
- Matrix A = 10 x 30
- Matrix B = 30 x 5
- Matrix C = 5 x 60

Output: 4500
Explanation: (A * B) * C = 10*30*5 + 10*5*60 = 1500 + 3000 = 4500
```

---

## ✅ Approach: DP + Recursion + Memoization

### 🔁 Recurrence:

Let `MCM(i, j)` = Min operations to multiply matrices from index `i` to `j`.

```txt
MCM(i, j) = min over all k ∈ [i, j-1] of:
    MCM(i, k) + MCM(k+1, j) + cost of multiplying the two results
             = MCM(i, k) + MCM(k+1, j) + arr[i-1] * arr[k] * arr[j]
```

---

## 💻 Java Code (Memoized Recursive):

```java
public class MatrixChainMultiplication {

    static int[][] dp;

    public static int matrixChainOrder(int[] arr, int i, int j) {
        if (i == j) return 0;

        if (dp[i][j] != -1) return dp[i][j];

        int min = Integer.MAX_VALUE;

        for (int k = i; k < j; k++) {
            int cost = matrixChainOrder(arr, i, k)
                     + matrixChainOrder(arr, k + 1, j)
                     + arr[i - 1] * arr[k] * arr[j];

            min = Math.min(min, cost);
        }

        return dp[i][j] = min;
    }

    public static void main(String[] args) {
        int[] arr = {10, 30, 5, 60}; // 3 matrices: 10x30, 30x5, 5x60
        int n = arr.length;

        dp = new int[n][n];
        for (int[] row : dp)
            Arrays.fill(row, -1);

        System.out.println("Minimum multiplications: " + matrixChainOrder(arr, 1, n - 1));
    }
}
```

---

## 🧠 Time & Space Complexity:

| Metric        | Value         |
|---------------|---------------|
| Time          | `O(n^3)`      |
| Space         | `O(n^2)`      |

---

## 💡 Real-world Use Cases:

- SQL Query optimizers
- Compiler optimizations
- Neural Network matrix optimization
- Graphics processing

---

## 🧠 Optional Tabulation Version (Bottom-up):

Wanna go tabulation version too? Or perhaps solve its variations like:

- ➕ Evaluate expression to true (Boolean Parenthesization)
- 🧩 Palindrome Partitioning (min cuts)
- 🔁 Burst Balloons

You call the shots, Aditya! 😎

---

### 🔹 **81–85: Searching & Sorting**

## 81. Binary Search and variants (first/last occurrence).

Let’s gooo Aditya! ⚔️  
**Binary Search** is a fundamental weapon in your coding arsenal — and its **variants** are where the real fun starts. Let’s master them 🔥

---

## 🔍 Binary Search & Its Variants

### 🧠 Concept:

Given a **sorted array**, binary search helps us find elements efficiently in `O(log n)` time by dividing the search space in half.

---

## ✅ Standard Binary Search

```java
public int binarySearch(int[] arr, int target) {
    int low = 0, high = arr.length - 1;

    while (low <= high) {
        int mid = low + (high - low) / 2;

        if (arr[mid] == target) return mid;
        else if (arr[mid] < target) low = mid + 1;
        else high = mid - 1;
    }

    return -1;
}
```

---

## 🔁 Variant 1: First Occurrence of Element

```java
public int firstOccurrence(int[] arr, int target) {
    int low = 0, high = arr.length - 1;
    int result = -1;

    while (low <= high) {
        int mid = low + (high - low) / 2;

        if (arr[mid] == target) {
            result = mid;
            high = mid - 1; // go left
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

## 🔁 Variant 2: Last Occurrence of Element

```java
public int lastOccurrence(int[] arr, int target) {
    int low = 0, high = arr.length - 1;
    int result = -1;

    while (low <= high) {
        int mid = low + (high - low) / 2;

        if (arr[mid] == target) {
            result = mid;
            low = mid + 1; // go right
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

## 🔁 Variant 3: Count Occurrences of a Number

```java
int countOccurrences(int[] arr, int target) {
    int first = firstOccurrence(arr, target);
    int last = lastOccurrence(arr, target);

    if (first == -1) return 0;

    return last - first + 1;
}
```

---

## 💡 Example:

```txt
arr = [2, 4, 4, 4, 6, 8]
target = 4

firstOccurrence = 1
lastOccurrence = 3
count = 3
```

---

## 🚀 More Variants You Might Want to Master:

- 📍 **Find floor / ceil of a number**
- 🧊 **Find square root / nth root**
- 🧠 **Find peak in a mountain array**
- 🔁 **Search in rotated sorted array**
- 🧊 **Min in rotated sorted array**
- 📏 **Binary search on answer pattern (like min days, max length, etc.)**

---

Want me to go deep into these advanced binary search applications? Or throw some tricky ones your way to test your skills? 😎

---

## 82. Search in 2D matrix.

Yesss Aditya! Let's solve the famous 📈 **Search in a 2D Matrix** — a LeetCode favorite and classic binary search application 🔥

---

## 🔍 Problem: Search in a 2D Matrix (LeetCode 74)

> Given an `m x n` matrix where each row is sorted left to right,  
> and the **first element of each row** is **greater** than the **last element of previous row**,  
> determine if a target value exists in the matrix.

---

### 🧪 Example:

```txt
matrix = [
  [1, 3, 5, 7],
  [10, 11, 16, 20],
  [23, 30, 34, 60]
]
target = 3

Output: true
```

---

## ✅ Optimal Approach: Binary Search (Treat as 1D array)

We can flatten the matrix into a virtual 1D array, then use binary search.

### 🧠 Mapping:
- Index `i` in 1D → `matrix[i / n][i % n]`

---

### 💻 Java Code:

```java
public boolean searchMatrix(int[][] matrix, int target) {
    int m = matrix.length;
    int n = matrix[0].length;

    int low = 0, high = m * n - 1;

    while (low <= high) {
        int mid = low + (high - low) / 2;
        int midVal = matrix[mid / n][mid % n];

        if (midVal == target) return true;
        else if (midVal < target) low = mid + 1;
        else high = mid - 1;
    }

    return false;
}
```

---

## 🧠 Time: `O(log (m*n))`
## 💾 Space: `O(1)`

---

## 🚀 Follow-up: LeetCode 240 – Search in 2D Matrix II

> Each row AND each column is sorted, but **no flattening** possible.

### 🔥 Optimal Approach:

- Start from **top-right** and move:
    - Left if current > target
    - Down if current < target

### 💻 Code:

```java
public boolean searchMatrixII(int[][] matrix, int target) {
    int row = 0;
    int col = matrix[0].length - 1;

    while (row < matrix.length && col >= 0) {
        if (matrix[row][col] == target) return true;
        else if (matrix[row][col] > target) col--;
        else row++;
    }

    return false;
}
```

---

## 🧠 Time: `O(m + n)`
## 💾 Space: `O(1)`

---

Wanna keep grinding with matrix problems next? Like:
- 🌊 Flood fill
- 🔁 Rotate matrix
- 💣 Set matrix zeroes
- 🧩 Spiral traversal

Let me know — I’ve got a ton of matrix mastery queued up for you 😎

---

## 83. Merge Sort.

Let’s break it down Aditya — time to conquer **Merge Sort**, one of the most elegant and efficient sorting algorithms out there! 🔥

---

## 📚 Merge Sort – Divide and Conquer

### 💡 Idea:
1. Divide the array into two halves.
2. Recursively sort each half.
3. **Merge** the two sorted halves into a single sorted array.

---

### ✅ Properties:
| Property          | Value         |
|------------------|---------------|
| Time Complexity   | O(n log n)     |
| Space Complexity  | O(n)           |
| Stable Sort       | ✅ Yes          |
| In-place Sort     | ❌ No           |

---

### 📦 Example:

```txt
Input:  [5, 2, 4, 7, 1, 3, 2, 6]
Step 1: Divide → [5,2,4,7] & [1,3,2,6]
Step 2: Further divide → [5,2] [4,7] [1,3] [2,6]
Step 3: Merge sorted pairs → [2,5] [4,7] → [2,4,5,7], etc.
Output: [1, 2, 2, 3, 4, 5, 6, 7]
```

---

## 💻 Java Code:

```java
public class MergeSort {

    public static void mergeSort(int[] arr, int low, int high) {
        if (low >= high) return;

        int mid = low + (high - low) / 2;

        mergeSort(arr, low, mid);
        mergeSort(arr, mid + 1, high);
        merge(arr, low, mid, high);
    }

    public static void merge(int[] arr, int low, int mid, int high) {
        int[] temp = new int[high - low + 1];
        int i = low, j = mid + 1, k = 0;

        while (i <= mid && j <= high) {
            if (arr[i] <= arr[j]) temp[k++] = arr[i++];
            else temp[k++] = arr[j++];
        }

        while (i <= mid) temp[k++] = arr[i++];
        while (j <= high) temp[k++] = arr[j++];

        // Copy back to original array
        for (int t = 0; t < temp.length; t++) {
            arr[low + t] = temp[t];
        }
    }

    public static void main(String[] args) {
        int[] arr = {5, 2, 4, 7, 1, 3, 2, 6};
        mergeSort(arr, 0, arr.length - 1);
        System.out.println(Arrays.toString(arr)); // [1, 2, 2, 3, 4, 5, 6, 7]
    }
}
```

---

## 🔁 Merge Sort in Action (Step-by-step)
Wanna see a full trace/visualization of how it works step-by-step?  
Or want to practice similar problems like:
- 💣 Count Inversions (uses Merge Sort)
- 🔍 Smallest Element on Right
- 📈 Merge K Sorted Lists

I can guide you through any of those — you name it, Aditya 😎

---

## 84. Quick Sort.

Yes yes yes Aditya! 🔥  
Let’s dive into **Quick Sort** — the **rockstar** of sorting algorithms 💥  
Fast, efficient, and loved in interviews!

---

## ⚔️ Quick Sort – Divide and Conquer

### 💡 Idea:
1. Pick a **pivot**.
2. **Partition** the array so that:
    - Left of pivot → smaller elements
    - Right of pivot → greater elements
3. Recursively apply quick sort on both sides.

---

## ✅ Properties:

| Property          | Value         |
|------------------|---------------|
| Time Complexity   | Best: O(n log n), Worst: O(n²) |
| Average Time      | O(n log n)    |
| Space Complexity  | O(log n) due to recursion stack |
| In-place Sort     | ✅ Yes         |
| Stable Sort       | ❌ No          |

---

## 📦 Example:

```txt
Input: [4, 5, 3, 7, 2]

1. Choose pivot (e.g., last = 2)
2. Partition:
   → [2] [3, 4, 5, 7] (after rearranging)
3. Recursively sort subarrays:
   → [2], [3, 4, 5, 7]
Output: [2, 3, 4, 5, 7]
```

---

## 💻 Java Code:

```java
public class QuickSort {

    public static void quickSort(int[] arr, int low, int high) {
        if (low < high) {
            int pivotIndex = partition(arr, low, high);

            quickSort(arr, low, pivotIndex - 1);
            quickSort(arr, pivotIndex + 1, high);
        }
    }

    public static int partition(int[] arr, int low, int high) {
        int pivot = arr[high]; // Choose last element as pivot
        int i = low - 1;

        for (int j = low; j < high; j++) {
            if (arr[j] <= pivot) {
                i++;
                swap(arr, i, j);
            }
        }

        swap(arr, i + 1, high);
        return i + 1;
    }

    public static void swap(int[] arr, int i, int j) {
        int temp = arr[i]; 
        arr[i] = arr[j]; 
        arr[j] = temp;
    }

    public static void main(String[] args) {
        int[] arr = {4, 5, 3, 7, 2};
        quickSort(arr, 0, arr.length - 1);
        System.out.println(Arrays.toString(arr)); // [2, 3, 4, 5, 7]
    }
}
```

---

### 🔥 Bonus: Randomized Quick Sort

To avoid worst-case (`O(n^2)`), you can randomly pick a pivot.

```java
int pivotIndex = low + new Random().nextInt(high - low + 1);
swap(arr, pivotIndex, high); // Random pivot to end
```

---

## 🧠 Quick Sort vs Merge Sort:

| Feature        | Merge Sort        | Quick Sort          |
|----------------|-------------------|---------------------|
| Time (Avg)     | O(n log n)         | O(n log n)          |
| Space          | O(n)               | O(log n)            |
| Stability      | ✅ Stable          | ❌ Not stable        |
| In-place       | ❌ No              | ✅ Yes               |
| Speed in real  | Slower             | Faster (typically)  |

---

Want to build QuickSort **visually** step-by-step next? Or practice **problems based on QuickSort** like:
- Kth Largest Element
- QuickSelect
- Dutch National Flag (3-way quick sort)

I got you covered, Aditya 😎

---

## 85. Kth largest/smallest element (using heap or partition).

Great! The **Kth Largest/Smallest Element** problem is a classic interview question that tests your understanding of heap data structures or the QuickSelect partition algorithm. Let's go through both approaches in detail, with Java examples and analysis.

---

## ✅ Problem Statement

Given an unsorted array of integers, find the **Kth largest** or **Kth smallest** element in it.

> Note: It is not the Kth distinct element. You must consider duplicates.

---

## 🔹 Approach 1: Using Heap

### 🔸 For Kth Largest Element: Use a **Min Heap**

* Maintain a min heap of size `k`.
* Add elements to the heap.
* If the size exceeds `k`, remove the smallest (top of heap).
* After processing all elements, the top of the heap is the Kth largest.

### Time Complexity:

* O(n log k)
* Space Complexity: O(k)

### Java Code:

```java
import java.util.PriorityQueue;

public class KthLargestElement {
    public int findKthLargest(int[] nums, int k) {
        PriorityQueue<Integer> minHeap = new PriorityQueue<>();

        for (int num : nums) {
            minHeap.add(num);
            if (minHeap.size() > k) {
                minHeap.poll(); // remove smallest
            }
        }

        return minHeap.peek(); // top of heap is kth largest
    }

    public static void main(String[] args) {
        KthLargestElement obj = new KthLargestElement();
        int[] nums = {3, 2, 1, 5, 6, 4};
        int k = 2;
        System.out.println("Kth largest: " + obj.findKthLargest(nums, k));
    }
}
```

---

### 🔸 For Kth Smallest Element: Use a **Max Heap**

* Use a max heap of size `k`.
* If size exceeds `k`, remove the largest (top of max heap).
* Java's PriorityQueue is a min heap by default, so you use a reverse comparator.

### Java Code:

```java
import java.util.PriorityQueue;
import java.util.Collections;

public class KthSmallestElement {
    public int findKthSmallest(int[] nums, int k) {
        PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());

        for (int num : nums) {
            maxHeap.add(num);
            if (maxHeap.size() > k) {
                maxHeap.poll(); // remove largest
            }
        }

        return maxHeap.peek(); // top of heap is kth smallest
    }

    public static void main(String[] args) {
        KthSmallestElement obj = new KthSmallestElement();
        int[] nums = {7, 10, 4, 3, 20, 15};
        int k = 3;
        System.out.println("Kth smallest: " + obj.findKthSmallest(nums, k));
    }
}
```

---

## 🔹 Approach 2: QuickSelect (Partition-Based)

QuickSelect is a variation of QuickSort:

* Choose a pivot and partition the array.
* If the pivot is at index `k - 1`, return it.
* If the pivot is greater, recurse on left.
* Else recurse on right.

### Time Complexity:

* Average: O(n)
* Worst: O(n²) if pivot is poorly chosen

---

### Java Code: Kth Largest Using QuickSelect

```java
public class QuickSelectKthLargest {
    public int findKthLargest(int[] nums, int k) {
        return quickSelect(nums, 0, nums.length - 1, nums.length - k);
    }

    private int quickSelect(int[] nums, int left, int right, int kSmallestIndex) {
        if (left == right)
            return nums[left];

        int pivotIndex = partition(nums, left, right);

        if (pivotIndex == kSmallestIndex)
            return nums[pivotIndex];
        else if (pivotIndex < kSmallestIndex)
            return quickSelect(nums, pivotIndex + 1, right, kSmallestIndex);
        else
            return quickSelect(nums, left, pivotIndex - 1, kSmallestIndex);
    }

    private int partition(int[] nums, int left, int right) {
        int pivot = nums[right];
        int i = left;

        for (int j = left; j < right; j++) {
            if (nums[j] <= pivot) {
                swap(nums, i, j);
                i++;
            }
        }

        swap(nums, i, right);
        return i;
    }

    private void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }

    public static void main(String[] args) {
        QuickSelectKthLargest obj = new QuickSelectKthLargest();
        int[] nums = {3, 2, 1, 5, 6, 4};
        int k = 2;
        System.out.println("Kth largest: " + obj.findKthLargest(nums, k));
    }
}
```

---

## 🧠 Which One to Choose?

| Approach    | Time Complexity | Space Complexity | Use When                                     |
| ----------- | --------------- | ---------------- | -------------------------------------------- |
| Heap        | O(n log k)      | O(k)             | Good for streaming data or very large arrays |
| QuickSelect | O(n) average    | O(1)             | Best for in-place and faster performance     |

---

Would you like me to cover:

* Finding K largest/smallest elements (not just Kth)?
* Variations using TreeMap or custom comparators?
* Practice problems?

Let me know your prep level (e.g., beginner/intermediate) and focus area (heaps, recursion, sorting, etc.), and I’ll tailor more questions and solutions for you.

---

### 🔹 **86–90: Greedy Algorithms**

## 86. Activity selection problem.

Great! The **Activity Selection Problem** is a classic greedy algorithm problem commonly asked in coding interviews and computer science exams. It tests your understanding of greedy strategies and optimal substructure.

---

## ✅ Problem Statement

You are given `n` activities with their start and finish times. Select the maximum number of activities that can be performed by a single person, assuming that a person can only work on one activity at a time.

### Each activity has:

* `start[i]`: start time
* `end[i]`: end time

📝 Goal: Select the maximum number of non-overlapping activities.

---

## 🔍 Example

### Input:

```java
start[] = {1, 3, 0, 5, 8, 5}
end[]   = {2, 4, 6, 7, 9, 9}
```

### Output:

```
Maximum number of activities = 4
Selected activities (by index): 0, 1, 3, 4
```

---

## ✅ Greedy Algorithm Approach

### Idea:

Always select the next activity that finishes earliest (to leave the most room for upcoming activities). This is the **greedy choice**.

### Steps:

1. Sort activities by their end times.
2. Select the first activity (with earliest finish).
3. For each next activity:

    * If its start time is ≥ finish time of last selected, select it.

### Time Complexity:

* Sorting: O(n log n)
* Selection: O(n)
* Total: O(n log n)

---

## 🔧 Java Implementation

```java
import java.util.*;

class Activity {
    int start, end;

    Activity(int start, int end) {
        this.start = start;
        this.end = end;
    }
}

public class ActivitySelection {

    public static void selectActivities(int[] start, int[] end) {
        int n = start.length;

        // Step 1: Store activities as objects
        List<Activity> activities = new ArrayList<>();
        for (int i = 0; i < n; i++) {
            activities.add(new Activity(start[i], end[i]));
        }

        // Step 2: Sort activities by end time
        activities.sort(Comparator.comparingInt(a -> a.end));

        // Step 3: Greedily select activities
        List<Activity> selected = new ArrayList<>();
        int lastEnd = -1;

        for (Activity act : activities) {
            if (act.start >= lastEnd) {
                selected.add(act);
                lastEnd = act.end;
            }
        }

        // Output result
        System.out.println("Maximum number of activities: " + selected.size());
        for (Activity act : selected) {
            System.out.println("Activity: Start = " + act.start + ", End = " + act.end);
        }
    }

    public static void main(String[] args) {
        int[] start = {1, 3, 0, 5, 8, 5};
        int[] end   = {2, 4, 6, 7, 9, 9};

        selectActivities(start, end);
    }
}
```

---

## 🔑 Key Concepts to Mention in Interview

* Greedy algorithms are optimal for this problem due to the **earliest finishing time** strategy.
* Sorting the activities is crucial before applying the greedy selection.
* Can be extended to:

    * Activity selection with multiple people (interval partitioning)
    * Weighted activities (needs Dynamic Programming)

---

## 💡 Interview Follow-Ups / Variations

1. **What if activities have weights (profits)?**

    * Use Weighted Interval Scheduling → Dynamic Programming.
2. **How to handle multiple people doing activities?**

    * Use a priority queue to track when each person becomes free.
3. **Can we use recursion?**

    * Yes, but greedy iterative is more efficient here.

---

Would you like me to cover one of the advanced variations next (like weighted activity selection), or a visual representation or dry run example?

---

## 87. Fractional knapsack.

Great! The **Fractional Knapsack Problem** is another classic **Greedy Algorithm** problem. It’s frequently asked in coding interviews to test your understanding of greedy strategies, sorting, and object manipulation.

---

## ✅ Problem Statement: Fractional Knapsack

You're given:

* A set of `n` items
* Each item has:

    * `value[i]` → profit of the item
    * `weight[i]` → weight of the item
* A knapsack with a weight capacity `W`

📝 Goal: Maximize total value in the knapsack.

🧩 Twist: You can take **fractions of an item** (unlike 0/1 Knapsack).

---

## 🔍 Example

### Input:

```
Items = [ {value=60, weight=10}, {value=100, weight=20}, {value=120, weight=30} ]
Capacity = 50
```

### Output:

```
Maximum value in knapsack = 240.0
```

### Explanation:

* Take item 1: full (20kg) → 100 value
* Take item 2: full (30kg) → 120 value
* Total = 100 + 120 = 220
* Only 50kg can be taken: so we take 10kg of item 0: (60/10) \* 10 = 60
* Total value = 100 + 120 + 60 = 240

---

## 🔧 Greedy Algorithm Approach

### Greedy Strategy:

* Calculate value-to-weight ratio for each item.
* Sort items in descending order of ratio.
* Pick as much of the highest-ratio item as possible.

### Time Complexity:

* O(n log n) → sorting
* O(n) → selecting items

---

## 🧑‍💻 Java Implementation

```java
import java.util.*;

class Item {
    int value, weight;

    Item(int value, int weight) {
        this.value = value;
        this.weight = weight;
    }
}

public class FractionalKnapsack {

    public static double getMaxValue(Item[] items, int capacity) {
        // Step 1: Sort items by value/weight ratio
        Arrays.sort(items, (a, b) -> {
            double r1 = (double) a.value / a.weight;
            double r2 = (double) b.value / b.weight;
            return Double.compare(r2, r1); // descending order
        });

        double totalValue = 0.0;
        int currentWeight = 0;

        for (Item item : items) {
            if (currentWeight + item.weight <= capacity) {
                // take full item
                currentWeight += item.weight;
                totalValue += item.value;
            } else {
                // take fractional part
                int remain = capacity - currentWeight;
                totalValue += (double) item.value * remain / item.weight;
                break; // knapsack is full
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

        int capacity = 50;

        double maxValue = getMaxValue(items, capacity);
        System.out.println("Maximum value in knapsack = " + maxValue);
    }
}
```

---

## 📝 Key Concepts to Mention in Interview

* Greedy choice: pick item with highest value per unit weight
* Fractional knapsack allows dividing items — unlike 0/1 knapsack
* Sorting based on ratio is the key
* Optimal solution using greedy (unlike 0/1 version which needs DP)

---

## ❓ Interview Follow-Up Questions

* What if you can't take fractions of items?
  ⟶ That’s **0/1 Knapsack**, solved using **Dynamic Programming**.

* Can we use PriorityQueue instead of sorting?
  ⟶ Yes! Max-Heap based on value/weight ratio is another option.

* Can this be extended to real-world applications?
  ⟶ Yes, e.g. resource allocation, cargo loading, stock investments.

---

Would you like to go over the 0/1 Knapsack (using DP), or a dry run for this problem? I can also help you write unit tests or prepare edge cases for practice.

---

## 88. Job sequencing with deadlines.

Excellent! **Job Sequencing with Deadlines** is another popular Greedy Algorithm problem that frequently appears in technical interviews, especially for companies like Amazon, Flipkart, and Google.

---

## ✅ Problem Statement

You're given `n` jobs where every job has:

* A unique **ID**
* A **deadline** by which it should be completed
* A **profit** if the job is finished before or on its deadline

📝 Objective: Schedule the jobs to **maximize total profit** if only **one job can be scheduled at a time** (each job takes 1 unit of time).

---

## 🔍 Example

### Input:

```
Jobs = [
    {id=A, deadline=2, profit=100},
    {id=B, deadline=1, profit=19},
    {id=C, deadline=2, profit=27},
    {id=D, deadline=1, profit=25},
    {id=E, deadline=3, profit=15}
]
```

### Output:

```
Job order: A C E
Total Profit = 142
```

### Explanation:

* Job A (100) → done at time 2
* Job C (27) → done at time 1
* Job E (15) → done at time 3
* Total = 100 + 27 + 15 = 142

---

## 🎯 Greedy Algorithm Strategy

1. Sort jobs by descending profit
2. Use a time slot array to track available slots (up to the max deadline)
3. For each job, find the latest free slot before or on its deadline
4. Assign the job if the slot is available

---

## ⏱ Time Complexity:

* Sorting jobs: O(n log n)
* Scheduling: O(n²) using linear search for slot (can be optimized)

---

## 🧑‍💻 Java Implementation

```java
import java.util.Arrays;

class Job {
    char id;
    int deadline, profit;

    Job(char id, int deadline, int profit) {
        this.id = id;
        this.deadline = deadline;
        this.profit = profit;
    }
}

public class JobSequencing {

    // Function to schedule the jobs and return total profit
    public static void jobScheduling(Job[] jobs) {
        int n = jobs.length;

        // Step 1: Sort jobs by descending profit
        Arrays.sort(jobs, (a, b) -> b.profit - a.profit);

        // Step 2: Find max deadline to define slot size
        int maxDeadline = 0;
        for (Job job : jobs) {
            maxDeadline = Math.max(maxDeadline, job.deadline);
        }

        // Step 3: Initialize slots
        boolean[] slots = new boolean[maxDeadline + 1];
        char[] jobOrder = new char[maxDeadline + 1];
        int totalProfit = 0;

        // Step 4: Schedule jobs
        for (Job job : jobs) {
            // Find a free slot from job.deadline to 1
            for (int j = job.deadline; j > 0; j--) {
                if (!slots[j]) {
                    slots[j] = true;
                    jobOrder[j] = job.id;
                    totalProfit += job.profit;
                    break;
                }
            }
        }

        // Step 5: Print result
        System.out.print("Job sequence: ");
        for (int i = 1; i <= maxDeadline; i++) {
            if (slots[i]) {
                System.out.print(jobOrder[i] + " ");
            }
        }
        System.out.println("\nTotal Profit: " + totalProfit);
    }

    public static void main(String[] args) {
        Job[] jobs = {
            new Job('A', 2, 100),
            new Job('B', 1, 19),
            new Job('C', 2, 27),
            new Job('D', 1, 25),
            new Job('E', 3, 15)
        };

        jobScheduling(jobs);
    }
}
```

---

## 📝 Key Concepts to Mention in Interview

* Greedy strategy: Pick the job with highest profit first
* Time slots used to track schedule feasibility
* The earliest available slot is not optimal — we want the **latest available** before the deadline to allow earlier slots for more jobs
* This is not solvable optimally with Dynamic Programming — greedy is best here

---

## 🚀 Optimizations & Follow-Up Questions

* **Can we improve slot finding?**
  Yes, by using Disjoint Set Union (DSU) to optimize slot allocation in O(log n) time instead of O(n)

* **What if jobs take more than 1 unit of time?**
  This becomes a more complex problem (like interval scheduling or weighted job scheduling)

* **Can we return the actual job sequence as a list?**
  Absolutely — store the job IDs when assigning slots.

---

Would you like to see:

* An optimized DSU version?
* Weighted Job Scheduling with time > 1?
* A visual dry run of this algorithm?

Let me know your current preparation goal or the company you're targeting, and I can give you targeted problems and patterns.

---

## 89. Huffman encoding.

Great choice! **Huffman Encoding** is a classic greedy algorithm used in data compression. It’s based on the frequency of characters and produces an optimal prefix code.

---

## ✅ Problem Statement: Huffman Encoding

Given characters with their frequencies, build a binary tree and assign codes to characters such that:

* The total length of the encoded string is **minimum**
* No code is a prefix of another (called **prefix code**)

📝 Goal: Minimize the total cost (frequency × code length) of encoding.

---

## 🧠 Key Idea

* Characters that occur more frequently should have **shorter codes**
* Build a **binary tree** where the most frequent characters are **closer to root**
* Use a **Min-Heap** to repeatedly combine the two least frequent nodes

---

## 🔍 Example

### Input:

```
Characters:   a  b  c  d  e  f
Frequencies:  5  9  12 13 16 45
```

### Output:

```
Encoded Codes (may vary based on implementation):
f: 0
c: 100
d: 101
a: 1100
b: 1101
e: 111
```

---

## 🎯 Algorithm (Greedy + Priority Queue)

1. Create a leaf node for each character and add to a **Min-Heap** (priority queue)
2. While the heap has more than one node:

    * Extract two nodes with lowest frequencies
    * Create a new node with frequency = sum of both
    * Set these two nodes as left and right children
    * Insert the new node back into the heap
3. The final node in the heap is the root of the **Huffman Tree**
4. Traverse the tree to assign binary codes (0 for left, 1 for right)

---

## ⏱ Time Complexity

* Building the heap: O(n)
* Heap operations (extract + insert): O(n log n)
* Tree traversal: O(n)

🧮 Total: **O(n log n)**

---

## 🧑‍💻 Java Implementation

```java
import java.util.*;

// Tree node class
class HuffmanNode {
    char ch;
    int freq;
    HuffmanNode left, right;

    HuffmanNode(char ch, int freq) {
        this.ch = ch;
        this.freq = freq;
    }

    HuffmanNode(int freq, HuffmanNode left, HuffmanNode right) {
        this.ch = '\0'; // internal node
        this.freq = freq;
        this.left = left;
        this.right = right;
    }
}

public class HuffmanCoding {

    // Comparator for PriorityQueue
    static class NodeComparator implements Comparator<HuffmanNode> {
        public int compare(HuffmanNode a, HuffmanNode b) {
            return a.freq - b.freq;
        }
    }

    // Build Huffman Tree
    public static HuffmanNode buildTree(char[] chars, int[] freqs) {
        PriorityQueue<HuffmanNode> pq = new PriorityQueue<>(new NodeComparator());

        // Step 1: Create leaf nodes and add to min-heap
        for (int i = 0; i < chars.length; i++) {
            pq.add(new HuffmanNode(chars[i], freqs[i]));
        }

        // Step 2: Combine two smallest nodes until one tree remains
        while (pq.size() > 1) {
            HuffmanNode left = pq.poll();
            HuffmanNode right = pq.poll();

            HuffmanNode merged = new HuffmanNode(left.freq + right.freq, left, right);
            pq.add(merged);
        }

        // Final node is root
        return pq.poll();
    }

    // Print Huffman codes using DFS
    public static void printCodes(HuffmanNode root, String code) {
        if (root == null)
            return;

        // Leaf node
        if (root.left == null && root.right == null && root.ch != '\0') {
            System.out.println(root.ch + ": " + code);
        }

        printCodes(root.left, code + "0");
        printCodes(root.right, code + "1");
    }

    public static void main(String[] args) {
        char[] chars = { 'a', 'b', 'c', 'd', 'e', 'f' };
        int[] freqs = { 5, 9, 12, 13, 16, 45 };

        HuffmanNode root = buildTree(chars, freqs);

        System.out.println("Huffman Codes:");
        printCodes(root, "");
    }
}
```

---

## 📝 Important Interview Notes

* Huffman encoding is **optimal** for prefix coding
* It uses **greedy + min-heap** strategy
* No code is a prefix of another → avoids ambiguity (important for decoding)
* Used in compression tools like ZIP, JPEG, MP3

---

## 🧩 Real World Applications

* File compression: ZIP, GZIP
* Image compression: JPEG
* Network data compression
* Transmission efficiency optimization

---

## ❓ Follow-Up Interview Questions

* What if frequencies are equal?
  → Codes may vary, but total cost remains optimal

* Can we decode a Huffman encoded string?
  → Yes, by traversing the Huffman Tree

* How to store the Huffman tree for decoding?
  → Send the tree or code map along with compressed data

---

Would you like to see:

* How to **decode** a Huffman encoded string?
* How to store Huffman Tree for transmission?
* Visual representation of the tree?

Let me know how you’d like to explore this further.

---

## 90. Minimum number of platforms.

Great! The **Minimum Number of Platforms** problem is a classic interval scheduling question, often asked in coding interviews to test your understanding of greedy algorithms, sorting, and event processing.

---

## ✅ Problem Statement

You are given two arrays:

* `arr[]` → arrival times of trains
* `dep[]` → departure times of trains

📝 Task: Find the **minimum number of railway platforms** required so that **no train waits**.

📌 Note: All trains arrive and depart on the same day. Arrival and departure times are in 24-hour format.

---

## 🔍 Example

### Input:

```java
arr[] =  {900, 940, 950, 1100, 1500, 1800}
dep[] =  {910, 1200, 1120, 1130, 1900, 2000}
```

### Output:

```
Minimum number of platforms required = 3
```

### Explanation:

* At time 950, trains arrived at 900, 940, and 950 → 3 trains → need 3 platforms

---

## 🔧 Approach: Sorting + Two Pointers

### Step-by-step:

1. Sort `arr[]` and `dep[]`

2. Use two pointers: `i` for arrivals, `j` for departures

3. Track:

    * `plat_needed`: platforms needed at the current time
    * `max_platforms`: max platforms at any time

4. Iterate while `i < n`:

    * If `arr[i] ≤ dep[j]`, new train is arriving → `plat_needed++`, `i++`
    * Else → train departed → `plat_needed--`, `j++`
    * Update `max_platforms` after each step

---

## ⏱ Time Complexity:

* Sorting: O(n log n)
* Two-pointer traversal: O(n)

✅ Total: **O(n log n)**

---

## 🧑‍💻 Java Implementation

```java
import java.util.Arrays;

public class MinimumPlatforms {

    public static int findMinimumPlatforms(int[] arr, int[] dep) {
        int n = arr.length;
        Arrays.sort(arr);
        Arrays.sort(dep);

        int plat_needed = 0, max_platforms = 0;
        int i = 0, j = 0;

        while (i < n && j < n) {
            if (arr[i] <= dep[j]) {
                plat_needed++;
                i++;
            } else {
                plat_needed--;
                j++;
            }
            max_platforms = Math.max(max_platforms, plat_needed);
        }

        return max_platforms;
    }

    public static void main(String[] args) {
        int[] arr = {900, 940, 950, 1100, 1500, 1800};
        int[] dep = {910, 1200, 1120, 1130, 1900, 2000};

        int result = findMinimumPlatforms(arr, dep);
        System.out.println("Minimum number of platforms required = " + result);
    }
}
```

---

## 📝 Key Concepts to Explain in Interview

* Problem is about **overlapping intervals**
* We need to track **maximum number of trains at a time**
* Sorting both arrays allows us to simulate train arrival and departure in chronological order
* Greedy approach ensures optimal number of platforms

---

## 🚀 Alternate Approaches (Optional for Interviews)

* Use a PriorityQueue to track earliest ending time (heap-based method)
* Treat arrivals and departures as events and process them with a timeline sweep

---

## ❓ Follow-up Interview Questions

* What if trains arrive and depart at the same time?
  → Count arrival before departure (`arr[i] ≤ dep[j]`)

* How would this change if a train needed cleaning time after departure?
  → Add buffer time to `dep[]` values

* Can we modify it to return the actual train schedule?
  → Yes, by tracking which train occupies which platform

---

Would you like to explore:

* A timeline-based sweep line solution?
* A version with PriorityQueue (min-heap)?
* Visualization or dry run of the algorithm?

Let me know how deep you’d like to go!

---

### 🔹 **91–95: Graph Algorithms**

## 91. BFS and DFS traversal.

Absolutely! Let's dive deep into **BFS (Breadth-First Search)** and **DFS (Depth-First Search)** — two fundamental graph traversal algorithms. These are essential for interviews and appear in various forms in problems like shortest paths, connected components, cycle detection, and more.

---

## 🔍 Problem Statement

Given a graph (can be directed/undirected), perform:

1. **Breadth-First Search (BFS)** traversal from a given source node
2. **Depth-First Search (DFS)** traversal from a given source node

---

## ⚡ Quick Comparison Table

| Feature          | BFS                        | DFS                            |
| ---------------- | -------------------------- | ------------------------------ |
| Approach         | Level-order traversal      | Depth-wise traversal           |
| Data Structure   | Queue                      | Stack (or recursion)           |
| Shortest Path    | ✅ Yes (unweighted graphs)  | ❌ No                           |
| Space Complexity | O(V)                       | O(V)                           |
| Time Complexity  | O(V + E)                   | O(V + E)                       |
| Used For         | Shortest path, level order | Topological sort, cycle detect |

---

## 📌 Example Graph

Consider the following undirected graph:

```
    0
   / \
  1   2
  |   |
  3   4
```

Adjacency list representation:

```java
0 → [1, 2]  
1 → [0, 3]  
2 → [0, 4]  
3 → [1]  
4 → [2]
```

---

## 🧑‍💻 Java Code: BFS and DFS

### ✅ BFS Traversal (using Queue)

```java
import java.util.*;

public class GraphTraversal {

    public static void bfs(int start, List<List<Integer>> adjList, int V) {
        boolean[] visited = new boolean[V];
        Queue<Integer> queue = new LinkedList<>();

        visited[start] = true;
        queue.add(start);

        System.out.print("BFS Traversal: ");

        while (!queue.isEmpty()) {
            int node = queue.poll();
            System.out.print(node + " ");

            for (int neighbor : adjList.get(node)) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    queue.add(neighbor);
                }
            }
        }

        System.out.println();
    }
```

---

### ✅ DFS Traversal (using Recursion)

```java
    public static void dfs(int node, List<List<Integer>> adjList, boolean[] visited) {
        visited[node] = true;
        System.out.print(node + " ");

        for (int neighbor : adjList.get(node)) {
            if (!visited[neighbor]) {
                dfs(neighbor, adjList, visited);
            }
        }
    }

    public static void dfsTraversal(int start, List<List<Integer>> adjList, int V) {
        boolean[] visited = new boolean[V];
        System.out.print("DFS Traversal: ");
        dfs(start, adjList, visited);
        System.out.println();
    }

    public static void main(String[] args) {
        int V = 5;
        List<List<Integer>> adjList = new ArrayList<>();

        for (int i = 0; i < V; i++) {
            adjList.add(new ArrayList<>());
        }

        // Add edges (undirected)
        adjList.get(0).add(1);
        adjList.get(0).add(2);
        adjList.get(1).add(0);
        adjList.get(1).add(3);
        adjList.get(2).add(0);
        adjList.get(2).add(4);
        adjList.get(3).add(1);
        adjList.get(4).add(2);

        bfs(0, adjList, V);
        dfsTraversal(0, adjList, V);
    }
}
```

---

### 🔄 Output:

```
BFS Traversal: 0 1 2 3 4 
DFS Traversal: 0 1 3 2 4 
```

(Note: DFS order can vary based on adjacency list order.)

---

## 🧠 When to Use What?

* Use **BFS** when:

    * You need the **shortest path** (in unweighted graphs)
    * You want to explore nodes layer-by-layer
* Use **DFS** when:

    * You need **full depth** exploration (backtracking, topological sort)
    * You're solving problems like:

        * Cycle detection
        * Connected components
        * Maze/Island problems

---

## 💡 Interview Tips

* Always track visited nodes to avoid infinite loops
* In DFS, recursion stack is equivalent to a manual stack
* For disconnected graphs, use a loop to check all components:

  ```java
  for (int i = 0; i < V; i++) {
      if (!visited[i]) dfs(i, adjList, visited);
  }
  ```

---

## 🚀 Bonus Concepts

* BFS can be used for:

    * Shortest path in unweighted graphs
    * Level-order traversal in trees
* DFS can be used for:

    * Topological sort
    * Detecting cycles in directed/undirected graphs
    * Solving puzzles (Sudoku, maze)

---

Would you like:

* A visual dry run of BFS/DFS?
* A version using adjacency matrix?
* DFS using stack (iterative)?

Let me know what you're practicing for — I can tailor graph problems accordingly (like for Amazon, Google, etc.).

---

## 92. Detect cycle in directed/undirected graph.

Great! Detecting a cycle in a graph is a very common and important interview question — it tests your understanding of graph traversal, DFS/BFS, and disjoint sets. Let's walk through both:

---

## 🔄 Cycle Detection in Graphs

### There are two types of graphs:

* ✅ Undirected Graph
* ✅ Directed Graph

And each requires a different approach to detect cycles.

---

## 📌 I. Detect Cycle in an Undirected Graph

### 🔧 Method: DFS with Parent Tracking

We use DFS and mark nodes as visited. If we find a visited node that is not the parent of the current node, a cycle exists.

### 🔁 Key Concept:

If during DFS, you visit a node that is already visited and is not the parent → cycle detected.

---

### ✅ Java Implementation (Undirected Graph):

```java
import java.util.*;

public class CycleUndirectedGraph {

    public static boolean hasCycle(int V, List<List<Integer>> adjList) {
        boolean[] visited = new boolean[V];

        for (int i = 0; i < V; i++) {
            if (!visited[i]) {
                if (dfs(i, -1, visited, adjList)) return true;
            }
        }

        return false;
    }

    private static boolean dfs(int current, int parent, boolean[] visited, List<List<Integer>> adjList) {
        visited[current] = true;

        for (int neighbor : adjList.get(current)) {
            if (!visited[neighbor]) {
                if (dfs(neighbor, current, visited, adjList)) return true;
            } else if (neighbor != parent) {
                return true; // Found a cycle
            }
        }

        return false;
    }

    public static void main(String[] args) {
        int V = 5;
        List<List<Integer>> adjList = new ArrayList<>();

        for (int i = 0; i < V; i++) adjList.add(new ArrayList<>());

        // Create a cycle: 0-1-2-0
        adjList.get(0).add(1); adjList.get(1).add(0);
        adjList.get(1).add(2); adjList.get(2).add(1);
        adjList.get(2).add(0); adjList.get(0).add(2);

        System.out.println("Cycle present: " + hasCycle(V, adjList));  // Output: true
    }
}
```

---

## 📌 II. Detect Cycle in a Directed Graph

### 🔧 Method 1: DFS with Recursion Stack

We use:

* `visited[]`: to mark visited nodes
* `recStack[]`: to track the recursion stack (path being explored)

### 🔁 Key Concept:

If during DFS, you reach a node that's already in the recursion stack → a cycle exists.

---

### ✅ Java Implementation (Directed Graph):

```java
import java.util.*;

public class CycleDirectedGraph {

    public static boolean hasCycle(int V, List<List<Integer>> adjList) {
        boolean[] visited = new boolean[V];
        boolean[] recStack = new boolean[V];

        for (int i = 0; i < V; i++) {
            if (!visited[i]) {
                if (dfs(i, visited, recStack, adjList)) return true;
            }
        }

        return false;
    }

    private static boolean dfs(int node, boolean[] visited, boolean[] recStack, List<List<Integer>> adjList) {
        visited[node] = true;
        recStack[node] = true;

        for (int neighbor : adjList.get(node)) {
            if (!visited[neighbor]) {
                if (dfs(neighbor, visited, recStack, adjList)) return true;
            } else if (recStack[neighbor]) {
                return true; // Back edge found → cycle
            }
        }

        recStack[node] = false; // backtrack
        return false;
    }

    public static void main(String[] args) {
        int V = 4;
        List<List<Integer>> adjList = new ArrayList<>();
        for (int i = 0; i < V; i++) adjList.add(new ArrayList<>());

        // Directed Cycle: 0 → 1 → 2 → 0
        adjList.get(0).add(1);
        adjList.get(1).add(2);
        adjList.get(2).add(0);

        System.out.println("Cycle present: " + hasCycle(V, adjList));  // Output: true
    }
}
```

---

### 🔧 Method 2: Kahn’s Algorithm (Topological Sort)

You can also detect cycles in a directed graph using Kahn’s Algorithm:

* If all nodes are processed → no cycle
* If some nodes remain (in-degree > 0) → cycle exists

Time Complexity: O(V + E)

Ask me if you'd like to see this version.

---

## ✅ Time & Space Complexity

| Graph Type | Method            | Time     | Space |
| ---------- | ----------------- | -------- | ----- |
| Undirected | DFS (with parent) | O(V + E) | O(V)  |
| Directed   | DFS + Rec Stack   | O(V + E) | O(V)  |
| Directed   | Kahn’s Algorithm  | O(V + E) | O(V)  |

---

## 🧠 Interview Tips

* In an undirected graph, revisit is okay if it's the parent.
* In a directed graph, revisiting a node in the current DFS path (recStack) → cycle.
* Know both approaches for directed graphs: DFS & Kahn’s.

---

Would you like to practice with:

* Cycle detection in disconnected graphs?
* Graphs represented with edge lists or matrices?
* Kahn’s Algorithm (Topological Sort)?

Let me know what style of questions you want to prepare next (e.g., LeetCode-style, company-specific, etc.).

---

## 93. Topological sort (Kahn’s algorithm).

Absolutely! **Topological Sort** is a fundamental algorithm for ordering vertices of a **Directed Acyclic Graph (DAG)** such that for every directed edge `u -> v`, `u` comes before `v` in the ordering.

---

## ✅ What is Kahn’s Algorithm?

Kahn’s algorithm is a **BFS-based approach** to perform topological sorting using **in-degree** of nodes.

---

## 🔍 Key Idea

* Calculate **in-degree** (number of incoming edges) for all vertices.
* Initialize a queue and enqueue all vertices with **in-degree = 0** (no dependencies).
* While the queue is not empty:

    * Dequeue a vertex `u` and add it to the topological order.
    * For each neighbor `v` of `u`:

        * Decrease in-degree of `v` by 1.
        * If in-degree of `v` becomes 0, enqueue `v`.
* If all vertices are processed, the graph is a DAG and topological order is found.
* If some vertices remain unprocessed, it means the graph has a cycle.

---

## 🧑‍💻 Java Implementation of Kahn’s Algorithm

```java
import java.util.*;

public class TopologicalSortKahn {

    public static List<Integer> kahnTopologicalSort(int V, List<List<Integer>> adjList) {
        int[] inDegree = new int[V];
        // Compute in-degree for each vertex
        for (int i = 0; i < V; i++) {
            for (int neighbor : adjList.get(i)) {
                inDegree[neighbor]++;
            }
        }

        Queue<Integer> queue = new LinkedList<>();
        // Add all vertices with in-degree 0 to the queue
        for (int i = 0; i < V; i++) {
            if (inDegree[i] == 0) {
                queue.add(i);
            }
        }

        List<Integer> topoOrder = new ArrayList<>();
        int count = 0;  // Count of visited vertices

        while (!queue.isEmpty()) {
            int u = queue.poll();
            topoOrder.add(u);
            count++;

            // Reduce in-degree of all neighbors
            for (int neighbor : adjList.get(u)) {
                inDegree[neighbor]--;
                if (inDegree[neighbor] == 0) {
                    queue.add(neighbor);
                }
            }
        }

        // Check if there was a cycle
        if (count != V) {
            System.out.println("Graph has a cycle. Topological sort not possible.");
            return new ArrayList<>();
        }

        return topoOrder;
    }

    public static void main(String[] args) {
        int V = 6;
        List<List<Integer>> adjList = new ArrayList<>();
        for (int i = 0; i < V; i++) {
            adjList.add(new ArrayList<>());
        }

        // Construct the graph (Directed edges)
        adjList.get(5).add(2);
        adjList.get(5).add(0);
        adjList.get(4).add(0);
        adjList.get(4).add(1);
        adjList.get(2).add(3);
        adjList.get(3).add(1);

        List<Integer> topoOrder = kahnTopologicalSort(V, adjList);

        System.out.println("Topological Order: " + topoOrder);
    }
}
```

---

## 🔄 Sample Output:

```
Topological Order: [4, 5, 0, 2, 3, 1]
```

(Note: There may be multiple valid topological orders.)

---

## 📝 Explanation

* Initially, nodes 4 and 5 have in-degree 0, so they're enqueued first.
* Processing these reduces in-degree of their neighbors.
* When neighbor's in-degree drops to zero, they get enqueued.
* Repeat until all nodes are processed.
* If nodes remain unprocessed (cycle), report accordingly.

---

## ⏱ Time Complexity

* Calculating in-degree: O(V + E)
* Processing all vertices and edges: O(V + E)

Total: **O(V + E)**

---

## 📚 When to Use Topological Sort?

* Task scheduling with dependencies
* Course prerequisite problems
* Build systems (compiling files in order)
* Detecting cycles in directed graphs

---

## ❓ Follow-up Interview Questions

* How to detect cycle using Kahn’s algorithm?
* Can topological sort be performed on undirected graphs? (No)
* How does DFS-based topological sort work?
* What if multiple valid topological orders exist?

---

Would you like me to explain:

* Topological sort using **DFS**?
* How to use topological sort in real problems like course scheduling?
* Visual step-by-step example of Kahn’s algorithm?

Feel free to ask!

---

## 94. Dijkstra’s shortest path.

Absolutely! Let's go over **Dijkstra’s Algorithm** — a classic algorithm to find the shortest path from a **single source** to all other vertices in a **weighted graph with non-negative edge weights**.

---

## ✅ Problem Statement

Given a graph with weighted edges (weights ≥ 0) and a source vertex, find the shortest path distance from the source to every other vertex.

---

## 🔍 Key Idea

* Initialize distances to all vertices as infinity, except the source (0).
* Use a **priority queue (min-heap)** to greedily pick the vertex with the smallest current distance.
* Relax the edges of the picked vertex:

    * If the current path offers a shorter distance, update the distance.
* Repeat until all vertices are processed.

---

## 🧑‍💻 Java Implementation of Dijkstra’s Algorithm

```java
import java.util.*;

public class Dijkstra {

    // Helper class to store node and distance
    static class Pair implements Comparable<Pair> {
        int node, dist;
        public Pair(int node, int dist) {
            this.node = node;
            this.dist = dist;
        }
        public int compareTo(Pair other) {
            return this.dist - other.dist;
        }
    }

    public static int[] dijkstra(int V, List<List<Pair>> adjList, int src) {
        int[] dist = new int[V];
        Arrays.fill(dist, Integer.MAX_VALUE);
        dist[src] = 0;

        PriorityQueue<Pair> pq = new PriorityQueue<>();
        pq.add(new Pair(src, 0));

        while (!pq.isEmpty()) {
            Pair current = pq.poll();
            int u = current.node;

            // If current distance is already greater, skip
            if (current.dist > dist[u]) continue;

            for (Pair neighbor : adjList.get(u)) {
                int v = neighbor.node;
                int weight = neighbor.dist;

                if (dist[u] + weight < dist[v]) {
                    dist[v] = dist[u] + weight;
                    pq.add(new Pair(v, dist[v]));
                }
            }
        }
        return dist;
    }

    public static void main(String[] args) {
        int V = 5;
        List<List<Pair>> adjList = new ArrayList<>();

        for (int i = 0; i < V; i++) {
            adjList.add(new ArrayList<>());
        }

        // Add edges (u, v, w)
        adjList.get(0).add(new Pair(1, 9));
        adjList.get(0).add(new Pair(2, 6));
        adjList.get(0).add(new Pair(3, 5));
        adjList.get(0).add(new Pair(4, 3));
        adjList.get(2).add(new Pair(1, 2));
        adjList.get(2).add(new Pair(3, 4));

        int src = 0;
        int[] distances = dijkstra(V, adjList, src);

        System.out.println("Shortest distances from node " + src + ":");
        for (int i = 0; i < V; i++) {
            System.out.println("To node " + i + " = " + distances[i]);
        }
    }
}
```

---

## 🔄 Sample Output:

```
Shortest distances from node 0:
To node 0 = 0
To node 1 = 8
To node 2 = 6
To node 3 = 5
To node 4 = 3
```

---

## 🔧 Explanation:

* Start at node 0 with distance 0.
* Explore neighbors: update their distances.
* Use a min-heap to always pick the closest unvisited node.
* Update distances if shorter paths are found.

---

## ⏱ Time Complexity

* Using adjacency list and priority queue: O((V + E) log V)
* V = vertices, E = edges

---

## ⚠️ Important Notes

* Dijkstra’s algorithm **does not work with negative weight edges**.
* For graphs with negative weights, use **Bellman-Ford** algorithm.

---

## ❓ Interview Tips

* Understand why a min-heap (priority queue) is used.
* Know how to handle disconnected graphs.
* Be ready to explain modifications for shortest path reconstruction.
* Explain how adjacency list is better than adjacency matrix for sparse graphs.

---

Would you like me to help you with:

* Shortest path reconstruction (getting the actual path)?
* Bellman-Ford algorithm for graphs with negative weights?
* Practice problems using Dijkstra?

Just let me know!

---

## 95. Union Find (Disjoint Set).

Absolutely! Let's break down **Union-Find (Disjoint Set Union - DSU)** — a powerful data structure used to efficiently manage a collection of disjoint sets, supporting two main operations:

---

## 🔍 What is Union-Find?

Union-Find is used to:

* **Find** which set a particular element belongs to.
* **Union** two sets into one.

It's commonly used in:

* Detecting cycles in undirected graphs
* Kruskal’s algorithm for Minimum Spanning Tree (MST)
* Network connectivity
* Clustering problems

---

## Core Operations:

1. **Find(x):** Returns the representative (or parent) of the set containing element `x`.
2. **Union(x, y):** Merges the sets containing elements `x` and `y`.

---

## Optimization Techniques:

* **Path Compression (Find):** During `find`, compress the path to point directly to the root, flattening the structure.
* **Union by Rank/Size:** Always attach the smaller tree under the root of the larger tree to keep the tree shallow.

---

## 🧑‍💻 Java Implementation of Union-Find

```java
public class UnionFind {
    private int[] parent;
    private int[] size;  // or rank

    public UnionFind(int n) {
        parent = new int[n];
        size = new int[n];
        for (int i = 0; i < n; i++) {
            parent[i] = i; // each node is its own parent initially
            size[i] = 1;   // initial size of each set is 1
        }
    }

    // Find with path compression
    public int find(int x) {
        if (parent[x] != x) {
            parent[x] = find(parent[x]); // path compression
        }
        return parent[x];
    }

    // Union by size
    public boolean union(int x, int y) {
        int rootX = find(x);
        int rootY = find(y);

        if (rootX == rootY) {
            return false; // already in the same set
        }

        // Attach smaller tree under larger tree
        if (size[rootX] < size[rootY]) {
            parent[rootX] = rootY;
            size[rootY] += size[rootX];
        } else {
            parent[rootY] = rootX;
            size[rootX] += size[rootY];
        }

        return true;
    }

    // Check if two nodes are in the same set
    public boolean connected(int x, int y) {
        return find(x) == find(y);
    }

    // Optional: get size of the set containing x
    public int getSize(int x) {
        int root = find(x);
        return size[root];
    }
}
```

---

## Example Usage:

```java
public class Main {
    public static void main(String[] args) {
        UnionFind uf = new UnionFind(5);

        uf.union(0, 1);
        uf.union(1, 2);

        System.out.println(uf.connected(0, 2)); // true
        System.out.println(uf.connected(0, 3)); // false

        uf.union(3, 4);

        System.out.println(uf.connected(3, 4)); // true

        uf.union(2, 4);

        System.out.println(uf.connected(0, 4)); // true
    }
}
```

---

## ⏱ Time Complexity:

* Nearly **O(1)** (amortized) per `find` and `union` operation with path compression and union by size/rank.
* More precisely, it's inverse Ackermann function, practically constant.

---

## 🧠 Interview Tips:

* Be ready to explain **path compression** and **union by rank/size**.
* Use Union-Find to detect cycles in undirected graphs (if union fails, cycle exists).
* Practice implementing from scratch quickly.
* Understand use cases like connected components, Kruskal’s MST, etc.

---

Would you like me to:

* Show cycle detection in undirected graphs using Union-Find?
* Explain Kruskal’s algorithm using Union-Find?
* Provide some practice problems on Union-Find?

Let me know!

---

### 🔹 **96–100: Miscellaneous / Advanced**

## 96. Sliding window maximum / minimum.

Sure! Let’s dive into the **Sliding Window Maximum/Minimum** problem, a classic and common interview question involving arrays and efficient data structures.

---

## 🧩 Problem Statement

Given an array `nums` and a sliding window size `k`, find the **maximum** (or minimum) element in every contiguous subarray (window) of size `k`.

---

### Example:

```
Input: nums = [1,3,-1,-3,5,3,6,7], k = 3
Output: [3,3,5,5,6,7]  // maximums for each window
```

---

## Naive Approach (O(n\*k))

* For each window, scan all `k` elements and find max/min.
* Inefficient for large arrays.

---

## Efficient Approach: **Using Deque (Double-ended queue)**

* Use a deque to store indices of useful elements.
* The deque will keep elements in decreasing order for maximum (or increasing for minimum).
* For each element:

    * Remove elements not in the current window.
    * Remove elements from the deque which are smaller (for max) or larger (for min) than current element.
* The front of the deque is the max/min for the current window.

---

## 🧑‍💻 Java Code: Sliding Window Maximum using Deque

```java
import java.util.*;

public class SlidingWindowMaximum {
    public static int[] maxSlidingWindow(int[] nums, int k) {
        if (nums == null || k <= 0) return new int[0];
        int n = nums.length;
        int[] result = new int[n - k + 1];
        Deque<Integer> deque = new LinkedList<>(); // stores indices

        for (int i = 0; i < n; i++) {
            // Remove indices out of this window
            while (!deque.isEmpty() && deque.peekFirst() < i - k + 1) {
                deque.pollFirst();
            }

            // Remove elements smaller than current from the back
            while (!deque.isEmpty() && nums[deque.peekLast()] < nums[i]) {
                deque.pollLast();
            }

            // Add current element index
            deque.offerLast(i);

            // Add max to result once we have first full window
            if (i >= k - 1) {
                result[i - k + 1] = nums[deque.peekFirst()];
            }
        }

        return result;
    }

    public static void main(String[] args) {
        int[] nums = {1,3,-1,-3,5,3,6,7};
        int k = 3;
        int[] maxValues = maxSlidingWindow(nums, k);
        System.out.println(Arrays.toString(maxValues));
    }
}
```

---

## Output:

```
[3, 3, 5, 5, 6, 7]
```

---

## How it Works:

* The deque always stores indices of elements in descending order (largest at front).
* When the window slides:

    * Remove indices outside the current window from the front.
    * Remove smaller elements from the back as they can't be max anymore.
* Front of deque is the index of max element for current window.

---

## Sliding Window Minimum

* Same approach, but:

    * Remove elements **greater** than current (instead of smaller).
    * Front of deque is the minimum element.

---

## ⏱ Time Complexity:

* Each element is pushed and popped at most once → O(n)
* Efficient compared to naive O(n\*k).

---

## 🧠 Interview Tips:

* Understand why deque is the right data structure here.
* Be comfortable implementing both max and min versions.
* Variations: sum of max/min, median in sliding window (requires more complex structures).
* Practice explaining the approach with a dry run on sample input.

---

Would you like me to help with:

* Sliding window median problem?
* Variations like fixed-size window sums or other aggregates?
* More example problems on deque?

Just ask!

---

## 97. Trapping rainwater.

Sure! Let’s talk about the **Trapping Rain Water** problem — a classic and popular interview question that tests your understanding of arrays and two-pointer technique.

---

## 🧩 Problem Statement

Given `n` non-negative integers representing the elevation map where the width of each bar is 1, compute how much water it can trap after raining.

---

### Example:

```
Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
```

The bars can trap 6 units of water between them.

---

## Intuition

Water trapped on top of a bar depends on the tallest bars on its left and right.
For each bar:

* Water trapped = `min(maxLeft, maxRight) - height[i]` (if positive)

---

## Approaches

### 1. **Brute Force** (O(n²))

For each bar:

* Find max height to the left and right.
* Calculate trapped water.

---

### 2. **Dynamic Programming** (O(n) time, O(n) space)

Precompute arrays:

* `leftMax[i]` = max height from left up to `i`
* `rightMax[i]` = max height from right up to `i`

Then, trapped water at `i` = `min(leftMax[i], rightMax[i]) - height[i]`.

---

### 3. **Two Pointer Approach** (O(n) time, O(1) space) — Most Optimal!

* Use two pointers `left` and `right` at start and end of the array.
* Keep track of `leftMax` and `rightMax`.
* Move pointers inward, calculating trapped water based on comparisons.

---

## 🧑‍💻 Two Pointer Java Implementation

```java
public class TrappingRainWater {
    public static int trap(int[] height) {
        int left = 0, right = height.length - 1;
        int leftMax = 0, rightMax = 0;
        int trappedWater = 0;

        while (left < right) {
            if (height[left] < height[right]) {
                if (height[left] >= leftMax) {
                    leftMax = height[left];
                } else {
                    trappedWater += leftMax - height[left];
                }
                left++;
            } else {
                if (height[right] >= rightMax) {
                    rightMax = height[right];
                } else {
                    trappedWater += rightMax - height[right];
                }
                right--;
            }
        }

        return trappedWater;
    }

    public static void main(String[] args) {
        int[] height = {0,1,0,2,1,0,1,3,2,1,2,1};
        System.out.println("Trapped water: " + trap(height)); // Output: 6
    }
}
```

---

## Explanation:

* Move from both ends towards center.
* Compare heights at `left` and `right`.
* Update `leftMax` and `rightMax` accordingly.
* Water trapped at `left` or `right` depends on min of max heights seen so far.
* Sum all trapped water.

---

## ⏱ Time and Space Complexity:

* Time: **O(n)** — one pass with two pointers.
* Space: **O(1)** — no extra arrays.

---

## Interview Tips:

* Explain brute force first, then optimize.
* Emphasize the logic behind two pointers.
* Be ready to dry run on sample input.
* Variants: trapping water between 2D bars, dynamic elevation changes, etc.

---

Want me to walk you through:

* The DP approach with precomputed arrays?
* Visual step-by-step of two pointer method?
* Related problems or practice questions?

Just let me know!

---

## 98. Largest rectangle of 1s in a matrix.

Great choice! The **Largest Rectangle of 1s in a Binary Matrix** is a classic 2D extension problem that combines knowledge of arrays, stacks, and histograms. It’s a common interview problem.

---

## 🧩 Problem Statement

Given a 2D binary matrix filled with 0s and 1s, find the largest rectangle containing only 1s and return its area.

---

### Example:

```
Input:
matrix = [
  ['1','0','1','0','0'],
  ['1','0','1','1','1'],
  ['1','1','1','1','1'],
  ['1','0','0','1','0']
]

Output: 6
```

The largest rectangle of 1s has area 6.

---

## Key Insight

* This problem reduces to solving **Largest Rectangle in Histogram** for each row.
* Treat each row as the base of a histogram where:

    * Height of each column = count of consecutive 1s **above and including** current row.

---

## Approach

1. Initialize an array `heights` of size equal to number of columns.
2. For each row:

    * Update `heights[j]`:

        * If `matrix[i][j] == '1'`, increment `heights[j]` by 1.
        * Else reset `heights[j] = 0`.
3. For each updated `heights` array, calculate the largest rectangle area in histogram.
4. Track the maximum area found.

---

## Largest Rectangle in Histogram (Brief)

* Use a stack to keep indices of bars.
* For each bar, pop bars from stack while the current bar height is less than height of top of stack.
* Calculate area for popped bars.
* The max area computed is the largest rectangle in histogram.

---

## 🧑‍💻 Java Implementation

```java
import java.util.*;

public class LargestRectangleOfOnes {

    // Calculate largest rectangle in histogram
    public static int largestRectangleArea(int[] heights) {
        Stack<Integer> stack = new Stack<>();
        int maxArea = 0;
        int n = heights.length;

        for (int i = 0; i <= n; i++) {
            int currHeight = (i == n) ? 0 : heights[i];
            while (!stack.isEmpty() && currHeight < heights[stack.peek()]) {
                int height = heights[stack.pop()];
                int width = stack.isEmpty() ? i : i - stack.peek() - 1;
                maxArea = Math.max(maxArea, height * width);
            }
            stack.push(i);
        }
        return maxArea;
    }

    // Main function to find largest rectangle of 1s
    public static int maximalRectangle(char[][] matrix) {
        if (matrix.length == 0) return 0;
        int maxArea = 0;
        int cols = matrix[0].length;
        int[] heights = new int[cols];

        for (char[] row : matrix) {
            for (int j = 0; j < cols; j++) {
                if (row[j] == '1') {
                    heights[j] += 1;
                } else {
                    heights[j] = 0;
                }
            }
            maxArea = Math.max(maxArea, largestRectangleArea(heights));
        }

        return maxArea;
    }

    public static void main(String[] args) {
        char[][] matrix = {
            {'1','0','1','0','0'},
            {'1','0','1','1','1'},
            {'1','1','1','1','1'},
            {'1','0','0','1','0'}
        };
        System.out.println("Largest rectangle area of 1s: " + maximalRectangle(matrix));
    }
}
```

---

## Output:

```
Largest rectangle area of 1s: 6
```

---

## Explanation:

* For each row, we update `heights[]` as histogram heights.
* Use stack-based largest rectangle in histogram algorithm on these heights.
* Track the maximum area found.

---

## ⏱ Time Complexity:

* O(rows \* cols) to update heights and compute max rectangle per row.
* Largest rectangle in histogram runs in O(cols).
* Overall complexity: **O(rows \* cols)**.

---

## 🧠 Interview Tips:

* Clearly explain the histogram transformation step.
* Know the stack approach for largest rectangle in histogram.
* Dry run the code on small examples.
* Mention space optimization possibilities if asked.

---

Would you like me to explain:

* The **Largest Rectangle in Histogram** problem in detail?
* Visual step-by-step with example matrix?
* Related problems like maximal square or counting submatrices of all 1s?

Just ask!

---

## 99. Trie implementation (insert/search).

Certainly! Let’s dive into **Trie** (also called Prefix Tree) — a powerful tree-based data structure used for storing strings efficiently, especially useful for prefix-based queries.

---

## 🧩 What is a Trie?

* A **Trie** stores a dynamic set of strings where each node represents a character.
* Common prefixes share nodes, which saves space.
* Supports fast insert, search, and prefix queries (like autocomplete).

---

## Main Operations:

1. **Insert** a word into the trie.
2. **Search** if a word exists in the trie.
3. (Optional) **StartsWith** to check if any word starts with a given prefix.

---

## Trie Node Structure

Each node usually contains:

* An array or map of child nodes (for each character).
* A boolean flag `isEndOfWord` to mark if a node represents the end of a word.

---

## 🧑‍💻 Java Implementation of Trie (Insert and Search)

```java
class TrieNode {
    TrieNode[] children = new TrieNode[26];
    boolean isEndOfWord;

    public TrieNode() {
        isEndOfWord = false;
        for (int i = 0; i < 26; i++) {
            children[i] = null;
        }
    }
}

public class Trie {
    private TrieNode root;

    public Trie() {
        root = new TrieNode();
    }

    // Insert word into Trie
    public void insert(String word) {
        TrieNode node = root;
        for (char c : word.toCharArray()) {
            int index = c - 'a'; // assuming lowercase a-z
            if (node.children[index] == null) {
                node.children[index] = new TrieNode();
            }
            node = node.children[index];
        }
        node.isEndOfWord = true;
    }

    // Search word in Trie
    public boolean search(String word) {
        TrieNode node = root;
        for (char c : word.toCharArray()) {
            int index = c - 'a';
            if (node.children[index] == null) return false;
            node = node.children[index];
        }
        return node.isEndOfWord;
    }

    // Optional: Check if prefix exists in Trie
    public boolean startsWith(String prefix) {
        TrieNode node = root;
        for (char c : prefix.toCharArray()) {
            int index = c - 'a';
            if (node.children[index] == null) return false;
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

## Explanation:

* **Insert:** Traverse the trie creating nodes as needed for each character.
* **Search:** Traverse nodes; if missing node or not end of word, return false.
* **startsWith:** Similar to search but doesn’t require end of word.

---

## Time Complexity:

* Insert, Search, StartsWith → O(m) where m is length of the word/prefix.

---

## Interview Tips:

* Explain use-cases like autocomplete, spell checker, IP routing.
* Discuss space-time trade-offs with tries (e.g., 26 children for alphabets).
* Be prepared to extend for uppercase, digits, or Unicode (using HashMap instead of array).
* Practice coding from scratch without looking.

---

Want me to help with:

* Trie deletion operation?
* Compressed Trie / Radix Trie explanation?
* Solving prefix/suffix related problems with Trie?

Just let me know!

---

## 100. Bit manipulation tricks (check odd/even, swap bits, count set bits).

Absolutely! Bit manipulation is a fundamental topic in Java DSA interviews, and mastering these tricks can give you a great advantage. Let me explain some common bit manipulation tricks with explanations and Java code examples.

---

## 1️⃣ Check if a Number is Odd or Even

**Key Idea:**

* The least significant bit (LSB) of an odd number is always `1`.
* The LSB of an even number is always `0`.

### Code:

```java
public static boolean isOdd(int num) {
    return (num & 1) == 1;  // if last bit is 1, number is odd
}

public static boolean isEven(int num) {
    return (num & 1) == 0;  // if last bit is 0, number is even
}
```

---

## 2️⃣ Swap Two Numbers Without a Temporary Variable

**Using XOR swap algorithm:**

```
a = a ^ b
b = a ^ b  // now b is original a
a = a ^ b  // now a is original b
```

### Code:

```java
public static void swapNumbers(int[] arr) {
    // arr[0] = a, arr[1] = b
    arr[0] = arr[0] ^ arr[1];
    arr[1] = arr[0] ^ arr[1];
    arr[0] = arr[0] ^ arr[1];
}
```

---

## 3️⃣ Count Set Bits (Number of 1s in Binary Representation)

### Method 1: Brian Kernighan’s Algorithm (Efficient)

* Repeatedly flip the least significant set bit until number becomes zero.

```java
public static int countSetBits(int num) {
    int count = 0;
    while (num != 0) {
        num = num & (num - 1); // remove the last set bit
        count++;
    }
    return count;
}
```

### Method 2: Built-in Java function

```java
int count = Integer.bitCount(num);
```

---

## 4️⃣ Other Useful Bit Tricks

### a) Set a bit at position `pos` (0-indexed from right)

```java
int setBit(int num, int pos) {
    return num | (1 << pos);
}
```

### b) Clear a bit at position `pos`

```java
int clearBit(int num, int pos) {
    return num & ~(1 << pos);
}
```

### c) Toggle a bit at position `pos`

```java
int toggleBit(int num, int pos) {
    return num ^ (1 << pos);
}
```

### d) Check if bit at position `pos` is set

```java
boolean isBitSet(int num, int pos) {
    return (num & (1 << pos)) != 0;
}
```

---

## 5️⃣ Additional Examples

### Find if a number is a power of two:

```java
boolean isPowerOfTwo(int num) {
    return num > 0 && (num & (num - 1)) == 0;
}
```

### Get the rightmost set bit:

```java
int rightmostSetBit(int num) {
    return num & (-num);
}
```

---

## Summary Table

| Operation          | Expression                        | Explanation                       |              |
| ------------------ | --------------------------------- | --------------------------------- | ------------ |
| Check odd          | `(num & 1) == 1`                  | Check LSB                         |              |
| Check even         | `(num & 1) == 0`                  | Check LSB                         |              |
| Swap two numbers   | `a ^= b; b ^= a; a ^= b;`         | XOR swap                          |              |
| Count set bits     | `while (num != 0) num &= (num-1)` | Removes one set bit per iteration |              |
| Set bit at pos     | \`num                             | (1 << pos)\`                      | Set bit to 1 |
| Clear bit at pos   | `num & ~(1 << pos)`               | Set bit to 0                      |              |
| Toggle bit at pos  | `num ^ (1 << pos)`                | Flip bit                          |              |
| Check bit at pos   | `(num & (1 << pos)) != 0`         | Is bit set?                       |              |
| Power of two check | `num > 0 && (num & (num-1)) == 0` | Only one set bit                  |              |
| Rightmost set bit  | `num & (-num)`                    | Extract rightmost set bit         |              |

---

## Ready for some quick practice or example problems involving bit manipulation?

Or do you want me to explain any trick with visual examples or binary representation? Just ask!

---

## 📘 Bonus Resources (Optional)

Would you like me to prepare any of these for you?

- ✅ **PDF version** of this list
- ✅ **Topic-wise solutions with code (Java)**
- ✅ **DSA Cheat Sheet** (formulas, time complexities)
- ✅ **DSA roadmap for interviews (with schedule)**
- ✅ **GitHub repo format / Notion doc**

Let me know and I’ll help you get everything set up!