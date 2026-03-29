# Data Structures Interview Questions - Complete Solutions

## Author: Enosh RD | Target: Data Science Roles with GenAI Focus
## Section: Intro to Data Structures

> **About this document:** Compiled after discussion with 100s of candidates, industry experts, and review of many interview portals.
> - **Importance levels:** 1 (lowest) → 3 (highest)
> - **Company names and roles may overlap across questions.**

---

## 1. What are the different types of data structures in Python?

**Roles/Companies:** —
**Importance:** ⭐ (1/3)

**Answer:**

Python provides both **built-in** and **user-defined** data structures:

**Built-in Data Structures:**

| Type | Ordered | Mutable | Duplicates | Example |
|------|---------|---------|------------|---------|
| `list` | Yes | Yes | Yes | `[1, 2, 3]` |
| `tuple` | Yes | No | Yes | `(1, 2, 3)` |
| `set` | No | Yes | No | `{1, 2, 3}` |
| `dict` | Yes (3.7+) | Yes | Keys: No | `{"a": 1}` |
| `str` | Yes | No | Yes | `"hello"` |

**User-defined / Advanced Data Structures:**
- **Stack** – LIFO (Last In First Out), implemented using `list` or `collections.deque`
- **Queue** – FIFO (First In First Out), implemented using `collections.deque` or `queue.Queue`
- **Linked List** – Nodes connected via pointers (manual implementation)
- **Tree** – Hierarchical structure (e.g., Binary Search Tree)
- **Graph** – Nodes connected by edges (adjacency list/matrix)
- **Heap** – Priority queue via `heapq` module

```python
# Quick examples
my_list  = [1, 2, 2, 3]          # mutable, ordered, allows duplicates
my_tuple = (1, 2, 2, 3)          # immutable, ordered, allows duplicates
my_set   = {1, 2, 3}             # mutable, unordered, unique elements
my_dict  = {"name": "Enosh", "age": 25}  # key-value pairs
```

---

## 2. What is recursion? How to implement Fibonacci series?

**Roles/Companies:** [Flipkart, Oyo, TCS]
**Importance:** ⭐⭐⭐ (3/3)

**Answer:**

**Recursion** is a programming technique where a function calls itself to solve a smaller sub-problem until it reaches a **base case** (stopping condition).

**Key components of recursion:**
1. **Base case** – condition to stop recursion (prevents infinite loop)
2. **Recursive case** – function calls itself with a simpler input

**Fibonacci Series using Recursion:**

```python
def fibonacci(n):
    # Base cases
    if n <= 0:
        return 0
    elif n == 1:
        return 1
    # Recursive case
    return fibonacci(n - 1) + fibonacci(n - 2)

# Print first 10 Fibonacci numbers
for i in range(10):
    print(fibonacci(i), end=" ")
# Output: 0 1 1 2 3 5 8 13 21 34
```

**Optimized version using memoization (important for interviews):**

```python
from functools import lru_cache

@lru_cache(maxsize=None)
def fibonacci_memo(n):
    if n <= 0:
        return 0
    elif n == 1:
        return 1
    return fibonacci_memo(n - 1) + fibonacci_memo(n - 2)

print(fibonacci_memo(50))  # Fast! Without memoization this would be very slow
```

**Time Complexity:**
- Without memoization: O(2^n) — exponential
- With memoization: O(n) — linear

> **Interview tip:** Always mention memoization/dynamic programming as an optimization over naive recursion.

---

## 3. Find the factorial of a number using Python?

**Roles/Companies:** —
**Importance:** ⭐⭐⭐ (3/3)

**Answer:**

**Factorial** of a number `n` (written as `n!`) is the product of all positive integers from 1 to n.
Example: `5! = 5 × 4 × 3 × 2 × 1 = 120`

**Method 1 — Recursive approach:**

```python
def factorial_recursive(n):
    if n < 0:
        raise ValueError("Factorial not defined for negative numbers")
    if n == 0 or n == 1:   # base case
        return 1
    return n * factorial_recursive(n - 1)  # recursive case

print(factorial_recursive(5))   # 120
print(factorial_recursive(0))   # 1
```

**Method 2 — Iterative approach:**

```python
def factorial_iterative(n):
    if n < 0:
        raise ValueError("Factorial not defined for negative numbers")
    result = 1
    for i in range(2, n + 1):
        result *= i
    return result

print(factorial_iterative(5))   # 120
```

**Method 3 — Using Python's built-in `math` module:**

```python
import math
print(math.factorial(5))   # 120
```

> **Interview tip:** Interviewers often ask all three approaches. Mention that recursive is elegant but has O(n) stack space overhead; iterative is preferred in production.

---

## 4. What is the disadvantage of nested if-else? How can we remove it? Show with Python code and example.

**Roles/Companies:** —
**Importance:** ⭐⭐⭐ (3/3)

**Answer:**

**Disadvantages of Nested if-else:**
1. **Reduced readability** — deep nesting makes code hard to follow ("Pyramid of Doom")
2. **Hard to maintain** — adding/removing conditions requires restructuring
3. **Higher cyclomatic complexity** — more branching = harder to test
4. **Error-prone** — mismatched indentation causes logic bugs

**Problem example (deeply nested):**

```python
# BAD: Nested if-else — hard to read
def classify_student(marks, attendance, assignments_done):
    if marks >= 40:
        if attendance >= 75:
            if assignments_done:
                return "Pass with Distinction"
            else:
                return "Pass but incomplete assignments"
        else:
            return "Fail due to low attendance"
    else:
        return "Fail due to low marks"
```

**Solutions to remove nested if-else:**

**1. Early Return (Guard Clauses) — preferred approach:**

```python
# GOOD: Guard clauses — flat and readable
def classify_student(marks, attendance, assignments_done):
    if marks < 40:
        return "Fail due to low marks"
    if attendance < 75:
        return "Fail due to low attendance"
    if not assignments_done:
        return "Pass but incomplete assignments"
    return "Pass with Distinction"
```

**2. Dictionary mapping (replaces if-elif chains):**

```python
# BAD: if-elif chain for grade
def get_grade_nested(score):
    if score >= 90:
        return "A"
    elif score >= 80:
        return "B"
    elif score >= 70:
        return "C"
    else:
        return "F"

# GOOD: using a list of tuples
def get_grade_clean(score):
    grades = [(90, "A"), (80, "B"), (70, "C")]
    return next((grade for threshold, grade in grades if score >= threshold), "F")
```

**3. Polymorphism / Strategy Pattern (OOP approach):**

```python
# Replace conditionals with class-based behavior
class PassWithDistinction:
    def result(self): return "Pass with Distinction"

class Fail:
    def result(self): return "Fail"
```

> **Key rule:** Each level of nesting adds cognitive load. Flatten wherever possible using guard clauses or data-driven lookups.

---

## 5. How would you reverse a string in Python without using built-in functions?

**Roles:** Data Science, Business Analyst
**Companies:** Wipro, TCS
**Importance:** ⭐⭐ (2/3)

**Answer:**

**Method 1 — Using a loop:**

```python
def reverse_string(s):
    reversed_str = ""
    for char in s:
        reversed_str = char + reversed_str   # prepend each character
    return reversed_str

print(reverse_string("Python"))   # nohtyP
```

**Method 2 — Using index traversal:**

```python
def reverse_string_index(s):
    reversed_str = ""
    for i in range(len(s) - 1, -1, -1):
        reversed_str += s[i]
    return reversed_str

print(reverse_string_index("DataScience"))   # ecneicSataD
```

**Method 3 — Using recursion:**

```python
def reverse_recursive(s):
    if len(s) <= 1:          # base case
        return s
    return reverse_recursive(s[1:]) + s[0]

print(reverse_recursive("Hello"))   # olleH
```

**For reference — built-in approach (not allowed here but know it):**

```python
# Slicing (most Pythonic)
print("Python"[::-1])         # nohtyP

# Built-in reversed()
print("".join(reversed("Python")))  # nohtyP
```

> **Interview tip:** Start with the loop-based approach to show understanding of string traversal, then optionally mention slicing as the Pythonic way.

---

## 6. Explain string immutability in Python.

**Roles:** Machine Learning Engineer, Data Science
**Companies:** Infosys, Cognizant
**Importance:** ⭐⭐ (2/3)

**Answer:**

**String immutability** means that once a string object is created in Python, its content **cannot be changed in place**. Any operation that appears to "modify" a string actually creates a **new string object**.

```python
s = "hello"
print(id(s))         # e.g., 140234567890

s = s + " world"     # creates a NEW string, does NOT modify the original
print(id(s))         # different id — it's a new object!

# This raises a TypeError — you cannot change a character in place:
# s[0] = "H"  →  TypeError: 'str' object does not support item assignment
```

**Why are strings immutable?**

1. **Security** — strings used as dictionary keys or in hashing must not change
2. **Performance** — Python interns (reuses) common strings to save memory
3. **Thread safety** — immutable objects are safe to share across threads without locks
4. **Hashability** — immutable objects can be used in sets and as dict keys

**Performance implication — string concatenation in loops:**

```python
# BAD: O(n²) — creates a new string every iteration
result = ""
for word in ["Data", "Science", "Python"]:
    result += word   # new object each time

# GOOD: use join() — O(n)
result = "".join(["Data", "Science", "Python"])
print(result)   # DataSciencePython
```

> **Interview tip:** Contrast with `list` which is mutable. The interviewer may also ask about `bytearray` as a mutable alternative to `bytes`.

---

## 7. What are the advantages of using lists in Python?

**Roles/Companies:** —
**Importance:** —

**Answer:**

Lists are one of Python's most versatile and widely used data structures. Key advantages:

**1. Dynamic sizing:**
```python
my_list = [1, 2, 3]
my_list.append(4)      # grows automatically
my_list.extend([5, 6]) # add multiple elements
print(my_list)          # [1, 2, 3, 4, 5, 6]
```

**2. Heterogeneous elements (mixed data types):**
```python
mixed = [1, "hello", 3.14, True, [1, 2]]  # valid in Python
```

**3. Ordered and indexable:**
```python
fruits = ["apple", "banana", "cherry"]
print(fruits[0])    # apple
print(fruits[-1])   # cherry (negative indexing)
print(fruits[1:3])  # ['banana', 'cherry'] (slicing)
```

**4. Mutable — supports in-place modification:**
```python
nums = [3, 1, 2]
nums.sort()          # in-place sort
nums[0] = 99         # direct assignment
del nums[1]          # deletion
```

**5. Rich built-in methods:**
```python
lst = [3, 1, 4, 1, 5]
lst.append(9)         # add to end
lst.insert(0, 0)      # insert at index
lst.remove(1)         # remove first occurrence
lst.pop()             # remove and return last
lst.count(1)          # count occurrences
lst.index(4)          # find index of value
```

**6. Supports list comprehension (Pythonic and fast):**
```python
squares = [x**2 for x in range(10)]
evens   = [x for x in range(20) if x % 2 == 0]
```

**Trade-offs to mention:**
- Searching is O(n) — use `set` or `dict` for O(1) lookups
- Not memory-efficient for large numeric data — use `numpy` arrays instead

---

## 8. How are Python sets different from lists and tuples?

**Roles:** Data Analytics
**Companies:** PayPal, IBM
**Importance:** ⭐⭐ (2/3)

**Answer:**

| Feature | `list` | `tuple` | `set` |
|---------|--------|---------|-------|
| **Ordered** | Yes | Yes | No |
| **Mutable** | Yes | No | Yes |
| **Duplicates** | Yes | Yes | No (auto-removed) |
| **Indexing** | Yes | Yes | No |
| **Hashable** | No | Yes (if elements are) | No |
| **Syntax** | `[1, 2]` | `(1, 2)` | `{1, 2}` |
| **Use case** | General ordered data | Fixed records | Unique items, fast lookup |

**Code demonstration:**

```python
my_list  = [1, 2, 2, 3, 3]   # duplicates kept
my_tuple = (1, 2, 2, 3, 3)   # duplicates kept
my_set   = {1, 2, 2, 3, 3}   # duplicates removed → {1, 2, 3}

print(my_list[0])    # 1  — indexing works
print(my_tuple[0])   # 1  — indexing works
# print(my_set[0])   # TypeError — sets are unordered, no indexing
```

**Where sets shine — set operations:**

```python
a = {1, 2, 3, 4}
b = {3, 4, 5, 6}

print(a | b)    # Union:        {1, 2, 3, 4, 5, 6}
print(a & b)    # Intersection: {3, 4}
print(a - b)    # Difference:   {1, 2}
print(a ^ b)    # Symmetric diff: {1, 2, 5, 6}
```

**Membership test — set is O(1), list is O(n):**

```python
large_list = list(range(1_000_000))
large_set  = set(range(1_000_000))

# Set lookup is dramatically faster:
999999 in large_set   # O(1) — hash-based
999999 in large_list  # O(n) — linear scan
```

> **Interview tip:** Sets are backed by a hash table — same as `dict` keys. This is why elements must be hashable (no lists or dicts inside a set).

---

## 9. What is the difference between a shallow copy and a deep copy in lists?

**Roles:** Machine Learning Engineer, Data Science
**Companies:** Google, Cognizant
**Importance:** ⭐⭐⭐ (3/3)

**Answer:**

| | Shallow Copy | Deep Copy |
|--|-------------|-----------|
| **What is copied** | Outer object + references to nested objects | Outer object + fully new copies of all nested objects |
| **Nested object changes** | Affect the copy (shared reference) | Do NOT affect the copy (independent) |
| **Module** | `copy.copy()` or `list[:]` | `copy.deepcopy()` |
| **Speed** | Faster | Slower |

**Visual explanation:**

```
Original: [ [1,2], [3,4] ]
              ↑        ↑
Shallow:  [ [1,2], [3,4] ]   ← same inner list objects (shared!)
Deep:     [ [1,2], [3,4] ]   ← completely new inner list objects
```

**Code demonstration:**

```python
import copy

original = [[1, 2], [3, 4], [5, 6]]

shallow = copy.copy(original)      # or: original[:]
deep    = copy.deepcopy(original)

# Modify a nested list
original[0][0] = 99

print(original)  # [[99, 2], [3, 4], [5, 6]]
print(shallow)   # [[99, 2], [3, 4], [5, 6]]  ← AFFECTED (shared reference)
print(deep)      # [[1, 2], [3, 4], [5, 6]]   ← NOT affected (independent copy)
```

**Adding/removing top-level elements — shallow copy is independent:**

```python
shallow.append([7, 8])
print(original)  # original NOT affected — only top-level is independent
```

**When to use which:**
- **Shallow copy** — flat lists (no nested mutable objects), performance-critical code
- **Deep copy** — nested structures (lists of lists, dicts of dicts), ML feature matrices, config objects

> **Interview tip:** This is a high-importance question at Google/Cognizant. Always draw the memory diagram mentally and walk the interviewer through what `id()` shows for nested objects.

---

## 10. When would you use a dictionary over a list?

**Roles/Companies:** —
**Importance:** ⭐⭐⭐ (3/3)

**Answer:**

Use a **dictionary** when you need **named, fast, key-based access**. Use a **list** when order and positional access matter more than labeling.

**Use dict over list when:**

**1. Data has natural key-value relationships:**
```python
# BAD: positional, unclear
student_list = ["Enosh", 25, "Data Science", 9.1]
print(student_list[2])   # What is index 2? Not obvious.

# GOOD: self-documenting
student_dict = {"name": "Enosh", "age": 25, "course": "Data Science", "cgpa": 9.1}
print(student_dict["course"])   # "Data Science" — immediately clear
```

**2. O(1) lookup by a unique identifier:**
```python
# BAD: O(n) search through list of tuples
employees_list = [("E001", "Alice"), ("E002", "Bob"), ("E003", "Carol")]
for emp_id, name in employees_list:
    if emp_id == "E002":
        print(name)

# GOOD: O(1) dictionary lookup
employees_dict = {"E001": "Alice", "E002": "Bob", "E003": "Carol"}
print(employees_dict["E002"])   # Bob — instant
```

**3. Counting frequencies:**
```python
words = ["apple", "banana", "apple", "cherry", "banana", "apple"]
freq = {}
for word in words:
    freq[word] = freq.get(word, 0) + 1

print(freq)   # {'apple': 3, 'banana': 2, 'cherry': 1}

# Even cleaner with collections.Counter:
from collections import Counter
print(Counter(words))
```

**4. Caching / memoization:**
```python
cache = {}
def fib(n):
    if n in cache:
        return cache[n]
    if n <= 1:
        return n
    cache[n] = fib(n-1) + fib(n-2)
    return cache[n]
```

**Summary — choose based on access pattern:**

| Scenario | Use |
|----------|-----|
| Ordered sequence, positional access | `list` |
| Named fields, key-based lookup | `dict` |
| Unique items, membership test | `set` |
| Fixed record, no changes needed | `tuple` |

---

## 11. How do you merge two dictionaries in Python?

**Roles:** Data Science, Data Analytics
**Companies:** TCS, Cognizant
**Importance:** ⭐⭐ (2/3)

**Answer:**

Python provides several ways to merge dictionaries. The approach you choose depends on your Python version and whether you want to modify in place.

**Method 1 — `|` operator (Python 3.9+, recommended):**

```python
dict1 = {"a": 1, "b": 2}
dict2 = {"b": 3, "c": 4}

merged = dict1 | dict2
print(merged)   # {'a': 1, 'b': 3, 'c': 4}
# Note: dict2 values win on key conflict ('b': 3)
```

**Method 2 — `|=` in-place merge (Python 3.9+):**

```python
dict1 = {"a": 1, "b": 2}
dict2 = {"b": 3, "c": 4}

dict1 |= dict2   # modifies dict1 in place
print(dict1)     # {'a': 1, 'b': 3, 'c': 4}
```

**Method 3 — Unpacking with `**` (Python 3.5+):**

```python
dict1 = {"a": 1, "b": 2}
dict2 = {"b": 3, "c": 4}

merged = {**dict1, **dict2}
print(merged)   # {'a': 1, 'b': 3, 'c': 4}
```

**Method 4 — `update()` method (in-place, all Python versions):**

```python
dict1 = {"a": 1, "b": 2}
dict2 = {"b": 3, "c": 4}

dict1.update(dict2)   # modifies dict1
print(dict1)           # {'a': 1, 'b': 3, 'c': 4}
```

**Method 5 — `ChainMap` (non-destructive view, no copy):**

```python
from collections import ChainMap

dict1 = {"a": 1, "b": 2}
dict2 = {"b": 3, "c": 4}

merged_view = ChainMap(dict1, dict2)
print(dict(merged_view))   # {'b': 2, 'c': 4, 'a': 1}
# Note: ChainMap gives priority to the FIRST dict for 'b'
```

**Handling conflicts explicitly:**

```python
# Keep all values when keys conflict (store as list)
dict1 = {"a": 1, "b": 2}
dict2 = {"b": 3, "c": 4}

merged = {}
for d in [dict1, dict2]:
    for key, val in d.items():
        if key in merged:
            merged[key] = [merged[key], val] if not isinstance(merged[key], list) else merged[key] + [val]
        else:
            merged[key] = val

print(merged)   # {'a': 1, 'b': [2, 3], 'c': 4}
```

**Quick comparison:**

| Method | Python Version | In-place | Priority on conflict |
|--------|---------------|----------|----------------------|
| `\|` operator | 3.9+ | No | Right dict wins |
| `\|=` operator | 3.9+ | Yes | Right dict wins |
| `{**d1, **d2}` | 3.5+ | No | Right dict wins |
| `.update()` | All | Yes | Right dict wins |
| `ChainMap` | All | No (view) | Left dict wins |

> **Interview tip:** Always mention what happens on key conflicts — it shows you think about edge cases. The `|` operator is the cleanest modern approach; `**` unpacking is most commonly seen in codebases targeting Python 3.5–3.8.

---

*End of Intro to Data Structures Interview Questions*
