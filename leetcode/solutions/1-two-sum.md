## C++ Code Solution

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int> &nums, int target) {
        unordered_map<int, int> m;

        for (int i = 0; i < nums.size(); i++) {
            int complement = target - nums[i];
            if (m.find(complement) != m.end()) {
                return {m[complement], i};
            }
            m[nums[i]] = i;
        }
        return {};
    }
};
```

<br>

---

<br>

## Enhanced Line-by-Line Explanation

### 1. Class Declaration & Function Signature

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int> &nums, int target) {
```

- **Class & Access Modifier:**
    
    - The `Solution` class encapsulates the function, adhering to LeetCode's expected format.
    - `public:` ensures that the `twoSum` method is accessible to external code (like the testing framework).
- **Function Signature:**
    
    - **Parameters:**
        - `vector<int> &nums`: Passed by reference to avoid copying the entire array, which improves efficiency, especially for large inputs.
        - `int target`: The integer sum we are trying to achieve by adding two numbers from `nums`.
    - **Return Type:**  
        A `vector<int>` containing exactly two indices that correspond to the two numbers summing to `target`.

<br>

---

<br>

### 2. Initialize the Hash Table

```cpp
unordered_map<int, int> m;
```

- **Purpose:**  
    Creates an `unordered_map` (a hash table) named `m` where:
    - **Key:** An integer value from `nums`.
    - **Value:** The index of that integer in the array.
- **Why Use a Hash Table?**  
    The hash table allows constant average time (`O(1)`) lookups to quickly check if the complement of the current number exists among the numbers we've already processed.

<br>

---

<br>

### 3. Iterate Through the Array

```cpp
for (int i = 0; i < nums.size(); i++) {
```

- **Loop Explanation:**
    
    - Iterates over the vector `nums` using the index `i`.
    - **Why Use a For-Loop with Indices?**  
        Accessing elements by index is necessary because we need to return the indices of the elements, not the values themselves.
- **Efficiency Note:**  
    This single loop ensures that we traverse the list only once, contributing to an overall time complexity of **O(n)**.
    

<br>

---

<br>

### 4. Calculate the Complement

```cpp
int complement = target - nums[i];
```

- **Purpose:**  
    Computes the **complement** which is the number needed (when added to `nums[i]`) to reach the `target`.
    
- **Detailed Reasoning:**
    
    - If `nums[i]` is one of the two numbers required, then the other number must be `target - nums[i]`.
    - Storing and using this value is crucial to determine if a previously seen number completes the pair.

<br>

---

<br>

### 5. Check if the Complement Exists

```cpp
if (m.find(complement) != m.end()) {
    return {m[complement], i};
}
```

- **Lookup Explanation:**
    - `m.find(complement)` searches the hash table for the `complement`.
    - If the iterator returned is **not equal** to `m.end()`, it indicates that the `complement` exists in the hash table.
- **Return Statement Details:**
    - If the complement is found, the solution is immediately returned as a vector containing two indices:
        - `m[complement]`: The index where the complement was previously stored.
        - `i`: The current index of `nums[i]`.
- **Efficiency Note:**  
    This constant-time lookup is a key reason for the overall linear time complexity.

<br>

---

<br>

### 6. Add the Current Number and its Index to the Hash Table

```cpp
m[nums[i]] = i;
```

- **Purpose:**  
    After checking for a valid pair, the current number (`nums[i]`) and its index (`i`) are added to the hash table.
    
- **Detailed Explanation:**
    
    - **Future Lookup:**  
        This step ensures that for every subsequent number in the array, the current number is available as a potential complement.
    - **Handling Duplicates:**  
        Even if the same number appears more than once, the first valid pair will be found because the complement check happens before insertion. In cases like `[3, 3]` with `target = 6`, the first `3` is stored, and when the second `3` is processed, its complement (which is also `3`) is found in the hash table.

<br>

---

<br>

### 7. Fallback Return Statement

```cpp
return {};
```

- **Purpose:**  
    Provides a return statement that outputs an empty vector.
    
- **Why Include This Line?**
    
    - **Completeness:**  
        Although the problem guarantees exactly one solution, this return statement is necessary to satisfy all code paths and maintain proper function syntax.
    - **Safety:**  
        Acts as a safeguard if, due to some unforeseen circumstance, no valid pair is found.

<br>

---

<br>

## Complexity Analysis

### Time Complexity: **O(n)**

- **Rationale:**
    - The algorithm processes each element in the array exactly once.
    - Both insertion and lookup in the `unordered_map` are average **O(1)** operations.
- **Overall:**  
    The combined operations result in **O(n)** time complexity.

### Space Complexity: **O(n)**

- **Rationale:**
    - In the worst-case scenario, the hash table may store every element of the array.
    - Thus, space usage grows linearly with the input size.

<br>

---

<br>

## Example Walkthrough

**Input:** `nums = [2, 7, 11, 15]`, `target = 9`

1. **Initialization:**
    
    - `unordered_map m` is empty.
2. **Iteration 1 (i = 0):**
    
    - `nums[0] = 2`
    - **Complement Calculation:** `complement = 9 - 2 = 7`
    - **Lookup:** `7` is not in `m`
    - **Insertion:** Add `{2: 0}` to `m`.
3. **Iteration 2 (i = 1):**
    
    - `nums[1] = 7`
    - **Complement Calculation:** `complement = 9 - 7 = 2`
    - **Lookup:** `2` is found in `m` (stored at index `0`)
    - **Return:** Immediately returns `[0, 1]`.