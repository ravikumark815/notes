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

### **List Comprehensions**

| Trick/Type | Purpose | Expression / Syntax | Example with Output | Output |
| :--------- | :------ | :------------------ | :------------------ | :----- |
| **Basic** | Creates a new list by transforming items from an iterable. | `[expr for item in iterable]` | `squares = [x*x for x in range(5)]` | `[0, 1, 4, 9, 16]` |
| **With Conditional Filtering** | Creates a list including only items that satisfy a condition. | `[expr for item in iterable if condition]` | `evens = [x for x in range(10) if x % 2 == 0]` | `[0, 2, 4, 6, 8]` |
| **Nested Loops (Flattening/Combinations)** | Simulates nested loops to process elements from multiple iterables or flatten nested lists. | `[expr for item1 in iterable1 for item2 in iterable2]` | `coords = [(x, y) for x in range(2) for y in range(3)]` | `[(0, 0), (0, 1), (0, 2), (1, 0), (1, 1), (1, 2)]` |
| **Nested with Conditions** | Combines nested iteration with conditional filtering on the inner loop. | `[expr for outer_item in outer_iterable for inner_item in inner_iterable if inner_condition]` | `matrix = [[1, 2], [3, 4]]; evens = [num for row in matrix for num in row if num % 2 == 0]` | `[2, 4]` |
| **Conditional Expression (if-else in expr)** | Applies different expressions based on a condition for each item. | `[expr_if_true if condition else expr_if_false for item in iterable]` | `parity_labels = ["Even" if x % 2 == 0 else "Odd" for x in range(5)]` | `['Even', 'Odd', 'Even', 'Odd', 'Even']` |
| **Using `zip()`** | Iterates over multiple iterables in parallel. | `[expr for item1, item2 in zip(iterable1, iterable2)]` | `l1 = [1, 2]; l2 = ['a', 'b']; combined = [f"{x}-{y}" for x, y in zip(l1, l2)]` | `['1-a', '2-b']` |
| **Using `enumerate()`** | Accesses both the index and value of items in an iterable. | `[expr for idx, item in enumerate(iterable)]` | `indexed_items = [f"Idx {i}: {val}" for i, val in enumerate(['A', 'B'])]` | `['Idx 0: A', 'Idx 1: B']` |

### **Dictionary Comprehensions**

| Trick/Type | Purpose | Expression / Syntax | Example with Output | Output |
| :--------- | :------ | :------------------ | :------------------ | :----- |
| **Basic** | Creates a new dictionary by defining key-value pairs from an iterable. | `{key_expr: value_expr for item in iterable}` | `dict_comp = {x: x*x for x in range(3)}` | `{0: 0, 1: 1, 2: 4}` |
| **With Conditional Filtering** | Creates a dictionary including only key-value pairs that satisfy a condition. | `{key_expr: value_expr for item in iterable if condition}` | `even_squares = {x: x*x for x in range(5) if x % 2 == 0}` | `{0: 0, 2: 4, 4: 16}` |
| **Swapping Keys and Values** | Creates a new dictionary by swapping the keys and values of an existing dictionary. | `{value: key for key, value in original_dict.items()}` | `original = {'a': 1, 'b': 2}; swapped = {v: k for k, v in original.items()}` | `{1: 'a', 2: 'b'}` |
| **Filtering a Dictionary** | Creates a new dictionary containing only specific items from an existing one based on a condition. | `{k: v for k, v in original_dict.items() if condition_on_k_or_v}` | `grades = {'A': 85, 'B': 92}; passed = {n: s for n, s in grades.items() if s >= 90}` | `{'B': 92}` |

### **Set Comprehensions**

| Trick/Type | Purpose | Expression / Syntax | Example with Output | Output |
| :--------- | :------ | :------------------ | :------------------ | :----- |
| **Basic** | Creates a new set, automatically ensuring unique elements, by transforming items from an iterable. | `{expr for item in iterable}` | `set_comp = {c for c in "hello"}` | `{'h', 'e', 'l', 'o'}` (order varies) |
| **With Conditional Filtering** | Creates a set including only unique items that satisfy a condition. | `{expr for item in iterable if condition}` | `unique_evens = {x for x in range(10) if x % 2 == 0 and x > 5}` | `{6, 8}` (order varies) |

### **Generator Expressions**

| Trick/Type | Purpose | Expression / Syntax | Example with Output | Output |
| :--------- | :------ | :------------------ | :------------------ | :----- |
| **Basic (Lazy Evaluation)** | Creates an *iterator* (a generator object) that yields values one by one on demand, rather than building the full sequence in memory. Ideal for large datasets. | `(expr for item in iterable if condition)` | `gen_exp = (x*x for x in range(3))` | `<generator object <genexpr> at 0x...>` |
| **Consumption (e.g., with `list()`, `next()`)** | Shows how to consume the values yielded by a generator expression. | `list(gen_expr_obj)` / `next(gen_expr_obj)` | `gen = (x for x in range(3)); first = next(gen); rest = list(gen)` | `first: 0, rest: [1, 2]` |
| **Direct Consumption (e.g., with `sum`, `max`)** | Can be passed directly to functions that consume iterators without explicit list conversion, maximizing memory efficiency. | `sum(expr for item in iterable)` | `total_sum_squares = sum(x*x for x in range(4))` | `14` |

### Important Considerations / Tricks

- Readability vs. Complexity: While powerful, overly complex comprehensions (e.g., deeply nested ones with multiple conditions) can reduce readability. Sometimes, traditional loops are clearer.

- Side Effects: Avoid putting expressions with side effects (e.g., print statements, modifying external variables) directly into comprehensions, as it can make code harder to debug and understand.

- Scope: The loop variable (e.g., 'x' in `[x for x in range(5)]`) is local to the comprehension in Python 3. It does not "leak" into the surrounding scope.

- Performance: Comprehensions are generally faster than explicit loops for equivalent operations because they are optimized at the C level.

## Strings

| Concept | Description | Example/Syntax |
| :---------- | :---------- | :--------------- |
| **Immutability** | Strings are immutable, meaning once created, their content cannot be changed. Operations like `replace()` return new strings. | `s = "hello"; s_new = s.replace('h', 'j'); print(s); print(s_new)`<br>Output:<br>`hello`<br>`jello` |
| **String Literals** | Strings can be defined using single, double, or triple quotes. | `'single quotes'`, `"double quotes"`, `"""multiline string"""` |
| **Raw Strings** | Prefix `r` before quote to treat backslashes `\` as literal characters, not escape sequences. Useful for regular expressions or Windows paths. | `path = r"C:\new\text.txt"; print(path)`<br>Output:<br>`C:\new\text.txt` |
| **Escape Sequences** | Special character combinations starting with `\` for non-printable characters or special formatting. | `\n` (newline), `\t` (tab), `\\` (literal backslash), `\'` (literal single quote) |
| **String Interning** | For short strings (and certain common ones), Python may reuse existing string objects for efficiency. | `s1 = "hello"; s2 = "hello"; print(s1 is s2)`<br>Output (often): `True` |
| **Unicode Support** | Python 3 strings are Unicode by default, handling a wide range of characters from different languages. | `s = "你好"; print(s)`<br>Output:<br>`你好` |

```python
s = "hello"

# Basic Access & Length
print("Original s:", s)
print("First char:", s[0])
print("Last char:", s[-1])
print("Slice (1:4):", s[1:4]) # 'ell'
print("Slice with step (::2):", s[::2]) # 'hlo'
print("Length:", len(s))

# Concatenation & Repetition
s_combined = "Hello" + " " + "World"
print("Concatenation:", s_combined) # 'Hello World'
s_repeated = "abc" * 3
print("Repetition:", s_repeated) # 'abcabcabc'

# Membership
print("'e' in s:", "e" in s) # True
print("'x' not in s:", "x" not in s) # True

# Basic String Methods (examples shown with print)
print("Uppercase:", s.upper()) # HELLO
print("Lowercase:", s.lower()) # hello
print("Title case:", "hello world".title()) # Hello World

# Replacement & Splitting
print("Replace 'l' with 'x':", s.replace("l", "x")) # hexxo
print("Split by 'e':", s.split("e")) # ['h', 'llo']

# Joining a list of strings
print("Join with '.':", ".".join(["a", "b", "c"])) # a.b.c

# Stripping whitespace
padded_s = "   Python is fun   "
print("Stripped:", padded_s.strip()) # 'Python is fun'

# Finding substrings
print("Find 'l':", s.find("l")) # 2 (first occurrence)
print("Find 'z':", s.find("z")) # -1 (not found)

# String formatting (f-strings - preferred Python 3.6+)
name = "Alice"
age = 30
print(f"Name: {name}, Age: {age}") # Name: Alice, Age: 30
print(f"Calculation: {2 * 3.5}") # Calculation: 7.0
```

### String Methods Reference

| Method | Description | Example | Output |
| :----- | :---------- | :------ | :------ |
| `len(s)` | Returns the length (number of characters) of the string. | `len("python")` | `6` |
| `s[index]` | Accesses character at a specific index (0-based). Supports negative indexing from end. | `"python"[0]` | `'p'` |
| `s[-1]` | Accesses the last character. | `"python"[-1]` | `'n'` |
| `s[start:end]` | Slices string from `start` up to (but not including) `end`. | `"python"[1:4]` | `'yth'` |
| `s[start:end:step]` | Slices with a step. Negative step reverses. | `"python"[::2]` | `'pto'` |
| `s[::-1]` | Reverses the string. | `"hello"[::-1]` | `'olleh'` |
| `s1 + s2` | Concatenates two strings. | `"Hello" + "World"` | `'HelloWorld'` |
| `s * n` | Repeats the string `n` times. | `"abc" * 2` | `'abcabc'` |
| `s.upper()` | Converts all characters to uppercase. | `"Hello".upper()` | `'HELLO'` |
| `s.lower()` | Converts all characters to lowercase. | `"WORLD".lower()` | `'world'` |
| `s.capitalize()` | Converts the first character to uppercase and the rest to lowercase. | `"hello world".capitalize()` | `'Hello world'` |
| `s.title()` | Converts the first character of each word to uppercase, and the rest to lowercase. | `"hello world".title()` | `'Hello World'` |
| `s.swapcase()` | Swaps case of all characters (upper to lower, lower to upper). | `"PyThOn".swapcase()` | `'pYtHoN'` |
| `s.strip([chars])` | Removes leading and trailing whitespace or specified characters. | ` "  hi  ".strip()` | `'hi'` |
| | | `",ab,c,".strip(',')` | `'ab,c'` |
| `s.lstrip([chars])` | Removes leading whitespace or specified characters. | ` "  hi  ".lstrip()` | `'hi  '` |
| `s.rstrip([chars])` | Removes trailing whitespace or specified characters. | ` "  hi  ".rstrip()` | `'  hi'` |
| `s.count(substring)` | Returns the number of non-overlapping occurrences of a substring. | `"banana".count("na")` | `2` |
| `s.find(substring[, start[, end]])` | Returns the lowest index where substring is found, or -1 if not found. | `"apple".find("pl")` | `1` |
| | | `"apple".find("z")` | `-1` |
| `s.index(substring[, start[, end]])` | Like `find()`, but raises `ValueError` if substring is not found. | `"apple".index("pp")` | `1` |
| | | ` "apple".index("z")` | `ValueError` |
| `s.rfind(substring[, start[, end]])` | Returns the highest index where substring is found, or -1. | `"banana".rfind("na")` | `4` |
| `s.rindex(substring[, start[, end]])` | Like `rfind()`, but raises `ValueError` if not found. | `"banana".rindex("an")` | `3` |
| `s.replace(old, new[, count])` | Returns a copy of the string with all occurrences of `old` replaced by `new`. `count` limits replacements. | `"hihi".replace("h","y")` | `'yiyi'` |
| | | `"hihi".replace("h","y",1)` | `'yihi'` |
| `s.split(delimiter[, maxsplit])` | Splits the string by `delimiter` into a list of substrings. If `delimiter` is not given, splits by whitespace. | `"a,b,c".split(",")` | `['a', 'b', 'c']` |
| | | `"a b c".split()` | `['a', 'b', 'c']` |
| | | `"a,b,c".split(",", 1)` | `['a', 'b,c']` |
| `s.rsplit(delimiter[, maxsplit])` | Splits from the right. | `"a,b,c".rsplit(",", 1)` | `['a,b', 'c']` |
| `s.partition(separator)` | Splits the string into a 3-tuple: (before, separator, after). | `"name=Alice".partition("=")` | `('name', '=', 'Alice')` |
| `s.rpartition(separator)` | Splits from the right into a 3-tuple. | `"a.b.c".rpartition(".")` | `('a.b', '.', 'c')` |
| `s.splitlines([keepends])` | Splits the string into a list of lines at line breaks. | `"a\nbc\n".splitlines()` | `['a', 'bc']` |
| `s.startswith(prefix[, start[, end]])` | Checks if string starts with `prefix`. | `"hello".startswith("he")` | `True` |
| `s.endswith(suffix[, start[, end]])` | Checks if string ends with `suffix`. | `"hello".endswith("lo")` | `True` |
| `s.isalpha()` | Returns `True` if all characters are alphabetic and string is not empty. | `"abc".isalpha()` | `True` |
| | | `"a1c".isalpha()` | `False` |
| `s.isdigit()` | Returns `True` if all characters are digits and string is not empty. | `"123".isdigit()` | `True` |
| | | `"1a3".isdigit()` | `False` |
| `s.isalnum()` | Returns `True` if all characters are alphanumeric (letters or numbers) and not empty. | `"abc12".isalnum()` | `True` |
| `s.isspace()` | Returns `True` if all characters are whitespace and string is not empty. | `"   ".isspace()` | `True` |
| `s.islower()` | Returns `True` if all cased characters are lowercase and there is at least one cased character. | `"hello".islower()` | `True` |
| `s.isupper()` | Returns `True` if all cased characters are uppercase and there is at least one cased character. | `"HELLO".isupper()` | `True` |
| `s.istitle()` | Returns `True` if string is titlecased (first letter of each word uppercase, others lowercase). | `"Hello World".istitle()` | `True` |
| `s.join(iterable)` | Concatenates elements of an iterable (e.g., list of strings) with the string as a separator. | `",".join(["a", "b", "c"])` | `'a,b,c'` |
| `s.ljust(width[, fillchar])` | Returns a left-justified string of given `width`. | `"hi".ljust(5, '-')` | `'hi---'` |
| `s.rjust(width[, fillchar])` | Returns a right-justified string of given `width`. | `"hi".rjust(5, '*')` | `'***hi'` |
| `s.center(width[, fillchar])` | Returns a center-justified string of given `width`. | `"hi".center(5, '=')` | `'=hi=='` |
| `s.zfill(width)` | Pads numeric string with zeros on the left to fill `width`. | `"25".zfill(4)` | `'0025'` |
| | | `"-25".zfill(5)` | `'-0025'` |

### String Formatting

| Method/Syntax | Description | Example | Output |
| :------------ | :---------- | :------ | :------ |
| **f-strings (Formatted String Literals)** | (Python 3.6+) Concise, readable way to embed expressions inside string literals. Most preferred. | `name="Bob"; age=25; print(f"Name: {name}, Age: {age:.1f}")` | `Name: Bob, Age: 25.0` |
| | | `print(f"{10/3:.2f}")` | `3.33` |
| **`.format()` Method** | (Older, but still common) Uses curly braces `{}` as placeholders. | `print("Name: {}, Age: {}".format("Alice", 30))` | `Name: Alice, Age: 30` |
| | | `print("Name: {name}, Age: {age}".format(name="Bob", age=25))` | `Name: Bob, Age: 25` |
| **`%` Operator (Printf-style)** | (Oldest, less common in modern Python) Uses `%s`, `%d`, etc., as placeholders. | `print("Name: %s, Age: %d" % ("Charlie", 22))` | `Name: Charlie, Age: 22` |

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