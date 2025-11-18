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
- [Generators](#generators)
- [Decorators](#decorators)
- [Comprehensions](#comprehensions)
- [Strings](#strings)
- [Lists](#lists)
- [Tuples](#tuples)
- [Dictionaries](#dictionaries)
- [Sets](#sets)
- [Frozen Sets](#frozen-sets)
- [Bytearray](#bytearray)
- [Collections Module](#collections-module)
  - [OrderedDict](#ordereddict)
  - [DefaultDict](#defaultdict)
  - [ChainMap](#chainmap)
  - [Deque](#deque)
  - [UserDict, UserList, UserString](#userdict-userlist-userstring)
- [Data Structures](#data-structures)
  - [Stack](#stack)
  - [Queue](#queue)
  - [Priority Queue](#priority-queue)
  - [Linked List](#linked-list)
  - [Binary Tree](#binary-tree)
  - [Graph](#graph)
- [None & Booleans](#none--booleans)
- [Type Conversion](#type-conversion)
- [Exception Handling](#exception-handling)
- [File I/O](#file-io)
- [Modules & Imports](#modules--imports)
- [Classes & OOP](#classes--oop)
- [Concurrency & Async Programming](#concurrency--async-programming)
  - [Threading](#threading)
  - [Multiprocessing](#multiprocessing)
  - [Asyncio](#asyncio)
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

### **Generator Expressions**

| Trick/Type | Purpose | Expression / Syntax | Example with Output | Output |
| :--------- | :------ | :------------------ | :------------------ | :----- |
| **Basic (Lazy Evaluation)** | Creates an *iterator* (a generator object) that yields values one by one on demand, rather than building the full sequence in memory. Ideal for large datasets. | `(expr for item in iterable if condition)` | `gen_exp = (x*x for x in range(3))` | `<generator object <genexpr> at 0x...>` |
| **Consumption (e.g., with `list()`, `next()`)** | Shows how to consume the values yielded by a generator expression. | `list(gen_expr_obj)` / `next(gen_expr_obj)` | `gen = (x for x in range(3)); first = next(gen); rest = list(gen)` | `first: 0, rest: [1, 2]` |
| **Direct Consumption (e.g., with `sum`, `max`)** | Can be passed directly to functions that consume iterators without explicit list conversion, maximizing memory efficiency. | `sum(expr for item in iterable)` | `total_sum_squares = sum(x*x for x in range(4))` | `14` |

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

| Method            | Description                                                                                          | Example                               | Output              |
| :---------------- | :--------------------------------------------------------------------------------------------------- | :------------------------------------ | :------------------ |
| `len(s)`          | Returns the length (number of characters) of the string.                                             | `len("python")`                       | `6`                 |
| `s[index]`        | Accesses character at a specific index (0-based). Supports negative indexing from end.               | `"python"[0]`                         | `'p'`               |
| `s[-1]`           | Accesses the last character.                                                                         | `"python"[-1]`                        | `'n'`               |
| `s[start:end]`    | Slices string from `start` up to (but not including) `end`.                                          | `"python"[1:4]`                       | `'yth'`             |
| `s[start:end:step]`| Slices with a step. Negative step reverses.                                                         | `"python"[::2]`                       | `'pto'`             |
| `s[::-1]`         | Reverses the string.                                                                                 | `"hello"[::-1]`                       | `'olleh'`           |
| `s1 + s2`         | Concatenates two strings.                                                                            | `"Hello" + "World"`                   | `'HelloWorld'`      |
| `s * n`           | Repeats the string `n` times.                                                                        | `"abc" * 2`                           | `'abcabc'`          |
| `s.upper()`       | Converts all characters to uppercase.                                                                | `"Hello".upper()`                     | `'HELLO'`           |
| `s.lower()`       | Converts all characters to lowercase.                                                                | `"WORLD".lower()`                     | `'world'`           |
| `s.capitalize()`  | Converts the first character to uppercase and the rest to lowercase.                                 | `"hello world".capitalize()`          | `'Hello world'`     |
| `s.title()`       | Converts the first character of each word to uppercase, and the rest to lowercase.                   | `"hello world".title()`               | `'Hello World'`     |
| `s.swapcase()`    | Swaps case of all characters (upper to lower, lower to upper).                                       | `"PyThOn".swapcase()`                 | `'pYtHoN'`          |
| `s.strip([chars])`| Removes leading and trailing whitespace or specified characters.                                     | `"  hi  ".strip()`                    | `'hi'`              |
|                   |                                                                                                      | `",ab,c,".strip(',')`                 | `'ab,c'`            |
| `s.lstrip([chars])`| Removes leading whitespace or specified characters.                                                 | `"  hi  ".lstrip()`                   | `'hi  '`            |
| `s.rstrip([chars])`| Removes trailing whitespace or specified characters.                                                | `"  hi  ".rstrip()`                   | `'  hi'`            |
| `s.count(substring)`| Returns the number of non-overlapping occurrences of a substring.                                  | `"banana".count("na")`                | `2`                 |
| `s.find(substring[, start[, end]])` | Returns the lowest index where substring is found, or -1 if not found.             | `"apple".find("pl")`                  | `1`                 |
|                   |                                                                                                      | `"apple".find("z")`                   | `-1`                |
| `s.index(substring[, start[, end]])`| Like `find()`, but raises `ValueError` if substring is not found.                  | `"apple".index("pp")`                 | `1`                 |
|                   |                                                                                                      | `"apple".index("z")`                  | `ValueError`        |
| `s.rfind(substring[, start[, end]])` | Returns the highest index where substring is found, or -1.                        | `"banana".rfind("na")`                | `4`                 |
| `s.rindex(substring[, start[, end]])`| Like `rfind()`, but raises `ValueError` if not found.                             | `"banana".rindex("an")`               | `3`                 |
| `s.replace(old, new[, count])`| Returns a copy of the string with all occurrences of `old` replaced by `new`. `count` limits replacements. | `"hihi".replace("h","y")` | `'yiyi'`      |
|                                     |                                                                                    | `"hihi".replace("h","y",1)`           | `'yihi'`            |
| `s.split(delimiter[, maxsplit])`| Splits the string by `delimiter` into a list of substrings. Default `delimiter` is whitespace | `"a,b,c".split(",")`           | `['a', 'b', 'c']`|
|                                     |                                                                                    | `"a b c".split()`                     | `['a', 'b', 'c']`   |
|                                     |                                                                                    | `"a,b,c".split(",", 1)`               | `['a', 'b,c']`      |
| `s.rsplit(delimiter[, maxsplit])`   | Splits from the right.                                                             | `"a,b,c".rsplit(",", 1)`              | `['a,b', 'c']`      |
| `s.partition(separator)`            | Splits the string into a 3-tuple: (before, separator, after).                      | `"name=Alice".partition("=")`         | `('name', '=', 'Alice')`|
| `s.rpartition(separator)`           | Splits from the right into a 3-tuple.                                              | `"a.b.c".rpartition(".")`             | `('a.b', '.', 'c')` |
| `s.splitlines([keepends])`          | Splits the string into a list of lines at line breaks.                             | `"a\nbc\n".splitlines()`              | `['a', 'bc']`       |
| `s.startswith(prefix[, start[, end]])`| Checks if string starts with `prefix`.                                           | `"hello".startswith("he")`            | `True`              |
| `s.endswith(suffix[, start[, end]])`| Checks if string ends with `suffix`.                                               | `"hello".endswith("lo")`              | `True`              |
| `s.isalpha()`                       | Returns `True` if all characters are alphabetic and string is not empty.           | `"abc".isalpha()`                     | `True`              |
|                                     |                                                                                    | `"a1c".isalpha()`                     | `False`             |
| `s.isdigit()`                       | Returns `True` if all characters are digits and string is not empty.               | `"123".isdigit()`                     | `True`              |
|                                     |                                                                                    | `"1a3".isdigit()`                     | `False`             |
| `s.isalnum()`                       | Returns `True` if all characters are alphanumeric and not empty.                   | `"abc12".isalnum()`                   | `True`              |
| `s.isspace()`                       | Returns `True` if all characters are whitespace and string is not empty.           | `"   ".isspace()`                     | `True`              |
| `s.islower()`                       | Returns `True` if all cased characters are lowercase                               | `"hello".islower()`                   | `True`              |
| `s.isupper()`                       | Returns `True` if all cased characters are uppercase                               | `"HELLO".isupper()`                   | `True`              |
| `s.istitle()`                       | Returns `True` if string is titlecased (first letter of each word uppercase)       | `"Hello World".istitle()`             | `True`              |
| `s.join(iterable)`                  | Concatenates elements of an iterable with the string as separator                  | `",".join(["a", "b", "c"])`           | `'a,b,c'`           |
| `s.ljust(width[, fillchar])`        | Returns a left-justified string of given `width`.                                  | `"hi".ljust(5, '-')`                  | `'hi---'`           |
| `s.rjust(width[, fillchar])`        | Returns a right-justified string of given `width`.                                 | `"hi".rjust(5, '*')`                  | `'***hi'`           |
| `s.center(width[, fillchar])`       | Returns a center-justified string of given `width`.                                | `"hi".center(5, '=')`                 | `'=hi=='`           |
| `s.zfill(width)`                    | Pads numeric string with zeros on the left to fill `width`.                        | `"25".zfill(4)`                       | `'0025'`            |
|                                     |                                                                                    | `"-25".zfill(5)`                      | `'-0025'`           |

### String Formatting

| Method/Syntax | Description | Example | Output |
| :------------ | :---------- | :------ | :------ |
| **f-strings (Formatted String Literals)** | (Python 3.6+) Concise, readable way to embed expressions inside string literals. Most preferred. | `name="Bob"; age=25; print(f"Name: {name}, Age: {age:.1f}")` | `Name: Bob, Age: 25.0` |
| | | `print(f"{10/3:.2f}")` | `3.33` |
| **`.format()` Method** | (Older, but still common) Uses curly braces `{}` as placeholders. | `print("Name: {}, Age: {}".format("Alice", 30))` | `Name: Alice, Age: 30` |
| | | `print("Name: {name}, Age: {age}".format(name="Bob", age=25))` | `Name: Bob, Age: 25` |
| **`%` Operator (Printf-style)** | (Oldest, less common in modern Python) Uses `%s`, `%d`, etc., as placeholders. | `print("Name: %s, Age: %d" % ("Charlie", 22))` | `Name: Charlie, Age: 22` |

### T-Strings (Template Strings) - Python 3.14+

T-strings are a new feature in Python 3.14 that provide safer string templating by allowing you to intercept and transform input values before combining them into a final string. Unlike f-strings which produce a `str` object, t-strings resolve to a `Template` instance.

| Feature | Description | Example |
|---------|-------------|---------|
| **Basic Syntax** | Use `t` or `T` prefix instead of `f` | `t"Hello, {name}!"` |
| **Template Object** | Returns `Template` instance, not string | `template = t"Value: {x}"; type(template)` → `<class 'Template'>` |
| **Security** | Safer for untrusted input - prevents code injection | Ideal for SQL queries, HTML templates |
| **Components Access** | Access static strings and interpolations separately | `template.strings`, `template.interpolations`, `template.values` |

```python
# Basic t-string usage
name = "Alice"
age = 30
template = t"Hello, {name}! You are {age} years old."

print(f"Type: {type(template)}")  # <class 'Template'>
print(f"Strings: {template.strings}")  # ('Hello, ', '! You are ', ' years old.')
print(f"Values: {template.values}")    # ('Alice', 30)

# Processing t-string components
def process_template(template):
    result = []
    for item in template:
        if isinstance(item, str):
            result.append(item.upper())  # Transform static strings
        else:  # Interpolation object
            result.append(f"[{item.value}]")  # Transform values
    return "".join(result)

processed = process_template(t"Hello {name}, welcome!")
print(processed)  # "HELLO [Alice], WELCOME!"

# Safe SQL query building
def safe_sql_query(template):
    query_parts = []
    params = []
    
    for item in template:
        if isinstance(item, str):
            query_parts.append(item)
        else:
            query_parts.append("?")  # Placeholder for parameter
            params.append(item.value)
    
    return "".join(query_parts), params

# Usage for SQL safety
username = "john_doe"
query, params = safe_sql_query(t"SELECT * FROM users WHERE name = {username}")
print(f"Query: {query}")    # "SELECT * FROM users WHERE name = ?"
print(f"Params: {params}")  # ['john_doe']

# HTML escaping example
import html

def safe_html_template(template):
    result = []
    for item in template:
        if isinstance(item, str):
            result.append(item)
        else:
            # Escape HTML in user input
            escaped_value = html.escape(str(item.value))
            result.append(escaped_value)
    return "".join(result)

user_input = "<script>alert('xss')</script>"
safe_html = safe_html_template(t"<p>User said: {user_input}</p>")
print(safe_html)  # <p>User said: &lt;script&gt;alert('xss')&lt;/script&gt;</p>

# Template reuse with functions
def create_greeting_template(name, time_of_day):
    return t"Good {time_of_day}, {name}! How are you today?"

# Lazy evaluation - template created but not processed until needed
morning_template = create_greeting_template("Bob", "morning")
evening_template = create_greeting_template("Alice", "evening")

# Convert template to string when needed
def template_to_string(template):
    result = []
    for item in template:
        if isinstance(item, str):
            result.append(item)
        else:
            # Apply formatting if specified
            value = item.value
            if item.format_spec:
                value = format(value, item.format_spec)
            result.append(str(value))
    return "".join(result)

print(template_to_string(morning_template))   # "Good morning, Bob! How are you today?"
print(template_to_string(evening_template))   # "Good evening, Alice! How are you today?"

# Advanced: Interpolation attributes
price = 19.99
template = t"Price: ${price:.2f}"
interpolation = template.interpolations[0]

print(f"Expression: {interpolation.expression}")    # "price"
print(f"Value: {interpolation.value}")              # 19.99
print(f"Format spec: {interpolation.format_spec}")  # ".2f"
print(f"Conversion: {interpolation.conversion}")    # None

# Self-documenting t-strings (like f-strings)
debug_template = t"Debug: {price = :.2f}"
print(debug_template.interpolations[0].conversion)  # 'r'

# Raw t-strings (prevent escape sequence interpretation)
path_template = rt"File path: {filename}\n"  # \n treated literally
```

## Lists

```python
# Initial list
my_list = [1, 2, "a", "b", 4]
print(f"Original list: {my_list}")

# --- Methods in action ---
# Adding elements
my_list.append(5)
my_list.extend([6, 7])

# Inserting at a specific position
my_list.insert(2, "new")

# Removing elements
my_list.remove("a")
popped_item = my_list.pop(1) # pop() removes item at index 1

print(f"After modifications: {my_list}")
print(f"Item popped: {popped_item}")

# Sorting and reversing
numbers = [3, 1, 4, 1, 5, 9]
numbers.sort()
print(f"Sorted list: {numbers}")

reversed_numbers = sorted(numbers, reverse=True) # returns a new, reversed list
print(f"New reversed list: {reversed_numbers}")

# --- Tricks and Slicing ---
print(f"Slice from index 2 to 4: {my_list[2:5]}")
print(f"Reversed list using a slice: {my_list[::-1]}")

```

| Category             | Method / Trick       | Description                                                                                  | Example                                 |
| :------------------- | :------------------- | :------------------------------------------------------------------------------------------- | :-------------------------------------- |
| **Adding Items**     | `append(x)`          | Adds a single item `x` to the end of the list.                                               | `my_list.append(8)`                     |
|                      | `extend(iterable)`   | Adds all items from an iterable (like another list) to the end.                              | `my_list.extend([9, 10])`               |
|                      | `insert(i, x)`       | Inserts item `x` at a specified index `i`.                                                   | `my_list.insert(0, "start")`            |
| **Removing Items**   | `remove(x)`          | Removes the **first occurrence** of item `x`. Raises a `ValueError` if not found.            | `my_list.remove('b')`                   |
|                      | `pop([i])`           | Removes and returns the item at a specific index `i`. If `i` is not specified, it removes and returns the **last item**. | `item = my_list.pop(0)`|
|                      | `del` statement      | Deletes an item at a specific index or a slice.                                              | `del my_list[2]` or `del my_list[1:3]`  |
| **Sorting & Reversing** | `sort(reverse=False)` | Sorts the list **in-place**. Use `reverse=True` for descending order.                    | `numbers.sort()`                        |
|                      | `sorted(iterable)`   | Returns a **new sorted list**, leaving the original unchanged.                               | `new_list = sorted(my_list)`            |
|                      | `reverse()`          | Reverses the list **in-place**.                                                              | `my_list.reverse()`                     |
| **Slicing Techniques** | `list[start:stop]`  | Extracts a sublist from `start` up to (but not including) `stop`.                           | `my_list[1:4]` -> `[2, 'new', 'b']`     |
|                      | `list[start:]`       | Extracts a sublist from `start` to the end of the list.                                      | `my_list[2:]` -> `['new', 'b', 4]`      |
|                      | `list[:stop]`        | Extracts a sublist from the beginning up to `stop`.                                          | `my_list[:3]` -> `[1, 2, 'new']`        |
|                      | `list[:]`            | Creates a **shallow copy** of the entire list.                                               | `new_list = my_list[:]`                 |
|                      | `list[::step]`       | Extracts a sublist using a step size.                                                        | `my_list[::2]` -> `[1, 'new', 4]`       |
|                      | `list[::-1]`         | A common trick to create a **new reversed copy** of a list.                                  | `reversed_copy = my_list[::-1]`         |
|                      | Negative Indices     | Uses negative numbers to count from the end of the list. `-1` is the last item, `-2` is the second to last. | `my_list[-1]` -> `4`, `my_list[:-1]` -> `[1, 2, 'new', 'b']` |
| **Searching & Counting** | `count(x)`        | Returns the number of times `x` appears in the list.                                        | `my_list.count(1)`                      |
|                      | `index(x)`           | Returns the index of the **first occurrence** of item `x`.                                   | `my_list.index('new')`                  |
|                      | `x in my_list`       | An efficient way to check for item membership, returning `True` or `False`.                  | `if 'a' in my_list:`                    |
| **Other Techniques** | `copy()` method      | Also creates a shallow copy. More explicit than slicing.                                     | `new_list = my_list.copy()`             |
|                      | List Comprehension   | A concise way to create a new list by iterating over an existing one.                        | `doubled = [n*2 for n in numbers]`      |
|                      | `list()`             | The constructor to create an empty list or convert another iterable to a list.               | `new_list = list(range(5))`             |
|                      | Concatenation        | Using the `+` operator creates a new list from two or more lists.                            | `combined = my_list + [8, 9]`           |

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

## Tuples

- Immutable sequences (cannot be modified after creation)  
- Useful for fixed collections of items  
- Support indexing, slicing, iteration  
- Can be nested, contain any data type  
- Allow unpacking  

```python
t = (1, "a", 3.5)
x, y, z = t
```

### Tricks & Tips

| Task                      | Code Example                             | Output / Notes                          |
|---------------------------|------------------------------------------|------------------------------------------|
| Length                   | `len(t)`                                 | `3`                                      |
| Indexing                 | `t[0]`, `t[-1]`                           | `1`, `3.5`                               |
| Slicing                  | `t[1:3]`                                  | `('a', 3.5)`                             |
| Concatenation            | `t + (4, 5)`                              | `(1, 'a', 3.5, 4, 5)`                    |
| Repetition               | `t * 2`                                   | `(1, 'a', 3.5, 1, 'a', 3.5)`             |
| Membership test          | `3.5 in t`                                | `True`                                   |
| Single-element tuple     | `(42,)`                                   | Comma required to make it a tuple        |
| Not a tuple              | `(42)`                                    | Just an `int`, not a tuple               |
| Tuple packing            | `pair = a, b`                             | No parentheses needed                    |
| Tuple unpacking          | `x, y = pair`                             | Works with any iterable of same length   |
| Swapping values          | `a, b = b, a`                             | Clean swap without temp variable         |
| Nested unpacking         | `x, (y, z) = (1, (2, 3))`                 | Supports deep patterns                   |
| Looping with unpacking   | `for x, y in [(1, 'a'), (2, 'b')]`        | Unpacks per item                         |
| Return multiple values   | `return a, b`                             | Returned as tuple                        |
| Unpack returned values   | `x, y = func()`                           | Matches return tuple                     |
| Convert to tuple         | `tuple("abc")`                            | `('a', 'b', 'c')`                         |

### Named Tuples

| Task                    | Code Example                                       | Output / Notes                          |
|-------------------------|----------------------------------------------------|------------------------------------------|
| Define namedtuple       | `Point = namedtuple("Point", "x y")`              | From `collections` module                |
| Create                  | `p = Point(3, 4)`                                  | `p` is like a lightweight class          |
| Access fields           | `p.x`, `p.y`                                       | Attribute-style access                   |

```python
from collections import namedtuple
Point = namedtuple("Point", "x y")
p = Point(3, 4)
print(p.x, p.y)
```

## Dictionaries

- Unordered collection of key-value pairs  
- Keys must be hashable (immutable), values can be any type  
- Fast lookups, insertions, deletions  

```python
d = {"a": 1, "b": 2}
d["c"] = 3
del d["a"]
for k, v in d.items():
    print(k, v)
```


### Common Dictionary Operations

| Method / Syntax     | Purpose / Description                                           | Example / Output                       |
|:--------------------|:----------------------------------------------------------------|:---------------------------------------|
| `d[k]`              | Access value for key `k`. Raises `KeyError` if `k` not found.   | `d["b"]` → `2`                         |
| `d.get(k, default)` | Returns value for `k`, or `default` if not found.               | `d.get("x", 0)` → `0`                  |
| `d[k] = v`          | Insert/Update: Set value `v` for key `k`. Adds or updates.      | `d["z"] = 100`                         |
| `del d[k]`          | Removes key `k` and its value. Raises `KeyError` if not found.  | `del d["a"]`                           |
| `d.pop(k)`          | Removes and returns value for key `k`.                          | `d.pop("b")` → `2`                     |
| `d.popitem()`       | Removes and returns **last** inserted key-value pair (as tuple) | `k, v = d.popitem()`                   |
| `d.clear()`         | Removes all key-value pairs.| `d.clear()`                       |                                        |
| `k in d`            | Checks if key `k` exists.                                       | `'a' in d` → `True`                    |
| `d.keys()`          | Returns a view of all keys.                                     | `for k in d.keys()`                    |
| `d.values()`        | Returns a view of all values.                                   | `for v in d.values()`                  |
| `d.items()`         | Returns a view of `(key, value)` pairs.                         | `for k, v in d.items()`                |
| `d.update(d2)`      | Merges `d2` into `d`. Overwrites existing keys.                 | `d.update({'x': 9})`                   |
| `dict()` constructor| Create a dict from key-value pairs or keyword args.             | `dict([('a', 1)])` or `dict(a=1, b=2)` |
| `len(d)`            | Number of key-value pairs in dict.                              | `len(d)` → `2`                         |
| `sorted(d)`         | Sorted list of dict’s keys.                                     | `sorted(d)` → `['a', 'b']`             |
| `copy()`            | Returns a **shallow copy**.                                     | `d2 = d.copy()`                        |

### Dictionary Comprehensions

| Trick/Type | Purpose | Expression/Syntax | Example | Output |
|:-----------|:--------|:------------------|:--------|:-------|
| **Basic**                | Creates a dictionary by defining key-value pairs from an iterable | `{key: value for item in iterable}`                   | `{x: x*x for x in range(3)}` | `{0: 0, 1: 1, 2: 4}` |
| **With Condition**       | Filters items based on a condition.                               | `{k: v for k, v in d.items() if condition}`           | `{x: x*x for x in range(5) if x % 2 == 0}`        | `{0: 0, 2: 4, 4: 16}`|
| **Swap Keys and Values** | Inverts a dictionary.                                             | `{v: k for k, v in d.items()}`                        | `{'a': 1, 'b': 2} → {1: 'a', 2: 'b'}`              | `{1: 'a', 2: 'b'}`|
| **Filter Dictionary**    | Filters a dictionary based on keys or values.                     | `{k: v for k, v in d.items() if condition_on_k_or_v}` | `grades = {'A': 85, 'B': 92}; {k: v for k, v in grades.items() if v >= 90}` | `{'B': 92}`|

## Sets

```python
s = {1, 2, 3}
s.add(4)
s.remove(2)
print(1 in s, 99 not in s)
```

### Set Operations

| Method / Syntax                    | Purpose / Description                                                      | Example / Output                          |
|-----------------------------------|----------------------------------------------------------------------------|-------------------------------------------|
| `s.add(x)`                        | Adds element `x` to the set.                                               | `s.add(5)`                                 |
| `s.remove(x)`                     | Removes element `x`. Raises `KeyError` if not found.                       | `s.remove(3)`                              |
| `s.discard(x)`                    | Removes element `x` if present. No error if not found.                     | `s.discard(99)`                            |
| `s.pop()`                         | Removes and returns an arbitrary element. Raises `KeyError` if empty.     | `x = s.pop()`                              |
| `s.clear()`                       | Removes all elements.                                                      | `s.clear()`                                |
| `x in s` / `x not in s`           | Membership check. Returns `True` or `False`.                              | `2 in s` → `True`                           |
| `len(s)`                          | Number of elements in the set.                                             | `len(s)` → `3`                              |

### Set Algebra

| Method / Operator                      | Purpose / Description                                                     | Example / Output                     |
|----------------------------------------|---------------------------------------------------------------------------|--------------------------------------|
| `s.union(t)` or `s \| t`               | Returns a new set with elements from both `s` and `t`.                    | `{1, 2}.union({2, 3})` → `{1, 2, 3}` |
| `s.intersection(t)` or `s & t`         | Elements common to both `s` and `t`.                                      | `{1, 2} & {2, 3}` → `{2}`            |
| `s.difference(t)` or `s - t`           | Elements in `s` but not in `t`.                                           | `{1, 2} - {2, 3}` → `{1}`            |
| `s.symmetric_difference(t)` or `s ^ t` | Elements in either `s` or `t` but not both | `{1, 2} ^ {2, 3}` → `{1, 3}` |                                      |
| `s.isdisjoint(t)`                      | Returns `True` if `s` and `t` have no elements in common                  | `{1, 2}.isdisjoint({3, 4})` → `True` |
| `s.issubset(t)` or `s <= t`            | Returns `True` if all `s` elements are in `t`                             | `{1, 2} <= {1, 2, 3}` → `True`       |
| `s.issuperset(t)` or `s >= t`          | Returns `True` if all `t` elements are in `s`.                            | `{1, 2, 3} >= {2}` → `True`          |
| `set(iterable)`                        | Converts iterable to set (removes duplicates).                            | `set("aabc")` → `{'a', 'b', 'c'}`    |

### Set Comprehensions

| Trick/Type | Purpose | Expression / Syntax | Example with Output | Output |
| :--------- | :------ | :------------------ | :------------------ | :----- |
| **Basic** | Creates a new set, automatically ensuring unique elements, by transforming items from an iterable. | `{expr for item in iterable}` | `set_comp = {c for c in "hello"}` | `{'h', 'e', 'l', 'o'}` (order varies) |
| **With Conditional Filtering** | Creates a set including only unique items that satisfy a condition. | `{expr for item in iterable if condition}` | `unique_evens = {x for x in range(10) if x % 2 == 0 and x > 5}` | `{6, 8}` (order varies) |

## Frozen Sets

- Frozen sets are **immutable** versions of sets. Once created, you cannot add, remove, or modify elements. 
- Hashable: They are hashable and can be used as dictionary keys or elements in other sets.
- Automatically removes duplicates like regular sets
- Unordered: Elements have no defined order

### Operations

| Operation | Method/Syntax | Description | Example | Output |
|:----------|:--------------|:------------|:--------|:-------|
| **Creation**    | `frozenset(iterable)` | Create from any iterable | `frozenset([1, 2, 3])` | `frozenset({1, 2, 3})` |
| **Empty**       | `frozenset()`         | Create empty frozen set  | `frozenset()`          | `frozenset()` |
| **Length**      | `len(fs)`             | Number of elements       | `len(frozenset([1, 2, 3]))` | `3` |
| **Membership**  | `x in fs`             | Check if element exists  | `2 in frozenset([1, 2, 3])` | `True` |
| **Union**       | `fs1 \| fs2` or `fs1.union(fs2)`       | Combine frozen sets | `frozenset([1, 2]) \| frozenset([2, 3])` | `frozenset({1, 2, 3})` |
| **Intersection**| `fs1 & fs2` or `fs1.intersection(fs2)` | Common elements     | `frozenset([1, 2]) & frozenset([2, 3])`  | `frozenset({2})`       |
| **Difference**  | `fs1 - fs2` or `fs1.difference(fs2)`   | Elements in fs1 but not fs2 | `frozenset([1, 2, 3]) - frozenset([2])` | `frozenset({1, 3})` |
| **Symmetric Difference** | `fs1 ^ fs2` or `fs1.symmetric_difference(fs2)` | Elements in either but not both | `frozenset([1, 2]) ^ frozenset([2, 3])`  | `frozenset({1, 3})` |

### Use Cases

```python
# As dictionary keys (sets can't be used as keys because they're mutable)
cache = {
    frozenset(['apple', 'banana']): 'fruit_combo_1',
    frozenset(['carrot', 'broccoli']): 'veggie_combo_1'
}

# As elements in sets
set_of_sets = {
    frozenset([1, 2]),
    frozenset([3, 4]),
    frozenset([1, 2])  # Duplicate, will be ignored
}
print(f"Set of frozen sets: {set_of_sets}")

# Immutable configuration
ALLOWED_PERMISSIONS = frozenset(['read', 'write', 'execute'])

# Converting between set and frozenset
regular_set = {1, 2, 3}
frozen_version = frozenset(regular_set)
back_to_set = set(frozen_version)

print(f"Original: {regular_set}")
print(f"Frozen: {frozen_version}")
print(f"Back to set: {back_to_set}")
```

## Bytearray

- Bytearray is a **mutable** sequence of bytes (integers from 0-255).
- **Mutable** : Can be modified after creation `ba[0] = 65`
- **Byte Values** : Each element is an integer 0-255 `bytearray([65, 66, 67])`
- **Sequence** : Supports indexing, slicing, iteration `ba[1:3]`, `for b in ba`

### Creation Methods

| Method | Description | Example | Output |
|:-------|:------------|:--------|:-------|
| **From List** | Create from list of integers | `bytearray([65, 66, 67])` | `bytearray(b'ABC')` |
| **From String** | Create from string with encoding | `bytearray('hello', 'utf-8')` | `bytearray(b'hello')` |
| **From Bytes** | Create from bytes object | `bytearray(b'hello')` | `bytearray(b'hello')` |
| **With Size** | Create with specific size (zeros) | `bytearray(5)` | `bytearray(b'\x00\x00\x00\x00\x00')` |
| **Empty** | Create empty bytearray | `bytearray()` | `bytearray(b'')` |

### Common Operations

| Operation | Method/Syntax | Description | Example | Output |
|:----------|:--------------|:------------|:--------|:-------|
| **Length** | `len(ba)` | Number of bytes | `len(bytearray(b'hello'))` | `5` |
| **Indexing** | `ba[i]` | Get byte at index | `bytearray(b'ABC')[0]` | `65` |
| **Slicing** | `ba[start:end]` | Get slice | `bytearray(b'hello')[1:4]` | `bytearray(b'ell')` |
| **Modify Element** | `ba[i] = value` | Set byte at index | `ba[0] = 72` | Changes first byte |
| **Append** | `ba.append(byte)` | Add single byte | `ba.append(33)` | Adds `!` (ASCII 33) |
| **Extend** | `ba.extend(iterable)` | Add multiple bytes | `ba.extend([65, 66])` | Adds `AB` |
| **Insert** | `ba.insert(i, byte)` | Insert byte at position | `ba.insert(0, 72)` | Insert `H` at start |
| **Remove** | `ba.remove(byte)` | Remove first occurrence | `ba.remove(65)` | Remove first `A` |
| **Pop** | `ba.pop([i])` | Remove and return byte | `ba.pop()` | Remove last byte |
| **Clear** | `ba.clear()` | Remove all bytes | `ba.clear()` | Empty bytearray |

### String-like Methods

| Method | Description | Example | Output |
|:-------|:------------|:--------|:-------|
| **decode()** | Convert to string | `bytearray(b'hello').decode('utf-8')` | `'hello'` |
| **find()** | Find substring | `bytearray(b'hello').find(b'll')` | `2` |
| **replace()** | Replace bytes | `bytearray(b'hello').replace(b'll', b'xx')` | `bytearray(b'hexxo')` |
| **split()** | Split on delimiter | `bytearray(b'a,b,c').split(b',')` | `[bytearray(b'a'), bytearray(b'b'), bytearray(b'c')]` |
| **join()** | Join with separator | `bytearray(b',').join([bytearray(b'a'), bytearray(b'b')])` | `bytearray(b'a,b')` |

### Practical Examples

```python
# Creating and modifying bytearrays
ba = bytearray(b'Hello')
print(f"Original: {ba}")  # bytearray(b'Hello')

# Modify individual bytes
ba[0] = ord('h')  # Change 'H' to 'h'
print(f"After modification: {ba}")  # bytearray(b'hello')

# Append and extend
ba.append(ord('!'))  # Add exclamation mark
ba.extend(b' World')  # Add more text
print(f"After append/extend: {ba}")  # bytearray(b'hello! World')

# Working with binary data
data = bytearray(10)  # 10 zero bytes
data[0:4] = b'HEAD'   # Set header
data[4] = 0xFF        # Set a flag byte
data[5:] = b'12345'   # Set remaining data
print(f"Binary data: {data}")

# Converting between types
text = "Hello, 世界"
ba = bytearray(text, 'utf-8')
print(f"UTF-8 bytes: {ba}")
decoded = ba.decode('utf-8')
print(f"Decoded back: {decoded}")

# File-like operations
buffer = bytearray()
buffer.extend(b'Line 1\n')
buffer.extend(b'Line 2\n')
print(f"Buffer contents:\n{buffer.decode()}")
```
---

## Collections Module

The `collections` module provides specialized container datatypes that extend Python's built-in containers (dict, list, set, tuple).

```python
from collections import OrderedDict, defaultdict, ChainMap, deque, Counter
from collections import UserDict, UserList, UserString
```

## OrderedDict

An `OrderedDict` is a dictionary that **remembers the order** in which keys were inserted. In Python 3.7+, regular dicts maintain insertion order, but `OrderedDict` provides additional methods and guarantees.

- **Insertion Order** : Maintains key insertion order. `OrderedDict([('a', 1), ('b', 2)])`
- **Equality** : Order matters in comparisons. `OrderedDict([('a',1), ('b',2)]) != OrderedDict([('b',2), ('a',1)])`

### Common Operations

| Operation | Method | Description | Example |
|:----------|:-------|:------------|:--------|
| **Create** | `OrderedDict()` | Create empty or from pairs | `OrderedDict([('x', 1), ('y', 2)])` |
| **Move Key** | `move_to_end(key, last=True)` | Move key to end (or beginning) | `od.move_to_end('x', last=False)` |
| **Pop Item** | `popitem(last=True)` | Remove from end (or beginning) | `od.popitem(last=False)` |
| **Reverse** | `reversed(od)` | Iterate in reverse order | `list(reversed(od))` |

```python
from collections import OrderedDict

# Creating OrderedDict
od = OrderedDict([('apple', 1), ('banana', 2), ('cherry', 3)])
print(f"Original: {od}")

# Moving elements
od.move_to_end('apple')  # Move to end
print(f"After move_to_end: {od}")

od.move_to_end('cherry', last=False)  # Move to beginning
print(f"After move to beginning: {od}")

# Popping from different ends
last_item = od.popitem()  # Remove from end
first_item = od.popitem(last=False)  # Remove from beginning
print(f"Popped last: {last_item}, first: {first_item}")
print(f"Remaining: {od}")
```

## DefaultDict

A `defaultdict` is a dictionary that **automatically creates missing values** using a factory function when a key is accessed but doesn't exist.

### Key Features

| Feature | Description | Example |
|:--------|:------------|:--------|
| **Auto-creation** | Missing keys get default values | `dd['missing_key']` creates entry |
| **Factory Function** | Callable that provides default values | `int`, `list`, `set`, custom functions |
| **No KeyError** | Never raises KeyError for missing keys | Safe to access any key |

### Common Factory Functions

| Factory | Default Value | Use Case | Example |
|:--------|:--------------|:---------|:--------|
| `int` | `0` | Counters, accumulators | `defaultdict(int)` |
| `list` | `[]` | Grouping items | `defaultdict(list)` |
| `set` | `set()` | Collecting unique items | `defaultdict(set)` |
| `str` | `''` | String building | `defaultdict(str)` |
| `lambda: 'N/A'` | `'N/A'` | Custom defaults | `defaultdict(lambda: 'N/A')` |

```python
from collections import defaultdict

# Counter example
counter = defaultdict(int)
text = "hello world"
for char in text:
    counter[char] += 1  # No need to check if key exists
print(f"Character count: {dict(counter)}")

# Grouping example
groups = defaultdict(list)
data = [('fruit', 'apple'), ('veggie', 'carrot'), ('fruit', 'banana')]
for category, item in data:
    groups[category].append(item)
print(f"Groups: {dict(groups)}")

# Set example for unique items
unique_groups = defaultdict(set)
data = [('A', 1), ('B', 2), ('A', 1), ('A', 3)]
for key, value in data:
    unique_groups[key].add(value)
print(f"Unique groups: {dict(unique_groups)}")
```

## ChainMap

A `ChainMap` groups multiple dictionaries into a **single, updateable view**. It searches through the underlying mappings in order until a key is found.

### Key Features

| Feature | Description | Example |
|:--------|:------------|:--------|
| **Multiple Dicts** | Combines multiple mappings | `ChainMap(dict1, dict2, dict3)` |
| **Search Order** | Searches dicts in order | First dict has priority |
| **Updates** | Modifications go to first dict | `cm['key'] = value` |
| **Context Management** | Can push/pop contexts | `cm.new_child()`, `cm.parents` |

### Common Operations

| Operation | Method | Description | Example |
|:----------|:-------|:------------|:--------|
| **Create** | `ChainMap(*dicts)` | Combine dictionaries | `ChainMap(d1, d2, d3)` |
| **New Context** | `new_child(m=None)` | Add new dict to front | `cm.new_child({'temp': 1})` |
| **Remove Context** | `parents` | All but first dict | `cm.parents` |
| **Update** | `cm[key] = value` | Modify first dict only | Updates go to first mapping |

```python
from collections import ChainMap

# Configuration example - command line overrides defaults
defaults = {'color': 'blue', 'size': 'medium', 'debug': False}
user_config = {'color': 'red', 'size': 'large'}
command_line = {'debug': True}

# Chain them (command_line has highest priority)
config = ChainMap(command_line, user_config, defaults)
print(f"Final config: {dict(config)}")
print(f"Color: {config['color']}")  # 'red' from user_config
print(f"Debug: {config['debug']}")  # True from command_line
print(f"Size: {config['size']}")    # 'large' from user_config

# Adding temporary context
with_temp = config.new_child({'temp_setting': 'test'})
print(f"With temp: {dict(with_temp)}")

# Modifications go to first dict
config['new_setting'] = 'value'
print(f"Command line dict: {command_line}")  # Contains new_setting
```

## Deque

A `deque` (double-ended queue) is a **list-like container** with fast appends and pops from **both ends**. It's implemented as a doubly-linked list.

### Key Features

| Feature | Description | Performance |
|:--------|:------------|:------------|
| **Double-ended** | Fast operations at both ends | O(1) append/pop |
| **Thread-safe** | Atomic operations | Safe for concurrent access |
| **Memory Efficient** | No need to shift elements | Better than list for queues |
| **Bounded** | Optional maximum length | Automatic eviction |

### Common Operations

| Operation | Method | Description | Performance | Example |
|:----------|:-------|:------------|:------------|:--------|
| **Append Right** | `append(x)` | Add to right end | O(1) | `dq.append(1)` |
| **Append Left** | `appendleft(x)` | Add to left end | O(1) | `dq.appendleft(0)` |
| **Pop Right** | `pop()` | Remove from right | O(1) | `dq.pop()` |
| **Pop Left** | `popleft()` | Remove from left | O(1) | `dq.popleft()` |
| **Extend Right** | `extend(iterable)` | Add multiple to right | O(k) | `dq.extend([1,2,3])` |
| **Extend Left** | `extendleft(iterable)` | Add multiple to left | O(k) | `dq.extendleft([1,2,3])` |
| **Rotate** | `rotate(n=1)` | Rotate n steps right | O(k) | `dq.rotate(2)` |

```python
from collections import deque

# Basic usage
dq = deque([1, 2, 3])
print(f"Initial: {dq}")

# Adding to both ends
dq.append(4)        # Add to right
dq.appendleft(0)    # Add to left
print(f"After appends: {dq}")

# Removing from both ends
right = dq.pop()      # Remove from right
left = dq.popleft()   # Remove from left
print(f"Removed right: {right}, left: {left}")
print(f"Remaining: {dq}")

# Rotation
dq.extend([4, 5, 6])
print(f"Before rotation: {dq}")
dq.rotate(2)  # Rotate 2 steps to the right
print(f"After rotate(2): {dq}")
dq.rotate(-1)  # Rotate 1 step to the left
print(f"After rotate(-1): {dq}")

# Bounded deque (useful for keeping last N items)
bounded = deque(maxlen=3)
for i in range(6):
    bounded.append(i)
    print(f"Added {i}: {bounded}")
```

## UserDict, UserList, UserString

These are **wrapper classes** that make it easier to create custom dictionary, list, and string-like classes by subclassing.

### UserDict Example

```python
from collections import UserDict

class CaseInsensitiveDict(UserDict):
    """Dictionary that treats keys case-insensitively"""
    
    def __setitem__(self, key, value):
        if isinstance(key, str):
            key = key.lower()
        super().__setitem__(key, value)
    
    def __getitem__(self, key):
        if isinstance(key, str):
            key = key.lower()
        return super().__getitem__(key)
    
    def __contains__(self, key):
        if isinstance(key, str):
            key = key.lower()
        return super().__contains__(key)

# Usage
ci_dict = CaseInsensitiveDict()
ci_dict['Name'] = 'Alice'
ci_dict['AGE'] = 30

print(ci_dict['name'])  # 'Alice'
print(ci_dict['age'])   # 30
print('NAME' in ci_dict)  # True
```

### UserList Example

```python
from collections import UserList

class LoggingList(UserList):
    """List that logs all modifications"""
    
    def append(self, item):
        print(f"Appending {item}")
        super().append(item)
    
    def remove(self, item):
        print(f"Removing {item}")
        super().remove(item)
    
    def __setitem__(self, index, value):
        print(f"Setting index {index} to {value}")
        super().__setitem__(index, value)

# Usage
log_list = LoggingList([1, 2, 3])
log_list.append(4)      # Logs: Appending 4
log_list[0] = 10        # Logs: Setting index 0 to 10
log_list.remove(2)      # Logs: Removing 2
```

### UserString Example

```python
from collections import UserString

class ReversibleString(UserString):
    """String that can be easily reversed"""
    
    def reverse(self):
        """Return a new reversed string"""
        return ReversibleString(self.data[::-1])
    
    def is_palindrome(self):
        """Check if string is a palindrome"""
        clean = ''.join(c.lower() for c in self.data if c.isalnum())
        return clean == clean[::-1]

# Usage
rs = ReversibleString("Hello World")
print(f"Original: {rs}")
print(f"Reversed: {rs.reverse()}")

palindrome = ReversibleString("A man a plan a canal Panama")
print(f"Is palindrome: {palindrome.is_palindrome()}")
```

---

## Data Structures

This section covers common data structures that can be implemented in Python, along with their operations and use cases.

## Stack

A **Last-In-First-Out (LIFO)** data structure. Elements are added and removed from the same end (top).

### Operations

| Operation | List Method | Deque Method | Time Complexity | Description |
|:----------|:------------|:-------------|:----------------|:------------|
| **Push** | `append(x)` | `append(x)` | O(1) | Add element to top |
| **Pop** | `pop()` | `pop()` | O(1) | Remove and return top element |
| **Peek/Top** | `stack[-1]` | `stack[-1]` | O(1) | View top element without removing |
| **Is Empty** | `len(stack) == 0` | `len(stack) == 0` | O(1) | Check if stack is empty |
| **Size** | `len(stack)` | `len(stack)` | O(1) | Get number of elements |

```python
from collections import deque

# Stack using list
stack_list = []
stack_list.append(1)    # Push
stack_list.append(2)    # Push
stack_list.append(3)    # Push
print(f"Stack: {stack_list}")
top = stack_list.pop()  # Pop
print(f"Popped: {top}, Stack: {stack_list}")

# Stack using deque (recommended for large stacks)
stack_deque = deque()
stack_deque.append('a')  # Push
stack_deque.append('b')  # Push
stack_deque.append('c')  # Push
print(f"Stack: {list(stack_deque)}")
top = stack_deque.pop()  # Pop
print(f"Popped: {top}, Stack: {list(stack_deque)}")

# Stack class implementation
class Stack:
    def __init__(self):
        self._items = deque()
    
    def push(self, item):
        self._items.append(item)
    
    def pop(self):
        if self.is_empty():
            raise IndexError("pop from empty stack")
        return self._items.pop()
    
    def peek(self):
        if self.is_empty():
            raise IndexError("peek from empty stack")
        return self._items[-1]
    
    def is_empty(self):
        return len(self._items) == 0
    
    def size(self):
        return len(self._items)

# Usage
stack = Stack()
stack.push(10)
stack.push(20)
print(f"Top: {stack.peek()}")  # 20
print(f"Size: {stack.size()}")  # 2
```

## Queue

A **First-In-First-Out (FIFO)** data structure. Elements are added at one end (rear) and removed from the other end (front).

### Operations

| Operation | Deque Method | Time Complexity | Description |
|:----------|:-------------|:----------------|:------------|
| **Enqueue** | `append(x)` | O(1) | Add element to rear |
| **Dequeue** | `popleft()` | O(1) | Remove and return front element |
| **Front** | `queue[0]` | O(1) | View front element |
| **Rear** | `queue[-1]` | O(1) | View rear element |
| **Is Empty** | `len(queue) == 0` | O(1) | Check if queue is empty |
| **Size** | `len(queue)` | O(1) | Get number of elements |

```python
from collections import deque
import queue

# Queue using deque (recommended)
q = deque()
q.append(1)      # Enqueue
q.append(2)      # Enqueue
q.append(3)      # Enqueue
print(f"Queue: {list(q)}")
front = q.popleft()  # Dequeue
print(f"Dequeued: {front}, Queue: {list(q)}")

# Thread-safe queue
thread_queue = queue.Queue()
thread_queue.put('a')    # Enqueue
thread_queue.put('b')    # Enqueue
item = thread_queue.get()  # Dequeue (blocks if empty)
print(f"Dequeued from thread queue: {item}")

# Queue class implementation
class Queue:
    def __init__(self):
        self._items = deque()
    
    def enqueue(self, item):
        self._items.append(item)
    
    def dequeue(self):
        if self.is_empty():
            raise IndexError("dequeue from empty queue")
        return self._items.popleft()
    
    def front(self):
        if self.is_empty():
            raise IndexError("front from empty queue")
        return self._items[0]
    
    def rear(self):
        if self.is_empty():
            raise IndexError("rear from empty queue")
        return self._items[-1]
    
    def is_empty(self):
        return len(self._items) == 0
    
    def size(self):
        return len(self._items)

# Usage
my_queue = Queue()
my_queue.enqueue('first')
my_queue.enqueue('second')
print(f"Front: {my_queue.front()}")  # 'first'
print(f"Size: {my_queue.size()}")    # 2
```

## Priority Queue / Heap

A queue where elements are served based on **priority** rather than insertion order. Higher priority elements are dequeued first.

### Operations

| Operation | heapq Method | Time Complexity | Description |
|:----------|:-------------|:----------------|:------------|
| **Insert** | `heappush(heap, item)` | O(log n) | Add element with priority |
| **Extract Min** | `heappop(heap)` | O(log n) | Remove and return highest priority |
| **Peek Min** | `heap[0]` | O(1) | View highest priority element |
| **Heapify** | `heapify(list)` | O(n) | Convert list to heap |

```python
import heapq
import queue

# Priority Queue using heapq (min-heap)
pq = []
heapq.heappush(pq, (3, 'task3'))  # (priority, item)
heapq.heappush(pq, (1, 'task1'))  # Lower number = higher priority
heapq.heappush(pq, (2, 'task2'))

print(f"Priority Queue: {pq}")
while pq:
    priority, task = heapq.heappop(pq)
    print(f"Processing: {task} (priority: {priority})")

# For max-heap, negate priorities
max_pq = []
heapq.heappush(max_pq, (-3, 'high'))
heapq.heappush(max_pq, (-1, 'low'))
heapq.heappush(max_pq, (-2, 'medium'))

while max_pq:
    neg_priority, item = heapq.heappop(max_pq)
    print(f"Max heap: {item} (priority: {-neg_priority})")

# Thread-safe Priority Queue
thread_pq = queue.PriorityQueue()
thread_pq.put((2, 'second'))
thread_pq.put((1, 'first'))
thread_pq.put((3, 'third'))

while not thread_pq.empty():
    priority, item = thread_pq.get()
    print(f"Thread PQ: {item} (priority: {priority})")

# Priority Queue class
class PriorityQueue:
    def __init__(self):
        self._heap = []
        self._index = 0  # For stable sorting
    
    def put(self, priority, item):
        # Use index for stable sorting when priorities are equal
        heapq.heappush(self._heap, (priority, self._index, item))
        self._index += 1
    
    def get(self):
        if self.empty():
            raise IndexError("get from empty priority queue")
        priority, index, item = heapq.heappop(self._heap)
        return priority, item
    
    def peek(self):
        if self.empty():
            raise IndexError("peek from empty priority queue")
        priority, index, item = self._heap[0]
        return priority, item
    
    def empty(self):
        return len(self._heap) == 0
    
    def size(self):
        return len(self._heap)

# Usage
pq = PriorityQueue()
pq.put(3, 'Low priority task')
pq.put(1, 'High priority task')
pq.put(2, 'Medium priority task')

while not pq.empty():
    priority, task = pq.get()
    print(f"Executing: {task} (priority: {priority})")
```

## Linked List

A linear data structure where elements (nodes) are stored in sequence, with each node containing data and a reference to the next node.

```python
class ListNode:
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None
        self.tail = None
        self.size = 0
    
    def append(self, data):
        """Add element to end of list"""
        new_node = ListNode(data)
        if not self.head:
            self.head = self.tail = new_node
        else:
            self.tail.next = new_node
            self.tail = new_node
        self.size += 1
    
    def prepend(self, data):
        """Add element to beginning of list"""
        new_node = ListNode(data)
        new_node.next = self.head
        self.head = new_node
        if not self.tail:
            self.tail = new_node
        self.size += 1
    
    def insert(self, index, data):
        """Insert element at specific index"""
        if index < 0 or index > self.size:
            raise IndexError("Index out of range")
        
        if index == 0:
            self.prepend(data)
            return
        if index == self.size:
            self.append(data)
            return
        
        new_node = ListNode(data)
        current = self.head
        for _ in range(index - 1):
            current = current.next
        
        new_node.next = current.next
        current.next = new_node
        self.size += 1
    
    def delete(self, data):
        """Delete first occurrence of data"""
        if not self.head:
            raise ValueError("List is empty")
        
        if self.head.data == data:
            self.head = self.head.next
            if not self.head:
                self.tail = None
            self.size -= 1
            return
        
        current = self.head
        while current.next and current.next.data != data:
            current = current.next
        
        if current.next:
            if current.next == self.tail:
                self.tail = current
            current.next = current.next.next
            self.size -= 1
        else:
            raise ValueError(f"Data {data} not found")
    
    def find(self, data):
        """Find index of data"""
        current = self.head
        index = 0
        while current:
            if current.data == data:
                return index
            current = current.next
            index += 1
        return -1
    
    def to_list(self):
        """Convert to Python list"""
        result = []
        current = self.head
        while current:
            result.append(current.data)
            current = current.next
        return result
    
    def __len__(self):
        return self.size
    
    def __str__(self):
        return str(self.to_list())

# Usage
ll = LinkedList()
ll.append(1)
ll.append(2)
ll.append(3)
ll.prepend(0)
print(f"Linked List: {ll}")  # [0, 1, 2, 3]

ll.insert(2, 1.5)
print(f"After insert: {ll}")  # [0, 1, 1.5, 2, 3]

ll.delete(1.5)
print(f"After delete: {ll}")  # [0, 1, 2, 3]

print(f"Find 2: index {ll.find(2)}")  # Find 2: index 2
print(f"Length: {len(ll)}")  # Length: 4
```

## Binary Tree

### Traversals

| Traversal | Order | Use Case |
|:----------|:------|:---------|
| **Inorder** | Left → Root → Right | Get sorted order in BST |
| **Preorder** | Root → Left → Right | Copy tree, prefix expressions |
| **Postorder** | Left → Right → Root | Delete tree, postfix expressions |
| **Level Order** | Level by level (BFS) | Print tree levels |

```python
from collections import deque

class TreeNode:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

class BinaryTree:
    def __init__(self):
        self.root = None
    
    def insert(self, data):
        """Insert into BST"""
        if not self.root:
            self.root = TreeNode(data)
        else:
            self._insert_recursive(self.root, data)
    
    def _insert_recursive(self, node, data):
        if data < node.data:
            if node.left is None:
                node.left = TreeNode(data)
            else:
                self._insert_recursive(node.left, data)
        else:
            if node.right is None:
                node.right = TreeNode(data)
            else:
                self._insert_recursive(node.right, data)
    
    def inorder_traversal(self, node=None):
        """Left → Root → Right"""
        if node is None:
            node = self.root
        
        result = []
        if node:
            result.extend(self.inorder_traversal(node.left))
            result.append(node.data)
            result.extend(self.inorder_traversal(node.right))
        return result
    
    def preorder_traversal(self, node=None):
        """Root → Left → Right"""
        if node is None:
            node = self.root
        
        result = []
        if node:
            result.append(node.data)
            result.extend(self.preorder_traversal(node.left))
            result.extend(self.preorder_traversal(node.right))
        return result
    
    def postorder_traversal(self, node=None):
        """Left → Right → Root"""
        if node is None:
            node = self.root
        
        result = []
        if node:
            result.extend(self.postorder_traversal(node.left))
            result.extend(self.postorder_traversal(node.right))
            result.append(node.data)
        return result
    
    def level_order_traversal(self):
        """Level by level (BFS)"""
        if not self.root:
            return []
        
        result = []
        queue = deque([self.root])
        
        while queue:
            node = queue.popleft()
            result.append(node.data)
            
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
        
        return result
    
    def search(self, data):
        """Search in BST"""
        return self._search_recursive(self.root, data)
    
    def _search_recursive(self, node, data):
        if not node or node.data == data:
            return node is not None
        
        if data < node.data:
            return self._search_recursive(node.left, data)
        else:
            return self._search_recursive(node.right, data)
    
    def height(self, node=None):
        """Calculate tree height"""
        if node is None:
            node = self.root
        
        if not node:
            return -1
        
        left_height = self.height(node.left)
        right_height = self.height(node.right)
        
        return 1 + max(left_height, right_height)

# Usage
bt = BinaryTree()
values = [50, 30, 70, 20, 40, 60, 80]
for val in values:
    bt.insert(val)

print(f"Inorder (sorted): {bt.inorder_traversal()}")
print(f"Preorder: {bt.preorder_traversal()}")
print(f"Postorder: {bt.postorder_traversal()}")
print(f"Level order: {bt.level_order_traversal()}")
print(f"Height: {bt.height()}")
print(f"Search 40: {bt.search(40)}")
print(f"Search 90: {bt.search(90)}")
```

## Graph

A collection of vertices (nodes) connected by edges. Can be directed or undirected, weighted or unweighted.

### Representations

| Method | Space | Edge Lookup | Add Vertex | Add Edge | Best For |
|:-------|:------|:------------|:-----------|:---------|:---------|
| **Adjacency List** | O(V + E) | O(degree) | O(1) | O(1) | Sparse graphs |
| **Adjacency Matrix** | O(V²) | O(1) | O(V²) | O(1) | Dense graphs |

### Common Algorithms

| Algorithm | Purpose | Time Complexity | Use Case |
|:----------|:--------|:----------------|:---------|
| **DFS** | Depth-first traversal | O(V + E) | Path finding, cycle detection |
| **BFS** | Breadth-first traversal | O(V + E) | Shortest path (unweighted) |
| **Dijkstra** | Shortest path (weighted) | O((V + E) log V) | GPS navigation |
| **Topological Sort** | Order vertices | O(V + E) | Task scheduling |

```python
from collections import defaultdict, deque

class Graph:
    def __init__(self, directed=False):
        self.graph = defaultdict(list)
        self.directed = directed
    
    def add_edge(self, u, v, weight=1):
        """Add edge between vertices u and v"""
        self.graph[u].append((v, weight))
        if not self.directed:
            self.graph[v].append((u, weight))
    
    def add_vertex(self, vertex):
        """Add vertex to graph"""
        if vertex not in self.graph:
            self.graph[vertex] = []
    
    def get_vertices(self):
        """Get all vertices"""
        return list(self.graph.keys())
    
    def get_edges(self):
        """Get all edges"""
        edges = []
        for u in self.graph:
            for v, weight in self.graph[u]:
                if self.directed or u <= v:  # Avoid duplicates in undirected
                    edges.append((u, v, weight))
        return edges
    
    def dfs(self, start, visited=None):
        """Depth-First Search"""
        if visited is None:
            visited = set()
        
        result = []
        if start not in visited:
            visited.add(start)
            result.append(start)
            
            for neighbor, _ in self.graph[start]:
                result.extend(self.dfs(neighbor, visited))
        
        return result
    
    def dfs_iterative(self, start):
        """Iterative DFS using stack"""
        visited = set()
        stack = [start]
        result = []
        
        while stack:
            vertex = stack.pop()
            if vertex not in visited:
                visited.add(vertex)
                result.append(vertex)
                
                # Add neighbors to stack (reverse order for consistent traversal)
                for neighbor, _ in reversed(self.graph[vertex]):
                    if neighbor not in visited:
                        stack.append(neighbor)
        
        return result
    
    def bfs(self, start):
        """Breadth-First Search"""
        visited = set()
        queue = deque([start])
        result = []
        
        visited.add(start)
        
        while queue:
            vertex = queue.popleft()
            result.append(vertex)
            
            for neighbor, _ in self.graph[vertex]:
                if neighbor not in visited:
                    visited.add(neighbor)
                    queue.append(neighbor)
        
        return result
    
    def shortest_path_bfs(self, start, end):
        """Find shortest path using BFS (unweighted)"""
        if start == end:
            return [start]
        
        visited = set()
        queue = deque([(start, [start])])
        visited.add(start)
        
        while queue:
            vertex, path = queue.popleft()
            
            for neighbor, _ in self.graph[vertex]:
                if neighbor not in visited:
                    new_path = path + [neighbor]
                    if neighbor == end:
                        return new_path
                    
                    visited.add(neighbor)
                    queue.append((neighbor, new_path))
        
        return None  # No path found
    
    def has_cycle(self):
        """Detect cycle in graph"""
        if not self.directed:
            return self._has_cycle_undirected()
        else:
            return self._has_cycle_directed()
    
    def _has_cycle_undirected(self):
        """Detect cycle in undirected graph"""
        visited = set()
        
        def dfs_cycle(vertex, parent):
            visited.add(vertex)
            for neighbor, _ in self.graph[vertex]:
                if neighbor not in visited:
                    if dfs_cycle(neighbor, vertex):
                        return True
                elif neighbor != parent:
                    return True
            return False
        
        for vertex in self.graph:
            if vertex not in visited:
                if dfs_cycle(vertex, None):
                    return True
        return False
    
    def _has_cycle_directed(self):
        """Detect cycle in directed graph using DFS"""
        WHITE, GRAY, BLACK = 0, 1, 2
        color = defaultdict(int)
        
        def dfs_cycle(vertex):
            color[vertex] = GRAY
            for neighbor, _ in self.graph[vertex]:
                if color[neighbor] == GRAY:
                    return True
                if color[neighbor] == WHITE and dfs_cycle(neighbor):
                    return True
            color[vertex] = BLACK
            return False
        
        for vertex in self.graph:
            if color[vertex] == WHITE:
                if dfs_cycle(vertex):
                    return True
        return False

# Usage Examples
print("=== Undirected Graph ===")
g = Graph(directed=False)
g.add_edge('A', 'B')
g.add_edge('A', 'C')
g.add_edge('B', 'D')
g.add_edge('C', 'D')
g.add_edge('D', 'E')

print(f"Vertices: {g.get_vertices()}")
print(f"Edges: {g.get_edges()}")
print(f"DFS from A: {g.dfs('A')}")
print(f"BFS from A: {g.bfs('A')}")
print(f"Shortest path A to E: {g.shortest_path_bfs('A', 'E')}")
print(f"Has cycle: {g.has_cycle()}")

print("\n=== Directed Graph ===")
dg = Graph(directed=True)
dg.add_edge('X', 'Y')
dg.add_edge('Y', 'Z')
dg.add_edge('Z', 'X')  # Creates cycle

print(f"DFS from X: {dg.dfs('X')}")
print(f"BFS from X: {dg.bfs('X')}")
print(f"Has cycle: {dg.has_cycle()}")
```

### Summary

| Data Structure | Best For | Time Complexity (Average) | Space Complexity |
|:---------------|:---------|:---------------------------|:-----------------|
| **Stack** | LIFO operations, undo functionality | Push/Pop: O(1) | O(n) |
| **Queue** | FIFO operations, task scheduling | Enqueue/Dequeue: O(1) | O(n) |
| **Priority Queue** | Priority-based processing | Insert/Extract: O(log n) | O(n) |
| **Linked List** | Dynamic size, frequent insertions | Insert/Delete: O(1) at known position | O(n) |
| **Binary Tree** | Hierarchical data, searching | Search/Insert: O(log n) balanced | O(n) |
| **Graph** | Relationships, networks | DFS/BFS: O(V + E) | O(V + E) |

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

### Common Exceptions

| Exception             | Raised When...                              |
|-----------------------|---------------------------------------------|
| `ZeroDivisionError`   | Division by zero                            |
| `TypeError`           | Wrong type used                             |
| `ValueError`          | Invalid value for a type                    |
| `KeyError`            | Missing key in dictionary                   |
| `IndexError`          | Index out of bounds                         |
| `AttributeError`      | Invalid attribute access                    |
| `ImportError`         | Failed import                               |

## File I/O

- **Use `with open(...)`**: ensures file is properly closed.
- Files are read/written as **text by default** (`"t"`), use `"b"` for binary.
- `strip()` is commonly used to remove newline characters while reading.

```python
with open("out.txt", "w") as f:
    f.write("Hi!\n")
with open("out.txt") as f:
    for line in f:
        print(line.strip())
```

### File Modes

| Mode | Description                          |
|------|--------------------------------------|
| `"r"`  | Read (default). Fails if file doesn't exist. |
| `"w"`  | Write. Creates file or truncates existing.   |
| `"a"`  | Append. Creates file if not exists.           |
| `"x"`  | Create. Fails if file exists.                |
| `"b"`  | Binary mode (add to other modes, e.g. `"rb"`) |
| `"t"`  | Text mode (default, can combine with others) |

### File Methods

| Method              | Description                            |
|---------------------|----------------------------------------|
| `f.read()`          | Read entire file as a string           |
| `f.readline()`      | Read one line                          |
| `f.readlines()`     | Read all lines as a list               |
| `f.write(s)`        | Write string `s` to file               |
| `f.writelines(lines)`| Write list of strings                 |
| `f.seek(pos)`       | Move file pointer to position `pos`    |
| `f.tell()`          | Current file pointer position          |
| `f.close()`         | Closes the file (auto-handled with `with`) |

## Modules & Imports

Python's module system allows you to organize code into reusable files and packages.

### Basic Import Syntax

| Syntax | Description | Example | Usage |
|:-------|:------------|:--------|:------|
| `import module` | Import entire module | `import math` | `math.sqrt(16)` |
| `from module import item` | Import specific item | `from math import sqrt` | `sqrt(16)` |
| `from module import *` | Import all public items | `from math import *` | `sqrt(16)` (not recommended) |
| `import module as alias` | Import with alias | `import numpy as np` | `np.array([1, 2, 3])` |
| `from module import item as alias` | Import item with alias | `from os.path import join as pathjoin` | `pathjoin("a", "b.txt")` |

### Common Import Patterns

```python
# Standard library imports
import os
import sys
from collections import defaultdict, Counter
from pathlib import Path

# Third-party imports
import requests
import pandas as pd
import numpy as np

# Local imports
from mypackage import mymodule
from .relative_module import function
from ..parent_package import another_module
```

### Module Search Path

| Location | Description | Example |
|:---------|:------------|:--------|
| **Current Directory** | Where the script is running | `./mymodule.py` |
| **PYTHONPATH** | Environment variable paths | `/usr/local/lib/python3.x` |
| **Standard Library** | Built-in Python modules | `math`, `os`, `sys` |
| **Site-packages** | Third-party installed packages | `requests`, `numpy` |

```python
import sys
print("Python path:")
for path in sys.path:
    print(f"  {path}")
```

### Creating Modules

```python
"""A simple math module"""

PI = 3.14159

def area_circle(radius):
    """Calculate area of a circle"""
    return PI * radius ** 2

def area_rectangle(length, width):
    """Calculate area of a rectangle"""
    return length * width

class Calculator:
    def add(self, a, b):
        return a + b
    
    def multiply(self, a, b):
        return a * b

# This runs only when module is executed directly
if __name__ == "__main__":
    print("Testing mymath module")
    print(f"Circle area (r=5): {area_circle(5)}")
```

### Using the Module
```python
import mymath
from mymath import area_circle, Calculator

# Using imported module
print(f"PI value: {mymath.PI}")
print(f"Circle area: {area_circle(3)}")

# Using imported class
calc = Calculator()
print(f"Addition: {calc.add(5, 3)}")
```

## Packages

A package is a directory containing multiple modules with an `__init__.py` file.

### Package Structure
```
mypackage/
    __init__.py
    module1.py
    module2.py
    subpackage/
        __init__.py
        submodule.py
```

### Package __init__.py
```python
"""MyPackage - A sample package"""

# Import commonly used items to package level
from .module1 import important_function
from .module2 import ImportantClass

# Define what gets imported with "from mypackage import *"
__all__ = ['important_function', 'ImportantClass', 'module1']

# Package-level constants
VERSION = "1.0.0"
```

### Using Packages
```python
# Import entire package
import mypackage

# Import specific modules
from mypackage import module1
from mypackage.subpackage import submodule

# Import specific items
from mypackage import important_function, ImportantClass

# Relative imports (within package)
from . import sibling_module
from ..parent_package import parent_module
```

## Advanced Import Concepts

### Conditional Imports
```python
try:
    import numpy as np
    HAS_NUMPY = True
except ImportError:
    HAS_NUMPY = False
    print("NumPy not available")

# Use different implementations based on availability
if HAS_NUMPY:
    def fast_calculation(data):
        return np.mean(data)
else:
    def fast_calculation(data):
        return sum(data) / len(data)
```

### Dynamic Imports
```python
import importlib

# Import module by name
module_name = "math"
math_module = importlib.import_module(module_name)
print(math_module.sqrt(16))

# Reload a module (useful in development)
importlib.reload(math_module)
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

- All methods must include `self` as the first parameter.
- Inheritance: `class Poodle(Dog): ...`
- Use `super().__init__()` to call base class constructor.
- Dunder (double underscore) methods can override default behavior.
- Properties:
    - Use a leading underscore (e.g. `_radius`) for the internal variable to avoid recursion.
    - Properties provide **controlled access** to internal attributes.
    - Helps avoid breaking external code when internals change.

### Class Terminology

| Term                 | Description |
|----------------------|-------------|
| `class`              | Defines a class |
| `object`             | An instance of a class |
| `self`               | Refers to the current instance |
| `__init__`           | Constructor (called on creation) |
| `super()`            | Access parent methods/constructor |

### Common Dunder Methods

| Method          | Purpose                         | Example Output |
|------------------|----------------------------------|----------------|
| `__str__`        | User-friendly string (`str(obj)`) | `"Dog: Buddy"` |
| `__repr__`       | Developer representation (`repr(obj)`) | `"Dog('Buddy')"` |
| `__len__`        | Called by `len(obj)`             | `len(obj)` |
| `__eq__`         | Equality operator `==`           | `obj1 == obj2` |
| `__lt__`, `__gt__`, etc. | Comparison operators `<`, `>` |  |
| `__getitem__`    | Enable bracket access `obj[i]`   |  |
| `__call__`       | Make object callable `obj()`     |  |

### Class Features

| Feature           | Description |
|-------------------|-------------|
| Instance Variable | `self.name = value` (per object) |
| Class Variable    | Shared across all instances |
| Method            | Regular function with `self` |
| Class Method      | Uses `@classmethod`, takes `cls` |
| Static Method     | Uses `@staticmethod`, no `self` or `cls` |

```python
class MyClass:
    class_var = 0
    def __init__(self, x):
        self.x = x
    @classmethod
    def cls_method(cls): ...
    @staticmethod
    def stat_method(): ...
```
### Property Decorators

Used to define **getter**, **setter**, and **deleter** methods while accessing them like attributes.

```python
class Circle:
    def __init__(self, radius):
        self._radius = radius

    @property
    def radius(self):
        return self._radius

    @radius.setter
    def radius(self, value):
        if value < 0:
            raise ValueError("Radius must be positive")
        self._radius = value

    @radius.deleter
    def radius(self):
        del self._radius
```

### Property Decorators Summary

| Decorator        | Purpose                          | Usage                        |
|------------------|----------------------------------|------------------------------|
| `@property`      | Getter — makes method act like attribute | `obj.name` calls `get_name()` |
| `@x.setter`      | Setter for `x` property          | `obj.name = "value"`         |
| `@x.deleter`     | Deleter for `x` property         | `del obj.name`               |

## Concurrency & Async Programming

Python offers three main approaches to concurrency, each suited for different types of tasks:

| Model | Best For | Execution | GIL Impact | Use Cases |
|-------|----------|-----------|------------|-----------|
| **Threading** | I/O-bound tasks | Multiple threads, single process | Limited by GIL for CPU tasks | File I/O, network requests, UI responsiveness |
| **Multiprocessing** | CPU-bound tasks | Multiple processes | Bypasses GIL completely | Mathematical computations, data processing |
| **Asyncio** | I/O-bound tasks | Single thread, event loop | No GIL issues | Network servers, web scraping, concurrent I/O |

### Threading

- Uses multiple threads within a single process
- Good for I/O-bound tasks but limited by GIL for CPU-bound work
- Threads share memory space (can lead to race conditions)

```python
import threading
import time
import requests

def fetch_url(url):
    response = requests.get(url)
    print(f"Status: {response.status_code} for {url}")

# Sequential approach
start = time.time()
urls = ["https://httpbin.org/delay/1"] * 3
for url in urls:
    fetch_url(url)
print(f"Sequential: {time.time() - start:.2f}s")

# Threading approach
start = time.time()
threads = []
for url in urls:
    thread = threading.Thread(target=fetch_url, args=(url,))
    threads.append(thread)
    thread.start()

for thread in threads:
    thread.join()  # Wait for all threads to complete
print(f"Threading: {time.time() - start:.2f}s")

# Thread-safe operations with Lock
import threading

counter = 0
lock = threading.Lock()

def increment():
    global counter
    for _ in range(100000):
        with lock:  # Ensures thread-safe access
            counter += 1

threads = [threading.Thread(target=increment) for _ in range(2)]
for t in threads:
    t.start()
for t in threads:
    t.join()
print(f"Counter: {counter}")  # Should be 200000
```

### Multiprocessing

- Creates separate processes, each with its own Python interpreter
- True parallelism for CPU-bound tasks
- Processes don't share memory (communication via IPC)

```python
import multiprocessing
import time

def cpu_bound_task(n):
    # Simulate CPU-intensive work
    result = sum(i * i for i in range(n))
    return result

# Sequential approach
start = time.time()
results = [cpu_bound_task(1000000) for _ in range(4)]
print(f"Sequential: {time.time() - start:.2f}s")

# Multiprocessing approach
start = time.time()
with multiprocessing.Pool() as pool:
    results = pool.map(cpu_bound_task, [1000000] * 4)
print(f"Multiprocessing: {time.time() - start:.2f}s")

# Process communication with Queue
def worker(queue, name):
    while True:
        item = queue.get()
        if item is None:
            break
        print(f"Worker {name} processing {item}")
        time.sleep(1)

if __name__ == "__main__":
    queue = multiprocessing.Queue()
    processes = []
    
    # Start worker processes
    for i in range(2):
        p = multiprocessing.Process(target=worker, args=(queue, f"P{i}"))
        p.start()
        processes.append(p)
    
    # Add work to queue
    for i in range(5):
        queue.put(f"task-{i}")
    
    # Signal workers to stop
    for _ in processes:
        queue.put(None)
    
    # Wait for processes to finish
    for p in processes:
        p.join()
```

### Asyncio

- Single-threaded concurrency using an event loop
- Cooperative multitasking with `async`/`await`
- Excellent for I/O-bound tasks with many concurrent operations

```python
import asyncio
import aiohttp
import time

# Basic async function
async def say_hello(name, delay):
    await asyncio.sleep(delay)
    print(f"Hello, {name}!")

# Running async functions
async def main():
    # Sequential execution
    await say_hello("Alice", 1)
    await say_hello("Bob", 1)
    
    # Concurrent execution
    await asyncio.gather(
        say_hello("Charlie", 1),
        say_hello("Diana", 1),
        say_hello("Eve", 1)
    )

# asyncio.run(main())

# Async HTTP requests
async def fetch_url_async(session, url):
    async with session.get(url) as response:
        return await response.text()

async def fetch_multiple_urls():
    urls = ["https://httpbin.org/delay/1"] * 3
    
    async with aiohttp.ClientSession() as session:
        start = time.time()
        # Concurrent requests
        tasks = [fetch_url_async(session, url) for url in urls]
        results = await asyncio.gather(*tasks)
        print(f"Async requests: {time.time() - start:.2f}s")

# asyncio.run(fetch_multiple_urls())

# Async generators and iteration
async def async_range(n):
    for i in range(n):
        await asyncio.sleep(0.1)  # Simulate async work
        yield i

async def consume_async_generator():
    async for value in async_range(5):
        print(f"Got: {value}")

# Producer-Consumer pattern with asyncio.Queue
async def producer(queue, name):
    for i in range(3):
        await asyncio.sleep(1)
        await queue.put(f"{name}-item-{i}")
    await queue.put(None)  # Sentinel value

async def consumer(queue, name):
    while True:
        item = await queue.get()
        if item is None:
            queue.task_done()
            break
        print(f"Consumer {name} got: {item}")
        queue.task_done()

async def producer_consumer_example():
    queue = asyncio.Queue()
    
    # Start producer and consumers
    await asyncio.gather(
        producer(queue, "P1"),
        consumer(queue, "C1"),
        consumer(queue, "C2")
    )

# Context managers and async with
async def async_context_example():
    async with aiohttp.ClientSession() as session:
        async with session.get("https://httpbin.org/json") as response:
            data = await response.json()
            print(data)

# Error handling in async code
async def might_fail(should_fail=False):
    await asyncio.sleep(1)
    if should_fail:
        raise ValueError("Something went wrong!")
    return "Success!"

async def handle_async_errors():
    tasks = [
        might_fail(False),
        might_fail(True),
        might_fail(False)
    ]
    
    results = await asyncio.gather(*tasks, return_exceptions=True)
    
    for i, result in enumerate(results):
        if isinstance(result, Exception):
            print(f"Task {i} failed: {result}")
        else:
            print(f"Task {i} succeeded: {result}")
```

#### Key Asyncio Concepts

| Concept | Description | Example |
|---------|-------------|---------|
| **Coroutine** | Function defined with `async def` | `async def my_func():` |
| **Awaitable** | Object that can be used with `await` | `await some_coroutine()` |
| **Event Loop** | Manages and executes async tasks | `asyncio.run(main())` |
| **Task** | Wrapped coroutine for concurrent execution | `asyncio.create_task(coro)` |
| **Future** | Placeholder for a result that will be available later | `asyncio.Future()` |


#### Common Asyncio Patterns

```python
# 1. Fire and forget
async def fire_and_forget():
    task = asyncio.create_task(some_background_work())
    # Don't await - runs in background
    return "Started background task"

# 2. Timeout handling
async def with_timeout():
    try:
        result = await asyncio.wait_for(slow_operation(), timeout=5.0)
        return result
    except asyncio.TimeoutError:
        return "Operation timed out"

# 3. Semaphore for limiting concurrency
async def limited_concurrency():
    semaphore = asyncio.Semaphore(3)  # Max 3 concurrent operations
    
    async def limited_task(n):
        async with semaphore:
            await asyncio.sleep(1)
            return f"Task {n} completed"
    
    tasks = [limited_task(i) for i in range(10)]
    results = await asyncio.gather(*tasks)
    return results

# 4. Async comprehensions (Python 3.6+)
async def async_comprehension():
    # Async list comprehension
    results = [await fetch_data(i) async for i in async_range(5)]
    
    # Async generator expression
    squared = (x**2 async for x in async_range(5) if x % 2 == 0)
    return results, squared
```

## Common Built-in Functions in Python

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

Collection of useful Python tricks, idioms, and lesser-known features that can make your code more elegant and efficient.

### Variable and Assignment Tricks

| Trick | Code | Description |
|:------|:-----|:------------|
| **Multiple Assignment** | `a, b, c = 1, 2, 3` | Assign multiple variables at once |
| **Swapping Variables** | `a, b = b, a` | Swap without temporary variable |
| **Unpacking with Star** | `first, *middle, last = [1,2,3,4,5]` | Collect middle elements |
| **Chained Assignment** | `a = b = c = 0` | Assign same value to multiple variables |
| **Conditional Assignment** | `x = a if condition else b` | Ternary operator |

```python
# Multiple assignment and unpacking
data = [1, 2, 3, 4, 5]
first, *middle, last = data
print(f"First: {first}, Middle: {middle}, Last: {last}")

# Swapping without temp variable
a, b = 10, 20
a, b = b, a
print(f"a: {a}, b: {b}")  # a: 20, b: 10

# Unpacking in loops
pairs = [(1, 'a'), (2, 'b'), (3, 'c')]
for num, letter in pairs:
    print(f"{num}: {letter}")
```

### String Tricks

| Trick | Code | Description |
|:------|:-----|:------------|
| **String Multiplication** | `'=' * 50` | Repeat string n times |
| **String Formatting** | `f"{value:>10}"` | Right-align in 10 characters |
| **String Checking** | `'abc'.isalpha()` | Check if all alphabetic |
| **String Translation** | `str.maketrans('abc', '123')` | Character mapping |
| **String Padding** | `'42'.zfill(5)` | Zero-pad to width |

```python
# String formatting tricks
name = "Python"
version = 3.9
print(f"{name:>10} {version:<5.1f}")  # Right and left align

# String multiplication for separators
print("=" * 50)
print("TITLE".center(50))
print("=" * 50)

# Check string properties
text = "Hello123"
print(f"Alphanumeric: {text.isalnum()}")
print(f"Has digits: {any(c.isdigit() for c in text)}")
```

### List and Sequence Tricks

| Trick | Code | Description |
|:------|:-----|:------------|
| **List Flattening** | `[item for sublist in lists for item in sublist]` | Flatten nested lists |
| **Remove Duplicates** | `list(dict.fromkeys(items))` | Preserve order while removing duplicates |
| **List Rotation** | `items[n:] + items[:n]` | Rotate list by n positions |
| **Chunking** | `[lst[i:i+n] for i in range(0, len(lst), n)]` | Split list into chunks |
| **Zip Transpose** | `list(zip(*matrix))` | Transpose 2D list |

```python
# Flatten nested lists
nested = [[1, 2], [3, 4], [5, 6]]
flattened = [item for sublist in nested for item in sublist]
print(f"Flattened: {flattened}")

# Remove duplicates preserving order
items = [1, 2, 2, 3, 1, 4]
unique = list(dict.fromkeys(items))
print(f"Unique: {unique}")

# Chunk list
data = list(range(10))
chunks = [data[i:i+3] for i in range(0, len(data), 3)]
print(f"Chunks: {chunks}")

# Transpose matrix
matrix = [[1, 2, 3], [4, 5, 6]]
transposed = list(zip(*matrix))
print(f"Transposed: {transposed}")
```

### Dictionary Tricks

| Trick | Code | Description |
|:------|:-----|:------------|
| **Dictionary Merge** | `{**dict1, **dict2}` | Merge dictionaries (Python 3.5+) |
| **Dictionary Inversion** | `{v: k for k, v in d.items()}` | Swap keys and values |
| **Get with Default** | `d.get(key, default)` | Safe key access |
| **Dictionary Sorting** | `dict(sorted(d.items()))` | Sort by keys |
| **Counter from Iterable** | `Counter(items)` | Count occurrences |

```python
from collections import Counter

# Dictionary merging
dict1 = {'a': 1, 'b': 2}
dict2 = {'c': 3, 'd': 4}
merged = {**dict1, **dict2}
print(f"Merged: {merged}")

# Dictionary inversion
original = {'a': 1, 'b': 2, 'c': 3}
inverted = {v: k for k, v in original.items()}
print(f"Inverted: {inverted}")

# Counting with Counter
text = "hello world"
counts = Counter(text)
print(f"Character counts: {counts}")
print(f"Most common: {counts.most_common(3)}")
```

### Function and Control Flow Tricks

| Trick | Code | Description |
|:------|:-----|:------------|
| **Default Arguments** | `def func(x, items=None): items = items or []` | Mutable default handling |
| **Function Caching** | `@functools.lru_cache(maxsize=128)` | Cache function results |
| **Enumerate with Start** | `enumerate(items, start=1)` | Start counting from specific number |
| **Zip with Fillvalue** | `itertools.zip_longest(a, b, fillvalue=0)` | Zip unequal length iterables |
| **Any/All Shortcuts** | `any(condition for item in items)` | Short-circuit evaluation |

```python
import functools
from itertools import zip_longest

# Function with mutable default argument (correct way)
def add_item(item, target_list=None):
    if target_list is None:
        target_list = []
    target_list.append(item)
    return target_list

# Caching expensive function calls
@functools.lru_cache(maxsize=128)
def fibonacci(n):
    if n < 2:
        return n
    return fibonacci(n-1) + fibonacci(n-2)

print(f"Fibonacci(10): {fibonacci(10)}")

# Any/All for quick checks
numbers = [2, 4, 6, 8, 10]
print(f"All even: {all(n % 2 == 0 for n in numbers)}")
print(f"Any > 5: {any(n > 5 for n in numbers)}")
```

### File and Path Tricks

| Trick | Code | Description |
|:------|:-----|:------------|
| **Path Joining** | `Path('folder') / 'file.txt'` | OS-independent path joining |
| **File Reading** | `Path('file.txt').read_text()` | Read entire file |
| **File Writing** | `Path('file.txt').write_text(content)` | Write entire file |
| **File Existence** | `Path('file.txt').exists()` | Check if file exists |
| **Temporary Files** | `with tempfile.NamedTemporaryFile() as f:` | Auto-cleanup temp files |

```python
from pathlib import Path
import tempfile

# Modern path handling
data_dir = Path('data')
config_file = data_dir / 'config.json'
print(f"Config path: {config_file}")

# Quick file operations
if config_file.exists():
    content = config_file.read_text()
    print(f"Config content: {content[:50]}...")

# Temporary file handling
with tempfile.NamedTemporaryFile(mode='w', suffix='.txt', delete=False) as f:
    f.write("Temporary content")
    temp_path = f.name
print(f"Temporary file: {temp_path}")
```

### Iteration and Generator Tricks

| Trick | Code | Description |
|:------|:-----|:------------|
| **Infinite Iterator** | `itertools.count(start=0, step=1)` | Infinite counting |
| **Cycle Iterator** | `itertools.cycle([1, 2, 3])` | Repeat sequence infinitely |
| **Chain Iterators** | `itertools.chain(iter1, iter2)` | Combine multiple iterators |
| **Groupby** | `itertools.groupby(data, key=func)` | Group consecutive elements |
| **Pairwise** | `zip(items, items[1:])` | Get consecutive pairs |

```python
import itertools

# Infinite iterators (be careful with these!)
counter = itertools.count(1, 2)  # 1, 3, 5, 7, ...
print(f"First 5 odd numbers: {[next(counter) for _ in range(5)]}")

# Cycle through options
colors = itertools.cycle(['red', 'green', 'blue'])
print(f"Next 7 colors: {[next(colors) for _ in range(7)]}")

# Group consecutive elements
data = [1, 1, 2, 2, 2, 3, 1, 1]
grouped = [(k, len(list(g))) for k, g in itertools.groupby(data)]
print(f"Grouped: {grouped}")

# Pairwise iteration
items = [1, 2, 3, 4, 5]
pairs = list(zip(items, items[1:]))
print(f"Consecutive pairs: {pairs}")
```

### Class and Object Tricks

| Trick | Code | Description |
|:------|:-----|:------------|
| **Slots** | `__slots__ = ['x', 'y']` | Memory-efficient attributes |
| **Property Decorator** | `@property` | Getter/setter methods |
| **Class Method** | `@classmethod` | Alternative constructors |
| **Static Method** | `@staticmethod` | Utility methods |
| **Context Manager** | `__enter__` and `__exit__` | Custom with statements |

```python
# Memory-efficient class with slots
class Point:
    __slots__ = ['x', 'y']
    
    def __init__(self, x, y):
        self.x = x
        self.y = y
    
    @classmethod
    def from_string(cls, coord_str):
        x, y = map(float, coord_str.split(','))
        return cls(x, y)
    
    @staticmethod
    def distance(p1, p2):
        return ((p1.x - p2.x)**2 + (p1.y - p2.y)**2)**0.5

# Usage
p1 = Point(0, 0)
p2 = Point.from_string("3,4")
print(f"Distance: {Point.distance(p1, p2)}")

# Custom context manager
class Timer:
    def __enter__(self):
        import time
        self.start = time.time()
        return self
    
    def __exit__(self, *args):
        import time
        print(f"Elapsed: {time.time() - self.start:.2f}s")

# Usage
with Timer():
    sum(range(1000000))
```

### Debugging and Development Tricks

| Trick | Code | Description |
|:------|:-----|:------------|
| **Pretty Printing** | `import pprint; pprint.pprint(data)` | Formatted output |
| **Variable Inspection** | `vars(obj)` or `obj.__dict__` | Object attributes |
| **Function Signature** | `inspect.signature(func)` | Function parameters |
| **Source Code** | `inspect.getsource(func)` | View function source |
| **Breakpoint** | `breakpoint()` | Python 3.7+ debugger |

```python
import pprint
import inspect

# Pretty printing complex data
complex_data = {
    'users': [
        {'name': 'Alice', 'age': 30, 'skills': ['Python', 'SQL']},
        {'name': 'Bob', 'age': 25, 'skills': ['JavaScript', 'React']}
    ]
}
pprint.pprint(complex_data, width=50)

# Function introspection
def example_func(a, b=10, *args, **kwargs):
    return a + b

print(f"Signature: {inspect.signature(example_func)}")
print(f"Parameters: {list(inspect.signature(example_func).parameters.keys())}")

# Quick debugging (Python 3.7+)
def debug_example():
    x = 42
    # breakpoint()  # Uncomment to enter debugger
    return x * 2
```

### Performance and Memory Tricks

| Trick | Code | Description |
|:------|:-----|:------------|
| **List vs Generator** | `(x for x in items)` vs `[x for x in items]` | Memory efficiency |
| **String Joining** | `''.join(strings)` | Faster than concatenation |
| **Set Membership** | `item in set_obj` | O(1) vs O(n) for lists |
| **Local Variable** | Assign global functions to local variables | Faster access |
| **Slots** | `__slots__` | Reduce memory usage |

```python
import sys

# Memory comparison: list vs generator
list_comp = [x**2 for x in range(1000)]
gen_comp = (x**2 for x in range(1000))

print(f"List size: {sys.getsizeof(list_comp)} bytes")
print(f"Generator size: {sys.getsizeof(gen_comp)} bytes")

# Efficient string building
words = ['Python', 'is', 'awesome']
# Slow: result = ''; for word in words: result += word + ' '
# Fast:
result = ' '.join(words)
print(f"Joined: {result}")

# Set membership for fast lookups
large_list = list(range(10000))
large_set = set(large_list)

# This is much faster for membership testing
print(f"9999 in set: {9999 in large_set}")  # O(1)
# print(f"9999 in list: {9999 in large_list}")  # O(n)
```

## Further Resources

- [Official Python 3 Docs](https://docs.python.org/3)
- [Real Python](https://realpython.com/)
- [The Python Tutorial](https://docs.python.org/3/tutorial/)
- [Awesome Python](https://awesome-python.com/)