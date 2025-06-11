# C++

## Table of Contents
- [Preset](#preset)
- [Compilation](#compilation)
- [Memory Map](#memory-map)
- [Data Types](#data-types)
- [Variables, Constants, Identifiers, Keywords](#variables-constants-identifiers-keywords)
- [Input/Output](#inputoutput)
- [Format Specifiers & Escape Sequences](#format-specifiers--escape-sequences)
- [Control Statements](#control-statements)
- [Functions](#functions)
- [Structures](#structures)
- [Classes & Objects](#classes--objects)
- [Inheritance, Polymorphism, Virtual/Abstract](#inheritance-polymorphism-virtualabstract)
- [Operator Overloading & Overriding](#operator-overloading--overriding)
- [Templates](#templates)
- [Arrays & STL Containers](#arrays--stl-containers)
- [Strings](#strings)
- [Streams](#streams)
- [Pointers, References & Smart Pointers](#pointers-references--smart-pointers)
- [Dynamic Memory](#dynamic-memory)
- [Type Aliases: typedef & using](#type-aliases-typedef--using)
- [Unions & Enumerations](#unions--enumerations)
- [Files & File Streams](#files--file-streams)
- [Exception Handling](#exception-handling)
- [Namespaces](#namespaces)
- [Preprocessor Directives & Macros](#preprocessor-directives--macros)
- [Best Practices & Pitfalls](#best-practices--pitfalls)
- [What's New in Recent C++ Standards](#whats-new-in-recent-c-standards)
- [Build & Debug Tips](#build--debug-tips)
- [Further Resources](#further-resources)

## Preset
- Invented by Bjarne Stroustrup (1979)
- Multi-paradigm: Procedural, Object-Oriented, Generic, Functional
- Middle-level (high & low-level features)
- Major Standards: C++98/03, C++11, C++14, C++17, C++20, C++23

## Compilation

| Stage         | Description                                 |
|---------------|---------------------------------------------|
| Preprocessing | Handles `#include`, macros, and directives. |
| Compilation   | Converts source code to assembly code.      |
| Assembling    | Translates assembly into machine code (object files). |
| Linking       | Combines object files and libraries into a single executable. |
| Loading       | Loads executable into memory for execution. |

## Memory Map

A running C++ program’s memory layout:

| Segment         | Description                                                       |
|-----------------|-------------------------------------------------------------------|
| **Text/Code**   | Executable code (read-only).                                      |
| **Data (Initialized)** | Global/static variables with initial values.               |
| **BSS (Uninitialized Data)** | Global/static variables with no explicit init.       |
| **Heap**        | Dynamically allocated memory (`new`, `malloc`).                   |
| **Stack**       | Function call frames, local variables.                            |

```
|--------------------------|
|      Stack               | ← Grows Down
|--------------------------|
|      Heap                | ← Grows Up
|--------------------------|
|   BSS Segment            |
|--------------------------|
|   Data Segment           |
|--------------------------|
|   Text/Code Segment      |
|--------------------------|
```

## Data Types

| Type            | Size (bits) | Typical Range / Value                    | Header         | Notes                |
|-----------------|-------------|------------------------------------------|----------------|----------------------|
| `bool`          | 1+          | `true`/`false`                           |                |                      |
| `char`          | 8           | -128 to 127                              |                |                      |
| `unsigned char` | 8           | 0 to 255                                 |                |                      |
| `short`         | 16          | -32,768 to 32,767                        |                |                      |
| `int`           | 32          | -2,147,483,648 to 2,147,483,647          |                |                      |
| `long`          | 32/64       | (platform dependent)                     |                |                      |
| `long long`     | 64          | -2^63 to 2^63-1                          |                |                      |
| `float`         | 32          | ±1.17e-38 to ±3.4e38                     |                |                      |
| `double`        | 64          | ±2.3e-308 to ±1.7e308                    |                |                      |
| `long double`   | 80/96/128   | ±3.4e-4932 to ±1.1e4932                  |                |                      |
| `std::string`   | varies      | Sequence of chars                        | `<string>`     | Use instead of char* |
| `std::vector<T>`| varies      | Dynamic array                            | `<vector>`     |                      |
| `auto`          | -           | Type deduced by compiler                 |                | C++11+               |
| `size_t`        | platform    | unsigned, for sizes/array indexing       | `<cstddef>`    |                      |
| `int32_t`, etc. | fixed-width | Exact-width integers                     | `<cstdint>`    |                      |

## Variables, Constants, Identifiers, Keywords

- **Variables:** Must start with a letter or `_`, case-sensitive.  
- **Constants:** Use `const` or `constexpr` for values not meant to change.
- **Identifiers:** Names for variables, functions, etc.
- **Keywords:** Reserved words (`class`, `public`, `private`, `protected`, `namespace`, `template`, `typename`, `using`, `new`, `delete`, `try`, `catch`, `throw`, `override`, `final`, `constexpr`, `nullptr`, etc.)

## Input/Output

| C                 | C++ Streams                          | Example                       | Output/Notes      |
|-------------------|--------------------------------------|-------------------------------|-------------------|
| `printf`, `scanf` | `cout`, `cin`, `cerr`, `clog`        | `std::cout << a << std::endl;`| Prints a + newline|
|                   | `getline(cin, s)`                    | `getline(std::cin, s);`       | Reads whole line  |

```cpp
#include <iostream>
int a;
std::cin >> a;
std::cout << "Value: " << a << std::endl;
```

## Format Specifiers & Escape Sequences

- **No %d, %f** in C++ streams; use manipulators.
- **Escape sequences**: Same as C (`\n`, `\t`, etc.)

| Manipulator      | Effect                             | Example                   | Output       |
|------------------|------------------------------------|---------------------------|--------------|
| `std::hex`       | Hexadecimal                        | `cout << hex << 255`      | `ff`         |
| `std::setw(4)`   | Width                              | `cout << setw(4) << 42`   | `  42`       |
| `std::setprecision(2)` | Decimal precision            | `cout << setprecision(2) << 3.1415` | `3.1` (default fixed) |
| `std::fixed`     | Fixed-point notation               | `cout << fixed << 3.1`    | `3.100000`   |

```cpp
#include <iomanip>
double pi = 3.14159;
std::cout << std::fixed << std::setprecision(2) << pi; // 3.14
```

## Control Statements

| Category        | Statements                                       |
|-----------------|--------------------------------------------------|
| Conditional     | `if`, `else if`, `else`, `switch`                |
| Loops           | `for`, `while`, `do-while`, range-based for      |
| Jump            | `return`, `goto`, `break`, `continue`            |

## Functions

- **Declaration:** `int add(int, int);`
- **Definition:**  
  ```cpp
  int add(int x, int y) { return x + y; }
  ```
- **Default Args:** `void foo(int x, int y = 3);`
- **Function Overloading:** Multiple functions with the same name but different parameters.
- **Inline Functions:** Suggests compiler to substitute function body directly.

```cpp
inline int square(int x) { return x * x; }
std::cout << square(4); // Output: 16
```

## Structures

- For plain data. Members public by default.

```cpp
struct Book {
    std::string title;
    int id;
};
Book b1 = {"C++ Primer", 123};
```

## Classes & Objects

- Encapsulate data + functions.  
- Members private by default.

```cpp
class Box {
public:
    Box(double l, double b, double h) : length(l), breadth(b), height(h) {}
    double getVolume() const { return length * breadth * height; }
private:
    double length, breadth, height;
};
Box b(2, 3, 4);
std::cout << b.getVolume(); // 24
```

## Inheritance, Polymorphism, Virtual/Abstract

### Inheritance

```cpp
class Base { ... };
class Derived : public Base { ... };
```
- Types: `public`, `protected`, `private` inheritance.

### Polymorphism & Virtual

```cpp
class Base { 
    public: virtual void show() { 
        std::cout << "Base\n"; 
    }
};
class Derived : public Base { 
    public: void show() override { 
        std::cout << "Derived\n"; 
    }
};
Base *ptr = new Derived();
ptr->show(); // Output: Derived
```

- **Pure Virtual (Abstract):** `virtual int area() const = 0;`
- **Destructor:** Always declare base destructor `virtual`!

## Operator Overloading & Overriding

- **Overloading:** Redefining an operator for class types.
- **Overriding:** Replacing a base class's virtual function in derived class.

### Operator Overloading Example

```cpp
class Point {
public:
    int x, y;
    Point(int a, int b): x(a), y(b) {}
    Point operator+(const Point &rhs) const {
        return Point(x + rhs.x, y + rhs.y);
    }
};

Point p1(1,2), p2(3,4);
Point p3 = p1 + p2; // p3.x = 4, p3.y = 6
std::cout << p3.x << " " << p3.y << std::endl; // 4 6
```

### Overriding Example

```cpp
class Base { public: virtual void show() { std::cout << "Base\n"; }};
class Derived : public Base { public: void show() override { std::cout << "Derived\n"; }};
Base *ptr = new Derived();
ptr->show(); // Output: Derived
```

## Templates

Write type-generic code.

```cpp
template<typename T>
T add(T a, T b) { return a + b; }
std::cout << add<int>(2,3); // 5
std::cout << add<double>(2.5, 3.1); // 5.6
```

## Arrays & STL Containers

**STL**: Standard Template Library (C++'s built-in generic container & algorithm library).

### Overview Table

| Container                | Header         | What it is                | Common Functions/Methods                    |
|--------------------------|---------------|---------------------------|---------------------------------------------|
| `std::vector<T>`         | `<vector>`    | Dynamic array             | `push_back`, `size`, `[]`, `at`, `clear`   |
| `std::array<T, N>`       | `<array>`     | Fixed-size array          | `size`, `[]`, `at`, `front`, `back`        |
| `std::list<T>`           | `<list>`      | Doubly-linked list        | `push_back`, `push_front`, `insert`, `erase`|
| `std::deque<T>`          | `<deque>`     | Double-ended queue        | `push_back`, `push_front`, `pop_back`, `pop_front`|
| `std::stack<T>`          | `<stack>`     | LIFO stack (adapter)      | `push`, `pop`, `top`, `empty`              |
| `std::queue<T>`          | `<queue>`     | FIFO queue (adapter)      | `push`, `pop`, `front`, `back`, `empty`    |
| `std::priority_queue<T>` | `<queue>`     | Heap/priority queue       | `push`, `pop`, `top`, `empty`              |
| `std::set<T>`            | `<set>`       | Sorted unique elements    | `insert`, `find`, `erase`, `count`         |
| `std::map<K, V>`         | `<map>`       | Sorted key-value pairs    | `insert`, `find`, `erase`, `[]`, `at`      |
| `std::unordered_set<T>`  | `<unordered_set>`| Hash set               | `insert`, `find`, `erase`, `count`         |
| `std::unordered_map<K,V>`| `<unordered_map>`| Hash map               | `insert`, `find`, `erase`, `[]`, `at`      |

### Usage Examples (with code)

#### Vector

```cpp
#include <vector>
std::vector<int> v = {1, 2, 3};
v.push_back(4);
for (int x : v) std::cout << x << " "; // Output: 1 2 3 4
```

#### Stack

```cpp
#include <stack>
std::stack<int> st;
st.push(10);
st.push(20);
std::cout << st.top(); // 20
st.pop();
```

#### Queue

```cpp
#include <queue>
std::queue<int> q;
q.push(1);
q.push(2);
std::cout << q.front(); // 1
q.pop();
```

#### Map

```cpp
#include <map>
std::map<std::string, int> age;
age["Alice"] = 30;
age["Bob"] = 25;
std::cout << age["Bob"]; // 25
```

#### Set

```cpp
#include <set>
std::set<int> s = {1, 2, 2, 3};
for (int x : s) std::cout << x << " "; // Output: 1 2 3
```

#### Unordered Map

```cpp
#include <unordered_map>
std::unordered_map<std::string, int> um;
um["foo"] = 42;
std::cout << um["foo"]; // 42
```

> For more, see [cppreference STL containers](https://en.cppreference.com/w/cpp/container).

## Strings

Use `std::string` (not `char*` or `char[]`).

### Common String Methods Table

| Method             | Description                | Example                               |
|--------------------|---------------------------|---------------------------------------|
| `size()`           | Length of string           | `s.size()`                            |
| `empty()`          | Is string empty?           | `s.empty()`                           |
| `clear()`          | Make empty                 | `s.clear()`                           |
| `at(i)`            | Character at position      | `s.at(2)`                             |
| `front()`, `back()`| First/last character       | `s.front()`                           |
| `append(str)`      | Concatenate                | `s.append("abc")`                     |
| `+=`               | Concatenate                | `s += "abc"`                          |
| `substr(pos, len)` | Substring                  | `s.substr(1,3)`                       |
| `insert(pos, str)` | Insert substring           | `s.insert(2, "abc")`                  |
| `erase(pos, len)`  | Remove substring           | `s.erase(1,3)`                        |
| `replace(pos, len, str)` | Replace substring    | `s.replace(0, 2, "hi")`               |
| `find(str)`        | Find substring             | `s.find("abc")`                       |
| `rfind(str)`       | Find from end              | `s.rfind("abc")`                      |
| `compare(str)`     | Compare strings            | `s.compare("abc")`                    |
| `c_str()`          | C-string pointer           | `printf("%s", s.c_str())`             |
| `getline(cin, s)`  | Read line from input       | `getline(cin, s)`                      |
| `std::stoi(s)`     | Convert string to int      | `std::stoi("123")`                    |
| `std::to_string(x)`| Convert number to string   | `std::to_string(42)`                  |

```cpp
#include <string>
std::string s = "hello";
s += " world";
std::cout << s << " " << s.size();
```

## Streams

- **Streams** are objects for reading/writing data.
- `cin` (input), `cout` (output), `cerr` (error), `ifstream` (file input), `ofstream` (file output)
- Support chaining: `cout << "Hi " << x << endl;`

```cpp
#include <fstream>
std::ofstream fout("file.txt");
fout << "Hello!\n";
fout.close();

std::ifstream fin("file.txt");
std::string line;
while (getline(fin, line)) std::cout << line << std::endl;
fin.close();
```

## Pointers, References & Smart Pointers

### Pointers

- Store memory addresses. Syntax: `int* p = &a;`
- Use `nullptr` (C++11+) instead of `NULL`.
- Can point to different objects, can be null.

### References

- C++ references are aliases, must be initialized and can't be reseated.
- Syntax: `int a = 5; int& r = a;`

### Smart Pointers (C++11+)

| Type             | Ownership         | Constructor Example                      | Notes                              |
|------------------|------------------|------------------------------------------|------------------------------------|
| `std::unique_ptr`| Single           | `auto p = std::make_unique<int>(5);`     | Not copyable, movable only         |
| `std::shared_ptr`| Shared           | `auto p = std::make_shared<int>(5);`     | Reference counted                  |
| `std::weak_ptr`  | Non-owning       | `std::weak_ptr<int> w = sp;`             | Use with shared_ptr to break cycles|

```cpp
#include <memory>
auto up = std::make_unique<int>(10);
auto sp = std::make_shared<int>(20);
std::cout << *up << " " << *sp; // 10 20
```

- Prefer smart pointers over raw pointers for ownership/resource management.

## Dynamic Memory

- Use `new`/`delete` for dynamic memory (prefer smart pointers and containers!).
- `int* p = new int(42); delete p;`
- `Box* boxes = new Box[4]; delete[] boxes;`

- **Advantages of `new`/`delete` over `malloc`/`free`:** Constructs/destructs objects, type safe, throws exceptions on failure.

## Type Aliases: typedef & using

- **typedef:** Old style.
  ```cpp
  typedef unsigned long ulong;
  typedef std::vector<int> IntVec;
  ```
- **using:** C++11+, more powerful (works for templates).
  ```cpp
  using ulong = unsigned long;
  using IntVec = std::vector<int>;
  template<typename T>
  using Vec = std::vector<T>;
  ```

## Unions & Enumerations

- **Union:** Same as C, but can have member functions/constructors in C++.
- **Enumeration:** C++ adds `enum class` for type safety.

```cpp
union Data {
    int i;
    float f;
    char c;
};

enum Color { Red, Green, Blue };
enum class Shape { Circle, Square, Triangle };
```

## Files & File Streams

| Stream         | Purpose              | Common Methods           |
|----------------|---------------------|--------------------------|
| `ifstream`     | File input          | `open`, `close`, `is_open`, `getline`, `>>` |
| `ofstream`     | File output         | `open`, `close`, `is_open`, `<<`             |
| `fstream`      | File input/output   | All above                |

```cpp
#include <fstream>
std::ofstream fout("out.txt");
fout << "hello" << std::endl;
fout.close();

std::ifstream fin("out.txt");
std::string s;
while (getline(fin, s)) std::cout << s << std::endl;
fin.close();
```

## Exception Handling

```cpp
try {
    // code that may throw
    throw std::runtime_error("error");
} catch (const std::exception& e) {
    std::cout << "Exception: " << e.what() << std::endl;
} catch (...) {
    std::cout << "Unknown exception" << std::endl;
}
```

- `throw` to raise, `try`/`catch` to handle.
- Always catch by (const) reference.
- Prefer `std::exception` hierarchy.

## Namespaces

Encapsulate identifiers to avoid name clashes.

```cpp
namespace first_space {
    void func() { std::cout << "Inside first_space" << std::endl; }
}
namespace second_space {
    void func() { std::cout << "Inside second_space" << std::endl; }
}
int main() {
    first_space::func();
    second_space::func();
}
```

## Preprocessor Directives & Macros

### Common Directives Table

| Directive      | Description                                        | Example                  |
|----------------|----------------------------------------------------|--------------------------|
| `#define`      | Macro or constant                                  | `#define MAX 100`        |
| `#undef`       | Undefine a macro                                   | `#undef MAX`             |
| `#include`     | Include a file                                     | `#include <iostream>`    |
| `#ifdef`       | If macro defined                                   | `#ifdef DEBUG`           |
| `#ifndef`      | If macro not defined                               | `#ifndef MAX`            |
| `#if`          | If compile-time condition                          | `#if VERSION > 2`        |
| `#else`        | Else for preprocessor                              | `#else`                  |
| `#elif`        | Else if                                            | `#elif VERSION == 2`     |
| `#endif`       | End if                                             | `#endif`                 |
| `#error`       | Stop compilation with error                        | `#error "Wrong version"` |
| `#pragma`      | Special compiler instruction                       | `#pragma once`           |
| `#line`        | Change line number/file                            | `#line 100 "myfile.cpp"` |

### Macro Patterns

| Macro Type           | Example                                  | Description                                    |
|----------------------|------------------------------------------|------------------------------------------------|
| Object-like          | `#define PI 3.14`                        | Simple replacement                             |
| Function-like        | `#define SQR(x) ((x)*(x))`               | Accepts arguments, no type checking            |
| Multi-line           | `#define LOG(msg) do { std::cout << msg; } while(0)` | Safe macro block              |
| Stringizing `#`      | `#define TO_STR(x) #x`                   | Converts parameter to string                   |
| Token Pasting `##`   | `#define COMB(a, b) a##b`                | Concatenates tokens                           |
| Variadic             | `#define DBG(fmt, ...) printf(fmt, __VA_ARGS__)` | Variable args (C99+)                  |
| Conditional Macro    | See `#ifdef`, `#ifndef`                  | Compile different code based on macros         |
| Undefining Macro     | `#undef PI`                              | Remove macro definition                       |

- Prefer `constexpr`, `const`, and `inline` functions/macros for type safety and clarity.

## Best Practices & Pitfalls

- Prefer STL containers, smart pointers, and RAII.
- Use `const` and `constexpr` generously.
- Avoid macros except for include guards.
- Avoid raw pointers and manual memory management.
- Always initialize variables.
- Use references for output parameters.
- Catch exceptions by (const) reference.
- Use range-based for and algorithms.
- Prefer `nullptr` over `NULL`.
- Always define a virtual destructor in base classes with virtual functions.
- Use `override` and `final` keywords for clarity.
- Use `auto` for type deduction where it improves readability.
- Use `using` over `typedef` for type aliases.

## Further Resources

- [cppreference.com](https://en.cppreference.com/)
- [C++ Core Guidelines](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines)
- [LearnCpp.com](https://www.learncpp.com/)
- [Modern C++ Features](https://github.com/AnthonyCalandra/modern-cpp-features)
- [Compiler Explorer](https://godbolt.org/)