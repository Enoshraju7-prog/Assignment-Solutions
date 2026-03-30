# M4 Functions - Theory Assignment
### PW Skills | Data Science | Python

---

## Q1. What is the difference between a function and a method in Python?

A **function** is a standalone reusable block of code that performs a specific task. It is defined using the `def` keyword and can be called directly anywhere in the program.

A **method** is a function that lives inside a class and is always called through an object. It always takes `self` as its first parameter.

```python
# Function — called directly
def add(a, b):
    return a + b

print(add(3, 4))  # 7

# Method — called through object
class Calculator:
    def add(self, a, b):
        return a + b

calc = Calculator()
print(calc.add(3, 4))  # 7
```

| | Function | Method |
|---|---|---|
| Defined | Outside class | Inside class |
| Called by | Name directly | Through object |
| First parameter | Anything | Always `self` |

---

## Q2. Explain the concept of function arguments and parameters in Python.

A **parameter** is a placeholder variable in the function definition.
An **argument** is the actual value passed when calling the function.

```python
def greet(name):       # 'name' is a parameter
    print(f"Hello {name}")

greet("Enosh")         # "Enosh" is an argument
```

**Types of arguments:**

- **Default arguments** — fallback value if nothing is passed
```python
def greet(name="stranger"):
    return f"Hello {name}"

greet()          # Hello stranger
greet("Enosh")   # Hello Enosh
```

- **`*args`** — accepts multiple positional values as a tuple
```python
def total(*args):
    print(args)    # (1, 2, 3)

total(1, 2, 3)
```

- **`**kwargs`** — accepts multiple keyword values as a dictionary
```python
def info(**kwargs):
    print(kwargs)    # {'name': 'Enosh', 'age': 22}

info(name="Enosh", age=22)
```

---

## Q3. What are the different ways to define and call a function in Python?

**Way 1 — Regular function using `def`**
```python
def add(a, b):
    return a + b

print(add(3, 4))   # 7
```

**Way 2 — Lambda function (one-liner, throwaway)**
```python
f = lambda x: x**2
print(f(4))        # 16
```

**Way 3 — Function with default arguments**
```python
def greet(name="stranger"):
    return f"Hello {name}, good to see you"

greet("Enosh")   # Hello Enosh, good to see you
greet()          # Hello stranger, good to see you
```

---

## Q4. What is the purpose of the `return` statement in a Python function?

The `return` statement sends a value back to whoever called the function. Without it, Python automatically returns `None`.

```python
# With return
def add(a, b):
    return a + b

result = add(3, 4)
print(result)      # 7

# Without return
def add(a, b):
    a + b

result = add(3, 4)
print(result)      # None
```

---

## Q5. What are iterators in Python and how do they differ from iterables?

An **iterable** is any object you can loop over — list, tuple, string.

An **iterator** is an object that gives one value at a time and remembers its current position using `iter()` and `next()`.

```python
my_list = [1, 2, 3]       # iterable

my_iter = iter(my_list)   # convert to iterator

print(next(my_iter))  # 1
print(next(my_iter))  # 2
print(next(my_iter))  # 3
print(next(my_iter))  # StopIteration — exhausted
```

| | Iterable | Iterator |
|---|---|---|
| What it is | Any loopable object | Object with position memory |
| How to use | `for` loop directly | `next()` to get values |
| Example | list, string, tuple | `iter(list)` |

---

## Q6. Explain the concept of generators in Python and how they are defined.

A **generator** is a special function that uses `yield` instead of `return` to produce values one at a time. It pauses at each `yield` and resumes from that point when `next()` is called.

```python
def power_of_2(n):
    for i in range(n):
        yield 2 ** i

g = power_of_2(4)
print(next(g))   # 1
print(next(g))   # 2
print(next(g))   # 4
print(next(g))   # 8
```

---

## Q7. What are the advantages of using generators over regular functions?

1. **Memory efficient** — values are generated one at a time, not stored all at once
2. **Lazy evaluation** — nothing runs until `next()` is called
3. **Simpler syntax** — easier than writing a full iterator class

```python
# Regular function — stores ALL in memory
def get_numbers(n):
    return [i for i in range(n)]    # entire list in RAM

# Generator — one at a time
def get_numbers(n):
    for i in range(n):
        yield i                      # only 1 item in RAM at a time
```

---

## Q8. What is a lambda function in Python and when is it typically used?

A **lambda function** is a small, anonymous one-liner function defined using the `lambda` keyword. It is used when the function is not reusable and the logic fits in a single expression.

```python
# Regular function
def square(x):
    return x ** 2

# Same as lambda
square = lambda x: x ** 2

print(square(4))   # 16
```

Lambda is typically used inside `map()`, `filter()`, and `sort()`:
```python
nums = [3, 1, 4, 1, 5]
nums.sort(key=lambda x: -x)   # sort descending
```

---

## Q9. Explain the purpose and usage of the `map()` function in Python.

`map()` applies a given function to every item in an iterable and returns a new iterator with the results.

```python
celsius = [0, 20, 37, 100]

fahrenheit = list(map(lambda x: (x * 9/5) + 32, celsius))

print(fahrenheit)   # [32.0, 68.0, 98.6, 212.0]
```

---

## Q10. What is the difference between `map()`, `reduce()`, and `filter()` functions in Python?

| | `map()` | `filter()` | `reduce()` |
|---|---|---|---|
| Purpose | Transform every item | Select items by condition | Cumulatively reduce to one value |
| Output | New list (same size) | Smaller or equal list | Single value |
| Items interact? | ❌ No | ❌ No | ✅ Yes |

```python
from functools import reduce

numbers = [1, 2, 3, 4, 5, 6]

# map — square every item
list(map(lambda x: x**2, numbers))         # [1, 4, 9, 16, 25, 36]

# filter — keep only evens
list(filter(lambda x: x % 2 == 0, numbers)) # [2, 4, 6]

# reduce — sum all items
reduce(lambda x, y: x + y, numbers)         # 21
```

---

## Q11. Internal Mechanism of `reduce()` for Sum on [47, 11, 42, 13]

```python
from functools import reduce

reduce(lambda x, y: x + y, [47, 11, 42, 13])
```

**Step-by-step trace:**

```
List: [47, 11, 42, 13]

Step 1:  x = 47,  y = 11  →  47 + 11  = 58
Step 2:  x = 58,  y = 42  →  58 + 42  = 100
Step 3:  x = 100, y = 13  →  100 + 13 = 113

Final Result → 113 ✅
```

**Visual flow:**
```
[47, 11, 42, 13]

 47 ──┐
      ├──► 47+11 = 58 ──┐
 11 ──┘                  ├──► 58+42 = 100 ──┐
                 42 ──────┘                  ├──► 100+13 = 113
                                     13 ─────┘
```

> **Rule:** `x` is always the accumulated result so far. `y` is always the next element in the list.

---

*Note: Q11 pen & paper diagram to be attached separately as per assignment instructions.*
