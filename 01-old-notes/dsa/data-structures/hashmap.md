# Hashmaps

A **hashmap** is a data structure that stores key-value pairs and provides fast operations like insertion, deletion, and lookup by using a hash function. Hashmaps are widely used in problem-solving due to their efficiency and simplicity.

<br>

---

<br>

### How Hashmaps Work Internally

1. **Core Concept**:

   - Hashmaps use a **hash function** to compute an index (bucket) for a given key.
   - The key-value pair is stored at this computed index, enabling quick lookups.

2. **Hash Function**:

   - A hash function converts a key into a hash code.
   - Example:
     ```python
     hash_code = hash("Mars")
     print(hash_code)
     ```
   - The computed hash code determines the bucket where the key-value pair is stored.

3. **Collision Handling**:

   - **Separate Chaining**: Use a linked list or similar structure to handle multiple keys mapping to the same bucket.
   - **Open Addressing**: Store the colliding keys in different slots found through probing (e.g., linear, quadratic).

<br>

---

<br>

### **Python Implementation of a Hashmap**

```python
# Minimal implementation of a hashmap using Python's dict
planet_data = {}

# Add key-value pairs
planet_data['planet'] = 'Mars'

# Access values
print(planet_data['planet'])

# Delete a key-value pair
del planet_data['planet']
```

<br>

---

<br>

### **Go Implementation of a Hashmap**

```go
package main

import "fmt"

func main() {
    // Minimal implementation of a hashmap using Go's map
    planetData := make(map[string]string)

    // Add key-value pairs
    planetData["planet"] = "Mars"

    // Access values
    fmt.Println(planetData["planet"])

    // Delete a key-value pair
    delete(planetData, "planet")
}
```

<br>

---

<br>

### **Hashmap Operations**

| **Operation**       | **Python Syntax**                 | **Go Syntax**                           | **Time Complexity** | **Space Complexity** |
| ------------------- | --------------------------------- | --------------------------------------- | ------------------- | -------------------- |
| **Create**          | `planet_data = {}`                | `planetData := make(map[string]string)` | O(1)                | O(n)                 |
| **Insert**          | `planet_data['key'] = value`      | `planetData["key"] = value`             | O(1) (average)      | O(n)                 |
| **Access**          | `planet_data['key']`              | `planetData["key"]`                     | O(1) (average)      | O(1)                 |
| **Check Existence** | `'key' in planet_data`            | `value, exists := planetData["key"]`    | O(1) (average)      | O(1)                 |
| **Delete**          | `del planet_data['key']`          | `delete(planetData, "key")`             | O(1) (average)      | O(n) (adjust bucket) |
| **Iterate**         | `for k, v in planet_data.items()` | `for k, v := range planetData`          | O(n)                | O(1)                 |

<br>

---

<br>

### **Advantages and Disadvantages**

#### **Advantages**:

- **Fast Operations**: Average O(1) time complexity for insertions, deletions, and lookups.
- **Dynamic Sizing**: Automatically adjusts size as elements are added.
- **Flexible Keys**:
  - Python: Immutable types (e.g., strings, tuples, numbers).
  - Go: Comparable types (e.g., strings, integers).

#### **Disadvantages**:

- **Memory Overhead**: Requires extra memory for internal structures and hash calculations.
- **Unordered**: Does not preserve insertion order (though Python’s `dict` does since version 3.7).
- **Not Suitable for Range Queries**: Hashmaps cannot efficiently retrieve keys within a range.

<br>

---

<br>

### **Key Details**

#### **Collision Handling**

- Collisions occur when two keys map to the same index in the hashmap.
- **Resolution Methods**:
  - **Separate Chaining**: Use a linked list to store all key-value pairs at the same index.
  - **Open Addressing**: Store the new key-value pair in a different slot.

#### **Resizing**

- Hashmaps resize when the load factor (number of elements/size) exceeds a threshold to maintain efficiency.
- Resizing involves rehashing all keys, which can temporarily increase time complexity.

#### **Memory Usage**

- Hashmaps trade memory for speed, often using more memory than necessary to minimize collisions.

<br>

---

<br>

### **Common Patterns for Hashmap Usage**

1. **Counting Frequencies**:

   - Count the occurrences of words, numbers, or objects efficiently.
     ```python
     from collections import Counter
     sentence = "mars earth mars mars jupiter"
     freq = Counter(sentence.split())
     print(freq)
     ```
     ```go
     package main
     import (
         "fmt"
         "strings"
     )
     func main() {
         sentence := "mars earth mars mars jupiter"
         words := strings.Fields(sentence)
         freq := make(map[string]int)
         for _, word := range words {
             freq[word]++
         }
         fmt.Println(freq)
     }
     ```

2. **Mapping Relationships**:

   - Example: Map planets to their orbital periods or other attributes.

3. **Memoization**:

   - Cache expensive computations to avoid redundant work.

4. **Tracking Seen Elements**:

   - Example: Use a hashmap to check for duplicates or track visited nodes in a graph.

<br>

---

<br>

### **When to Use Hashmaps**

1. **Fast Lookups**: Hashmaps are ideal when you need quick data retrieval based on keys.
2. **Key-Value Mapping**: Useful for representing relationships.
3. **Eliminating Duplicates**: Helps in efficiently removing or counting duplicates in a dataset.

<br>

---

<br>

### **Limitations**

- **Not Ordered**: If ordering matters, use a data structure like a sorted map or `OrderedDict` (Python).
- **Memory Intensive**: Overhead can be high for large datasets.
- **Range Queries**: Inefficient for finding elements in a numerical or lexicographical range.

<br>

---

<br>

### **Conceptual Visualization**

Imagine a hashmap as an array of buckets:

| Index | Keys Stored        | Values Stored |
| ----- | ------------------ | ------------- |
| 0     | `["planet"]`       | `["Mars"]`    |
| 1     | `["num_of_moons"]` | `[2]`         |
| 2     | `["is_habitable"]` | `[False]`     |

To retrieve a value:

1. Compute the hash for the key.
2. Modulo the hash by the size of the hashmap to find the bucket index.
3. Retrieve the value from the bucket.
