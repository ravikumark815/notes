# Python
## Preset
- Created by Guido van Rossum in 1990, Python 3 released in 2008
- Emphasizes readability and simplicity
- Official docs: [docs.python.org/3](https://docs.python.org/3)

## Table of Contents

- [Data Types](#data-types)
- [Variables, Assignment & Naming](#variables-assignment--naming)
- [Input/Output](#inputoutput)
- [Operators](#operators)
- [Control Flow](#control-flow)
- [Functions](#functions)
- [Comprehensions](#comprehensions)
- [Strings](#strings)
- [Lists](#lists)
- [Tuples](#tuples)
- [Dictionaries](#dictionaries)
- [Sets](#sets)
- [None & Booleans](#none--booleans)
- [Type Conversion](#type-conversion)
- [Exception Handling](#exception-handling)
- [File I/O](#file-io)
- [Modules & Imports](#modules--imports)
- [Classes & OOP](#classes--oop)
- [Common Built-in Functions](#common-built-in-functions)
- [Common Libraries & Modules](#common-libraries--modules)
- [Virtual Environments & Pip](#virtual-environments--pip)
- [Handy Tricks](#handy-tricks)
- [What's New (3.x Highlights)](#whats-new-3x-highlights)
- [Further Resources](#further-resources)

## Data Types

| Name             | Type       | Description                                          | Examples                                     |
| :--------------- | :--------- | :--------------------------------------------------- | :--------------------------------------------|
| Integer          | `int`      | Whole numbers                                        | `3`, `300`, `-200`                           |
| Floating point   | `float`    | Decimal numbers                                      | `2.3`, `4.6`, `100.0`                        |
| String           | `str`      | Ordered sequence of characters                       | `"hello"`, `'John'`                          |
| List             | `list`     | Ordered, mutable sequence of objects                 | `[10, "hello", 200.3]`                       |
| Dictionary       | `dict`     | Unordered collection of key-value pairs              | `{"k1": "v1", "k2": 10}`                     |
| Tuple            | `tuple`    | Ordered, immutable sequence of objects               | `(10, "hello", 2.3)`                         |
| Set              | `set`      | Unordered collection of unique objects               | `{"a", "b"}`                                 |
| Frozenset        | `frozenset`| Immutable version of a set                           | `frozenset({"a", "b"})`                      |
| Boolean          | `bool`     | Logical values representing True or False            | `True`, `False`                              |
| NoneType         | `NoneType` | Represents the absence of a value or a null value    | `None`                                       |
| Complex Number   | `complex`  | Numbers with a real and an imaginary part            | `3+5j`, `2.5-1.2j`                           |
| Bytes            | `bytes`    | Immutable sequence of single byte values (0-255)     | `b'hello'`, `bytes([65, 66])`                |
| Bytearray        | `bytearray`| Mutable sequence of single byte values (0-255)       | `bytearray(b'hello')`, `bytearray([65, 66])` |
| Range            | `range`    | Immutable sequence of numbers, often used for looping| `range(5)`, `range(1, 10, 2)`                |

## Variables, Assignment & Naming

```python
x = 5
my_name = "Alice"
PI = 3.14159
a, b, c = 1, 2, 3
x, y = y, x  # swap
```
- Use `snake_case` for variables.
- Constants are uppercase by convention, but not enforced.

## Input/Output

```python
name = input("Enter your name: ")
age_str = input("Enter your age: ")
age_int = int(age_str) # Converting input string to an integer

# Basic Output
print("Hello,", name)
print(f"Hello, {name}!") # f-strings (Py3.6+)
print("Sum:", 2 + 2, sep=" | ", end=" :) \n")

# Controlling Output
print("Line 1", end=" ") # Prevent newline, useful for printing on the same line
print("Line 2")
print("Item1", "Item2", "Item3", sep=", ") # Custom separator between arguments

# Printing to Standard Error (for error messages)
import sys
print("This is an error message.", file=sys.stderr)
```

## Operators

| Type       | Operators                                                |
|------------|---------------------------------------------------------|
| Arithmetic | `+`, `-`, `*`, `/`, `//` (floor), `%`, `**` (power)     |
| Comparison | `==`, `!=`, `<`, `>`, `<=`, `>=`                        |
| Logical    | `and`, `or`, `not`                                      |
| Membership | `in`, `not in`                                          |
| Identity   | `is`, `is not`                                          |
| Bitwise    | `&`, `|`, `^`, `~`, `<<`, `>>`                          |
| Assignment | `=`, `+=`, `-=`, `*=`, `/=`, `%=`, `//=`, `**=`         |

## Control Flow

```python
x = 10
if x > 5:
    print("Greater")
elif x == 5:
    print("Equal")
else:
    print("Less")

for i in range(3):
    print(i)

while x > 0:
    x -= 1

# Loop Constructs
for i in range(3):
    print(i)

while x > 0:
    x -= 1

# Loop with else
for item in [1, 2, 3]:
    print(item)
else:
    print("Loop ended")  # This runs if the loop completes without a 'break'

# Loop Control Statements
for i in range(5):
    if i == 2:
        continue # Skips current iteration
    if i == 4:
        break    # Exits loop entirely
    print(i)

# Structural Pattern Matching (Python 3.10+)
status_code = 200
match status_code:
    case 200:
        print("OK")
    case 404:
        print("Not Found")
    case 500:
        print("Server Error")
    case _:
        print("Unknown Status")
```

## Functions

```python
def add(a, b=0):
    return a + b

def multi_return():
    return 1, 2, 3 # packed into a tuple

# Arbitrary Arguments (*args and **kwargs)
def var_args(*args, **kwargs):
    print(f"Positional arguments (args): {args}") # tuple
    print(f"Keyword arguments (kwargs): {kwargs}") # dictionary

# Lambda
square = lambda x: x * x
print(f"Lambda square(5): {square(5)}")

def greet(name: str) -> str:
    # Adds type hints for parameters and return value.
    return f"Hello, {name}!"

# Nested Functions
def outer_function(msg):
    def inner_function():
        print(msg)
    return inner_function

# Generators (using 'yield') - for lazy evaluation/memory efficiency
def fibonacci_sequence(n):
    a, b = 0, 1
    count = 0
    while count < n:
        yield a # Pauses execution and returns 'a', resumes from here next time
        a, b = b, a + b
        count += 1

# Function Attributes (rarely used, but possible)
def count_calls():
    # counter counts the number of times the function is called
    count_calls.counter += 1
    print(f"Function called {count_calls.counter} times.")

# Call
print(f"add(3, 4): {add(3, 4)}")
print(f"add(5): {add(5)}") # Using default argument
x, y, z = multi_return() # Unpacking multiple return values
print(f"multi_return unpacked: x={x}, y={y}, z={z}")
```

## Generators

- Functions that can be paused and resumed, producing a sequence of values lazily.
- They use the `yield` keyword instead of `return`.
- When to use?
    1. Memory efficiency: When dealing with very large datasets or infinite sequences, generators produce values one at a time, keeping only the current state in memory.
    2. Performance: Avoids computing all results upfront if only a few are needed.
    3. Readability: Can make code cleaner for sequence generation.

```python
def count_up_to(n):
    # A simple generator that yields numbers from 0 up to (but not including) n."""
    i = 0
    while i < n:
        yield i # Pauses here, returns 'i', and remembers its state for the next call
        i += 1

my_generator = count_up_to(5) # This creates a generator object, doesn't run the code yet

print(f"Type of my_generator: {type(my_generator)}") # Output: <class 'generator'>

# Iterating over the generator (each next() call resumes from the last yield)
print(next(my_generator)) # Output: 0
print(next(my_generator)) # Output: 1

for num in my_generator: # Continues from where it left off (2, 3, 4)
    print(num)
```

## Decorators

- A design pattern that allows you to add new functionality to an existing function or method without modifying its structure. They are essentially "wrappers" that execute code before and/or after the wrapped function.
- How do they work? A decorator is a function that takes another function as an argument, extends its behavior, and returns a new (or modified) function.
- Key points:
    - Functions are First-Class Objects: They can be passed as arguments and returned from other functions.
    - Closure: The `wrapper` function "remembers" the `func` from its enclosing scope.
    - `@syntax`: Just a cleaner way to apply decorators.
    - Use Cases: Logging, timing, authentication, caching, validation, framework routing.

```python
# Simple Logging Decorator
def log_function_call(func):
    """
    A decorator that logs when the decorated function is called
    and what its return value is.
    """
    def wrapper(*args, **kwargs):
        print(f"--- Calling function: {func.__name__} ---")
        result = func(*args, **kwargs) # Execute the original function
        print(f"--- Function {func.__name__} finished. Result: {result} ---")
        return result
    return wrapper

@log_function_call # This is equivalent to: `add_numbers = log_function_call(add_numbers)`
def add_numbers(a, b):
    print("Inside add_numbers function.")
    return a + b

sum_result = add_numbers(10, 5)
print(f"Sum result outside decorator: {sum_result}")

# # --- Calling function: add_numbers ---
# Inside add_numbers function.
# --- Function add_numbers finished. Result: 15 ---
# Sum result outside decorator: 15
```

## Comprehensions

```python
squares = [x*x for x in range(5)]
evens = [x for x in range(10) if x % 2 == 0]
dict_comp = {x: x*x for x in range(5)}
set_comp = {c for c in "hello"}
```

## Strings

```python
s = "hello"
print(s.upper(), s.lower(), s.title())
print(s[0], s[-1], s[1:4])
print("len:", len(s))
print("a" in s)
print(s.replace("l", "x"))
print(s.split("e"))
print(".".join(["a", "b", "c"]))
```

| Method         | Description                     | Example                   |
|----------------|--------------------------------|---------------------------|
| `s.upper()`    | Uppercase                      | `"hi".upper()` → `"HI"`   |
| `s.lower()`    | Lowercase                      | `"Hi".lower()` → `"hi"`   |
| `s.title()`    | Title case                     | `"hi there".title()`      |
| `s.strip()`    | Trim whitespace                | `" hi ".strip()`          |
| `s.find("x")`  | First index or -1              | `"abc".find("b")`         |
| `s.replace()`  | Replace substring              | `"hi".replace("h","y")`   |
| `s.split()`    | Split by delimiter             | `"a,b".split(",")`        |
| `s.join()`     | Join iterable                  | `",".join(["a","b"])`     |

## Lists

```python
lst = [1, 2, "a"]
lst.append(4)
lst.insert(1, "b")
lst.remove("a")
item = lst.pop()
lst[0] = 99
print(lst[:2], lst[::-1])
```

| Method         | Description                  |
|----------------|-----------------------------|
| `append(x)`    | Add to end                  |
| `insert(i,x)`  | Insert at index             |
| `remove(x)`    | Remove first occurrence     |
| `pop([i])`     | Remove & return (default last)|
| `sort()`       | Sort in-place               |
| `reverse()`    | Reverse in-place            |
| `extend(iter)` | Extend list                 |
| `count(x)`     | Count occurrences           |

## Tuples

- Immutable, can unpack

```python
t = (1, "a", 3.5)
x, y, z = t
```

## Dictionaries

```python
d = {"a": 1, "b": 2}
d["c"] = 3
del d["a"]
for k, v in d.items():
    print(k, v)
```

| Method         | Description                  |
|----------------|-----------------------------|
| `keys()`       | Keys view                   |
| `values()`     | Values view                 |
| `items()`      | (key, value) pairs          |
| `get(k, [d])`  | Value or default            |
| `pop(k)`       | Remove and return value     |
| `update(d2)`   | Update with another dict    |

## Sets

```python
s = {1, 2, 3}
s.add(4)
s.remove(2)
print(1 in s, 99 not in s)
```

| Method         | Description                  |
|----------------|-----------------------------|
| `add(x)`       | Add x                       |
| `remove(x)`    | Remove x                    |
| `discard(x)`   | Remove if exists            |
| `pop()`        | Remove & return elem        |
| `union(other)` | Union                       |
| `intersection(other)` | Intersection         |

## None & Booleans

- `None` is Python's null value.
- Boolean logic: `True`, `False`
- Falsy: `None`, `0`, `0.0`, `''`, `[]`, `{}`, `set()`, `False`

## Type Conversion

```python
int("123"), float("3.14"), str(123), list("abc")
dict([("a",1),("b",2)]), set([1,2,2,3])
tuple([1,2,3]), list((4,5,6))
```

## Exception Handling

```python
try:
    result = 10 / 0
except ZeroDivisionError as e:
    print("Error:", e)
except Exception:
    print("Other error")
else:
    print("No error")
finally:
    print("Always runs")
```

## File I/O

```python
with open("out.txt", "w") as f:
    f.write("Hi!\n")
with open("out.txt") as f:
    for line in f:
        print(line.strip())
```

## Modules & Imports

```python
import math
from collections import Counter
from os.path import join as pathjoin

print(math.sqrt(16))
print(Counter("hello"))
print(pathjoin("a", "b.txt"))
```

## Classes & OOP

```python
class Dog:
    def __init__(self, name):
        self.name = name
    def speak(self):
        print(f"{self.name} says woof!")

d = Dog("Buddy")
d.speak()
```

- All methods have `self` as first parameter.
- Inherit: `class Poodle(Dog): ...`
- `super().__init__()` to call base class constructor.
- Dunder methods: `__str__`, `__repr__`, `__len__`, etc. for customizing behavior.

## Common Built-in Functions

| Function     | Description                        |
|--------------|------------------------------------|
| `len(x)`     | Length                             |
| `type(x)`    | Type of object                     |
| `isinstance(x, T)` | Type check                   |
| `range(n)`   | Range iterator                     |
| `enumerate(x)` | (index, value) pairs             |
| `zip(a, b)`  | Pair elements                     |
| `map(f, it)` | Apply function                    |
| `filter(f, it)` | Filter values                   |
| `sum(x)`     | Sum elements                      |
| `min(x)`, `max(x)`| Min/Max                       |
| `sorted(x)`  | Sorted list                       |
| `reversed(x)`| Reverse iterator                  |
| `any(x)`, `all(x)`| Boolean check                |

## Common Libraries & Modules

- `os`, `sys`, `math`, `random`, `datetime`, `time`, `collections`, `itertools`, `functools`, `re`, `json`, `csv`, `argparse`, `subprocess`, `threading`, `multiprocessing`, `unittest`, `logging`, `http.server`, `socket`, `asyncio`

## Virtual Environments & Pip

```bash
python3 -m venv env
source env/bin/activate
pip install requests
pip freeze > requirements.txt
```
- Use [pip](https://pip.pypa.io/) to install packages from PyPI.

## Handy Tricks

| Trick                         | Example / Code Snippet                                  | Output/Explanation                                           |
|-------------------------------|--------------------------------------------------------|-------------------------------------------------------------|
| Swap two variables            | `a, b = b, a`                                          | Swaps values of `a` and `b`                                 |
| Multiple assignment           | `x, y, z = 1, 2, 3`                                    | Assigns 1→x, 2→y, 3→z                                       |
| Unpack with *rest             | `a, *rest = [1, 2, 3, 4]`                              | `a=1`, `rest=[2,3,4]`                                       |
| Ternary (inline if-else)      | `x = "yes" if cond else "no"`                          | Assigns `"yes"` if `cond` is True, else `"no"`              |
| Enumerate with index          | `for idx, val in enumerate(['a','b']):`                | idx=0,val='a'; idx=1,val='b'                                |
| List flattening               | `[y for x in [[1,2],[3]] for y in x]`                  | `[1,2,3]`                                                   |
| Dict invert                   | `{v: k for k, v in d.items()}`                         | Swaps keys and values                                       |
| Chained comparison            | `1 < x < 10`                                           | True if `x` in (1,10)                                       |
| Input as int                  | `n = int(input())`                                     | Reads integer from input                                    |
| Slicing with step             | `s[::2]`                                               | Every second character                                      |
| Reverse string/list           | `s[::-1]`                                              | Reverses `s`                                                |
| FizzBuzz one-liner            | `["FizzBuzz" if i%15==0 else "Fizz" if i%3==0 else "Buzz" if i%5==0 else i for i in range(1,16)]` | FizzBuzz logic in a list                                    |
| Repeat string/list            | `['a'] * 4`                                            | `['a', 'a', 'a', 'a']`                                      |
| Merge two dicts (3.5+)        | `{**d1, **d2}`                                         | Merges dictionaries d1 and d2                               |
| Counter for frequencies       | `from collections import Counter; Counter("hello")`    | `{'l':2,'h':1,'e':1,'o':1}`                                 |
| Most common in list           | `max(lst, key=lst.count)`                              | Most frequent element in lst                                |
| Sort by key in dict           | `sorted(d.items(), key=lambda x:x[1])`                 | Sort dict by values                                         |
| Get unique & sorted           | `sorted(set([3,1,2,3]))`                               | `[1,2,3]`                                                   |
| All combinations (itertools)  | `from itertools import permutations; list(permutations([1,2,3]))` | All permutations of list                                    |
| Transpose matrix              | `list(zip(*matrix))`                                   | Transposes 2D matrix/list                                   |
| Read entire file as string    | `with open('f.txt') as f: data = f.read()`             | Reads all file content at once                              |
| Print without newline         | `print('hi', end='')`                                  | Prints "hi" without newline                                 |
| Ignore value (dummy var)      | `_, y = (1, 2)`                                        | Common idiom for unused vars                                |

**Example: Dict Invert and Flatten**

```python
d = {'a': 1, 'b': 2}
inv = {v: k for k, v in d.items()}
print(inv)  # {1: 'a', 2: 'b'}

lst = [[1,2],[3,4]]
flat = [item for sub in lst for item in sub]
print(flat)  # [1,2,3,4]
```

## Further Resources

- [Official Python 3 Docs](https://docs.python.org/3)
- [Real Python](https://realpython.com/)
- [The Python Tutorial](https://docs.python.org/3/tutorial/)
- [Awesome Python](https://awesome-python.com/)