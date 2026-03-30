# Data Types and Structures — Theoretical Questions & Answers

**Name:** Enosh Raju Devisetti
**Email:** enoshraju7@gmail.com
**Assignment:** Data Types and Structures — Theoretical Questions

---

**1. What are data structures, and why are they important?**

Answer: Data structures are ways of organizing and storing data so that it can be accessed and manipulated efficiently. They are important because they help write optimized and faster programs, manage memory efficiently, and solve real-world problems (like searching, sorting, storing records). Examples include lists, tuples, sets, and dictionaries in Python.

---

**2. Explain the difference between mutable and immutable data types with examples.**

Answer:
- **Mutable**: Objects whose value can be changed after creation. Example: list, dict, set.
  ```python
  lst = [1, 2, 3]
  lst[0] = 99   # Allowed — list is mutable
  ```
- **Immutable**: Objects whose value cannot be changed after creation. Example: int, float, str, tuple.
  ```python
  s = "hello"
  s[0] = "H"   # TypeError — string is immutable
  ```

---

**3. What are the main differences between lists and tuples in Python?**

Answer:

| Feature | List | Tuple |
|---------|------|-------|
| Syntax | `[1, 2, 3]` | `(1, 2, 3)` |
| Mutability | Mutable (can change) | Immutable (cannot change) |
| Performance | Slightly slower | Faster (read-only) |
| Use case | Dynamic data | Fixed/constant data |
| As dict key | No | Yes (hashable) |

---

**4. Describe how dictionaries store data.**

Answer: Dictionaries store data as **key-value pairs** using a **hash table** internally. Each key is passed through a hash function to generate a unique index, and the corresponding value is stored at that index. This allows O(1) average-case lookup. Keys must be immutable (hashable), and each key must be unique.

Example:
```python
d = {"name": "Enosh", "age": 22}
print(d["name"])  # "Enosh"
```

---

**5. Why might you use a set instead of a list in Python?**

Answer: A set is preferred over a list when:
- You need **unique elements only** (sets automatically remove duplicates)
- You need **fast membership testing** — `in` is O(1) for sets vs O(n) for lists
- You need **set operations** like union, intersection, difference
- Order does not matter

Example: Removing duplicates: `set([1, 2, 2, 3]) → {1, 2, 3}`

---

**6. What is a string in Python, and how is it different from a list?**

Answer: A string is an **immutable** sequence of characters. A list is a **mutable** sequence that can hold any data type.

| Feature | String | List |
|---------|--------|------|
| Type of elements | Characters only | Any data type |
| Mutable | No | Yes |
| Syntax | `"hello"` | `['h','e','l','l','o']` |
| Methods | `.upper()`, `.split()`, etc. | `.append()`, `.sort()`, etc. |

---

**7. How do tuples ensure data integrity in Python?**

Answer: Tuples are **immutable**, meaning once created, their elements cannot be changed, added, or removed. This ensures data integrity by:
- Preventing accidental modification of important data
- Making the tuple **hashable** → usable as dictionary keys or set elements
- Clearly communicating to other programmers that this data should not change (e.g., GPS coordinates, employee IDs)

---

**8. What is a hash table, and how does it relate to dictionaries in Python?**

Answer: A hash table is a data structure that maps keys to values using a **hash function**. The hash function converts a key into an integer (hash code) which determines where the value is stored in memory.

Python dictionaries are built on hash tables:
- `d["name"]` → hash("name") → index → value retrieved in O(1)
- This is why dict keys must be **hashable** (immutable types only)
- Collision handling is done internally by Python

---

**9. Can lists contain different data types in Python?**

Answer: Yes. Python lists are **heterogeneous** — they can store elements of different data types in the same list.

```python
mixed = [1, "hello", 3.14, True, [1, 2], {"key": "val"}]
```
This is possible because Python lists store references (pointers) to objects, not the objects themselves.

---

**10. Explain why strings are immutable in Python.**

Answer: Strings are immutable in Python for three main reasons:
1. **Hashability**: Immutable strings can be used as dictionary keys and set elements
2. **Memory efficiency**: Python interns (reuses) identical string literals, saving memory
3. **Thread safety**: Multiple threads can share strings without risk of data corruption

Any "modification" to a string creates a new string object:
```python
s = "hello"
s2 = s.upper()   # New object "HELLO" — original unchanged
```

---

**11. What advantages do dictionaries offer over lists for certain tasks?**

Answer:
- **O(1) lookup by key** vs O(n) linear search in lists
- **Meaningful keys**: Access data by name (e.g., `d["name"]`) instead of position (`lst[0]`)
- **No need to know position**: Don't need to remember where data is stored
- **Natural key-value modeling**: Ideal for records, configs, JSON-like data
- **Counting/grouping**: Frequency counters are easy with dicts

---

**12. Describe a scenario where using a tuple would be preferable over a list.**

Answer: Tuples are preferable when the data should not change:
- **GPS coordinates**: `location = (12.9716, 77.5946)` — latitude and longitude should not change
- **RGB colors**: `color = (255, 0, 0)` — red should stay red
- **Database records**: Rows fetched from a database (read-only data)
- **Dictionary keys**: `{(1, 2): "point A"}` — tuples can be keys, lists cannot
- **Function returning multiple values**: `return name, age` returns a tuple

---

**13. How do sets handle duplicate values in Python?**

Answer: Sets automatically **ignore duplicates**. When you add an element that already exists, the set remains unchanged. Internally, sets use a hash table — each element's hash is computed and if the same hash already exists, the duplicate is discarded.

```python
s = {1, 2, 2, 3, 3, 3}
print(s)  # {1, 2, 3} — duplicates removed automatically
s.add(2)  # Already exists, ignored
print(s)  # {1, 2, 3} — unchanged
```

---

**14. How does the "in" keyword work differently for lists and dictionaries?**

Answer:
- **List**: `in` checks **values** — scans every element from start (O(n) time)
  ```python
  3 in [1, 2, 3, 4]   # True — scans all elements
  ```
- **Dictionary**: `in` checks **keys only** — uses hash table (O(1) time)
  ```python
  "name" in {"name": "Enosh", "age": 22}   # True — checks keys, not values
  ```
  To check values in a dict: `"Enosh" in d.values()`

---

**15. Can you modify the elements of a tuple? Explain why or why not.**

Answer: No, you **cannot modify** the elements of a tuple because tuples are **immutable**.

```python
t = (1, 2, 3)
t[0] = 99   # TypeError: 'tuple' object does not support item assignment
```

This is by design — tuples are meant for data that should remain constant. However, if a tuple contains a mutable object (like a list), the contents of that inner object can be changed:
```python
t = ([1, 2], [3, 4])
t[0].append(99)   # Allowed — the list inside is mutable
print(t)  # ([1, 2, 99], [3, 4])
```

---

**16. What is a nested dictionary, and give an example of its use case.**

Answer: A nested dictionary is a dictionary where the **values are also dictionaries**. Used to represent hierarchical or structured data.

```python
employees = {
    "E001": {"name": "Ajay", "dept": "Engineering", "salary": 75000},
    "E002": {"name": "Jane", "dept": "Marketing",   "salary": 65000},
}
print(employees["E001"]["name"])   # "Ajay"
```

Use cases: Student records, employee databases, JSON-like API responses, configuration files.

---

**17. Describe the time complexity of accessing elements in a dictionary.**

Answer:
- **Access by key** (`d["key"]`): **O(1)** average case — hash table lookup
- **Worst case**: O(n) — very rare, only when many hash collisions occur (Python handles this well internally)
- **Search in values** (`val in d.values()`): O(n) — must scan all values
- **Insert / Delete**: O(1) average case

This makes dictionaries one of the most efficient data structures for lookup operations.

---

**18. In what situations are lists preferred over dictionaries?**

Answer: Lists are preferred when:
- **Order matters** and you access data by **position/index**
- You need to store **duplicate values**
- You work with **sequential data** (iteration, sorting, slicing)
- You implement **stacks** (`pop()`) or **queues** (`deque`)
- **Simple collection** without need for labels/keys (e.g., a list of numbers to sum)
- Memory is a concern — lists use less memory than dicts

---

**19. Why are dictionaries considered unordered, and how does that affect data retrieval?**

Answer: Dictionaries were **unordered** in Python versions before 3.7 because the hash table did not guarantee insertion order. From **Python 3.7+**, dictionaries maintain **insertion order** as an implementation detail (guaranteed in 3.8+).

Effect on data retrieval:
- You **cannot** access dict elements by position (`d[0]` → KeyError)
- You **must** access by key (`d["name"]`)
- Iterating gives items in insertion order (Python 3.7+)

---

**20. Explain the difference between a list and a dictionary in terms of data retrieval.**

Answer:

| | List | Dictionary |
|--|--|--|
| Access by | **Integer index** `lst[0]` | **Key** `d["name"]` |
| Speed | O(n) for search by value | O(1) for key lookup |
| When to use | Positional access needed | Meaningful key access needed |
| Example | `["Enosh", 22, "Bangalore"]` | `{"name":"Enosh","age":22}` |

List retrieval: you must know the **position**.
Dict retrieval: you access by a **meaningful label** (key), much more readable.

---
