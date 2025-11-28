# C++ - Senior Software Engineer Interview Guide

## Table of Contents
- [Preset](#preset)
- [Compilation Process](#compilation-process)
- [Memory Layout & Management](#memory-layout--management)
- [Data Types & Type System](#data-types--type-system)
- [Variables, Constants, Identifiers](#variables-constants-identifiers)
- [Input/Output & Streams](#inputoutput--streams)
- [Control Flow](#control-flow)
- [Functions & Callable Objects](#functions--callable-objects)
- [Lambda Expressions](#lambda-expressions)
- [Classes & Objects](#classes--objects)
- [The Rule of 3/5/0](#the-rule-of-350)
- [Const Correctness](#const-correctness)
- [Inheritance & Polymorphism](#inheritance--polymorphism)
- [Virtual Functions & vtables](#virtual-functions--vtables)
- [Operator Overloading](#operator-overloading)
- [Templates & Generic Programming](#templates--generic-programming)
- [Template Metaprogramming & Type Traits](#template-metaprogramming--type-traits)
- [Move Semantics & Rvalue References](#move-semantics--rvalue-references)
- [RAII & Resource Management](#raii--resource-management)
- [Pointers & References](#pointers--references)
- [Dynamic Memory Management](#dynamic-memory-management)
- [Smart Pointers](#smart-pointers)
- [Type Aliases: typedef & using](#type-aliases-typedef--using)
- [Unions & Enumerations](#unions--enumerations)
- [Files & File Streams](#files--file-streams)
- [STL Containers](#stl-containers)
- [STL Algorithms](#stl-algorithms)
- [Strings](#strings)
- [Concurrency & Multithreading](#concurrency--multithreading)
- [Memory Model & Atomics](#memory-model--atomics)
- [Exception Handling](#exception-handling)
- [Namespaces](#namespaces)
- [Preprocessor & Macros](#preprocessor--macros)
- [Design Patterns in C++](#design-patterns-in-c)
- [Performance & Optimization](#performance--optimization)
- [Modern C++ Features by Standard](#modern-c-features-by-standard)
- [Build Systems](#build-systems)
- [Testing & Debugging](#testing--debugging)
- [Common Interview Problems](#common-interview-problems)
- [Best Practices & Pitfalls](#best-practices--pitfalls)
- [Further Resources](#further-resources)

---

## Preset

**Creator:** Bjarne Stroustrup (1979)  
**Paradigms:** Multi-paradigm (Procedural, Object-Oriented, Generic, Functional)  
**Level:** Middle-level (combines high & low-level features)  
**Major Standards:** C++98/03, C++11, C++14, C++17, C++20, C++23

**Philosophy:** Zero-overhead abstraction, "you don't pay for what you don't use"

---

## Compilation Process

| Stage | Description | Output |
|-------|-------------|--------|
| **Preprocessing** | Handles `#include`, `#define`, conditional compilation | `.i` file |
| **Compilation** | Converts source to assembly, performs syntax/semantic analysis | `.s` file |
| **Assembly** | Translates assembly to machine code | `.o`/`.obj` file |
| **Linking** | Combines object files, resolves symbols, creates executable | Executable/library |

### Key Concepts

**Translation Unit:** A single source file after preprocessing (includes all headers)

**One Definition Rule (ODR):**
- Functions, variables, classes can be declared multiple times
- Must be defined exactly once across all translation units
- Exception: `inline` functions, templates, `constexpr` can be defined in headers

**Linkage Types:**
```cpp
// External linkage (visible across translation units)
int global_var = 42;
void function() {}

// Internal linkage (visible only within translation unit)
static int internal_var = 10;
namespace { int anon_var = 20; }  // Anonymous namespace
const int const_var = 30;         // const has internal linkage by default

// No linkage (local variables)
void foo() { int local = 5; }
```

---

## Memory Layout & Management

### Process Memory Layout

```
High Address
|--------------------------|
|   Command Line & Env     |
|--------------------------|
|        Stack             | ← Grows Down
|          ↓               |
|                          |
|          ↑               |
|        Heap              | ← Grows Up
|--------------------------|
|   BSS (Uninitialized)    |
|--------------------------|
|   Data (Initialized)     |
|--------------------------|
|     Text (Code)          |
|--------------------------|
Low Address
```

### Memory Segments

| Segment | Contents | Lifetime | Size |
|---------|----------|----------|------|
| **Stack** | Local variables, function parameters, return addresses | Automatic | Limited (~1-8MB) |
| **Heap** | Dynamic memory (`new`, `malloc`) | Manual/RAII | Large |
| **Data** | Initialized global/static variables | Program lifetime | Fixed |
| **BSS** | Uninitialized global/static variables | Program lifetime | Fixed |
| **Text** | Executable code, constants | Program lifetime | Fixed |

### Stack vs Heap

| Feature | Stack | Heap |
|---------|-------|------|
| **Allocation** | Automatic | Manual (`new`/`delete`) |
| **Speed** | Very fast (pointer bump) | Slower (memory manager) |
| **Size** | Limited | Large |
| **Lifetime** | Scope-based | Explicit management |
| **Fragmentation** | None | Possible |
| **Thread Safety** | Per-thread | Shared, needs sync |

```cpp
void example() {
    int stack_var = 42;              // Stack
    int* heap_var = new int(42);     // Heap
    static int static_var = 42;      // Data segment
    delete heap_var;
}
```

### Memory Alignment

```cpp
struct Unaligned {
    char c;    // 1 byte
    // 3 bytes padding
    int i;     // 4 bytes
    char d;    // 1 byte
    // 3 bytes padding
};  // Total: 12 bytes (not 6!)

// Control alignment
struct alignas(16) Aligned {
    int x;
};

// Check alignment
static_assert(alignof(Aligned) == 16);
```

---

## Data Types & Type System

### Fundamental Types

| Type | Size | Range | Notes |
|------|------|-------|-------|
| `bool` | 1 byte | `true`/`false` | |
| `char` | 1 byte | -128 to 127 | Implementation-defined signedness |
| `unsigned char` | 1 byte | 0 to 255 | |
| `short` | 2 bytes | -32,768 to 32,767 | |
| `int` | 4 bytes | -2³¹ to 2³¹-1 | |
| `long` | 4/8 bytes | Platform-dependent | |
| `long long` | 8 bytes | -2⁶³ to 2⁶³-1 | C++11+ |
| `float` | 4 bytes | ±3.4e±38 (7 digits) | |
| `double` | 8 bytes | ±1.7e±308 (15 digits) | |
| `long double` | 8/16 bytes | Extended precision | |

### Fixed-Width Types (C++11)

```cpp
#include <cstdint>
int8_t, int16_t, int32_t, int64_t      // Signed
uint8_t, uint16_t, uint32_t, uint64_t  // Unsigned
size_t, ptrdiff_t                       // Platform-specific
```

### Type Qualifiers

```cpp
const int x = 10;           // Cannot modify
volatile int y = 20;        // Prevent optimization
mutable int z = 30;         // Modifiable in const methods
constexpr int w = 40;       // Compile-time constant (C++11+)
```

### Type Deduction

```cpp
auto x = 42;                    // int
auto y = 3.14;                  // double
auto& ref = x;                  // int&
const auto& cref = x;           // const int&
auto* ptr = &x;                 // int*

decltype(x) a = x;              // Same type as x
decltype(auto) b = (x);         // C++14: preserves references

// Trailing return type
auto add(int a, int b) -> int { return a + b; }
```

---

## Variables, Constants, Identifiers

### Variable Declaration & Initialization

```cpp
int a;                  // Default initialization (undefined for primitives)
int b = 5;              // Copy initialization
int c(5);               // Direct initialization
int d{5};               // Uniform initialization (C++11) - prevents narrowing
int e = {5};            // Copy-list initialization

// Multiple declarations
int x = 1, y = 2, *ptr = &x;
```

### Constants

```cpp
const int MAX = 100;              // Runtime constant
constexpr int SIZE = 50;          // Compile-time constant
#define MACRO_CONST 200           // Preprocessor (avoid)

// constexpr functions (C++11+)
constexpr int square(int x) { return x * x; }
constexpr int result = square(5);  // Evaluated at compile time
```

### Storage Classes

```cpp
auto int x = 5;         // Automatic (default for local vars)
static int y = 10;      // Static storage, internal linkage
extern int z;           // External linkage (declaration)
register int r = 15;    // Hint to store in register (deprecated)
thread_local int t = 20; // Thread-local storage (C++11)
```

---

## Input/Output & Streams

### Standard Streams

```cpp
#include <iostream>

std::cin   // Standard input
std::cout  // Standard output
std::cerr  // Standard error (unbuffered)
std::clog  // Standard log (buffered)

// Basic I/O
int x;
std::cin >> x;
std::cout << "Value: " << x << std::endl;

// Read entire line
std::string line;
std::getline(std::cin, line);
```

### Stream Manipulators

```cpp
#include <iomanip>

std::cout << std::hex << 255;                    // ff
std::cout << std::setw(10) << 42;                //         42
std::cout << std::setprecision(2) << 3.14159;    // 3.1
std::cout << std::fixed << std::setprecision(2) << 3.14159;  // 3.14
std::cout << std::left << std::setw(10) << "Hi"; // Hi        
std::cout << std::boolalpha << true;             // true
```

---

## Control Flow

### Conditional Statements

```cpp
// if-else
if (condition) {
    // code
} else if (other_condition) {
    // code
} else {
    // code
}

// switch
switch (value) {
    case 1:
        // code
        break;
    case 2:
    case 3:  // Fall-through
        // code
        break;
    default:
        // code
}

// Ternary operator
int result = (condition) ? value1 : value2;

// if with initializer (C++17)
if (auto it = map.find(key); it != map.end()) {
    // use it
}
```

### Loops

```cpp
// for loop
for (int i = 0; i < 10; ++i) {
    // code
}

// Range-based for (C++11)
std::vector<int> vec = {1, 2, 3, 4, 5};
for (int x : vec) {          // Copy
    std::cout << x;
}
for (const auto& x : vec) {  // Const reference (preferred)
    std::cout << x;
}

// while loop
while (condition) {
    // code
}

// do-while loop
do {
    // code
} while (condition);
```

### Jump Statements

```cpp
break;      // Exit loop or switch
continue;   // Skip to next iteration
return;     // Exit function
goto label; // Jump to label (avoid!)
```

---

## Functions & Callable Objects

### Function Basics

```cpp
// Declaration
int add(int a, int b);

// Definition
int add(int a, int b) {
    return a + b;
}

// Default arguments
void foo(int x, int y = 10, int z = 20);

// Function overloading
int add(int a, int b);
double add(double a, double b);
int add(int a, int b, int c);
```

### Inline Functions

```cpp
inline int square(int x) {
    return x * x;
}
// Suggests compiler to substitute function body directly
// Defined in header files
```

### Function Pointers

```cpp
int add(int a, int b) { return a + b; }

// Function pointer
int (*func_ptr)(int, int) = add;
int result = func_ptr(3, 4);  // 7

// Using type alias
using BinaryOp = int(*)(int, int);
BinaryOp op = add;
```

### std::function (C++11)

```cpp
#include <functional>

std::function<int(int, int)> func = add;
func = [](int a, int b) { return a * b; };  // Can hold lambdas
```

### Pass by Value vs Reference

```cpp
void by_value(int x) {          // Copy
    x = 10;  // Doesn't affect original
}

void by_reference(int& x) {     // Reference
    x = 10;  // Modifies original
}

void by_const_ref(const int& x) {  // Const reference (efficient, safe)
    // x = 10;  // Error: cannot modify
}

void by_pointer(int* x) {       // Pointer
    if (x) *x = 10;
}
```

---

## Lambda Expressions

**Syntax:** `[capture](parameters) -> return_type { body }`

### Basic Lambdas

```cpp
// Simple lambda
auto lambda = []() { std::cout << "Hello\n"; };
lambda();

// With parameters
auto add = [](int a, int b) { return a + b; };
int sum = add(3, 4);  // 7

// Explicit return type
auto divide = [](int a, int b) -> double {
    return static_cast<double>(a) / b;
};
```

### Capture Modes

```cpp
int x = 10, y = 20;

[x]() { }           // Capture x by value
[&x]() { }          // Capture x by reference
[=]() { }           // Capture all by value
[&]() { }           // Capture all by reference
[=, &x]() { }       // All by value except x by reference
[&, x]() { }        // All by reference except x by value
[this]() { }        // Capture this pointer
[*this]() { }       // Capture object by value (C++17)

// Mutable lambda (can modify captured values)
[x]() mutable { x = 20; }
```

### Lambda Use Cases

```cpp
#include <algorithm>
#include <vector>

std::vector<int> vec = {1, 2, 3, 4, 5};

// With STL algorithms
std::for_each(vec.begin(), vec.end(), [](int x) {
    std::cout << x << " ";
});

// Sorting with custom comparator
std::sort(vec.begin(), vec.end(), [](int a, int b) {
    return a > b;  // Descending order
});

// Count elements > 3
int count = std::count_if(vec.begin(), vec.end(), [](int x) {
    return x > 3;
});

// Generic lambda (C++14)
auto generic = [](auto x, auto y) { return x + y; };
generic(1, 2);      // int
generic(1.5, 2.5);  // double
```

---

## Classes & Objects

### Class Basics

```cpp
class Rectangle {
private:
    double width, height;

public:
    // Constructor
    Rectangle(double w, double h) : width(w), height(h) {}
    
    // Member functions
    double area() const { return width * height; }
    double perimeter() const { return 2 * (width + height); }
    
    // Getters/Setters
    double getWidth() const { return width; }
    void setWidth(double w) { width = w; }
};

// Usage
Rectangle rect(5.0, 3.0);
std::cout << rect.area();  // 15
```

### Constructors

```cpp
class MyClass {
public:
    // Default constructor
    MyClass() : value(0) {}
    
    // Parameterized constructor
    MyClass(int v) : value(v) {}
    
    // Copy constructor
    MyClass(const MyClass& other) : value(other.value) {}
    
    // Move constructor (C++11)
    MyClass(MyClass&& other) noexcept : value(other.value) {
        other.value = 0;
    }
    
    // Delegating constructor (C++11)
    MyClass(int v, int multiplier) : MyClass(v * multiplier) {}
    
private:
    int value;
};
```

### Member Initializer List

```cpp
class Example {
public:
    // Prefer initializer list over assignment in constructor body
    Example(int a, int b) : x(a), y(b), z(x + y) {}
    // More efficient, required for const members and references
    
private:
    int x, y, z;
};
```

### Static Members

```cpp
class Counter {
public:
    Counter() { ++count; }
    static int getCount() { return count; }
    
private:
    static int count;  // Declaration
};

// Definition (outside class)
int Counter::count = 0;
```

### Friend Functions & Classes

```cpp
class Box {
private:
    double width;
    
public:
    Box(double w) : width(w) {}
    
    // Friend function
    friend void printWidth(const Box& b);
    
    // Friend class
    friend class BoxPrinter;
};

void printWidth(const Box& b) {
    std::cout << b.width;  // Can access private members
}
```

---

## The Rule of 3/5/0

### Rule of Three (C++98)

If a class requires a user-defined:
1. **Destructor**
2. **Copy constructor**
3. **Copy assignment operator**

Then it probably requires all three.

```cpp
class Resource {
private:
    int* data;
    
public:
    // Constructor
    Resource(int size) : data(new int[size]) {}
    
    // 1. Destructor
    ~Resource() {
        delete[] data;
    }
    
    // 2. Copy constructor
    Resource(const Resource& other) {
        data = new int[/* size */];
        // Copy data
    }
    
    // 3. Copy assignment operator
    Resource& operator=(const Resource& other) {
        if (this != &other) {
            delete[] data;
            data = new int[/* size */];
            // Copy data
        }
        return *this;
    }
};
```

### Rule of Five (C++11)

Add move semantics:
4. **Move constructor**
5. **Move assignment operator**

```cpp
class Resource {
private:
    int* data;
    size_t size;
    
public:
    Resource(size_t s) : data(new int[s]), size(s) {}
    
    ~Resource() { delete[] data; }
    
    // Copy constructor
    Resource(const Resource& other) : data(new int[other.size]), size(other.size) {
        std::copy(other.data, other.data + size, data);
    }
    
    // Copy assignment
    Resource& operator=(const Resource& other) {
        if (this != &other) {
            delete[] data;
            data = new int[other.size];
            size = other.size;
            std::copy(other.data, other.data + size, data);
        }
        return *this;
    }
    
    // Move constructor
    Resource(Resource&& other) noexcept : data(other.data), size(other.size) {
        other.data = nullptr;
        other.size = 0;
    }
    
    // Move assignment
    Resource& operator=(Resource&& other) noexcept {
        if (this != &other) {
            delete[] data;
            data = other.data;
            size = other.size;
            other.data = nullptr;
            other.size = 0;
        }
        return *this;
    }
};
```

### Rule of Zero

If you can avoid defining any of these special member functions (by using RAII classes like `std::vector`, `std::unique_ptr`), do so!

```cpp
class BetterResource {
private:
    std::vector<int> data;  // Handles everything automatically!
    
public:
    BetterResource(size_t size) : data(size) {}
    // No need for destructor, copy/move constructors, or assignment operators!
};
```

---

## Const Correctness

### Const Variables

```cpp
const int x = 10;        // Cannot modify x
int const y = 20;        // Same as above

const int* ptr1 = &x;    // Pointer to const int (can't modify *ptr1)
int* const ptr2 = &y;    // Const pointer to int (can't modify ptr2)
const int* const ptr3 = &x;  // Const pointer to const int
```

### Const Member Functions

```cpp
class MyClass {
private:
    int value;
    mutable int cache;  // Can be modified in const methods
    
public:
    // Const member function - promises not to modify object
    int getValue() const {
        cache = value;  // OK: mutable
        // value = 10;  // Error: cannot modify
        return value;
    }
    
    void setValue(int v) {  // Non-const
        value = v;
    }
};

const MyClass obj(42);
obj.getValue();   // OK
// obj.setValue(10);  // Error: cannot call non-const method on const object
```

### Const and Pointers

```cpp
void foo(const int* ptr);        // Cannot modify *ptr
void bar(int* const ptr);        // Cannot modify ptr
void baz(const int* const ptr);  // Cannot modify ptr or *ptr

// Const cast (use sparingly!)
const int x = 10;
int* ptr = const_cast<int*>(&x);  // Removes const (undefined behavior if modified)
```

---

## Inheritance & Polymorphism

### Inheritance Types

```cpp
class Base {
public:
    int pub;
protected:
    int prot;
private:
    int priv;
};

// Public inheritance (is-a relationship)
class PublicDerived : public Base {
    // pub remains public
    // prot remains protected
    // priv is inaccessible
};

// Protected inheritance
class ProtectedDerived : protected Base {
    // pub becomes protected
    // prot remains protected
    // priv is inaccessible
};

// Private inheritance (implementation detail)
class PrivateDerived : private Base {
    // pub becomes private
    // prot becomes private
    // priv is inaccessible
};
```

### Polymorphism

```cpp
class Animal {
public:
    virtual void makeSound() const {
        std::cout << "Some sound\n";
    }
    virtual ~Animal() = default;  // Always virtual destructor!
};

class Dog : public Animal {
public:
    void makeSound() const override {  // override keyword (C++11)
        std::cout << "Woof!\n";
    }
};

class Cat : public Animal {
public:
    void makeSound() const override final {  // final: cannot override further
        std::cout << "Meow!\n";
    }
};

// Usage
Animal* animal = new Dog();
animal->makeSound();  // "Woof!" - runtime polymorphism
delete animal;
```

### Abstract Classes

```cpp
class Shape {
public:
    virtual double area() const = 0;  // Pure virtual function
    virtual ~Shape() = default;
};

class Circle : public Shape {
private:
    double radius;
    
public:
    Circle(double r) : radius(r) {}
    double area() const override {
        return 3.14159 * radius * radius;
    }
};

// Shape s;  // Error: cannot instantiate abstract class
Circle c(5.0);  // OK
```

### Multiple Inheritance

```cpp
class A {
public:
    void funcA() {}
};

class B {
public:
    void funcB() {}
};

class C : public A, public B {
public:
    void funcC() {
        funcA();  // From A
        funcB();  // From B
    }
};
```

### Diamond Problem & Virtual Inheritance

```cpp
class Base {
public:
    int value;
};

class Derived1 : virtual public Base {};  // Virtual inheritance
class Derived2 : virtual public Base {};

class Final : public Derived1, public Derived2 {
    // Only one copy of Base::value
};
```

---

## Virtual Functions & vtables

### How Virtual Functions Work

```cpp
class Base {
public:
    virtual void func1() {}
    virtual void func2() {}
    void func3() {}  // Non-virtual
};

class Derived : public Base {
public:
    void func1() override {}  // Overrides Base::func1
    void func3() {}           // Hides Base::func3 (not override!)
};
```

**vtable (Virtual Table):**
- Each class with virtual functions has a vtable
- vtable contains pointers to virtual function implementations
- Each object has a hidden vptr (virtual pointer) pointing to its class's vtable

```
Base object:
[vptr] -> Base vtable: [&Base::func1, &Base::func2]
[data members]

Derived object:
[vptr] -> Derived vtable: [&Derived::func1, &Base::func2]
[data members]
```

### Virtual Destructor

```cpp
class Base {
public:
    virtual ~Base() {  // ALWAYS virtual in base classes!
        std::cout << "Base destructor\n";
    }
};

class Derived : public Base {
public:
    ~Derived() override {
        std::cout << "Derived destructor\n";
    }
};

Base* ptr = new Derived();
delete ptr;  // Calls both destructors correctly
```

### Object Slicing

```cpp
class Base {
public:
    int x;
    virtual void print() { std::cout << "Base\n"; }
};

class Derived : public Base {
public:
    int y;
    void print() override { std::cout << "Derived\n"; }
};

Derived d;
Base b = d;  // Object slicing! Only Base part is copied
b.print();   // "Base" - not polymorphic!

Base* ptr = &d;
ptr->print();  // "Derived" - polymorphic through pointer
```

---

## Operator Overloading

### Overloadable Operators

```cpp
class Complex {
private:
    double real, imag;
    
public:
    Complex(double r = 0, double i = 0) : real(r), imag(i) {}
    
    // Binary operators (member function)
    Complex operator+(const Complex& other) const {
        return Complex(real + other.real, imag + other.imag);
    }
    
    Complex operator-(const Complex& other) const {
        return Complex(real - other.real, imag - other.imag);
    }
    
    // Unary operators
    Complex operator-() const {
        return Complex(-real, -imag);
    }
    
    // Compound assignment
    Complex& operator+=(const Complex& other) {
        real += other.real;
        imag += other.imag;
        return *this;
    }
    
    // Comparison
    bool operator==(const Complex& other) const {
        return real == other.real && imag == other.imag;
    }
    
    // Stream operators (friend functions)
    friend std::ostream& operator<<(std::ostream& os, const Complex& c) {
        os << c.real << " + " << c.imag << "i";
        return os;
    }
    
    friend std::istream& operator>>(std::istream& is, Complex& c) {
        is >> c.real >> c.imag;
        return is;
    }
    
    // Subscript operator
    double& operator[](int index) {
        return (index == 0) ? real : imag;
    }
    
    // Function call operator
    double operator()() const {
        return std::sqrt(real * real + imag * imag);
    }
    
    // Conversion operator
    operator double() const {
        return real;
    }
};

// Non-member operator (when left operand is not your class)
Complex operator*(double scalar, const Complex& c) {
    return Complex(scalar * c.real, scalar * c.imag);
}
```

### Operators That Cannot Be Overloaded

- `::` (scope resolution)
- `.` (member access)
- `.*` (pointer-to-member access)
- `?:` (ternary)
- `sizeof`
- `typeid`

---

## Templates & Generic Programming

### Function Templates

```cpp
template<typename T>
T max(T a, T b) {
    return (a > b) ? a : b;
}

// Usage
int i = max(3, 7);           // T = int
double d = max(3.5, 2.1);    // T = double
std::string s = max(std::string("hello"), std::string("world"));

// Explicit template argument
auto result = max<double>(3, 7.5);
```

### Class Templates

```cpp
template<typename T>
class Stack {
private:
    std::vector<T> elements;
    
public:
    void push(const T& elem) {
        elements.push_back(elem);
    }
    
    void pop() {
        if (!elements.empty()) {
            elements.pop_back();
        }
    }
    
    T top() const {
        return elements.back();
    }
    
    bool empty() const {
        return elements.empty();
    }
};

// Usage
Stack<int> intStack;
intStack.push(42);

Stack<std::string> stringStack;
stringStack.push("hello");
```

### Template Specialization

```cpp
// Primary template
template<typename T>
class MyClass {
public:
    void print() { std::cout << "Generic\n"; }
};

// Full specialization
template<>
class MyClass<int> {
public:
    void print() { std::cout << "Int specialization\n"; }
};

// Partial specialization (for class templates only)
template<typename T>
class MyClass<T*> {
public:
    void print() { std::cout << "Pointer specialization\n"; }
};
```

### Variadic Templates (C++11)

```cpp
// Base case
void print() {}

// Recursive case
template<typename T, typename... Args>
void print(T first, Args... args) {
    std::cout << first << " ";
    print(args...);  // Recursive call
}

// Usage
print(1, 2.5, "hello", 'c');  // 1 2.5 hello c

// Fold expressions (C++17)
template<typename... Args>
auto sum(Args... args) {
    return (args + ...);  // Unary right fold
}

int total = sum(1, 2, 3, 4, 5);  // 15
```

---

## Template Metaprogramming & Type Traits

### Type Traits (C++11)

```cpp
#include <type_traits>

// Check type properties
static_assert(std::is_integral<int>::value, "int is integral");
static_assert(std::is_floating_point<double>::value, "double is floating point");
static_assert(std::is_pointer<int*>::value, "int* is pointer");
static_assert(std::is_class<std::string>::value, "string is class");

// Type modifications
using IntPtr = std::add_pointer<int>::type;  // int*
using ConstInt = std::add_const<int>::type;  // const int
using IntRef = std::add_lvalue_reference<int>::type;  // int&

// Remove qualifiers
using PlainInt = std::remove_const<const int>::type;  // int
using PlainInt2 = std::remove_reference<int&>::type;  // int
```

### SFINAE (Substitution Failure Is Not An Error)

```cpp
// Enable function only for integral types
template<typename T>
typename std::enable_if<std::is_integral<T>::value, T>::type
increment(T value) {
    return value + 1;
}

// C++17: if constexpr
template<typename T>
auto process(T value) {
    if constexpr (std::is_integral<T>::value) {
        return value + 1;
    } else if constexpr (std::is_floating_point<T>::value) {
        return value + 0.1;
    } else {
        return value;
    }
}
```

### Concepts (C++20)

```cpp
#include <concepts>

// Define a concept
template<typename T>
concept Numeric = std::is_arithmetic_v<T>;

// Use concept
template<Numeric T>
T add(T a, T b) {
    return a + b;
}

// More complex concept
template<typename T>
concept Printable = requires(T t) {
    { std::cout << t } -> std::same_as<std::ostream&>;
};
```

---

## Move Semantics & Rvalue References

### Lvalues vs Rvalues

```cpp
int x = 10;      // x is lvalue (has address)
int y = x + 5;   // x+5 is rvalue (temporary)

int& lref = x;   // Lvalue reference
// int& lref2 = 5;  // Error: cannot bind lvalue ref to rvalue

int&& rref = 5;  // Rvalue reference (C++11)
int&& rref2 = x + 5;  // OK: binds to temporary
```

### std::move

```cpp
#include <utility>

std::string str = "hello";
std::string str2 = std::move(str);  // str is now in valid but unspecified state

// std::move doesn't move anything! It just casts to rvalue reference
// Actual move happens in move constructor/assignment
```

### Move Constructor & Assignment

```cpp
class MyString {
private:
    char* data;
    size_t size;
    
public:
    // Constructor
    MyString(const char* str) {
        size = std::strlen(str);
        data = new char[size + 1];
        std::strcpy(data, str);
    }
    
    // Destructor
    ~MyString() {
        delete[] data;
    }
    
    // Copy constructor (expensive)
    MyString(const MyString& other) {
        size = other.size;
        data = new char[size + 1];
        std::strcpy(data, other.data);
    }
    
    // Move constructor (cheap)
    MyString(MyString&& other) noexcept
        : data(other.data), size(other.size) {
        other.data = nullptr;  // Leave other in valid state
        other.size = 0;
    }
    
    // Copy assignment
    MyString& operator=(const MyString& other) {
        if (this != &other) {
            delete[] data;
            size = other.size;
            data = new char[size + 1];
            std::strcpy(data, other.data);
        }
        return *this;
    }
    
    // Move assignment
    MyString& operator=(MyString&& other) noexcept {
        if (this != &other) {
            delete[] data;
            data = other.data;
            size = other.size;
            other.data = nullptr;
            other.size = 0;
        }
        return *this;
    }
};

// Usage
MyString s1("hello");
MyString s2 = std::move(s1);  // Move constructor
MyString s3("world");
s3 = std::move(s2);  // Move assignment
```

### Perfect Forwarding

```cpp
template<typename T>
void wrapper(T&& arg) {
    // Forward arg preserving its value category
    function(std::forward<T>(arg));
}

// Universal/Forwarding reference rules:
// T&& in template context is universal reference
// Binds to both lvalues and rvalues
```

---

## RAII & Resource Management

**RAII:** Resource Acquisition Is Initialization

### Core Principle

```cpp
class FileHandle {
private:
    FILE* file;
    
public:
    // Acquire resource in constructor
    FileHandle(const char* filename) {
        file = fopen(filename, "r");
        if (!file) throw std::runtime_error("Cannot open file");
    }
    
    // Release resource in destructor
    ~FileHandle() {
        if (file) fclose(file);
    }
    
    // Delete copy operations
    FileHandle(const FileHandle&) = delete;
    FileHandle& operator=(const FileHandle&) = delete;
    
    // Allow move operations
    FileHandle(FileHandle&& other) noexcept : file(other.file) {
        other.file = nullptr;
    }
    
    FILE* get() const { return file; }
};

// Usage - automatic cleanup!
void processFile() {
    FileHandle fh("data.txt");
    // Use fh.get()
    // File automatically closed when fh goes out of scope
}
```

### Lock Guard Example

```cpp
#include <mutex>

std::mutex mtx;

void criticalSection() {
    std::lock_guard<std::mutex> lock(mtx);  // Acquires lock
    // Critical section
    // Lock automatically released when lock goes out of scope
}
```

---

## Pointers & References

### Pointers

```cpp
int x = 42;
int* ptr = &x;        // Pointer to x
int value = *ptr;     // Dereference: get value (42)

// Null pointer
int* null_ptr = nullptr;  // C++11+ (prefer over NULL)

// Pointer arithmetic
int arr[] = {1, 2, 3, 4, 5};
int* p = arr;
p++;                  // Points to arr[1]
int val = *(p + 2);   // arr[3]

// Pointer to pointer
int** pptr = &ptr;
int value2 = **pptr;  // 42

// Const pointers
const int* ptr1 = &x;       // Pointer to const int (can't modify *ptr1)
int* const ptr2 = &x;       // Const pointer to int (can't modify ptr2)
const int* const ptr3 = &x; // Const pointer to const int

// Function pointers
int add(int a, int b) { return a + b; }
int (*func_ptr)(int, int) = add;
int result = func_ptr(3, 4);  // 7

// Void pointer (generic pointer)
void* void_ptr = &x;
int* int_ptr = static_cast<int*>(void_ptr);
```

### References

```cpp
int x = 42;
int& ref = x;         // Reference to x (alias)
ref = 10;             // Modifies x

// References must be initialized
// int& bad_ref;      // Error!

// Const reference
const int& cref = x;
// cref = 20;         // Error: cannot modify

// Reference vs Pointer
// - References cannot be null
// - References cannot be reseated
// - References are automatically dereferenced
// - Pointers can be null and reseated

// Rvalue reference (C++11)
int&& rref = 42;      // Binds to temporary
// int&& rref2 = x;   // Error: x is lvalue

// Forwarding reference (universal reference)
template<typename T>
void func(T&& arg) {  // Can bind to lvalue or rvalue
    // ...
}
```

### Pointer vs Reference Comparison

| Feature | Pointer | Reference |
|---------|---------|-----------|
| **Null value** | Can be null | Cannot be null |
| **Reassignment** | Can point to different objects | Cannot be reseated |
| **Syntax** | Requires `*` and `&` | Transparent (like variable) |
| **Memory** | Takes memory (address size) | No additional memory (alias) |
| **Arithmetic** | Supports pointer arithmetic | No arithmetic |
| **Initialization** | Can be uninitialized | Must be initialized |

---

## Dynamic Memory Management

### new and delete

```cpp
// Single object
int* ptr = new int(42);        // Allocate and initialize
delete ptr;                     // Deallocate
ptr = nullptr;                  // Good practice

// Array
int* arr = new int[10];         // Allocate array
delete[] arr;                   // Must use delete[] for arrays!

// Placement new (construct at specific address)
char buffer[sizeof(int)];
int* p = new (buffer) int(42);  // Construct int in buffer
p->~int();                      // Must manually call destructor
```

### new vs malloc

| Feature | new/delete | malloc/free |
|---------|------------|-------------|
| **Type** | Type-safe | Returns void* |
| **Constructor** | Calls constructor | No constructor |
| **Destructor** | Calls destructor | No destructor |
| **Failure** | Throws exception | Returns NULL |
| **Size** | Automatic | Must specify bytes |
| **Overloadable** | Yes | No |

```cpp
// new (C++)
int* p1 = new int(42);          // Calls constructor
delete p1;                       // Calls destructor

// malloc (C)
int* p2 = (int*)malloc(sizeof(int));
*p2 = 42;
free(p2);
```

### Memory Leaks

```cpp
// Memory leak example
void leak() {
    int* ptr = new int(42);
    // Forgot to delete!
}  // Memory leaked

// Correct
void no_leak() {
    int* ptr = new int(42);
    // Use ptr
    delete ptr;
}

// Better: Use RAII (smart pointers)
void best() {
    std::unique_ptr<int> ptr = std::make_unique<int>(42);
    // Automatically deleted
}
```

### Common Dynamic Memory Errors

```cpp
// 1. Double delete
int* ptr = new int(42);
delete ptr;
delete ptr;  // Undefined behavior!

// 2. Delete mismatch
int* arr = new int[10];
delete arr;  // Wrong! Should be delete[]

// 3. Dangling pointer
int* ptr = new int(42);
delete ptr;
*ptr = 10;  // Undefined behavior!

// 4. Memory leak
void leak() {
    int* ptr = new int(42);
    ptr = new int(100);  // Lost reference to first allocation
}

// 5. Use after free
int* ptr = new int(42);
delete ptr;
std::cout << *ptr;  // Undefined behavior!
```

---

## Type Aliases: typedef & using

### typedef (C++98)

```cpp
// Basic typedef
typedef unsigned long ulong;
typedef int* IntPtr;
typedef void (*FuncPtr)(int, int);

// With structs
typedef struct {
    int x, y;
} Point;

Point p = {10, 20};

// Array typedef
typedef int IntArray[10];
IntArray arr;  // int arr[10]
```

### using (C++11) - Preferred

```cpp
// Basic type alias
using ulong = unsigned long;
using IntPtr = int*;
using FuncPtr = void(*)(int, int);

// More readable for complex types
using StringVector = std::vector<std::string>;
using IntMap = std::map<std::string, int>;

// Template aliases (only with using!)
template<typename T>
using Vec = std::vector<T>;

Vec<int> v1;        // std::vector<int>
Vec<std::string> v2; // std::vector<std::string>

// Function pointer alias
using Callback = std::function<void(int)>;
Callback cb = [](int x) { std::cout << x; };
```

### typedef vs using

| Feature | typedef | using |
|---------|---------|-------|
| **Syntax** | C-style | Modern, clearer |
| **Template aliases** | No | Yes |
| **Readability** | Less clear for complex types | More clear |
| **Recommendation** | Legacy code | Prefer in new code |

```cpp
// typedef - harder to read
typedef void (*ComplexFunc)(int, double, std::string);

// using - clearer
using ComplexFunc = void(*)(int, double, std::string);

// Template alias (only using)
template<typename T>
using Ptr = std::shared_ptr<T>;

Ptr<int> p = std::make_shared<int>(42);
```

---

## Unions & Enumerations

### Unions

```cpp
// Union: all members share same memory
union Data {
    int i;
    float f;
    char c;
};

Data d;
d.i = 10;
std::cout << d.i;  // 10
d.f = 3.14f;
std::cout << d.i;  // Undefined! (memory reinterpreted)

// Size is size of largest member
static_assert(sizeof(Data) >= sizeof(float));

// Anonymous union
struct Packet {
    int type;
    union {
        int int_val;
        float float_val;
        char char_val;
    };  // Anonymous union
};

Packet p;
p.type = 1;
p.int_val = 42;  // Direct access
```

### Tagged Union (Discriminated Union)

```cpp
struct Value {
    enum Type { INT, FLOAT, STRING } type;
    
    union {
        int i;
        float f;
        char* s;
    };
    
    Value(int val) : type(INT), i(val) {}
    Value(float val) : type(FLOAT), f(val) {}
    Value(const char* val) : type(STRING), s(strdup(val)) {}
    
    ~Value() {
        if (type == STRING) free(s);
    }
};

// C++17: std::variant (type-safe alternative)
#include <variant>
std::variant<int, float, std::string> v = 42;
v = 3.14f;
v = "hello";
```

### Enumerations

```cpp
// Traditional enum (C-style)
enum Color {
    RED,      // 0
    GREEN,    // 1
    BLUE      // 2
};

Color c = RED;
int val = c;  // Implicit conversion to int

// Enum with explicit values
enum Status {
    OK = 0,
    ERROR = -1,
    PENDING = 100
};

// Enum class (C++11) - Strongly typed
enum class TrafficLight {
    Red,
    Yellow,
    Green
};

TrafficLight light = TrafficLight::Red;
// int x = light;  // Error: no implicit conversion
int x = static_cast<int>(light);  // Explicit conversion

// Specify underlying type
enum class Byte : uint8_t {
    Zero = 0,
    Max = 255
};

// Enum class comparison
if (light == TrafficLight::Red) {
    // Stop
}
```

### enum vs enum class

| Feature | enum | enum class |
|---------|------|------------|
| **Scope** | Global scope | Scoped to enum |
| **Implicit conversion** | Yes (to int) | No |
| **Type safety** | Weak | Strong |
| **Underlying type** | Implementation-defined | Can specify |
| **Recommendation** | Legacy code | Prefer in new code |

```cpp
// enum - name pollution
enum Color { Red, Green, Blue };
enum Status { Red, Green };  // Error: redefinition!

// enum class - no pollution
enum class Color { Red, Green, Blue };
enum class Status { Red, Green };  // OK!

Color c = Color::Red;
Status s = Status::Red;
// if (c == s) {}  // Error: different types
```

---

## Files & File Streams

### File Stream Classes

| Class | Purpose | Header |
|-------|---------|--------|
| `std::ifstream` | Input file stream (reading) | `<fstream>` |
| `std::ofstream` | Output file stream (writing) | `<fstream>` |
| `std::fstream` | Input/output file stream | `<fstream>` |

### Writing to Files

```cpp
#include <fstream>
#include <iostream>

// Method 1: Constructor
std::ofstream outfile("output.txt");
if (outfile.is_open()) {
    outfile << "Hello, World!\n";
    outfile << "Line 2\n";
    outfile.close();
}

// Method 2: open()
std::ofstream out;
out.open("output.txt", std::ios::out);
if (out) {
    out << "Data\n";
    out.close();
}

// Append mode
std::ofstream append_file("log.txt", std::ios::app);
append_file << "New log entry\n";
append_file.close();

// Binary mode
std::ofstream binary_file("data.bin", std::ios::binary);
int data[] = {1, 2, 3, 4, 5};
binary_file.write(reinterpret_cast<char*>(data), sizeof(data));
binary_file.close();
```

### Reading from Files

```cpp
#include <fstream>
#include <string>

// Read line by line
std::ifstream infile("input.txt");
std::string line;
while (std::getline(infile, line)) {
    std::cout << line << "\n";
}
infile.close();

// Read word by word
std::ifstream in("data.txt");
std::string word;
while (in >> word) {
    std::cout << word << " ";
}
in.close();

// Read entire file
std::ifstream file("file.txt");
std::string content((std::istreambuf_iterator<char>(file)),
                     std::istreambuf_iterator<char>());
file.close();

// Binary read
std::ifstream binary_in("data.bin", std::ios::binary);
int data[5];
binary_in.read(reinterpret_cast<char*>(data), sizeof(data));
binary_in.close();
```

### File Open Modes

| Mode | Description |
|------|-------------|
| `std::ios::in` | Open for reading |
| `std::ios::out` | Open for writing |
| `std::ios::app` | Append to end |
| `std::ios::ate` | Seek to end on open |
| `std::ios::trunc` | Truncate file if exists |
| `std::ios::binary` | Binary mode |

```cpp
// Combine modes with |
std::fstream file("data.txt", std::ios::in | std::ios::out | std::ios::binary);
```

### File Operations

```cpp
#include <fstream>

std::fstream file("data.txt", std::ios::in | std::ios::out);

// Check if open
if (!file.is_open()) {
    std::cerr << "Failed to open file\n";
    return;
}

// Get/set position
file.seekg(0, std::ios::beg);  // Seek to beginning (get)
file.seekp(0, std::ios::end);  // Seek to end (put)

// Get current position
std::streampos pos = file.tellg();

// Check end of file
if (file.eof()) {
    std::cout << "End of file reached\n";
}

// Check for errors
if (file.fail()) {
    std::cerr << "I/O error\n";
}

// Clear error flags
file.clear();

// Close file
file.close();
```

### RAII File Handling

```cpp
class FileGuard {
private:
    std::fstream file;
    
public:
    FileGuard(const std::string& filename, std::ios::openmode mode)
        : file(filename, mode) {
        if (!file.is_open()) {
            throw std::runtime_error("Cannot open file");
        }
    }
    
    ~FileGuard() {
        if (file.is_open()) {
            file.close();
        }
    }
    
    std::fstream& get() { return file; }
};

// Usage - automatic cleanup
void process() {
    FileGuard fg("data.txt", std::ios::in);
    std::string line;
    while (std::getline(fg.get(), line)) {
        // Process line
    }
    // File automatically closed
}
```

### C++17: std::filesystem

```cpp
#include <filesystem>
namespace fs = std::filesystem;

// Check if file exists
if (fs::exists("file.txt")) {
    std::cout << "File exists\n";
}

// Get file size
auto size = fs::file_size("file.txt");

// Copy file
fs::copy_file("source.txt", "dest.txt");

// Remove file
fs::remove("file.txt");

// Create directory
fs::create_directory("new_dir");

// Iterate directory
for (const auto& entry : fs::directory_iterator(".")) {
    std::cout << entry.path() << "\n";
}

// Get file path components
fs::path p = "/home/user/file.txt";
std::cout << p.filename() << "\n";    // file.txt
std::cout << p.extension() << "\n";   // .txt
std::cout << p.parent_path() << "\n"; // /home/user
```

---

## Smart Pointers

### std::unique_ptr

```cpp
#include <memory>

// Exclusive ownership
std::unique_ptr<int> ptr1 = std::make_unique<int>(42);
// std::unique_ptr<int> ptr2 = ptr1;  // Error: cannot copy

// Can move
std::unique_ptr<int> ptr2 = std::move(ptr1);  // ptr1 is now nullptr

// Array version
std::unique_ptr<int[]> arr = std::make_unique<int[]>(10);
arr[0] = 42;

// Custom deleter
auto deleter = [](int* p) {
    std::cout << "Deleting " << *p << "\n";
    delete p;
};
std::unique_ptr<int, decltype(deleter)> ptr3(new int(10), deleter);
```

### std::shared_ptr

```cpp
// Shared ownership (reference counted)
std::shared_ptr<int> ptr1 = std::make_shared<int>(42);
std::shared_ptr<int> ptr2 = ptr1;  // OK: both own the resource

std::cout << ptr1.use_count();  // 2

ptr2.reset();  // Decrements reference count
std::cout << ptr1.use_count();  // 1

// Resource deleted when last shared_ptr is destroyed
```

### std::weak_ptr

```cpp
// Non-owning reference (breaks circular references)
std::shared_ptr<int> sptr = std::make_shared<int>(42);
std::weak_ptr<int> wptr = sptr;

// Check if resource still exists
if (auto locked = wptr.lock()) {
    std::cout << *locked;  // 42
}

sptr.reset();  // Resource deleted
if (wptr.expired()) {
    std::cout << "Resource no longer exists\n";
}
```

### Circular Reference Problem

```cpp
struct Node {
    std::shared_ptr<Node> next;
    std::weak_ptr<Node> prev;  // Use weak_ptr to break cycle!
};

std::shared_ptr<Node> n1 = std::make_shared<Node>();
std::shared_ptr<Node> n2 = std::make_shared<Node>();
n1->next = n2;
n2->prev = n1;  // No circular reference!
```

---

## STL Containers

### Container Overview & Complexity

| Container | Type | Ordered | Duplicates | Access | Insert (end) | Insert (middle) | Delete | Search | Header |
|-----------|------|---------|------------|--------|--------------|-----------------|--------|--------|--------|
| `array` | Sequence | No | Yes | O(1) | N/A | N/A | N/A | O(n) | `<array>` |
| `vector` | Sequence | No | Yes | O(1) | O(1) amortized | O(n) | O(n) | O(n) | `<vector>` |
| `stack` | Adapter | No | Yes | O(1) top | O(1) | N/A | O(1) | N/A | `<stack>` |
| `queue` | Adapter | No | Yes | O(1) front/back | O(1) | N/A | O(1) | N/A | `<queue>` |
| `deque` | Sequence | No | Yes | O(1) | O(1) | O(n) | O(n) | O(n) | `<deque>` |
| `priority_queue` | Adapter | Yes (heap) | Yes | O(1) top | O(log n) | N/A | O(log n) | N/A | `<queue>` |
| `list` | Sequence | No | Yes | O(n) | O(1) | O(1) | O(1) | O(n) | `<list>` |
| `forward_list` | Sequence | No | Yes | O(n) | O(1) | O(1) | O(1) | O(n) | `<forward_list>` |
| `map` | Associative | Yes (by key) | No | O(log n) | O(log n) | O(log n) | O(log n) | O(log n) | `<map>` |
| `multimap` | Associative | Yes (by key) | Yes | O(log n) | O(log n) | O(log n) | O(log n) | O(log n) | `<map>` |
| `unordered_map` | Unordered | No | No | O(1) avg | O(1) avg | O(1) avg | O(1) avg | O(1) avg | `<unordered_map>` |
| `unordered_multimap` | Unordered | No | Yes | O(1) avg | O(1) avg | O(1) avg | O(1) avg | O(1) avg | `<unordered_map>` |
| `set` | Associative | Yes | No | O(log n) | O(log n) | O(log n) | O(log n) | O(log n) | `<set>` |
| `multiset` | Associative | Yes | Yes | O(log n) | O(log n) | O(log n) | O(log n) | O(log n) | `<set>` |
| `unordered_set` | Unordered | No | No | O(1) avg | O(1) avg | O(1) avg | O(1) avg | O(1) avg | `<unordered_set>` |
| `unordered_multiset` | Unordered | No | Yes | O(1) avg | O(1) avg | O(1) avg | O(1) avg | O(1) avg | `<unordered_set>` |


---

### std::pair

```cpp
#include <utility>

// Declaration & Initialization
std::pair<int, std::string> p1(1, "one");
std::pair<int, std::string> p2 = {2, "two"};
auto p3 = std::make_pair(3, "three");

// Access
int first = p1.first;           // 1
std::string second = p1.second; // "one"

// Comparison (lexicographic)
std::pair<int, int> a(1, 2), b(1, 3);
bool less = a < b;  // true (compares first, then second)

// Swap
p1.swap(p2);

// Output: 1 one
std::cout << p1.first << " " << p1.second << "\n";
```

**Time Complexity:** All operations O(1)

---

### std::array

**Fixed-size array (C++11)**

```cpp
#include <array>

// Declaration & Initialization
std::array<int, 5> arr = {1, 2, 3, 4, 5};
std::array<int, 5> arr2{};  // All zeros

// Access - O(1)
int x = arr[2];
int y = arr.at(2);
int first = arr.front();
int last = arr.back();
int* data = arr.data();

// Modification (size is fixed!)
arr[0] = 10;
arr.fill(42);  // Fill all with 42 - O(n)

// Capacity
size_t sz = arr.size();      // Always 5
size_t max_sz = arr.max_size();
bool empty = arr.empty();

// Iterators: begin(), end(), rbegin(), rend()

// Swap
std::array<int, 5> arr3 = {6, 7, 8, 9, 10};
arr.swap(arr3);  // O(n)

// Output: 1 2 3 4 5
```

---

### std::vector

**Dynamic array with contiguous memory**

```cpp
#include <vector>

// Declaration & Initialization
std::vector<int> v1;                    // Empty
std::vector<int> v2(5);                 // 5 elements (default 0)
std::vector<int> v3(5, 10);             // 5 elements (all 10)
std::vector<int> v4 = {1, 2, 3, 4, 5};  // Initializer list
std::vector<int> v5(v4);                // Copy constructor
std::vector<int> v6(v4.begin(), v4.end()); // Range constructor

// Access - O(1)
int x = v4[2];          // No bounds check
int y = v4.at(2);       // Bounds check (throws)
int first = v4.front(); // First element
int last = v4.back();   // Last element
int* data = v4.data();  // Pointer to underlying array

// Modification
v4.push_back(6);        // Add to end - O(1) amortized
v4.pop_back();          // Remove from end - O(1)
v4.emplace_back(7);     // Construct in place - O(1) amortized
v4.insert(v4.begin() + 2, 10);  // Insert at position - O(n)
v4.erase(v4.begin() + 2);       // Erase at position - O(n)
v4.erase(v4.begin(), v4.begin() + 3); // Erase range - O(n)
v4.clear();             // Remove all - O(n)
v4.assign(5, 100);      // Assign 5 elements of value 100 - O(n)

// Capacity
size_t sz = v4.size();      // Number of elements - O(1)
size_t cap = v4.capacity(); // Allocated capacity - O(1)
bool empty = v4.empty();    // Check if empty - O(1)
v4.reserve(100);            // Reserve capacity - O(n)
v4.shrink_to_fit();         // Reduce capacity to size - O(n)
v4.resize(10);              // Resize to 10 elements - O(n)
v4.resize(15, 42);          // Resize to 15, new elements = 42 - O(n)

// Iterators
auto it = v4.begin();       // Iterator to first
auto end = v4.end();        // Iterator past last
auto rit = v4.rbegin();     // Reverse iterator to last
auto rend = v4.rend();      // Reverse iterator before first

// Iteration
for (int x : v4) { std::cout << x << " "; }
for (auto it = v4.begin(); it != v4.end(); ++it) { std::cout << *it << " "; }
for (auto it = v4.rbegin(); it != v4.rend(); ++it) { std::cout << *it << " "; }

// Swap
std::vector<int> v7 = {1, 2, 3};
v4.swap(v7);  // O(1)

// Output: 1 2 3 4 5
```

---

### std::stack

**LIFO stack (adapter)**

```cpp
#include <stack>

// Declaration & Initialization
std::stack<int> st;
std::stack<int, std::vector<int>> st_vec;  // Specify underlying container

// Modification
st.push(1);         // Add to top - O(1)
st.push(2);
st.push(3);
st.emplace(4);      // Construct in place - O(1)
st.pop();           // Remove from top - O(1)

// Access
int top = st.top(); // Access top - O(1)

// Capacity
size_t sz = st.size();
bool empty = st.empty();

// Swap
std::stack<int> st2;
st.swap(st2);

// Output: 3 (top element)
```

---

### std::queue

**FIFO queue (adapter)**

```cpp
#include <queue>

// Declaration & Initialization
std::queue<int> q;
std::queue<int, std::list<int>> q_list;  // Specify underlying container

// Modification
q.push(1);          // Add to back - O(1)
q.push(2);
q.push(3);
q.emplace(4);       // Construct in place - O(1)
q.pop();            // Remove from front - O(1)

// Access
int front = q.front();  // Access front - O(1)
int back = q.back();    // Access back - O(1)

// Capacity
size_t sz = q.size();
bool empty = q.empty();

// Swap
std::queue<int> q2;
q.swap(q2);

// Output: front=2, back=4
```

---

### std::deque

**Double-ended queue (efficient insertion/deletion at both ends)**

```cpp
#include <deque>

// Declaration & Initialization
std::deque<int> dq = {1, 2, 3, 4, 5};

// Access - O(1)
int x = dq[2];
int y = dq.at(2);
int first = dq.front();
int last = dq.back();

// Modification
dq.push_back(6);        // Add to end - O(1)
dq.push_front(0);       // Add to front - O(1)
dq.pop_back();          // Remove from end - O(1)
dq.pop_front();         // Remove from front - O(1)
dq.emplace_back(7);     // Construct at end - O(1)
dq.emplace_front(-1);   // Construct at front - O(1)
dq.insert(dq.begin() + 2, 10);  // Insert - O(n)
dq.erase(dq.begin() + 2);       // Erase - O(n)
dq.clear();             // Remove all - O(n)

// Capacity
size_t sz = dq.size();
bool empty = dq.empty();
dq.resize(10);

// Iterators: begin(), end(), rbegin(), rend()

// Output: 0 1 2 3 4 5 6
```

---

### std::priority_queue

**Max heap by default (adapter)**

```cpp
#include <queue>

// Declaration & Initialization
std::priority_queue<int> pq;  // Max heap
std::priority_queue<int, std::vector<int>, std::greater<int>> min_pq;  // Min heap

// Custom comparator
auto cmp = [](int a, int b) { return a > b; };  // Min heap
std::priority_queue<int, std::vector<int>, decltype(cmp)> custom_pq(cmp);

// Modification
pq.push(3);         // Insert - O(log n)
pq.push(1);
pq.push(4);
pq.push(1);
pq.push(5);
pq.emplace(9);      // Construct in place - O(log n)
pq.pop();           // Remove top - O(log n)

// Access
int top = pq.top(); // Access top (max) - O(1)

// Capacity
size_t sz = pq.size();
bool empty = pq.empty();

// Swap
std::priority_queue<int> pq2;
pq.swap(pq2);

// Output: 5 (max element after removing 9)

// Min heap example
min_pq.push(3);
min_pq.push(1);
min_pq.push(4);
int min = min_pq.top();  // 1
```

---

### std::list

**Doubly-linked list**

```cpp
#include <list>

// Declaration & Initialization
std::list<int> lst = {1, 2, 3, 4, 5};

// Access - O(n) (no random access)
int first = lst.front();
int last = lst.back();

// Modification
lst.push_back(6);       // Add to end - O(1)
lst.push_front(0);      // Add to front - O(1)
lst.pop_back();         // Remove from end - O(1)
lst.pop_front();        // Remove from front - O(1)
lst.emplace_back(7);    // Construct at end - O(1)
lst.emplace_front(-1);  // Construct at front - O(1)

auto it = lst.begin();
std::advance(it, 2);    // Move iterator - O(n)
lst.insert(it, 10);     // Insert at iterator - O(1)
lst.erase(it);          // Erase at iterator - O(1)
lst.clear();            // Remove all - O(n)

// List-specific operations
lst.remove(3);          // Remove all elements == 3 - O(n)
lst.remove_if([](int x) { return x % 2 == 0; }); // Remove if predicate - O(n)
lst.unique();           // Remove consecutive duplicates - O(n)
lst.sort();             // Sort - O(n log n)
lst.reverse();          // Reverse - O(n)

std::list<int> lst2 = {10, 20, 30};
lst.merge(lst2);        // Merge sorted lists - O(n)
lst.splice(lst.begin(), lst2);  // Transfer elements - O(1)

// Capacity
size_t sz = lst.size();
bool empty = lst.empty();

// Iterators: begin(), end(), rbegin(), rend()

// Output: 0 1 2 10 3 4 5 6
```

---

### std::forward_list

**Singly-linked list (more memory efficient than list)**

```cpp
#include <forward_list>

// Declaration & Initialization
std::forward_list<int> flst = {1, 2, 3, 4, 5};

// Access
int first = flst.front();  // No back()!

// Modification
flst.push_front(0);        // Add to front - O(1)
flst.pop_front();          // Remove from front - O(1)
flst.emplace_front(-1);    // Construct at front - O(1)

auto it = flst.before_begin();
flst.insert_after(it, 10); // Insert after iterator - O(1)
flst.erase_after(it);      // Erase after iterator - O(1)
flst.clear();              // Remove all - O(n)

// List-specific operations
flst.remove(3);
flst.remove_if([](int x) { return x % 2 == 0; });
flst.unique();
flst.sort();
flst.reverse();

// Capacity
bool empty = flst.empty();
// No size() method!

// Iterators: begin(), end() (no reverse iterators)

// Output: -1 0 10 1 2 3 4 5
```

---

### std::map

**Ordered map (Red-Black Tree, key-value pairs)**

```cpp
#include <map>

// Declaration & Initialization
std::map<std::string, int> m;
std::map<std::string, int> m2 = {{"Alice", 30}, {"Bob", 25}};
std::map<int, std::string, std::greater<int>> m_desc;  // Descending by key

// Insertion - O(log n)
m["Charlie"] = 35;       // Insert or update
m.insert({"David", 40});
m.insert(std::make_pair("Eve", 28));
m.emplace("Frank", 32);
auto [it, inserted] = m.insert({"Alice", 30});

// Access - O(log n)
int age = m["Alice"];    // Creates if doesn't exist!
int age2 = m.at("Bob");  // Throws if doesn't exist

// Deletion - O(log n)
m.erase("Charlie");      // Erase by key
m.erase(m.begin());      // Erase by iterator
m.clear();               // Remove all

// Search - O(log n)
auto it = m.find("Alice");
bool exists = m.count("Alice") > 0;
bool contains = m.contains("Alice");  // C++20

// Bounds - O(log n)
auto lb = m.lower_bound("Bob");
auto ub = m.upper_bound("Bob");

// Capacity
size_t sz = m.size();
bool empty = m.empty();

// Iterators: begin(), end(), rbegin(), rend()
for (const auto& [key, value] : m) {  // C++17 structured binding
    std::cout << key << ": " << value << "\n";
}

// Output:
// Alice: 30
// Bob: 25
// Charlie: 35
```

---

### std::multimap

**Ordered multimap (allows duplicate keys)**

```cpp
#include <map>

// Declaration & Initialization
std::multimap<std::string, int> mm;

// Insertion - O(log n)
mm.insert({"Alice", 30});
mm.insert({"Alice", 31});  // Duplicate key allowed
mm.emplace("Bob", 25);

// No operator[] (ambiguous with duplicates)

// Search - O(log n)
int count = mm.count("Alice");  // Returns 2
auto range = mm.equal_range("Alice");  // Returns pair of iterators
for (auto it = range.first; it != range.second; ++it) {
    std::cout << it->first << ": " << it->second << "\n";
}

// Deletion - O(log n)
mm.erase("Alice");  // Erases all entries with key "Alice"

// Output:
// Alice: 30
// Alice: 31
```
---

### std::unordered_map

**Hash map (unordered key-value pairs)**

```cpp
#include <unordered_map>

// Declaration & Initialization
std::unordered_map<std::string, int> um;
std::unordered_map<std::string, int> um2 = {{"Alice", 30}, {"Bob", 25}};

// Insertion - O(1) average
um["Charlie"] = 35;
um.insert({"David", 40});
um.emplace("Eve", 28);

// Access - O(1) average
int age = um["Alice"];
int age2 = um.at("Bob");

// Deletion - O(1) average
um.erase("Charlie");
um.clear();

// Search - O(1) average
auto it = um.find("Alice");
bool exists = um.count("Alice") > 0;
bool contains = um.contains("Alice");  // C++20

// Capacity
size_t sz = um.size();
bool empty = um.empty();

// Hash table properties
size_t buckets = um.bucket_count();
float load = um.load_factor();

// Iterators: begin(), end() (no ordering)
for (const auto& [key, value] : um) {
    std::cout << key << ": " << value << "\n";
}

// Output (order not guaranteed):
// Bob: 25
// Alice: 30
// David: 40
```

---

### std::unordered_multimap

**Hash multimap (allows duplicate keys)**

```cpp
#include <unordered_map>

std::unordered_multimap<std::string, int> umm;
umm.insert({"Alice", 30});
umm.insert({"Alice", 31});  // Duplicate key allowed
int count = umm.count("Alice");  // Returns 2

// Output (order not guaranteed):
// Alice: 30
// Alice: 31
```

---

### Container Adapters Summary

| Adapter | Underlying Container | Operations | Use Case |
|---------|---------------------|------------|----------|
| `stack` | `deque` (default), `vector`, `list` | `push`, `pop`, `top` | LIFO operations |
| `queue` | `deque` (default), `list` | `push`, `pop`, `front`, `back` | FIFO operations |
| `priority_queue` | `vector` (default), `deque` | `push`, `pop`, `top` | Heap operations |

---

### std::set

**Ordered set (Red-Black Tree, unique elements)**

```cpp
#include <set>

// Declaration & Initialization
std::set<int> s = {3, 1, 4, 1, 5, 9};  // Sorted, unique: {1, 3, 4, 5, 9}
std::set<int, std::greater<int>> s_desc;  // Descending order

// Insertion - O(log n)
s.insert(2);
s.insert({6, 7, 8});
s.emplace(10);
auto [it, inserted] = s.insert(5);  // Returns pair<iterator, bool>

// Deletion - O(log n)
s.erase(3);              // Erase by value
s.erase(s.begin());      // Erase by iterator
s.erase(s.begin(), s.find(5));  // Erase range
s.clear();               // Remove all

// Search - O(log n)
auto it = s.find(4);     // Returns iterator or end()
bool exists = s.count(4) > 0;  // Returns 0 or 1
bool contains = s.contains(4);  // C++20

// Bounds - O(log n)
auto lb = s.lower_bound(4);  // First >= 4
auto ub = s.upper_bound(4);  // First > 4
auto [low, high] = s.equal_range(4);  // Range of elements == 4

// Capacity
size_t sz = s.size();
bool empty = s.empty();

// Iterators: begin(), end(), rbegin(), rend()
for (int x : s) { std::cout << x << " "; }  // Sorted order

// Output: 1 2 3 4 5 6 7 8 9 10
```

---

### std::multiset

**Ordered multiset (allows duplicates)**

```cpp
#include <set>

// Declaration & Initialization
std::multiset<int> ms = {3, 1, 4, 1, 5, 9, 1};  // {1, 1, 1, 3, 4, 5, 9}

// All operations same as set, but:
ms.insert(1);  // Can insert duplicates
int count = ms.count(1);  // Returns number of occurrences (4)

// Erase all occurrences
ms.erase(1);  // Removes all 1s

// Erase single occurrence
auto it = ms.find(3);
if (it != ms.end()) ms.erase(it);

// Output: 1 1 1 1 3 4 5 9
```

---

### std::unordered_set

**Hash set (unordered, unique elements)**

```cpp
#include <unordered_set>

// Declaration & Initialization
std::unordered_set<int> us = {3, 1, 4, 1, 5, 9};  // Unordered, unique

// Insertion - O(1) average
us.insert(2);
us.emplace(10);

// Deletion - O(1) average
us.erase(3);
us.clear();

// Search - O(1) average
auto it = us.find(4);
bool exists = us.count(4) > 0;
bool contains = us.contains(4);  // C++20

// Capacity
size_t sz = us.size();
bool empty = us.empty();

// Hash table properties
size_t buckets = us.bucket_count();
float load = us.load_factor();
float max_load = us.max_load_factor();
us.rehash(100);  // Set bucket count
us.reserve(100);  // Reserve for at least 100 elements

// Iterators: begin(), end() (no reverse iterators, no ordering)
for (int x : us) { std::cout << x << " "; }  // Unordered

// Output: 9 5 4 2 1 (order not guaranteed)
```

---

### std::unordered_multiset

**Hash multiset (allows duplicates)**

```cpp
#include <unordered_set>

std::unordered_multiset<int> ums = {1, 2, 2, 3, 3, 3};
ums.insert(2);  // Can insert duplicates
int count = ums.count(2);  // Returns 3

// Output: 3 3 3 2 2 2 1 (order not guaranteed)
```
---

## STL Algorithms

```cpp
#include <algorithm>
#include <numeric>
#include <vector>

std::vector<int> vec = {3, 1, 4, 1, 5, 9, 2, 6};
```

### Sorting & Searching

```cpp
// Sort
std::sort(vec.begin(), vec.end());  // Ascending
std::sort(vec.begin(), vec.end(), std::greater<int>());  // Descending

// Binary search (requires sorted)
bool found = std::binary_search(vec.begin(), vec.end(), 5);
auto it = std::lower_bound(vec.begin(), vec.end(), 5);  // First >= 5
auto it2 = std::upper_bound(vec.begin(), vec.end(), 5);  // First > 5

// Find
auto it3 = std::find(vec.begin(), vec.end(), 5);
if (it3 != vec.end()) { /* found */ }

// Find with predicate
auto it4 = std::find_if(vec.begin(), vec.end(), [](int x) { return x > 5; });
```

### Modifying Algorithms

```cpp
// Transform
std::vector<int> result(vec.size());
std::transform(vec.begin(), vec.end(), result.begin(), [](int x) {
    return x * 2;
});

// Fill
std::fill(vec.begin(), vec.end(), 0);

// Replace
std::replace(vec.begin(), vec.end(), 1, 10);  // Replace all 1s with 10

// Remove (doesn't actually remove, returns new end)
auto new_end = std::remove(vec.begin(), vec.end(), 5);
vec.erase(new_end, vec.end());  // Actually remove

// Remove if
vec.erase(std::remove_if(vec.begin(), vec.end(), [](int x) {
    return x % 2 == 0;
}), vec.end());

// Unique (remove consecutive duplicates)
std::sort(vec.begin(), vec.end());
auto last = std::unique(vec.begin(), vec.end());
vec.erase(last, vec.end());
```

### Numeric Algorithms

```cpp
// Accumulate (sum)
int sum = std::accumulate(vec.begin(), vec.end(), 0);

// Product
int product = std::accumulate(vec.begin(), vec.end(), 1, std::multiplies<int>());

// Min/Max
int min_val = *std::min_element(vec.begin(), vec.end());
int max_val = *std::max_element(vec.begin(), vec.end());
auto [min_it, max_it] = std::minmax_element(vec.begin(), vec.end());

// Count
int count = std::count(vec.begin(), vec.end(), 5);
int count_if = std::count_if(vec.begin(), vec.end(), [](int x) { return x > 5; });
```

### Other Useful Algorithms

```cpp
// Reverse
std::reverse(vec.begin(), vec.end());

// Rotate
std::rotate(vec.begin(), vec.begin() + 3, vec.end());

// Shuffle
std::random_device rd;
std::mt19937 g(rd());
std::shuffle(vec.begin(), vec.end(), g);

// Partition
auto pivot = std::partition(vec.begin(), vec.end(), [](int x) {
    return x % 2 == 0;
});

// All/Any/None of
bool all_positive = std::all_of(vec.begin(), vec.end(), [](int x) { return x > 0; });
bool any_negative = std::any_of(vec.begin(), vec.end(), [](int x) { return x < 0; });
bool none_zero = std::none_of(vec.begin(), vec.end(), [](int x) { return x == 0; });
```

---

## Strings

### std::string Operations

```cpp
#include <string>

std::string s = "hello";

// Concatenation
s += " world";
s = s + "!";
s.append(" more");

// Access
char c = s[0];         // No bounds check
char c2 = s.at(0);     // Bounds check
char first = s.front();
char last = s.back();

// Substring
std::string sub = s.substr(0, 5);  // "hello"

// Find
size_t pos = s.find("world");
if (pos != std::string::npos) { /* found */ }

size_t last_pos = s.rfind("o");  // Find from end

// Replace
s.replace(0, 5, "hi");  // Replace "hello" with "hi"

// Insert/Erase
s.insert(2, "XX");
s.erase(2, 2);

// Compare
int cmp = s.compare("hello");  // <0, 0, or >0

// Conversion
int num = std::stoi("123");
double d = std::stod("3.14");
std::string str = std::to_string(42);

// C-string
const char* cstr = s.c_str();
```

### String Streams

```cpp
#include <sstream>

// String to stream
std::istringstream iss("10 20 30");
int a, b, c;
iss >> a >> b >> c;

// Stream to string
std::ostringstream oss;
oss << "Value: " << 42;
std::string result = oss.str();

// String stream (both input and output)
std::stringstream ss;
ss << 100;
int value;
ss >> value;
```

---

## Concurrency & Multithreading

### std::thread

```cpp
#include <thread>
#include <iostream>

void task(int id) {
    std::cout << "Thread " << id << "\n";
}

int main() {
    std::thread t1(task, 1);
    std::thread t2(task, 2);
    
    t1.join();  // Wait for t1 to finish
    t2.join();  // Wait for t2 to finish
    
    // Or detach (runs independently)
    std::thread t3(task, 3);
    t3.detach();
}
```

### Mutex & Lock Guard

```cpp
#include <mutex>

std::mutex mtx;
int shared_counter = 0;

void increment() {
    std::lock_guard<std::mutex> lock(mtx);  // RAII lock
    ++shared_counter;
    // Automatically unlocked when lock goes out of scope
}

// Unique lock (more flexible)
void increment2() {
    std::unique_lock<std::mutex> lock(mtx);
    ++shared_counter;
    lock.unlock();  // Can manually unlock
    // Do other work
    lock.lock();    // Can relock
}
```

### Condition Variables

```cpp
#include <condition_variable>
#include <queue>

std::mutex mtx;
std::condition_variable cv;
std::queue<int> data_queue;

// Producer
void producer() {
    for (int i = 0; i < 10; ++i) {
        std::unique_lock<std::mutex> lock(mtx);
        data_queue.push(i);
        cv.notify_one();  // Wake up one waiting thread
    }
}

// Consumer
void consumer() {
    while (true) {
        std::unique_lock<std::mutex> lock(mtx);
        cv.wait(lock, [] { return !data_queue.empty(); });
        int value = data_queue.front();
        data_queue.pop();
        lock.unlock();
        // Process value
    }
}
```

### std::async & std::future

```cpp
#include <future>

int compute(int x) {
    return x * x;
}

int main() {
    // Launch async task
    std::future<int> result = std::async(std::launch::async, compute, 5);
    
    // Do other work...
    
    // Get result (blocks if not ready)
    int value = result.get();  // 25
}
```

### std::promise

```cpp
void task(std::promise<int> prom) {
    // Do work
    prom.set_value(42);  // Set result
}

int main() {
    std::promise<int> prom;
    std::future<int> fut = prom.get_future();
    
    std::thread t(task, std::move(prom));
    
    int result = fut.get();  // Wait for result
    t.join();
}
```

---

## Memory Model & Atomics

### std::atomic

```cpp
#include <atomic>

std::atomic<int> counter(0);

void increment() {
    counter++;  // Atomic operation
    counter.fetch_add(1);  // Explicit atomic add
}

// Compare and swap
int expected = 5;
int desired = 10;
bool success = counter.compare_exchange_strong(expected, desired);
```

### Memory Ordering

```cpp
std::atomic<int> x(0);
std::atomic<int> y(0);

// Relaxed (no synchronization)
x.store(1, std::memory_order_relaxed);

// Acquire-Release (synchronization)
x.store(1, std::memory_order_release);
int val = x.load(std::memory_order_acquire);

// Sequential consistency (default, strongest)
x.store(1, std::memory_order_seq_cst);
```

---

## Exception Handling

### Basic Exception Handling

```cpp
try {
    // Code that may throw
    throw std::runtime_error("Error occurred");
} catch (const std::runtime_error& e) {
    std::cerr << "Runtime error: " << e.what() << "\n";
} catch (const std::exception& e) {
    std::cerr << "Exception: " << e.what() << "\n";
} catch (...) {
    std::cerr << "Unknown exception\n";
}
```

### Standard Exception Hierarchy

```
std::exception
├── std::logic_error
│   ├── std::invalid_argument
│   ├── std::domain_error
│   ├── std::length_error
│   └── std::out_of_range
└── std::runtime_error
    ├── std::range_error
    ├── std::overflow_error
    └── std::underflow_error
```

### Custom Exceptions

```cpp
class MyException : public std::exception {
private:
    std::string message;
    
public:
    MyException(const std::string& msg) : message(msg) {}
    
    const char* what() const noexcept override {
        return message.c_str();
    }
};

// Usage
throw MyException("Custom error");
```

### Exception Safety Guarantees

1. **No-throw guarantee:** Never throws exceptions
2. **Strong guarantee:** If exception thrown, program state unchanged
3. **Basic guarantee:** If exception thrown, no resources leaked
4. **No guarantee:** May leak resources or corrupt state

```cpp
// No-throw
void foo() noexcept {
    // Cannot throw
}

// Conditional noexcept
template<typename T>
void bar(T t) noexcept(noexcept(T(t))) {
    // noexcept if T's copy constructor is noexcept
}
```

---

## Namespaces

### Defining Namespaces

```cpp
namespace MyNamespace {
    int value = 42;
    void function() {}
    
    namespace Nested {
        int nested_value = 10;
    }
}

// Access
int x = MyNamespace::value;
MyNamespace::function();
int y = MyNamespace::Nested::nested_value;

// Using declaration
using MyNamespace::value;
int z = value;  // OK

// Using directive (avoid in headers!)
using namespace MyNamespace;
int w = value;  // OK
```

### Anonymous Namespaces

```cpp
namespace {
    // Internal linkage (like static)
    int internal_var = 10;
    void internal_func() {}
}
```

### Namespace Aliases

```cpp
namespace fs = std::filesystem;
fs::path p = "/path/to/file";
```

---

## Preprocessor & Macros

### Common Directives

```cpp
#define MAX 100                    // Object-like macro
#define SQUARE(x) ((x) * (x))      // Function-like macro
#undef MAX                         // Undefine

#include <iostream>                // Include header
#include "myheader.h"

#ifdef DEBUG                       // Conditional compilation
    // Debug code
#endif

#ifndef HEADER_H                   // Include guard
#define HEADER_H
    // Header content
#endif

#if VERSION > 2
    // Code for version > 2
#elif VERSION == 2
    // Code for version 2
#else
    // Code for other versions
#endif

#pragma once                       // Modern include guard
```

### Predefined Macros

```cpp
__FILE__      // Current file name
__LINE__      // Current line number
__DATE__      // Compilation date
__TIME__      // Compilation time
__cplusplus   // C++ standard version
__func__      // Current function name (C++11)
```

### Macro Techniques

```cpp
// Stringizing
#define TO_STRING(x) #x
TO_STRING(hello)  // "hello"

// Token pasting
#define CONCAT(a, b) a##b
CONCAT(hello, world)  // helloworld

// Variadic macros
#define LOG(fmt, ...) printf(fmt, __VA_ARGS__)
LOG("Value: %d\n", 42);
```

**Best Practice:** Prefer `constexpr`, `inline`, and templates over macros!

---

## Design Patterns in C++

### Singleton

```cpp
class Singleton {
private:
    Singleton() {}  // Private constructor
    
public:
    static Singleton& getInstance() {
        static Singleton instance;  // Thread-safe in C++11+
        return instance;
    }
    
    // Delete copy and move
    Singleton(const Singleton&) = delete;
    Singleton& operator=(const Singleton&) = delete;
};

// Usage
Singleton& s = Singleton::getInstance();
```

### Factory

```cpp
class Product {
public:
    virtual void use() = 0;
    virtual ~Product() = default;
};

class ConcreteProductA : public Product {
public:
    void use() override { std::cout << "Product A\n"; }
};

class ConcreteProductB : public Product {
public:
    void use() override { std::cout << "Product B\n"; }
};

class Factory {
public:
    static std::unique_ptr<Product> createProduct(char type) {
        if (type == 'A') return std::make_unique<ConcreteProductA>();
        if (type == 'B') return std::make_unique<ConcreteProductB>();
        return nullptr;
    }
};
```

### Observer

```cpp
class Observer {
public:
    virtual void update(int state) = 0;
    virtual ~Observer() = default;
};

class Subject {
private:
    std::vector<Observer*> observers;
    int state;
    
public:
    void attach(Observer* obs) {
        observers.push_back(obs);
    }
    
    void setState(int s) {
        state = s;
        notify();
    }
    
    void notify() {
        for (auto obs : observers) {
            obs->update(state);
        }
    }
};
```

### Strategy

```cpp
class Strategy {
public:
    virtual int execute(int a, int b) = 0;
    virtual ~Strategy() = default;
};

class AddStrategy : public Strategy {
public:
    int execute(int a, int b) override { return a + b; }
};

class MultiplyStrategy : public Strategy {
public:
    int execute(int a, int b) override { return a * b; }
};

class Context {
private:
    std::unique_ptr<Strategy> strategy;
    
public:
    void setStrategy(std::unique_ptr<Strategy> s) {
        strategy = std::move(s);
    }
    
    int executeStrategy(int a, int b) {
        return strategy->execute(a, b);
    }
};
```

---

## Performance & Optimization

### Compiler Optimizations

```bash
g++ -O0  # No optimization
g++ -O1  # Basic optimization
g++ -O2  # Recommended for production
g++ -O3  # Aggressive optimization
g++ -Os  # Optimize for size
```

### Inline Functions

```cpp
inline int add(int a, int b) {
    return a + b;
}
// Suggests compiler to substitute function body
// Reduces function call overhead
```

### constexpr

```cpp
constexpr int factorial(int n) {
    return (n <= 1) ? 1 : n * factorial(n - 1);
}

constexpr int result = factorial(5);  // Computed at compile time!
```

### Move Semantics

```cpp
// Avoid unnecessary copies
std::vector<int> createVector() {
    std::vector<int> v(1000000);
    return v;  // Move, not copy (RVO/NRVO)
}

std::vector<int> vec = createVector();  // No copy!
```

### Reserve Capacity

```cpp
std::vector<int> vec;
vec.reserve(1000);  // Avoid reallocations
for (int i = 0; i < 1000; ++i) {
    vec.push_back(i);
}
```

### Pass by Reference

```cpp
// Bad: copies large object
void process(std::vector<int> vec) { }

// Good: no copy
void process(const std::vector<int>& vec) { }
```

### Cache Locality

```cpp
// Bad: poor cache locality
struct Bad {
    int a;
    char padding[60];
    int b;
};

// Good: data together
struct Good {
    int a;
    int b;
};
```

### Profiling Tools

- **gprof:** GNU profiler
- **Valgrind:** Memory profiler
- **perf:** Linux performance analyzer
- **Intel VTune:** Advanced profiler

---

## Modern C++ Features by Standard

### C++11

- `auto` keyword
- Range-based for loops
- Lambda expressions
- `nullptr`
- Smart pointers (`unique_ptr`, `shared_ptr`, `weak_ptr`)
- Move semantics & rvalue references
- `constexpr`
- Variadic templates
- `std::thread`, `std::mutex`, `std::atomic`
- `std::array`, `std::unordered_map`, `std::unordered_set`
- Uniform initialization `{}`
- `override` and `final`
- Delegating constructors
- `static_assert`
- `decltype`

### C++14

- Generic lambdas
- `auto` return type deduction
- Binary literals (`0b1010`)
- Digit separators (`1'000'000`)
- `std::make_unique`
- `[[deprecated]]` attribute

### C++17

- Structured bindings
- `if` and `switch` with initializers
- `std::optional`, `std::variant`, `std::any`
- `std::string_view`
- Fold expressions
- `constexpr if`
- Inline variables
- `std::filesystem`
- Parallel algorithms
- `[[nodiscard]]`, `[[maybe_unused]]` attributes

### C++20

- Concepts
- Ranges
- Coroutines
- Modules
- `constexpr` improvements
- `std::span`
- `std::format`
- Three-way comparison operator (`<=>`)
- Designated initializers
- `consteval`, `constinit`
- `std::jthread`

### C++23

- `std::expected`
- `std::mdspan`
- `std::print`
- `if consteval`
- Deducing `this`
- Multidimensional subscript operator

---

## Build Systems

### g++ Compilation

```bash
# Compile single file
g++ -std=c++17 -Wall -Wextra -O2 main.cpp -o program

# Compile multiple files
g++ -std=c++17 file1.cpp file2.cpp -o program

# Separate compilation
g++ -c file1.cpp  # Creates file1.o
g++ -c file2.cpp  # Creates file2.o
g++ file1.o file2.o -o program  # Link
```

### Makefile

```makefile
CXX = g++
CXXFLAGS = -std=c++17 -Wall -Wextra -O2

SRCS = main.cpp utils.cpp
OBJS = $(SRCS:.cpp=.o)
TARGET = program

all: $(TARGET)

$(TARGET): $(OBJS)
	$(CXX) $(CXXFLAGS) -o $@ $^

%.o: %.cpp
	$(CXX) $(CXXFLAGS) -c $<

clean:
	rm -f $(OBJS) $(TARGET)

.PHONY: all clean
```

### CMake

```cmake
cmake_minimum_required(VERSION 3.10)
project(MyProject)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_executable(program main.cpp utils.cpp)

# Add include directories
target_include_directories(program PRIVATE include)

# Link libraries
target_link_libraries(program pthread)
```

```bash
# Build
mkdir build && cd build
cmake ..
make
```

---

## Testing & Debugging

### Google Test

```cpp
#include <gtest/gtest.h>

int add(int a, int b) { return a + b; }

TEST(AddTest, PositiveNumbers) {
    EXPECT_EQ(add(2, 3), 5);
    EXPECT_EQ(add(10, 20), 30);
}

TEST(AddTest, NegativeNumbers) {
    EXPECT_EQ(add(-2, -3), -5);
}

int main(int argc, char** argv) {
    testing::InitGoogleTest(&argc, argv);
    return RUN_ALL_TESTS();
}
```

### Assertions

```cpp
#include <cassert>

void foo(int* ptr) {
    assert(ptr != nullptr);  // Debug assertion
    // Use ptr
}

// Static assertion (compile-time)
static_assert(sizeof(int) == 4, "int must be 4 bytes");
```

### GDB Debugging

```bash
# Compile with debug symbols
g++ -g program.cpp -o program

# Run with gdb
gdb ./program

# Common commands
(gdb) break main        # Set breakpoint
(gdb) run               # Run program
(gdb) next              # Step over
(gdb) step              # Step into
(gdb) continue          # Continue execution
(gdb) print variable    # Print variable
(gdb) backtrace         # Show call stack
(gdb) quit              # Exit gdb
```

### Valgrind (Memory Leaks)

```bash
valgrind --leak-check=full ./program
```

---

## Common Interview Problems

### 1. Implement Smart Pointer

```cpp
template<typename T>
class SmartPtr {
private:
    T* ptr;
    
public:
    explicit SmartPtr(T* p = nullptr) : ptr(p) {}
    
    ~SmartPtr() { delete ptr; }
    
    // Disable copy
    SmartPtr(const SmartPtr&) = delete;
    SmartPtr& operator=(const SmartPtr&) = delete;
    
    // Enable move
    SmartPtr(SmartPtr&& other) noexcept : ptr(other.ptr) {
        other.ptr = nullptr;
    }
    
    SmartPtr& operator=(SmartPtr&& other) noexcept {
        if (this != &other) {
            delete ptr;
            ptr = other.ptr;
            other.ptr = nullptr;
        }
        return *this;
    }
    
    T& operator*() const { return *ptr; }
    T* operator->() const { return ptr; }
    T* get() const { return ptr; }
};
```

### 2. Thread-Safe Singleton

```cpp
class Singleton {
private:
    Singleton() {}
    static std::mutex mtx;
    static std::unique_ptr<Singleton> instance;
    
public:
    static Singleton& getInstance() {
        std::call_once(flag, []() {
            instance.reset(new Singleton());
        });
        return *instance;
    }
    
private:
    static std::once_flag flag;
};

std::unique_ptr<Singleton> Singleton::instance;
std::once_flag Singleton::flag;
```

### 3. LRU Cache

```cpp
class LRUCache {
private:
    int capacity;
    std::list<std::pair<int, int>> cache;  // key, value
    std::unordered_map<int, std::list<std::pair<int, int>>::iterator> map;
    
public:
    LRUCache(int cap) : capacity(cap) {}
    
    int get(int key) {
        if (map.find(key) == map.end()) return -1;
        
        // Move to front
        cache.splice(cache.begin(), cache, map[key]);
        return map[key]->second;
    }
    
    void put(int key, int value) {
        if (map.find(key) != map.end()) {
            cache.erase(map[key]);
        }
        
        cache.push_front({key, value});
        map[key] = cache.begin();
        
        if (cache.size() > capacity) {
            int old_key = cache.back().first;
            cache.pop_back();
            map.erase(old_key);
        }
    }
};
```

### 4. Producer-Consumer

```cpp
template<typename T>
class BlockingQueue {
private:
    std::queue<T> queue;
    std::mutex mtx;
    std::condition_variable cv;
    size_t capacity;
    
public:
    BlockingQueue(size_t cap) : capacity(cap) {}
    
    void push(T item) {
        std::unique_lock<std::mutex> lock(mtx);
        cv.wait(lock, [this] { return queue.size() < capacity; });
        queue.push(std::move(item));
        cv.notify_one();
    }
    
    T pop() {
        std::unique_lock<std::mutex> lock(mtx);
        cv.wait(lock, [this] { return !queue.empty(); });
        T item = std::move(queue.front());
        queue.pop();
        cv.notify_one();
        return item;
    }
};
```

### 5. Custom String Class

```cpp
class String {
private:
    char* data;
    size_t len;
    
public:
    String(const char* str = "") {
        len = std::strlen(str);
        data = new char[len + 1];
        std::strcpy(data, str);
    }
    
    ~String() { delete[] data; }
    
    String(const String& other) {
        len = other.len;
        data = new char[len + 1];
        std::strcpy(data, other.data);
    }
    
    String& operator=(const String& other) {
        if (this != &other) {
            delete[] data;
            len = other.len;
            data = new char[len + 1];
            std::strcpy(data, other.data);
        }
        return *this;
    }
    
    String(String&& other) noexcept : data(other.data), len(other.len) {
        other.data = nullptr;
        other.len = 0;
    }
    
    String& operator=(String&& other) noexcept {
        if (this != &other) {
            delete[] data;
            data = other.data;
            len = other.len;
            other.data = nullptr;
            other.len = 0;
        }
        return *this;
    }
    
    const char* c_str() const { return data; }
    size_t length() const { return len; }
};
```

---

## Best Practices & Pitfalls

### Best Practices

1. **Use RAII** for resource management
2. **Prefer smart pointers** over raw pointers
3. **Use `const` liberally** for correctness
4. **Pass by const reference** for large objects
5. **Use `override` and `final`** for clarity
6. **Prefer `std::array` and `std::vector`** over C arrays
7. **Use range-based for loops** when possible
8. **Initialize all variables**
9. **Use `nullptr`** instead of `NULL`
10. **Prefer `using` over `typedef`**
11. **Use `auto`** for complex types
12. **Avoid `using namespace std`** in headers
13. **Make destructors virtual** in base classes
14. **Use `noexcept`** for move operations
15. **Prefer algorithms** over hand-written loops

### Common Pitfalls

1. **Memory leaks** - forgetting to delete
2. **Dangling pointers** - using deleted memory
3. **Buffer overflows** - array bounds violations
4. **Object slicing** - copying derived to base
5. **Undefined behavior** - uninitialized variables
6. **Race conditions** - unsynchronized access
7. **Deadlocks** - circular lock dependencies
8. **Exception safety** - resource leaks on exceptions
9. **Virtual destructor** - not virtual in base class
10. **Copy vs Move** - unnecessary copies
11. **Iterator invalidation** - modifying while iterating
12. **Integer overflow** - unchecked arithmetic
13. **Null pointer dereference**
14. **Use after move** - accessing moved-from objects
15. **Implicit conversions** - unexpected behavior

### Interview Tips

1. **Explain your thought process** clearly
2. **Ask clarifying questions** before coding
3. **Consider edge cases** (null, empty, large inputs)
4. **Discuss time/space complexity**
5. **Write clean, readable code**
6. **Test your code** with examples
7. **Know STL containers and algorithms**
8. **Understand memory management**
9. **Be familiar with modern C++ features**
10. **Practice common patterns** (RAII, Rule of 5, etc.)

---

## Further Resources

### Documentation
- [cppreference.com](https://en.cppreference.com/) - Comprehensive C++ reference
- [C++ Core Guidelines](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines) - Best practices
- [ISO C++ FAQ](https://isocpp.org/faq) - Official FAQ

### Learning
- [LearnCpp.com](https://www.learncpp.com/) - Beginner to advanced tutorials
- [Modern C++ Features](https://github.com/AnthonyCalandra/modern-cpp-features) - C++11/14/17/20 features
- [Effective Modern C++](https://www.oreilly.com/library/view/effective-modern-c/9781491908419/) - Scott Meyers

### Tools
- [Compiler Explorer](https://godbolt.org/) - See assembly output
- [C++ Insights](https://cppinsights.io/) - See compiler transformations
- [Quick Bench](https://quick-bench.com/) - Benchmark code online

### Practice
- [LeetCode](https://leetcode.com/) - Coding problems
- [HackerRank](https://www.hackerrank.com/) - C++ challenges
- [Codeforces](https://codeforces.com/) - Competitive programming

### Books
- **The C++ Programming Language** - Bjarne Stroustrup
- **Effective C++** - Scott Meyers
- **C++ Primer** - Stanley Lippman
- **Modern C++ Design** - Andrei Alexandrescu