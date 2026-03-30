# M4 Functions — Interview Questions & Answers
### PW Skills | Data Science | Python

> **Strategy:** Each answer is a 2-liner — one sentence of concept, one line of code. Easy to say out loud.

---

## Functions

### Q1. What is the importance of functions in Python?

Functions avoid repeating code by packaging logic into a reusable block — call it once, use it anywhere.

```python
def add(a, b): return a + b
print(add(3, 4))  # 7 — same function works for any inputs
```

---

### Q2. Explain the difference between default arguments and keyword arguments. `[Infosys, Microsoft]` ⭐⭐⭐

A **default argument** has a fallback value baked into the definition; a **keyword argument** is when the caller names the parameter explicitly at call time.

```python
def greet(name, msg="Hello"):  # 'msg' is a default argument
    return f"{msg}, {name}"

greet("Enosh")               # uses default → "Hello, Enosh"
greet("Enosh", msg="Hi")     # 'msg' passed as keyword argument → "Hi, Enosh"
```

---

### Q3. What are `*args` and `**kwargs` in Python? `[Swiggy, Google]` ⭐⭐

`*args` collects any number of positional arguments into a **tuple**; `**kwargs` collects any number of keyword arguments into a **dict**.

```python
def show(*args, **kwargs): print(args, kwargs)
show(1, 2, 3, name="Enosh", age=22)  # (1, 2, 3)  {'name': 'Enosh', 'age': 22}
```

---

### Q4. How do iterators differ from generators? Provide examples.

An **iterator** is a class that implements `__iter__` and `__next__`; a **generator** is a function that uses `yield` — Python auto-creates the iterator protocol for you.

```python
# Iterator (manual)                     # Generator (automatic)
class Sq:                               def squares(n):
    def __init__(self, n): self.i, self.n = 0, n   for i in range(n): yield i*i
    def __iter__(self): return self
    def __next__(self):
        if self.i >= self.n: raise StopIteration
        v = self.i*self.i; self.i += 1; return v

print(list(Sq(4)))       # [0, 1, 4, 9]
print(list(squares(4)))  # [0, 1, 4, 9]
```

---

## Lambda, Map, Reduce, and Filter

### Q5. Explain lambda functions. How are they different from normal functions? `[Amazon, TCS]` ⭐⭐⭐

A **lambda** is a one-line anonymous function — no `def`, no `return`, used when the logic is too small to deserve a name.

```python
square = lambda x: x ** 2     # lambda — throwaway, inline
def square(x): return x ** 2  # def — named, reusable, can have docstrings/multiple lines
print(square(5))  # 25
```

---

### Q6. How would you use `map()`, `filter()`, and `reduce()`? `[Google, Flipkart]` ⭐⭐

`map` transforms every item, `filter` keeps items matching a condition, `reduce` collapses all items into one value.

```python
from functools import reduce
nums = [1, 2, 3, 4, 5]
print(list(map(lambda x: x**2, nums)))          # [1, 4, 9, 16, 25]
print(list(filter(lambda x: x % 2 == 0, nums))) # [2, 4]
print(reduce(lambda x, y: x + y, nums))         # 15
```

---

### Q7. What is the benefit of using lambda with `map` and `filter`? `[TCS, IBM]` ⭐⭐

Lambda keeps the transformation logic right next to the function call — no need to define a separate named function for a one-time operation.

```python
# Without lambda — extra ceremony for a throwaway operation
def double(x): return x * 2
list(map(double, [1, 2, 3]))      # [2, 4, 6]

# With lambda — inline, no clutter
list(map(lambda x: x * 2, [1, 2, 3]))  # [2, 4, 6]
```

---

## OOPs in Python

### Q8. What are classes and objects in Python? Explain with examples.

A **class** is a blueprint; an **object** is a live instance created from that blueprint with its own data.

```python
class Dog:
    def __init__(self, name): self.name = name
    def bark(self): return f"{self.name} says Woof!"

d = Dog("Bruno")   # d is an object
print(d.bark())    # Bruno says Woof!
```

---

### Q9. Explain the concept of inheritance in Python. `[Infosys, Cognizant]` ⭐⭐⭐

Inheritance lets a child class reuse all attributes and methods of a parent class, and optionally override them.

```python
class Animal:
    def speak(self): return "Some sound"

class Dog(Animal):                        # Dog inherits Animal
    def speak(self): return "Woof!"       # overrides parent method

print(Dog().speak())   # Woof!
```

---

### Q10. Difference between single and multiple inheritance? `[Capgemini, Flipkart]` ⭐⭐

**Single** — child inherits from one parent; **Multiple** — child inherits from two or more parents, combining their features.

```python
class A:
    def hello(self): return "A"

class B:
    def world(self): return "B"

class C(A, B): pass          # multiple inheritance
print(C().hello(), C().world())  # A  B
```

---

### Q11. What is encapsulation and how is it implemented in Python? `[IBM, Zomato]` ⭐⭐⭐

Encapsulation hides internal data and exposes it only through controlled methods — use single `_` for protected, double `__` for private.

```python
class BankAccount:
    def __init__(self, bal): self.__balance = bal          # private
    def get_balance(self): return self.__balance           # controlled access
    def deposit(self, amt): self.__balance += amt

acc = BankAccount(1000)
acc.deposit(500)
print(acc.get_balance())   # 1500
# print(acc.__balance)     # AttributeError — hidden!
```

---

### Q12. What are static methods and class methods? Explain with an example.

A **classmethod** receives the class (`cls`) as first arg and can modify class state; a **staticmethod** receives nothing special — it's just a regular function namespaced inside a class.

```python
class MathUtils:
    pi = 3.14159

    @classmethod
    def circle_area(cls, r): return cls.pi * r * r    # uses class variable

    @staticmethod
    def add(a, b): return a + b                        # no class/instance needed

print(MathUtils.circle_area(5))  # 78.53...
print(MathUtils.add(3, 4))       # 7
```

---

### Q13. What are dunder methods in Python? Why are they useful? `[Microsoft, Swiggy]` ⭐⭐

**Dunder (double-underscore) methods** like `__init__`, `__str__`, `__len__` let you define how built-in operators and functions behave on your custom objects.

```python
class Vector:
    def __init__(self, x, y): self.x, self.y = x, y
    def __add__(self, other): return Vector(self.x + other.x, self.y + other.y)
    def __repr__(self): return f"Vector({self.x}, {self.y})"

print(Vector(1, 2) + Vector(3, 4))  # Vector(4, 6) — '+' works on custom class!
```

---

### Q14. Difference between method overriding and method overloading? `[Infosys, Paytm]` ⭐⭐⭐

**Overriding** — child class redefines a parent method (runtime polymorphism); **Overloading** — same method name with different signatures (Python doesn't support it natively, use default args instead).

```python
# Overriding
class Animal:
    def sound(self): return "..."
class Cat(Animal):
    def sound(self): return "Meow"   # overrides parent

# Overloading (Python way — default args simulate it)
def add(a, b, c=0): return a + b + c
print(add(1, 2))      # 3
print(add(1, 2, 3))   # 6
```

---

### Q15. Explain the use of decorators in Python and provide an example. `[Amazon, Wipro]` ⭐⭐⭐

A **decorator** is a function that wraps another function to add behavior before/after it runs — without changing the original function's code.

```python
def logger(func):
    def wrapper(*args, **kwargs):
        print(f"Calling {func.__name__}")
        result = func(*args, **kwargs)
        print(f"Done")
        return result
    return wrapper

@logger
def add(a, b): return a + b

add(3, 4)
# Calling add
# Done
```

---

## Git Commands Cheat Sheet — Used in This Project

| Task | Command |
|------|---------|
| Clone a repo | `git clone <url>` |
| Pull latest changes | `git pull` |
| Check status | `git status` |
| **Rename a folder** | `git mv "OldName" "NewName"` |
| **Stage specific files** | `git add "M4 Functions/"` |
| Stage all changes | `git add .` |
| **Commit with message** | `git commit -m "your message"` |
| **Push to GitHub** | `git push origin main` |
| View commit log | `git log --oneline` |

> **Rename flow:** `git mv` handles the rename + staging in one step — Git tracks it as a rename (not delete + add), so history is preserved.
