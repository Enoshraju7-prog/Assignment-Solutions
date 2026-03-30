# Week 1 Assignment - Python Basics
## PW Skills Data Science with GenAI Course
### Student: Enosh RD

---

## Theoretical Questions

### 1. What is Python, and why is it popular?

**Answer:**
Python is a high-level, interpreted programming language known for its simple and readable syntax.

**Why it's popular:**
- Easy to learn and read
- Rich library ecosystem (NumPy, Pandas, TensorFlow)
- Versatile (web, data science, ML, automation)
- Strong community support
- Great for rapid development and prototyping

---

### 2. What is an interpreter in Python?

**Answer:**
An interpreter is a program that executes Python code line by line, converting it to machine code in real-time without needing prior compilation.

**Key points:**
- Executes code directly without creating executable files
- Makes debugging easier (immediate error detection)
- Python uses CPython as its default interpreter

---

### 3. What are pre-defined keywords in Python?

**Answer:**
Keywords are reserved words with special meanings that cannot be used as identifiers. Python has 35 keywords including:

`if`, `else`, `elif`, `for`, `while`, `def`, `class`, `return`, `import`, `from`, `try`, `except`, `True`, `False`, `None`, `and`, `or`, `not`, `in`, `is`, `break`, `continue`, `pass`, `lambda`, `with`, etc.

---

### 4. Can keywords be used as variable names?

**Answer:**
No, keywords cannot be used as variable names because they have predefined meanings in Python.

```python
# This will cause SyntaxError
if = 5        # Error
for = "test"  # Error

# Correct usage
if_value = 5  # Valid
for_loop = "test"  # Valid
```

---

### 5. What is mutability in Python?

**Answer:**
Mutability refers to whether an object's content can be changed after creation.

**Mutable:** Can be modified after creation (list, dict, set)
**Immutable:** Cannot be modified after creation (int, float, str, tuple)

```python
# Mutable
my_list = [1, 2, 3]
my_list[0] = 10  # Works

# Immutable
my_tuple = (1, 2, 3)
# my_tuple[0] = 10  # TypeError
```

---

### 6. Why are lists mutable, but tuples are immutable?

**Answer:**
This is a design decision in Python:

**Lists (mutable):**
- Designed for dynamic data that changes
- Support operations like append, remove, sort
- Use more memory and are slower

**Tuples (immutable):**
- Designed for fixed data that shouldn't change
- Provide data integrity and safety
- More memory efficient and faster
- Can be used as dictionary keys (hashable)

```python
# List - for changing data
tasks = ['task1', 'task2']
tasks.append('task3')  # Allowed

# Tuple - for fixed data
coordinates = (10, 20)
# coordinates[0] = 15  # Not allowed
```

---

### 7. What is the difference between "==" and "is" operators in Python?

**Answer:**

| Operator | Purpose | Checks |
|----------|---------|--------|
| `==` | Value equality | If values are equal |
| `is` | Identity | If both refer to same object |

```python
a = [1, 2, 3]
b = [1, 2, 3]
c = a

print(a == b)  # True (same values)
print(a is b)  # False (different objects)
print(a is c)  # True (same object)
```

---

### 8. What are logical operators in Python?

**Answer:**
Logical operators are used to combine conditional statements:

- `and`: Returns True if both conditions are True
- `or`: Returns True if at least one condition is True
- `not`: Reverses the boolean value

```python
x = 10
y = 5

print(x > 5 and y < 10)  # True
print(x < 5 or y < 10)   # True
print(not(x > 5))        # False
```

---

### 9. What is type casting in Python?

**Answer:**
Type casting is converting one data type to another using built-in functions.

```python
# String to integer
num = int("42")      # 42

# Integer to float
decimal = float(5)   # 5.0

# Float to integer
whole = int(3.7)     # 3

# To string
text = str(100)      # "100"

# To boolean
flag = bool(1)       # True
```

---

### 10. What is the difference between implicit and explicit type casting?

**Answer:**

**Implicit (Automatic):**
Python automatically converts types when needed.
```python
x = 5      # int
y = 2.5    # float
z = x + y  # z = 7.5 (float) - automatic conversion
```

**Explicit (Manual):**
Programmer manually converts using functions.
```python
num_str = "42"
num = int(num_str)  # Manual conversion
result = num + 10   # 52
```

---

### 11. What is the purpose of conditional statements in Python?

**Answer:**
Conditional statements allow programs to make decisions and execute different code based on conditions.

**Purpose:**
- Decision making in programs
- Execute code selectively
- Control program flow
- Handle different scenarios

```python
age = 18
if age >= 18:
    print("Adult")
else:
    print("Minor")
```

---

### 12. How does the elif statement work?

**Answer:**
`elif` (else if) allows checking multiple conditions in sequence. It's evaluated only if previous conditions are False.

```python
score = 75

if score >= 90:
    print("Grade A")
elif score >= 80:
    print("Grade B")
elif score >= 70:
    print("Grade C")  # This executes
else:
    print("Grade F")
```

**Flow:** Check conditions top to bottom, execute first True block, skip rest.

---

### 13. What is the difference between for and while loops?

**Answer:**

| Feature | for loop | while loop |
|---------|----------|------------|
| **Use** | Known iterations | Unknown iterations |
| **When** | Iterating sequences | Condition-based looping |
| **Syntax** | `for item in sequence:` | `while condition:` |
| **Control** | Automatic | Manual counter needed |

```python
# For loop - known iterations
for i in range(5):
    print(i)

# While loop - condition-based
count = 0
while count < 5:
    print(count)
    count += 1
```

---

### 14. Describe a scenario where a while loop is more suitable than a for loop.

**Answer:**
While loops are better when:
1. Number of iterations is unknown
2. Loop depends on user input or external conditions
3. Need to continue until specific condition is met

**Example Scenarios:**
```python
# User input validation
while True:
    password = input("Enter password: ")
    if len(password) >= 8:
        break
    print("Password too short!")

# Game loop
while player_health > 0:
    play_game()

# Reading file until end
while data := file.read(1024):
    process(data)
```

---

## Practical Questions

### 1. Write a Python program to print "Hello, World!"

```python
print("Hello, World!")
```

**Output:**
```
Hello, World!
```

---

### 2. Write a Python program that displays your name and age.

```python
name = "Enosh RD"
age = 22

print(f"Name: {name}")
print(f"Age: {age}")

# Alternative
print("Name:", name)
print("Age:", age)
```

**Output:**
```
Name: Enosh RD
Age: 22
```

---

### 3. Write code to print all the pre-defined keywords in Python using the keyword library.

```python
import keyword

# Print all keywords
print("Python Keywords:")
print(keyword.kwlist)

# Count of keywords
print(f"\nTotal keywords: {len(keyword.kwlist)}")

# Print keywords line by line
print("\nKeywords:")
for kw in keyword.kwlist:
    print(kw)
```

**Output:**
```
Python Keywords:
['False', 'None', 'True', 'and', 'as', 'assert', 'async', 'await', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']

Total keywords: 35
```

---

### 4. Write a program that checks if a given word is a Python keyword.

```python
import keyword

def check_keyword(word):
    if keyword.iskeyword(word):
        print(f"'{word}' is a Python keyword")
    else:
        print(f"'{word}' is NOT a Python keyword")

# Test cases
check_keyword("if")
check_keyword("for")
check_keyword("variable")
check_keyword("print")

# User input version
user_word = input("Enter a word to check: ")
check_keyword(user_word)
```

**Output:**
```
'if' is a Python keyword
'for' is a Python keyword
'variable' is NOT a Python keyword
'print' is NOT a Python keyword
```

---

### 5. Create a list and tuple in Python, and demonstrate how attempting to change an element works differently for each.

```python
# Creating list and tuple
my_list = [1, 2, 3, 4, 5]
my_tuple = (1, 2, 3, 4, 5)

print("Original List:", my_list)
print("Original Tuple:", my_tuple)

# Modifying list (WORKS)
my_list[0] = 100
print("\nAfter modification:")
print("Modified List:", my_list)

# Attempting to modify tuple (FAILS)
try:
    my_tuple[0] = 100
except TypeError as e:
    print(f"Error modifying tuple: {e}")

# List is mutable
my_list.append(6)
my_list.remove(2)
print("\nFinal List:", my_list)

# Tuple is immutable
print("Tuple remains:", my_tuple)
```

**Output:**
```
Original List: [1, 2, 3, 4, 5]
Original Tuple: (1, 2, 3, 4, 5)

After modification:
Modified List: [100, 2, 3, 4, 5]
Error modifying tuple: 'tuple' object does not support item assignment

Final List: [100, 3, 4, 5, 6]
Tuple remains: (1, 2, 3, 4, 5)
```

---

### 6. Write a function to demonstrate the behavior of mutable and immutable arguments.

```python
def modify_immutable(num):
    """Demonstrates immutable behavior"""
    print(f"Inside function (before): {num}")
    num = num + 10
    print(f"Inside function (after): {num}")

def modify_mutable(lst):
    """Demonstrates mutable behavior"""
    print(f"Inside function (before): {lst}")
    lst.append(100)
    print(f"Inside function (after): {lst}")

# Test immutable
print("=== IMMUTABLE (int) ===")
x = 5
print(f"Before function call: {x}")
modify_immutable(x)
print(f"After function call: {x}")

print("\n=== MUTABLE (list) ===")
my_list = [1, 2, 3]
print(f"Before function call: {my_list}")
modify_mutable(my_list)
print(f"After function call: {my_list}")
```

**Output:**
```
=== IMMUTABLE (int) ===
Before function call: 5
Inside function (before): 5
Inside function (after): 15
After function call: 5

=== MUTABLE (list) ===
Before function call: [1, 2, 3]
Inside function (before): [1, 2, 3]
Inside function (after): [1, 2, 3, 100]
After function call: [1, 2, 3, 100]
```

---

### 7. Write a program that performs basic arithmetic operations on two user-input numbers.

```python
# Get user input
num1 = float(input("Enter first number: "))
num2 = float(input("Enter second number: "))

# Perform operations
addition = num1 + num2
subtraction = num1 - num2
multiplication = num1 * num2
division = num1 / num2 if num2 != 0 else "Cannot divide by zero"
floor_division = num1 // num2 if num2 != 0 else "Cannot divide by zero"
modulus = num1 % num2 if num2 != 0 else "Cannot divide by zero"
exponent = num1 ** num2

# Display results
print(f"\n{num1} + {num2} = {addition}")
print(f"{num1} - {num2} = {subtraction}")
print(f"{num1} * {num2} = {multiplication}")
print(f"{num1} / {num2} = {division}")
print(f"{num1} // {num2} = {floor_division}")
print(f"{num1} % {num2} = {modulus}")
print(f"{num1} ** {num2} = {exponent}")
```

**Output Example:**
```
Enter first number: 10
Enter second number: 3

10.0 + 3.0 = 13.0
10.0 - 3.0 = 7.0
10.0 * 3.0 = 30.0
10.0 / 3.0 = 3.3333333333333335
10.0 // 3.0 = 3.0
10.0 % 3.0 = 1.0
10.0 ** 3.0 = 1000.0
```

---

### 8. Write a program to demonstrate the use of logical operators.

```python
# Get user input
age = int(input("Enter your age: "))
has_license = input("Do you have a driving license? (yes/no): ").lower() == "yes"
has_car = input("Do you own a car? (yes/no): ").lower() == "yes"

print("\n=== Logical Operators Demo ===")

# AND operator
if age >= 18 and has_license:
    print("✓ You can drive (age >= 18 AND has license)")
else:
    print("✗ Cannot drive")

# OR operator
if has_license or age >= 21:
    print("✓ Eligible for car rental (has license OR age >= 21)")
else:
    print("✗ Not eligible for car rental")

# NOT operator
if not has_car:
    print("✓ You might need to buy a car")
else:
    print("✓ You already have a car")

# Complex condition
if age >= 18 and has_license and (has_car or True):
    print("✓ Can drive independently")

# Multiple conditions
if (age >= 18 and has_license) or age >= 21:
    print("✓ Meets basic requirements")
```

**Output Example:**
```
Enter your age: 20
Do you have a driving license? (yes/no): yes
Do you own a car? (yes/no): no

=== Logical Operators Demo ===
✓ You can drive (age >= 18 AND has license)
✓ Eligible for car rental (has license OR age >= 21)
✓ You might need to buy a car
✓ Can drive independently
✓ Meets basic requirements
```

---

### 9. Write a Python program to convert user input from string to integer, float, and boolean types.

```python
# Get string input
user_input = input("Enter a number: ")

print("\n=== Type Conversions ===")

# String to Integer
try:
    int_value = int(user_input)
    print(f"Integer: {int_value} (type: {type(int_value)})")
except ValueError:
    print("Cannot convert to integer")

# String to Float
try:
    float_value = float(user_input)
    print(f"Float: {float_value} (type: {type(float_value)})")
except ValueError:
    print("Cannot convert to float")

# String to Boolean
bool_value = bool(user_input)  # Empty string is False, any other string is True
print(f"Boolean: {bool_value} (type: {type(bool_value)})")

# Additional conversions
print("\n=== Additional Examples ===")
print(f"int('42') = {int('42')}")
print(f"float('3.14') = {float('3.14')}")
print(f"int(float('3.14')) = {int(float('3.14'))}")
print(f"bool('') = {bool('')}")
print(f"bool('hello') = {bool('hello')}")
print(f"bool(0) = {bool(0)}")
print(f"bool(1) = {bool(1)}")
```

**Output Example:**
```
Enter a number: 42

=== Type Conversions ===
Integer: 42 (type: <class 'int'>)
Float: 42.0 (type: <class 'float'>)
Boolean: True (type: <class 'bool'>)

=== Additional Examples ===
int('42') = 42
float('3.14') = 3.14
int(float('3.14')) = 3
bool('') = False
bool('hello') = True
bool(0) = False
bool(1) = True
```

---

### 10. Write code to demonstrate type casting with list elements.

```python
# Original list with mixed types
mixed_list = ['10', '20', '30', '40', '50']
print("Original list (strings):", mixed_list)
print("Type:", type(mixed_list[0]))

# Convert list elements to integers
int_list = [int(x) for x in mixed_list]
print("\nConverted to integers:", int_list)
print("Type:", type(int_list[0]))

# Convert list elements to floats
float_list = [float(x) for x in mixed_list]
print("\nConverted to floats:", float_list)
print("Type:", type(float_list[0]))

# Using map function
map_int_list = list(map(int, mixed_list))
print("\nUsing map to int:", map_int_list)

# Converting numeric list to strings
numeric_list = [1, 2, 3, 4, 5]
string_list = [str(x) for x in numeric_list]
print("\nNumeric to string:", string_list)

# Mixed conversions
mixed_data = ['10', '20.5', '30', '40.8']
converted = [int(float(x)) for x in mixed_data]
print("\nString -> Float -> Int:", converted)
```

**Output:**
```
Original list (strings): ['10', '20', '30', '40', '50']
Type: <class 'str'>

Converted to integers: [10, 20, 30, 40, 50]
Type: <class 'int'>

Converted to floats: [10.0, 20.0, 30.0, 40.0, 50.0]
Type: <class 'float'>

Using map to int: [10, 20, 30, 40, 50]

Numeric to string: ['1', '2', '3', '4', '5']

String -> Float -> Int: [10, 20, 30, 40]
```

---

### 11. Write a program that checks if a number is positive, negative, or zero.

```python
# Get user input
number = float(input("Enter a number: "))

# Check and display result
if number > 0:
    print(f"{number} is POSITIVE")
elif number < 0:
    print(f"{number} is NEGATIVE")
else:
    print(f"{number} is ZERO")

# Alternative using ternary operator
result = "POSITIVE" if number > 0 else "NEGATIVE" if number < 0 else "ZERO"
print(f"Result: {result}")
```

**Output Examples:**
```
Enter a number: 5
5.0 is POSITIVE
Result: POSITIVE

Enter a number: -3
-3.0 is NEGATIVE
Result: NEGATIVE

Enter a number: 0
0.0 is ZERO
Result: ZERO
```

---

### 12. Write a for loop to print numbers from 1 to 10.

```python
# Method 1: Using range
print("Method 1: Using range")
for i in range(1, 11):
    print(i, end=" ")

# Method 2: With list
print("\n\nMethod 2: With list")
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
for num in numbers:
    print(num, end=" ")

# Method 3: One line
print("\n\nMethod 3: All at once")
for i in range(1, 11):
    print(i)
```

**Output:**
```
Method 1: Using range
1 2 3 4 5 6 7 8 9 10 

Method 2: With list
1 2 3 4 5 6 7 8 9 10 

Method 3: All at once
1
2
3
4
5
6
7
8
9
10
```

---

### 13. Write a Python program to find the sum of all even numbers between 1 and 50.

```python
# Method 1: Using for loop with if
total = 0
for num in range(1, 51):
    if num % 2 == 0:
        total += num

print(f"Sum of even numbers (Method 1): {total}")

# Method 2: Using range with step
total2 = 0
for num in range(2, 51, 2):  # Start at 2, step by 2
    total2 += num

print(f"Sum of even numbers (Method 2): {total2}")

# Method 3: Using sum with list comprehension
total3 = sum([num for num in range(1, 51) if num % 2 == 0])
print(f"Sum of even numbers (Method 3): {total3}")

# Method 4: Using mathematical formula
# Sum of even numbers = n(n+1) where n is count of even numbers
total4 = sum(range(2, 51, 2))
print(f"Sum of even numbers (Method 4): {total4}")

# Display even numbers
print("\nEven numbers between 1 and 50:")
even_numbers = [num for num in range(1, 51) if num % 2 == 0]
print(even_numbers)
```

**Output:**
```
Sum of even numbers (Method 1): 650
Sum of even numbers (Method 2): 650
Sum of even numbers (Method 3): 650
Sum of even numbers (Method 4): 650

Even numbers between 1 and 50:
[2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30, 32, 34, 36, 38, 40, 42, 44, 46, 48, 50]
```

---

### 14. Write a program to reverse a string using a while loop.

```python
# Get user input
text = input("Enter a string to reverse: ")

# Method 1: Using while loop
reversed_text = ""
index = len(text) - 1

while index >= 0:
    reversed_text += text[index]
    index -= 1

print(f"Original: {text}")
print(f"Reversed: {reversed_text}")

# Method 2: Alternative while loop approach
print("\n=== Alternative Method ===")
text2 = "Hello World"
reversed_text2 = ""
i = 0

while i < len(text2):
    reversed_text2 = text2[i] + reversed_text2
    i += 1

print(f"Original: {text2}")
print(f"Reversed: {reversed_text2}")
```

**Output:**
```
Enter a string to reverse: Python

Original: Python
Reversed: nohtyP

=== Alternative Method ===
Original: Hello World
Reversed: dlroW olleH
```

---

### 15. Write a Python program to calculate the factorial of a number provided by the user using a while loop.

```python
# Get user input
num = int(input("Enter a number to calculate factorial: "))

# Validate input
if num < 0:
    print("Factorial is not defined for negative numbers")
elif num == 0:
    print("Factorial of 0 is 1")
else:
    # Calculate factorial using while loop
    factorial = 1
    counter = 1
    
    print(f"\nCalculating {num}! = ", end="")
    
    while counter <= num:
        factorial *= counter
        if counter < num:
            print(f"{counter} × ", end="")
        else:
            print(f"{counter} = {factorial}")
        counter += 1
    
    print(f"\nFactorial of {num} is {factorial}")

# Alternative method
print("\n=== Alternative Method ===")
n = 5
fact = 1
i = n

while i > 0:
    fact *= i
    i -= 1

print(f"Factorial of {n} is {fact}")
```

**Output:**
```
Enter a number to calculate factorial: 5

Calculating 5! = 1 × 2 × 3 × 4 × 5 = 120

Factorial of 5 is 120

=== Alternative Method ===
Factorial of 5 is 120
```

---

## Summary

This assignment covers:
- ✅ Python fundamentals and popularity
- ✅ Keywords and identifiers
- ✅ Mutability vs Immutability
- ✅ Type casting (implicit & explicit)
- ✅ Operators (logical, comparison, identity)
- ✅ Conditional statements (if, elif, else)
- ✅ Loops (for and while)
- ✅ 15 practical programs demonstrating concepts

**All questions answered with:**
- Concise theoretical explanations
- Working code examples
- Expected outputs
- Multiple approaches where applicable

---

**Prepared by:** Enosh RD  
**Course:** PW Skills Data Science with GenAI  
**Week:** 1 - Python Basics
