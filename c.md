# C

## Table of Contents
- [Preset](#preset)
- [Structure of C Program](#structure-of-c-program)
- [Compilation Process](#compilation-process)
- [Memory Map](#memory-map)
- [Data Types](#data-types)
- [Operators](#operators)
- [Variables, Constants, Identifiers, Keywords](#variables-constants-identifiers-keywords)
- [Scope, Type Qualifiers, Storage Classes](#scope-type-qualifiers-storage-classes)
- [Input/Output](#inputoutput)
- [Format Specifiers & Escape Sequences](#format-specifiers--escape-sequences)
- [Control Statements](#control-statements)
- [Functions](#functions)
- [Command-line Arguments](#command-line-arguments)
- [Date & Time](#date--time)
- [Strings](#strings)
- [Arrays](#arrays)
- [Pointers](#pointers)
- [Dynamic Memory Allocation](#dynamic-memory-allocation)
- [Structures, Unions, Enumerations, Bit Fields](#structures-unions-enumerations-bit-fields)
- [Files](#files)
- [Preprocessor Directives & Macros](#preprocessor-directives--macros)
- [Bit Manipulation](#bit-manipulation)
- [Common Program Error Signals](#common-program-error-signals)
- [Useful Libraries](#useful-libraries)
- [Best Practices & Pitfalls](#best-practices--pitfalls)
- [GCC/Clang Compilation Tips](#gccclang-compilation-tips)

## Preset

- Invented by Dennis Ritchie (1972, Bell Labs) to write Unix OS.
- General purpose, modular, and portable.
- Allows low-level memory access.
- C Standards: C89/90 (ANSI C), C99, C11, C18, C23/C24.

## Structure of C Program

```c
#include <stdio.h>

int main(void) {
    printf("Hello, World!\n");
    return 0;
}
```

| Part                  | Example                          | Description                                      |
|-----------------------|----------------------------------|--------------------------------------------------|
| Header                | `#include <stdio.h>`             | Include standard/header files                    |
| main()                | `int main() { ... }`             | Program execution starts here                    |
| Variable Declaration  | `int a = 10;`                    | Declare and initialize variables                 |
| Body                  | `printf("%d", a);`               | Statements (actual code)                         |
| Return                | `return 0; }`                    | Returns value to OS (0 = success)                |

- Header Files: Contain function declarations and macros.
- Main Method: Entry point.
- Variable Declaration: Must declare before use.
- Body: Logic of function/program.
- Return: Return value per function type.

## Compilation Process

```
+--------------+
|  Source Code |
|   (.c/.cpp)  |
+--------------+
       |
       v
+-----------------+
| Preprocessing   |
|    (.i)         |
+-----------------+
       |
       v
+--------------+
| Compilation  |
|   (.s)       |
+--------------+
       |
       v
+--------------+
| Assembling   |
|   (.o)       |
+--------------+
       |
       v
+-----------------+
|   Linking       |
| (a.out / .exe)  |
+-----------------+
       |
       v
+---------------+
|  Executable   |
| (machine code)|
+---------------+
```

- **Source File:** `.c` file written in editor.
- **Preprocessor:** Handles macros, includes, removes comments (`.i`).
- **Compiler:** Converts to assembly (`.s`).
- **Assembler:** Converts to object code (`.o`).
- **Linker:** Combines objects, resolves references, produces executable.
- **Loader:** Loads executable into memory for execution.

> Save all intermediate files:  `gcc -Wall -save-temps filename.c -o filename`

## Memory Map

```
+-----------------------+ High address
|      Stack            |
|  (local variables,    |
|   function calls)     |
|   Grows downward      |
+-----------------------+
|       Heap            |
|  (dynamic memory,     |
|   malloc/new/free)    |
|   Grows upward        |
+-----------------------+
|   BSS Segment         |
| (uninitialized static |
|   and global data)    |
+-----------------------+
|   Data Segment        |
| (initialized static   |
|   and global data)    |
+-----------------------+
|   Text/Code Segment   |
|   (executable code)   |
+-----------------------+ Low address
```

## Data Types

| Type                     | Bits/Size         | Range                                       | Library         |
|--------------------------|-------------------|---------------------------------------------|-----------------|
| `char`                   | 8                 | -128 to 127                                 |                 |
| `unsigned char`          | 8                 | 0 to 255                                    |                 |
| `signed char`            | 8                 | -128 to 127                                 |                 |
| `int`                    | 16/32 (platform)  | -32768 to 32767 / -2,147,483,648 to 2,147,483,647 |                 |
| `unsigned int`           | 16/32             | 0 to 65535 / 0 to 4,294,967,295             |                 |
| `short int`              | 16                | -32768 to 32767                             |                 |
| `unsigned short int`     | 16                | 0 to 65535                                  |                 |
| `long int`               | 32                | -2,147,483,648 to 2,147,483,647             |                 |
| `unsigned long int`      | 32                | 0 to 4,294,967,295                          |                 |
| `long long int`          | 64                | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 |           |
| `unsigned long long int` | 64                | 0 to 18,446,744,073,709,551,615             |                 |
| `float`                  | 32                | ±1.17e-38 to ±3.4e38                        | `<float.h>`     |
| `double`                 | 64                | ±2.3e-308 to ±1.7e308                       | `<float.h>`     |
| `long double`            | 80/96/128         | ±3.4e-4932 to ±1.1e4932                     | `<float.h>`     |
| `bool`                   | 1 (implementation)| `true` or `false`                           | `<stdbool.h>`   |
| `size_t`                 | Platform          | Unsigned type for sizes, array indexing      | `<stddef.h>`    |
| `int32_t`, etc.          | Fixed-width types | Exact-width integers                         | `<stdint.h>`    |

## Operators

| Category     | Symbols                                   | Associativity        | Precedence       |
|--------------|-------------------------------------------|----------------------|------------------|
| Assignment   | =, +=, -=, *=, /=, %=, &=, \|=, ^=, >>=, <<= | Right-to-Left        | Lowest           |
| Arithmetic   | +, -, *, /, %, ++, --                     | Left-to-Right        | Medium-high      |
| Relational   | ==, !=, >, <, >=, <=                      | Left-to-Right        | Medium           |
| Logical      | &&, \|\|, !                               | &&, \|\|: Left-to-Right<br>!: Right-to-Left | Low |
| Bitwise      | &, \|, ^                                  | Left-to-Right        | Medium           |
| Ternary      | `?:`                                      | Right-to-Left        | Low              |
| Pointer      | &, *                                      | Right-to-Left        | High             |
| Misc         | sizeof(), . (obj.val), ->, []             | Left-to-Right        | Highest          |

## Variables, Constants, Identifiers, Keywords

- **Variables:** Named storage for data. Must start with a letter or `_`; case-sensitive.
- **Constants:** Use `const` or `#define` for values not meant to change.
- **Identifiers:** Names for variables, functions, etc.
- **Keywords:** Reserved by C.

| auto     | break    | case     | char     | const    | continue | default  | do       |
|----------|----------|----------|----------|----------|----------|----------|----------|
| double   | else     | enum     | extern   | float    | for      | goto     | if       |
| int      | long     | register | return   | short    | signed   | sizeof   | static   |
| struct   | switch   | typedef  | union    | unsigned | void     | volatile | while    |

## Scope, Type Qualifiers, Storage Classes

### Scope

| Scope                      | Meaning                                              |
|----------------------------|-----------------------------------------------------|
| File Scope                 | Valid throughout the file                           |
| Block Scope                | Valid within `{ ... }`                              |
| Function Prototype Scope   | Valid only inside prototype                         |
| Function Scope             | Valid only inside function                          |

### Type Qualifiers

| Qualifier    | Description                                                                  |
|--------------|------------------------------------------------------------------------------|
| `const`      | Value cannot be changed after initialization                                 |
| `volatile`   | May change in ways unanticipated by the compiler                             |
| `restrict`   | Pointer is the only reference to the object                                  |
| `_Atomic`    | Special atomic access (C11 and later)                                        |

### Storage Classes

| Specifier  | Description                                                                    |
|------------|--------------------------------------------------------------------------------|
| `auto`     | Default for local variables (automatic storage)                                |
| `extern`   | Defined elsewhere; accessible across files                                     |
| `static`   | Persists for program lifetime, scope-limited                                   |
| `register` | Hints to store in CPU register (may be ignored)                                |

#### Example

```c
#include <stdio.h>
int global_var = 10;    // global, file scope
static int file_static = 20; // static, file scope

void demo() {
    auto int local = 5;
    static int func_static = 0; // persists across calls
    register int reg_var = 100;
    const int constant = 3;
    volatile int may_change = 42;
}
```

## Input/Output

| Function     | Description                                                                                                     |
|--------------|----------------------------------------------------------------------------------------------------------------|
| `scanf()`    | Reads formatted input; stops at whitespace for `%s`                                                             |
| `gets()`     | Reads line until newline/EOF; **unsafe**, deprecated in C11                                                    |
| `fgets()`    | Reads line (safer), up to `n-1` chars; includes newline                                                        |
| `puts()`     | Prints string, adds newline                                                                                    |
| `printf()`   | Formatted output                                                                                               |
| `getchar()`  | Reads next character from stdin                                                                                |
| `putchar()`  | Writes a character to stdout                                                                                   |
| `getch()`    | Reads a character without echo (non-standard, `<conio.h>`)                                                    |
| `getche()`   | Like `getch()`, but echoes (non-standard)                                                                     |
| `fscanf()`   | Reads formatted input from file                                                                                |
| `fprintf()`  | Writes formatted output to file                                                                                |
| `fgetc()`    | Reads next character from file                                                                                 |
| `fputc()`    | Writes character to file                                                                                       |
| `fputs()`    | Writes string to file                                                                                          |

> ⚠️ **Never use `gets()`**. Use `fgets()` for safe input.

## Format Specifiers & Escape Sequences

### Format Specifiers

| Data Type                 | Format Specifier      |
|---------------------------|----------------------|
| `int`                     | `%d`, `%i`           |
| `char`                    | `%c`                 |
| `float`                   | `%f`                 |
| `double`                  | `%lf`                |
| `short int`               | `%hd`                |
| `unsigned int`            | `%u`                 |
| `long int`                | `%ld` or `%li`       |
| `long long int`           | `%lld` or `%lli`     |
| `unsigned long int`       | `%lu`                |
| `unsigned long long int`  | `%llu`               |
| `long double`             | `%Lf`                |
| `size_t`                  | `%zu`                |

### Escape Sequences

| Escape Sequence | Description                 |
|-----------------|----------------------------|
| `\a`            | Alarm/Bell                 |
| `\b`            | Backspace                  |
| `\f`            | Form Feed                  |
| `\n`            | New Line                   |
| `\r`            | Carriage Return            |
| `\t`            | Horizontal Tab             |
| `\v`            | Vertical Tab               |
| `\\`            | Backslash                  |
| `\'`            | Single Quote               |
| `\"`            | Double Quote               |
| `\?`            | Question Mark              |
| `\ooo`          | Octal value (e.g. `\075`)  |
| `\xhh`          | Hex value (e.g. `\x4B`)    |
| `\0`            | Null Character             |

## Control Statements

| Category        | Statements                                       |
|-----------------|--------------------------------------------------|
| Conditional     | `if`, `else if`, `else`, `switch`                |
| Loops           | `for`, `while`, `do-while`                       |
| Jump            | `return`, `goto`, `break`, `continue`, `exit()`  |
| Expression      | Any statement ending with `;`                    |

### Example

```c
int num = 10;
if (num > 0)
    printf("Positive\n");
else
    printf("Non-positive\n");

for (int i = 1; i <= 5; i++)
    printf("%d ", i);

while (num > 0) {
    printf("Num: %d\n", num);
    num--;
}
```

> **Switch-case:** Always add `break` to prevent fall-through.

## Functions

- **Declaration (Prototype):** Tells compiler about function.
- **Definition:** Actual implementation.
- **Calling:** Executes function code.
- **Void Function:** No return value.
- **Returning pointer:** Functions may return pointers.
- **Recursion:** Function calls itself.

### Example

```c
int add(int, int); // prototype

int main() {
    printf("%d\n", add(2, 3));
    return 0;
}

int add(int x, int y) {
    return x + y;
}
```

- **Void:** `void greet() { printf("Hi"); }`
- **Returning pointers:** `int* alloc() { return malloc(sizeof(int)); }`
- **Recursion:** `int fact(int n) { return n <= 1 ? 1 : n * fact(n - 1); }`

## Command-line Arguments

```c
int main(int argc, char *argv[]) {
    // argc: Number of arguments (including program name)
    // argv: Array of argument strings
    for (int i = 0; i < argc; i++)
        printf("%s\n", argv[i]);
    return 0;
}
```
- Useful for passing values to program at runtime.

## Strings

- C strings are arrays of `char` ending with `'\0'`.
- Declared as arrays or pointers.

### Declaration & Initialization

```c
char str1[] = "Hello";
char str2[10] = "World";
char str3[6] = {'H', 'e', 'l', 'l', 'o', '\0'};
char *str4 = "Literal"; // read-only in modern C
```

### Input/Output

```c
char buf[100];
scanf("%99s", buf);       // Reads up to whitespace
fgets(buf, sizeof(buf), stdin); // Reads a line, includes spaces/newline
printf("%s\n", buf);
```

> ⚠️ Use `fgets` for lines with spaces.  
> ⚠️ Never write to string literals.

### String Functions (`<string.h>`)

| Function                | Description                                                         | Example                                      |
|-------------------------|---------------------------------------------------------------------|----------------------------------------------|
| `strlen(s)`             | Length (excluding `'\0'`)                                          | `int n = strlen(str);`                       |
| `strcpy(dest, src)`     | Copy string                                                         | `strcpy(dest, src);`                         |
| `strncpy(dest, src, n)` | Copy up to `n` chars                                                | `strncpy(dest, src, n);`                     |
| `strcat(dest, src)`     | Concatenate                                                         | `strcat(dest, src);`                         |
| `strncat(dest, src, n)` | Concatenate up to `n` chars                                         | `strncat(dest, src, n);`                     |
| `strcmp(a, b)`          | Compare (`0` if equal)                                              | `strcmp(a, b)`                               |
| `strncmp(a, b, n)`      | Compare up to `n` chars                                             | `strncmp(a, b, n)`                           |
| `strchr(s, c)`          | First occurrence of `c` in `s`                                      | `strchr(str, 'a')`                           |
| `strrchr(s, c)`         | Last occurrence of `c` in `s`                                       | `strrchr(str, 'a')`                          |
| `strstr(big, small)`    | First occurrence of `small` in `big`                                | `strstr(big, small)`                         |
| `strpbrk(s, accept)`    | First occurrence of any char from `accept` in `s`                   | `strpbrk(str, "aeiou")`                      |
| `strspn(s, accept)`     | Length of leading segment with only `accept` chars                  | `strspn(str, "abc")`                         |
| `strcspn(s, reject)`    | Length of leading segment with none of `reject` chars               | `strcspn(str, "xyz")`                        |
| `strtok(s, delim)`      | Tokenize string                                                     | `strtok(str, ",")`                           |
| `memset(s, c, n)`       | Set memory                                                          | `memset(str, 0, 100)`                        |
| `memcpy(dest, src, n)`  | Copy memory                                                         | `memcpy(dest, src, 10)`                      |
| `memmove(dest, src, n)` | Safe copy (overlap OK)                                              | `memmove(dest, src, 10)`                     |
| `memcmp(a, b, n)`       | Compare memory                                                      | `memcmp(a, b, 10)`                           |

- Always ensure destination arrays are large enough!
- Use `strncpy`, `strncat` for safety, but always ensure null-termination.

## Date & Time

- Use `<time.h>` for time/date manipulation.

```c
#include <stdio.h>
#include <time.h>

int main() {
    time_t now = time(NULL);
    printf("Current time: %s", ctime(&now));
    struct tm *t = localtime(&now);
    printf("Year: %d, Month: %d, Day: %d\n", t->tm_year+1900, t->tm_mon+1, t->tm_mday);
    return 0;
}
```

## Arrays

- **1D Array:** `type arr[size];`
    ```c
    int arr[10];
    ```
- **2D Array:** `type arr[rows][cols];`
    ```c
    double mat[3][4];
    ```
- **Multi-dimensional:** `type arr[size1][size2]...[sizeN];`
    ```c
    int m[4][3][4][5];
    ```

- Arrays are **zero-indexed**.
- Passed as pointers to functions (`void foo(int arr[])`).
- Use `sizeof(arr)/sizeof(arr[0])` for element count (inside scope of definition).

## Pointers

- A pointer holds the address of another variable.
- **Declaration:** `int *p = &var;`
- Dereference using `*p`, get address using `&var`.
- Always initialize pointers; use `NULL` if not pointing anywhere.

### Pointer Arithmetic

- `p++` advances pointer by `sizeof(type)`.
- Arrays and pointers are closely related.

### Function Pointers

- Store function addresses, enable callbacks.
    ```c
    int add(int a, int b) { return a + b; }
    int (*fptr)(int, int) = add;
    printf("%d\n", fptr(2, 3));
    ```

### Pointers and `const`

| Declaration                | Meaning                                    |
|----------------------------|--------------------------------------------|
| `int *const ptr`           | Constant pointer to int (cannot change address) |
| `const int *ptr`           | Pointer to constant int (cannot change value) |
| `const int *const ptr`     | Constant pointer to constant int           |

### Pointer to Pointer, Void Pointer

```c
int a = 10;
int *p = &a;
int **pp = &p; // pointer to pointer

void *vp = p; // generic pointer (must cast to use)
```

## Dynamic Memory Allocation

- Allocates memory at runtime from heap.
- **Always check for `NULL` return value.**
- **Always free memory to prevent leaks.**

| Function      | Description                                                        | Syntax Example                      | Notes               |
|---------------|--------------------------------------------------------------------|-------------------------------------|---------------------|
| `malloc()`    | Allocates memory (uninitialized)                                   | `p = malloc(size);`                 | Returns `void*`    |
| `calloc()`    | Allocates, zero-initializes memory                                 | `p = calloc(n, size);`              | Returns `void*`    |
| `realloc()`   | Resizes allocated memory block                                     | `p = realloc(p, new_size);`         | May move memory    |
| `free()`      | Frees allocated memory                                             | `free(p);`                          |                    |

### Example

```c
int *arr = malloc(n * sizeof(int));
if (!arr) { /* handle error */ }
free(arr);
arr = NULL; // after free
```

- `calloc` is safer for arrays as it initializes to zero.
- `realloc(ptr, 0)` is like `free(ptr)` (implementation-defined).
- **Common errors:** forgetting to `free()`, double `free()`, dereferencing freed memory.

## Structures, Unions, Enumerations, Bit Fields

### Structures

- Group variables of different types.
    ```c
    struct student {
        char name[30];
        int age;
    };
    typedef struct student STUDENT;

    STUDENT ram;
    strcpy(ram.name, "Ram");
    ram.age = 5;
    ```

### Unions

- One member active at a time (members share memory).
    ```c
    union student {
        char name[30];
        int age;
    };
    ```

### Enumerations

- Named integer constants.
    ```c
    enum week {MON, TUE, WED, THU, FRI, SAT, SUN};
    enum week today = WED;
    ```

### Bit Fields

- Specify number of bits for structure members.
    ```c
    struct {
        unsigned int flag1 : 1;
        unsigned int flag2 : 2;
        unsigned int flag3 : 3;
    } bits;
    ```

- Useful for compact data (flags, protocol headers, etc.).

## Files

| Function      | Description                                                                 |
|---------------|-----------------------------------------------------------------------------|
| `fopen()`     | Opens a file (`"r"`, `"w"`, `"a"`, etc.)                                    |
| `fclose()`    | Closes an opened file                                                       |
| `fprintf()`   | Writes formatted output to a file                                           |
| `fscanf()`    | Reads formatted input from a file                                           |
| `fgets()`     | Reads a string from a file                                                  |
| `fputs()`     | Writes a string to a file                                                   |
| `fgetc()`     | Reads a character from a file                                               |
| `fputc()`     | Writes a character to a file                                                |
| `feof()`      | Checks end-of-file                                                          |
| `fseek()`     | Moves file pointer                                                          |
| `ftell()`     | Gets current file position                                                  |
| `rewind()`    | Resets file pointer to start                                                |
| `remove()`    | Deletes a file                                                              |
| `rename()`    | Renames a file                                                              |

### Example

```c
FILE *file = fopen("sample.txt", "w");
if (file) {
    fprintf(file, "Hello!\n");
    fclose(file);
}
```
- Use `perror("msg")` to print file-related errors.

## Preprocessor Directives & Macros

### Preprocessor Directives

| Directive      | Description                                        | Example                  |
|----------------|----------------------------------------------------|--------------------------|
| `#define`      | Macro or constant                                  | `#define MAX 100`        |
| `#undef`       | Undefine a macro                                   | `#undef MAX`             |
| `#include`     | Include a file                                     | `#include <stdio.h>`     |
| `#ifdef`       | If macro defined                                   | `#ifdef DEBUG`           |
| `#ifndef`      | If macro not defined                               | `#ifndef MAX`            |
| `#if`          | If compile-time condition                          | `#if VERSION > 2`        |
| `#else`        | Else for preprocessor                              | `#else`                  |
| `#elif`        | Else if                                            | `#elif VERSION == 2`     |
| `#endif`       | End if                                             | `#endif`                 |
| `#error`       | Stop compilation with error                        | `#error "Wrong version"` |
| `#pragma`      | Special compiler instruction                       | `#pragma once`           |
| `#line`        | Change line number/file                            | `#line 100 "myfile.c"`   |

#### Common `#pragma` Examples

- `#pragma once`: Include file only once (non-standard, widely supported).
- `#pragma GCC optimize("O3")`: GCC optimization.
- `#pragma pack(1)`: Change struct alignment.
- `#pragma warning(disable:4996)`: Disable warning (MSVC).
- `#pragma message("Compiling...")`: Show message at compile time.

### Macros

| Macro Type           | Example                                  | Description                                    |
|----------------------|------------------------------------------|------------------------------------------------|
| Object-like          | `#define PI 3.14`                        | Simple replacement                             |
| Function-like        | `#define SQR(x) ((x)*(x))`               | Accepts arguments, no type checking            |
| Multi-line           | `#define LOG(msg) do { printf(msg); } while(0)` | Safe macro block                        |
| Stringizing `#`      | `#define TO_STR(x) #x`                   | Converts parameter to string                   |
| Token Pasting `##`   | `#define COMB(a, b) a##b`                | Concatenates tokens                           |
| Variadic             | `#define DBG(fmt, ...) printf(fmt, __VA_ARGS__)` | Variable args (C99+)                  |
| Conditional Macro    | See `#ifdef`, `#ifndef`                  | Compile different code based on macros         |
| Undefining Macro     | `#undef PI`                              | Remove macro definition                       |

### Macro Pitfalls

- Arguments may be evaluated multiple times:  
  ```c
  #define SQR(x) ((x)*(x))
  int y = SQR(i++); // i++ is evaluated twice!
  ```
- Use parentheses and prefer inline functions for complex macros.

### Predefined Macros

| Macro         | Description                                |
|---------------|--------------------------------------------|
| `__FILE__`    | Current source filename                    |
| `__LINE__`    | Current line number                        |
| `__DATE__`    | Compilation date (string)                  |
| `__TIME__`    | Compilation time (string)                  |
| `__STDC__`    | Defined if compiler is ANSI C compliant    |
| `__func__`    | Name of the current function (C99+)        |

## Bit Manipulation

| Task                              | Expression                                          | Description                                                |
|------------------------------------|-----------------------------------------------------|------------------------------------------------------------|
| Check if number is odd             | `if (n & 1)`                                       | LSB is 1 if odd                                            |
| Clear lowest set bit               | `n & (n - 1)`                                      | Turns off rightmost 1-bit                                  |
| Divide by 2                        | `n >> 1`                                           | Logical right shift                                        |
| Multiply by 2                      | `n << 1`                                           | Logical left shift                                         |
| Convert to lowercase               | `ch | 32`                                          | Sets 6th bit, ASCII only                                   |
| Convert to uppercase               | `ch & ~32`                                         | Clears 6th bit, ASCII only                                 |
| Check power of 2                   | `n != 0 && (n & (n - 1)) == 0`                     | True if single bit set                                     |
| Set k-th bit                       | `n | (1 << k)`                                     | Sets kth bit                                               |
| Unset k-th bit                     | `n & ~(1 << k)`                                    | Clears kth bit                                             |
| Check k-th bit                     | `if (n & (1 << k))`                                | Checks kth bit                                             |
| Toggle k-th bit                    | `n ^ (1 << k)`                                     | Flips kth bit                                              |
| Count set bits                     | `while(n){ n &= (n-1); count++; }`                 | Brian Kernighan’s algorithm                                |
| Isolate rightmost 1-bit            | `n & -n`                                           | Gives only rightmost set bit                               |
| Swap two numbers                   | `a ^= b; b ^= a; a ^= b;`                          | XOR swap                                                   |
| Find rightmost different bit       | `(a ^ b) & -(a ^ b)`                               | Finds lowest bit where a and b differ                      |
| Set all bits below k (not k)       | `(1 << k) - 1`                                     | All lower bits set up to k-1                               |
| Round up to next power of two      | `n--; n |= n >> 1; n |= n >> 2; ...; n++`          | For 32-bit unsigned ints                                   |
| Find log2 (highest set bit)        | `31 - __builtin_clz(n)`                            | GCC/Clang built-in                                         |
| Parity (even/odd set bits)         | `__builtin_parity(n)`                              | 1 if odd, 0 if even number of bits                         |
| Absolute value using bits          | `(x ^ (x >> 31)) - (x >> 31)`                      | Absolute value, no branching                               |
| Reverse all bits                   | `__builtin_bitreverse32(n)`                        | GCC/Clang built-in                                         |
| Get lowest zero bit                | `~n & (n + 1)`                                     | Isolates lowest unset bit                                  |
| Turn on rightmost 0-bit            | `n | (n + 1)`                                      | Sets rightmost 0 bit                                       |

## Common Program Error Signals

| Signal   | Name                   | Description                                                                 | Common Causes                                             |
|----------|------------------------|-----------------------------------------------------------------------------|-----------------------------------------------------------|
| `SIGFPE` | Floating Point Exception | Arithmetic error, e.g., division by zero                                   | Division by zero, invalid floating-point operation        |
| `SIGILL` | Illegal Instruction    | Illegal, privileged, or corrupted instruction                               | Stack corruption, executing invalid code                  |
| `SIGSEGV`| Segmentation Fault     | Invalid memory access                                                       | NULL/wild pointer, buffer overflow                        |
| `SIGBUS` | Bus Error              | Misaligned or physically invalid access                                     | Unaligned access, non-existent physical address           |
| `SIGABRT`| Abort Signal           | Abnormal program termination (abort, assert)                                | Failed assertion, internal errors                         |
| `SIGTRAP`| Trace/Breakpoint Trap  | Triggered by debugger, trap/exception                                       | Debug breakpoints, intentional traps                      |
| `SIGTERM`| Termination Signal     | Requests graceful program termination                                       | `kill` command, system shutdown                           |
| `SIGKILL`| Kill Signal            | Forces immediate termination (cannot be caught or ignored)                  | `kill -9`, resource violation                             |
| `SIGINT` | Interrupt              | Sent by user (Ctrl+C)                                                       | User interruption                                         |

## Useful Libraries

- `<stdio.h>`: Standard I/O
- `<stdlib.h>`: General utilities, memory allocation
- `<string.h>`: String operations
- `<math.h>`: Math functions
- `<ctype.h>`: Character handling
- `<stdbool.h>`: Boolean type
- `<stdint.h>`: Fixed-width integer types
- `<stddef.h>`: Common macros/types (`size_t`, `ptrdiff_t`)
- `<assert.h>`: Diagnostics
- `<errno.h>`: Error codes
- `<signal.h>`: Handling Signals
- `<limits.h>`
- `<locale.h>`
- `<time.h>`: Date and time

## GCC/Clang Compilation Tips

- `-Wall -Wextra`: Enable most warnings.
- `-g`: Include debug info for gdb/lldb.
- `-O2`, `-O3`: Optimization levels.
- `-std=c99` or `-std=c11`: Specify C standard.
- `-fsanitize=address`: Detect memory errors.
- `-pedantic`: Warn on non-standard code.
- `-o output`: Name the output file.