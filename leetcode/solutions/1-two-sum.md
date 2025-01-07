## Problem Description

Given an array of integers `nums` and an integer `target`, return _indices of the two numbers such that they add up to `target`_.

You may assume that each input would have **_exactly_ one solution**, and you may not use the _same_ element twice.

You can return the answer in any order.

**Example 1:**

**Input:** nums = [2,7,11,15], target = 9
**Output:** [0,1]
**Explanation:** Because nums[0] + nums[1] == 9, we return [0, 1].

**Example 2:**

**Input:** nums = [3,2,4], target = 6
**Output:** [1,2]

**Example 3:**

**Input:** nums = [3,3], target = 6
**Output:** [0,1]

**Constraints:**

- `2 <= nums.length <= 104`
- `-109 <= nums[i] <= 109`
- `-109 <= target <= 109`
- **Only one valid answer exists.**

**Follow-up:** Can you come up with an algorithm that is less than $O(n^2)$ time complexity?

<br>

---

<br>

## Code Solution

```python
from typing import List

class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        seen = {}
        for index, value in enumerate(nums):
            complement = target - value
            if complement in seen:
                return [seen[complement], index]
            seen[value] = index
        return []
```

<br>

---

<br>

## Line-by-Line Explanation

### 1. Function Definition

```python
def twoSum(self, nums: List[int], target: int) -> List[int]:
```

- **Purpose:** Defines the function `twoSum` which takes:
  - `nums`: A list of integers.
  - `target`: An integer representing the target sum.
- **Return Type:** Returns a list containing two integers representing indices of the numbers.

<br>

---

<br>

### 2. Initialize `seen` Dictionary

```python
seen = {}
```

- **Purpose:** `seen` is a dictionary to store numbers encountered so far as keys, and their indices as values.
- **Why?** This enables efficient lookup for the complement of the current number in `O(1)` time.

<br>

---

<br>

### 3. Loop Through `nums`

```python
for index, value in enumerate(nums):
```

- **Purpose:** Iterates through the `nums` array with:
  - `index`: The current index in the array.
  - `value`: The value of the element at the current index.
- **Why?** Allows us to examine each number and calculate its complement relative to the target.

<br>

---

<br>

### 4. Calculate Complement

```python
complement = target - value
```

- **Purpose:** Calculates the `complement`, which is the value needed to reach the `target` when added to `value`.
- **Why?** To determine if this complement already exists in the dictionary `seen`.

<br>

---

<br>

### 5. Check for Complement

```python
if complement in seen:
    return [seen[complement], index]
```

- **Purpose:** Checks if the `complement` is already stored in `seen`.
- **If True:** Returns the indices:
  - `seen[complement]`: The index of the complement stored in the dictionary.
  - `index`: The current index of the number in the loop.
- **Why?** This ensures we find the indices of the two numbers that add up to `target`.

<br>

---

<br>

### 6. Add Current Value to `seen`

```python
seen[value] = index
```

- **Purpose:** Adds the current `value` as a key in `seen`, with its corresponding `index` as the value.
- **Why?** Updates the dictionary with the latest number and its index for future lookups.

<br>

---

<br>

### 7. Return (Not Used in This Case)

```python
return []
```

- **Purpose:** A safeguard to return an empty list if no solution is found (though guaranteed by the problem constraints).

<br>

---

<br>

## Complexity Analysis

### Time Complexity: **O(n)**

- **Why?**
  - The function iterates through the `nums` list exactly once (`O(n)`).
  - Lookup and insertion into the dictionary are both `O(1)` operations.
- **Total:** `O(n)` for the loop.

### Space Complexity: **O(n)**

- **Why?**
  - The `seen` dictionary can store up to `n` elements in the worst case, where `n` is the length of `nums`.
- **Total:** `O(n)` for the dictionary.

<br>

---

<br>

## Example Walkthrough

### Input: `nums = [2, 7, 11, 15], target = 9`

1. **Initialization:**

   - `seen = {}`

2. **First Iteration (index = 0, value = 2):**

   - `complement = 9 - 2 = 7`
   - `7 not in seen`
   - Update `seen`: `{2: 0}`

3. **Second Iteration (index = 1, value = 7):**

   - `complement = 9 - 7 = 2`
   - `2 in seen` (at index 0)
   - Return `[seen[2], 1] = [0, 1]`

### Output: `[0, 1]`

<br>

---

<br>

## Summary

This solution efficiently finds the indices of two numbers that sum to the target using a single pass through the array and a dictionary for constant-time lookups. It leverages the difference between the target and the current number (the complement) to track and quickly locate pairs.
