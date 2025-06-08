# C
## Preset
- Invented by Dennis Ritchie, 1972, Bell Labs to write Unix OS
- General Purpose, modular and portable
- Low-level memory access
- C-Standards: C89/90 (1989/90), C99 (1999), C11 (2011), C18(2018), C24(2024)

## Structure of C Program:
|   |   |   |
|---|---|---|
| Header | #include <stdio.h> |
| main() | int main() { |
| Variable Declaration | int a = 10; |
| Body | printf(“%d”, a”); |
| Return | return 0; }|

- Header Files inclusion: Contains C function declarations and macro definitions to be shared between source files.
- Main Method: Execution starts from this function.
- Variable Declaration: Variables that are to be used in the function. No variables can be used without being declared.
- Body: Refers to operations that are performed in the functions.
- Return: Depending on return type of the function, the return refers to the returning values from a function

## Memory Map
![](https://github.com/ravikumark815/notes/blob/main/c-images/memory-map.png)

## Compilation
![](https://github.com/ravikumark815/notes/blob/main/c-images/compilation.png)

- **Source File:** Create a c program using an editor and save the file as filename.c
- **Pre-processor:** This phase includes the following and produces filename.i
    - Removal of comments
    - Expansion of Macros
    - Expansion of Included files
    - Conditional Compilation
- **Compiling:** Compiles filename.i and produces filename.s which includes assembly-level instructions. 
- **Assembler:** Takes filename.s as output and produces filename.o – object code. Existing code is converted into machine language. 
- **Linking:** All function calls linked, adds extra code to mark delimiters of each block and forms a executable file.
- **Loading:** Loading the process to main memory

> To save all intermediate files during compilation: `$gcc -Wall -save-temps filename.c –o filename`

## Comments:
- Single Line: `//`
- Multiline: `/* */`
> ✅ Prefer using multi line comments everytime

## Data Types:
| Type                   | Bits   | Range                                  | Library        |
| :--------------------- | :----- | :------------------------------------- | :------------- |
| char                   | 8      | -127 to 127                           |                |
| unsigned char          | 8      | 0 to 255                              |                |
| signed char            | 8      | -127 to 127                           |                |
| int                    | 16/32  | -32768 to 32767                       |                |
| unsigned int           | 16/32  | 0 to 65535                            |                |
| signed int             | 16/32  | -32768 to 32767                       |                |
| short int              | 16     | -32768 to 32767                       |                |
| unsigned short int     | 16     | 0 to 65535                            |                |
| signed short int       | 16     | -32768 to 32767                       |                |
| long int               | 32     | $-2^{31}$ to $2^{31}-1$                |                |
| long long int          | 64     | $-2^{63}$ to $2^{63}-1$                |                |
| signed long int        | 32     | $-2^{31}$ to $2^{31}-1$                |                |
| unsigned long int      | 32     | 0 to $2^{32}-1$                       |                |
| unsigned long long int | 64     | 0 to $2^{64}-1$                       |                |
| float                  | 32     | $\pm 1.17 \times 10^{-38}$ to $\pm 3.4 \times 10^{38}$ | `<float.h>`    |
| double                 | 64     | $\pm 2.3 \times 10^{-308}$ to $\pm 1.7 \times 10^{308}$ | `<float.h>`    |
| long double            | 80/96/128| $\pm 3.4 \times 10^{-4932}$ to $\pm 1.1 \times 10^{4932}$ | `<float.h>`    |
| bool                   | (Implementation-defined) | `true` or `false`                     | `<stdbool.h>`  |
| float _Complex_        | (Implementation-defined) |                                       | `<complex.h>`  |
| float _Imaginary_      | (Implementation-defined) |                                       | `<complex.h>`  |
| double _Complex_       | (Implementation-defined) |                                       | `<complex.h>`  |
| double _Imaginary_     | (Implementation-defined) |                                       | `<complex.h>`  |
| long double _Complex_  | (Implementation-defined) |                                       | `<complex.h>`  |
| long double _Imaginary_| (Implementation-defined) |                                       | `<complex.h>`  |

## Operators:
| Operators     | Symbols                                 | Associativity | Precedence      |
|---------------|-----------------------------------------|---------------|-----------------|
| Assignment    | =, +=, -=, *=, /=, %=, &=, \|=, ^=, >>=, <<= | Right-to-Left | Lowest          |
| Arithmetic    | +, -, *, /, %, ++, --                   | Left-to-Right | Medium-high     |
| Relational    | ==, !=, >, <, >=, <=                     | Left-to-Right | Medium          |
| Logical       | &&, \|\|, !                              | Left-to-Right (&& and \|\|), Right-to-Left (!) | Low             |
| Bitwise       | &, \|, ^                                | Left-to-Right | Medium          |
| Ternary       | Condition ? True : False                | Right-to-Left | Low             |
| Pointer       | &, * | Right-to-Left | Medium-high     |
| Misc          | sizeof(), . (obj.val), &(ptr), *(access) | Left-to-Right | Highest         |

## Identifiers
- **Variables and Constants:**
    - Named location which has some memory allocated to it.
    - Always start with letter/_, only alphanumeric, no whitespace, no keywords.
- **Keywords:** 
    - Predefined and reserved words that have special meanings to the compiler in C.

|          |          |          |          |          |          |          |          |
|----------|----------|----------|----------|----------|----------|----------|----------|
| auto     | break    | case     | char     | const    | continue | default  | do       |
| double   | else     | enum     | extern   | float    | for      | goto     | if       |
| int      | long     | register | return   | short    | signed   | sizeof   | static   |
| struct   | switch   | typedef  | union    | unsigned | void     | volatile | while    |

## Scope Rules

| Scope                    | Meaning                                                                 |
|--------------------------|-------------------------------------------------------------------------|
| File Scope               | Starts at the beginning of the file and ends at the end of the file     |
| Block Scope              | Starts at the opening `{` and ends at the closing `}`                   |
| Function Prototype Scope| Identifiers declared in a function prototype; visible within the prototype |
| Function Scope           | Starts at the opening `{` of a function and ends at the closing `}` of the function |

## Type Qualifiers

| Qualifier | Description                                                                                                |
|-----------|------------------------------------------------------------------------------------------------------------|
| `const`   | Variables of type `const` cannot be changed by the program. They can only be given an initial value.        |
| `volatile`| Variable's value may be changed in ways not explicitly specified by the program. A global variable passed to the OS's clock routine is a good example. |
| `restrict`| To specify that a pointer is an exclusive method of accessing a specific object or area of memory.        |
| `_Atomic`  | A variable that may be read or written atomically - without interference from other threads or processes. |

## Storage Class Specifiers

| Specifier  | Description                                                                                                   |
|------------|---------------------------------------------------------------------------------------------------------------|
| `auto`     | Default storage class for all the variables declared inside a function or a block.                              |
| `extern`   | Used to specify that an object is declared with external linkage elsewhere in the program.                    |
| `static`   | Permanent variables within their own function or file. They maintain their values between function calls.       |
| `register` | Variables declared with `register` are stored in CPU registers instead of RAM for faster access.              |

```c
#include <stdio.h>
int global_var = 10; // Global variable
static int static_global_var = 20; // Initialized data segment

void demoFunction() {
    auto int auto_var = 5;
    printf("auto_var: %d\n", auto_var);

    static int static_func_var = 0; // static (within function)
    static_func_var++;
    printf("static_func_var: %d (This value persists!)\n", static_func_var);

    register int register_var = 100; // register (request to store in register)
    printf("register_var: %d (May or may not be in a register)\n", register_var);

    const int const_var = 3; // const (type qualifier)
    printf("const_var: %d (Cannot be modified)\n", const_var);
    // const_var = 4; // This would cause a compilation error

    volatile int volatile_var = 42; // volatile (type qualifier)
    printf("volatile_var: %d (Value might change unexpectedly)\n", volatile_var);
}

extern int global_var; // extern (declared in another file, but defined here)

int main() {
    printf("global_var (from main): %d\n", global_var); // extern (accessing global variable)

    demoFunction();
    demoFunction(); // Call again to see static variable's persistence

    printf("static_global_var (from main): %d\n",static_global_var);

    return 0;
}

/* Output
global_var (from main): 10
auto_var: 5
static_func_var: 1 (This value persists!)
register_var: 100 (May or may not be in a register)
const_var: 3 (Cannot be modified)
volatile_var: 42 (Value might change unexpectedly)
auto_var: 5
static_func_var: 2 (This value persists!)
register_var: 100 (May or may not be in a register)
const_var: 3 (Cannot be modified)
volatile_var: 42 (Value might change unexpectedly)
static_global_var (from main): 20
*/
```

## Input/Output

| Function     | Description |
|--------------|-------------|
| `scanf()`    | Reads formatted input from stdin. Stops reading a string at the first whitespace character (space, tab, or newline). |
| `gets()`     | Reads an entire line from stdin until a newline or EOF is encountered. **Unsafe**: Does not perform bounds checking and can cause buffer overflows. **Deprecated** in C11. |
| `fgets()`    | Reads a line from stdin into a buffer, stopping after `n-1` characters, a newline, or EOF, whichever comes first. Includes the newline character in the buffer if encountered. **Safer alternative to `gets()`.** |
| `puts()`     | Writes a string to stdout followed by a newline character. |
| `printf()`   | Writes formatted output to stdout. |
| `getchar()`  | Reads the next character from stdin. Waits for the Enter key. |
| `putchar()`  | Writes a single character to stdout. |
| `getch()`    | Reads a character from the keyboard without echoing it to the console and without waiting for Enter. (Non-standard, typically available in `<conio.h>` on Windows/DOS.) |
| `getche()`   | Similar to `getch()` but echoes the character to the console. (Also non-standard, typically in `<conio.h>`.) |
| `fscanf()`   | Reads formatted input from a file. |
| `fprintf()`  | Writes formatted output to a file. |
| `fgetc()`    | Reads the next character from a file. |
| `fputc()`    | Writes a character to a file. |
| `fputs()`    | Writes a string to a file stream. |

> ⚠️ Note: `gets()` is considered dangerous and was removed from the C11 standard. Use `fgets()` instead.

## Format Specifiers

| Data Type                 | Format Specifier |
|---------------------------|------------------|
| `int`                     | `%d`, `%i`       |
| `char`                    | `%c`             |
| `float`                   | `%f`             |
| `double`                  | `%lf`            |
| `short int`               | `%hd`            |
| `unsigned int`            | `%u`             |
| `long int`                | `%ld` or `%li`   |
| `long long int`           | `%lld` or `%lli` |
| `unsigned long int`       | `%lu`            |
| `unsigned long long int`  | `%llu`           |
| `signed char`             | `%c`             |
| `unsigned char`           | `%c`             |
| `long double`             | `%Lf`            |

## Escape Sequences

| Escape Sequence | Description                 |
|------------------|-----------------------------|
| `\a`             | Alarm or Beep               |
| `\b`             | Backspace                   |
| `\f`             | Form Feed                   |
| `\n`             | New Line                    |
| `\r`             | Carriage Return             |
| `\t`             | Horizontal Tab              |
| `\v`             | Vertical Tab                |
| `\\`             | Backslash                   |
| `\'`             | Single Quote                |
| `\"`             | Double Quote                |
| `\?`             | Question Mark               |
| `\ooo`           | Octal Number (e.g., `\075`) |
| `\xhh`           | Hexadecimal Number (e.g., `\x4B`) |
| `\0`             | Null Character              |

## Control Statements in C

| Category       | Statements                                           |
|----------------|------------------------------------------------------|
| Conditional    | `if`, `else if`, `else`, `switch`                   |
| Loops          | `for`, `while`, `do-while`                          |
| Jump           | `return`, `goto`, `break`, `continue`, `exit()`     |
| Expression     | Any general statement followed by `;` (semicolon)   |


```c
// if-else-if
int num = 10;
if (num > 0)
    printf("Positive\n");
else
    printf("Non-positive\n");
// Output: Positive

// for
for (int i = 1; i <= 5; i++)
    printf("%d ", i);
// Output: 1 2 3 4 5

// while
int count = 3;
while (count > 0) {
    printf("Count: %d\n", count);
    count--;
}
// Output:
// Count: 3
// Count: 2
// Count: 1

// break & continue
for (int j = 1; j <= 5; j++) {
    if (j == 3) {
        printf("Skip 3\n");
        continue;
    }
    if (j == 5) {
        printf("Break at 5\n");
        break;
    }
    printf("%d ", j);
}
// Output:
// 1 2 Skip 3
// Break at 5

// goto
int k = 0;
repeat:
if (k < 3) {
    printf("Repeat %d\n", k);
    k++;
    goto repeat;
}
// Output:
// Repeat 0
// Repeat 1
// Repeat 2

```

## Common Program Error Signals in C/C++

| Signal   | Name                  | Description                                                                 | Common Causes                                         |
|----------|-----------------------|-----------------------------------------------------------------------------|-------------------------------------------------------|
| `SIGFPE` | Floating Point Exception | Arithmetic error such as division by zero or overflow.                    | Division by zero, invalid floating-point operation    |
| `SIGILL` | Illegal Instruction   | Attempt to execute an illegal, privileged, or corrupted instruction.       | Stack corruption, executing invalid binary code       |
| `SIGSEGV`| Segmentation Fault    | Invalid memory access (outside allocated memory space).                    | Dereferencing NULL/wild pointer, buffer overflow      |
| `SIGBUS` | Bus Error             | Misaligned or physically invalid memory access.                            | Accessing non-existent physical address, unaligned access on certain architectures |
| `SIGABRT`| Abort Signal          | Abnormal program termination. Typically triggered by `abort()` or failed `assert()`. | Failed assertion, internal fatal errors               |
| `SIGSYS` | Bad System Call       | Invalid argument or misuse of system call.                                 | Calling non-implemented syscall, bad syscall arguments |
| `SIGTRAP`| Trace/Breakpoint Trap | Triggered by debuggers or to indicate a trap/exception.                    | Debug breakpoint hit, intentional traps for debugging |
| `SIGTERM`| Termination Signal    | Requests program termination (gracefully).                                 | `kill` command or system shutdown                     |
| `SIGKILL`| Kill Signal           | Forces immediate termination (cannot be caught or ignored).               | `kill -9` or critical resource violations              |
| `SIGINT` | Interrupt             | Sent when user types Ctrl+C at terminal.                                   | User interruption                                     |

## Preprocessor Directives

In C, all lines beginning with `#` are handled by the **preprocessor**, which processes these directives *before* compilation.

### Common Preprocessor Directives

| Directive    | Description                                                                             | Example Usage                       |
|--------------|-----------------------------------------------------------------------------------------|-------------------------------------|
| `#define`    | Defines a macro or symbolic constant                                                    | `#define MAX 100`                   |
| `#undef`     | Undefines a macro                                                                       | `#undef MAX`                        |
| `#include`   | Includes a file into the source file                                                     | `#include <stdio.h>`                |
| `#ifdef`     | Checks if a macro is defined                                                            | `#ifdef DEBUG`                      |
| `#ifndef`    | Checks if a macro is not defined                                                        | `#ifndef MAX`                       |
| `#if`        | Tests a compile-time condition                                                          | `#if VERSION > 2`                   |
| `#else`      | Specifies alternative code to compile if condition is not met                            | `#else`                             |
| `#elif`      | Else if, another condition to test if previous `#if` or `#elif` failed                  | `#elif VERSION == 2`                |
| `#endif`     | Ends preprocessor conditional                                                           | `#endif`                            |
| `#error`     | Prints an error message and stops compilation                                            | `#error "Wrong version!"`           |
| `#pragma`    | Provides special instructions to the compiler, varies by compiler                       | `#pragma once`                      |
| `#line`      | Changes the compiler’s internal line number and optionally the filename                  | `#line 100 "myfile.c"`              |

### Common `#pragma` Examples

| Pragma Directive        | Description                                                                                         | Example Usage                        | Constraints                                      |
|------------------------ |-----------------------------------------------------------------------------------------------------|-------------------------------------- |--------------------------------------------|
| `#pragma once`          | Ensures the file is included only once in a single compilation.                                     | `#pragma once`                       | Non-standard, but widely supported         |
| `#pragma GCC optimize`  | Instructs GCC to apply specific optimizations.                                                      | `#pragma GCC optimize ("O3")`        | GCC specific                               |
| `#pragma pack`          | Changes memory alignment of structure members.                                                      | `#pragma pack(1)`                    | Use with caution, affects portability      |
| `#pragma warning`       | Enables, disables, or modifies compiler warnings (MSVC, some GCC/Clang).                           | `#pragma warning(disable:4996)`      | MSVC specific                              |
| `#pragma region`/`end`  | Marks code regions for folding in editors/IDEs (Visual Studio).                                    | `#pragma region MyRegion` ... `#pragma endregion` | MSVC/IDEs only                |
| `#pragma message`       | Outputs a message during compilation.                                                               | `#pragma message("Compiling file...")`| MSVC, GCC, Clang                           |
| `#pragma deprecated`    | Marks functions or types as deprecated (MSVC, some GCC/Clang).                                     | `#pragma deprecated(func)`           | MSVC, some GCC/Clang                       |

## Macros

| Macro Type                  | Example                                            | Description                                                               |
|-----------------------------|---------------------------------------------------|---------------------------------------------------------------------------|
| **Object-like Macro**       | `#define PI 3.14`                                 | Simple replacement of tokens with text.                                   |
| **Function-like Macro**     | `#define SQUARE(x) ((x) * (x))`                   | Macros that take arguments (no type checking).                            |
| **Multi-line Macro**        | <br/>`#define LOG(msg) \`<br/>`  printf(msg); \`<br/>`  write_log(msg)` | Macro definition split across lines using `\`.   |
| **Stringizing (`#`)**       | `#define TO_STRING(x) #x`                         | Converts a macro parameter to a string literal.                           |
| **Token Pasting (`##`)**    | `#define COMBINE(a, b) a##b`                      | Concatenates two tokens.                                                  |
| **Variadic Macro**          | `#define ERROR(fmt, ...) fprintf(stderr, fmt, __VA_ARGS__)` | Macro that accepts variable arguments (C99+).             |
| **Conditional Macro**       | `#ifdef DEBUG`<br/>`#define LOG(x) printf(x)`<br/>`#else`<br/>`#define LOG(x)`<br/>`#endif` | Macro defined only if a condition is met.              |
| **Undefining Macro**        | `#undef PI`                                       | Removes a macro definition.                                               |

- **Predefined Macros in C:**

| Macro         | Description                       |
|---------------|-----------------------------------|
| `__FILE__`    | Name of the current source file   |
| `__LINE__`    | Current line number in the source file |
| `__DATE__`    | Compilation date (string)         |
| `__TIME__`    | Compilation time (string)         |
| `__STDC__`    | Defined if the compiler conforms to ANSI C |
| `__func__`    | Print the function name |

## Files
| Function     | Description                                                                 |
|--------------|-----------------------------------------------------------------------------|
| `fopen()`     | Opens a file in a specified mode (`"r"`, `"w"`, `"a"`, etc.)                |
| `fclose()`    | Closes an opened file                                                       |
| `fprintf()`   | Writes formatted output to a file                                           |
| `fscanf()`    | Reads formatted input from a file                                           |
| `fgets()`     | Reads a string from a file                                                  |
| `fputs()`     | Writes a string to a file                                                   |
| `fgetc()`     | Reads a character from a file                                               |
| `fputc()`     | Writes a character to a file                                                |
| `feof()`      | Checks for the end of a file                                                |
| `fseek()`     | Moves the file pointer to a specific location                              |
| `ftell()`     | Returns the current file pointer position                                  |
| `rewind()`    | Moves the file pointer to the beginning of a file                          |
| `remove()`    | Deletes a file                                                              |
| `rename()`    | Renames a file                                                              |

```c
#include <stdio.h>

int main() {
    FILE *file;

    // Writing to a file
    file = fopen("sample.txt", "w");
    if (file != NULL) {
        fprintf(file, "Hello, World!\n");
        fprintf(file, "This is a sample file.\n");
        fclose(file);
        printf("File 'sample.txt' written successfully.\n");
    } else {
        printf("Error opening file for writing.\n");
        return 1;
    }

    // Reading from a file
    file = fopen("sample.txt", "r");
    if (file != NULL) {
        printf("\nReading from file 'sample.txt':\n");
        char buffer[100];
        while (fgets(buffer, sizeof(buffer), file) != NULL) {
            printf("%s", buffer);
        }
        fclose(file);
    } else {
        printf("Error opening file for reading.\n");
        return 1;
    }

    // Appending to a file
    file = fopen("sample.txt", "a");
    if (file != NULL) {
        fprintf(file, "Appending to the file.\n");
        fclose(file);
        printf("\nFile 'sample.txt' appended successfully.\n");
    } else {
        printf("Error opening file for appending.\n");
        return 1;
    }

    return 0;
}
/*
Output:
File 'sample.txt' written successfully.

Reading from file 'sample.txt':
Hello, World!
This is a sample file.

File 'sample.txt' appended successfully.
*/
```
## Bit Manipulation

| Task                              | Bit Manipulation Expression           | Description                                                |
|------------------------------------|---------------------------------------|------------------------------------------------------------|
| Check if number is odd             | `if (n & 1)`                         | If LSB is 1, number is odd                                 |
| Clear the lowest set bit           | `num & (num - 1)`                    | Turns off the rightmost 1-bit                              |
| Divide by 2                        | `num >> 1`                           | Logical right shift by 1 (divides by 2)                    |
| Multiply by 2                      | `num << 1`                           | Logical left shift by 1 (multiplies by 2)                  |
| Convert to lowercase               | `ch | 32`                            | Sets the 6th bit, works only for alphabetic characters     |
| Convert to uppercase               | `ch & ~32`                           | Clears the 6th bit, works only for alphabetic characters   |
| Check power of 2                   | `if ((num & (num - 1)) == 0)`        | True only if num has a single bit set                      |
| Set k-th bit                       | `num | (1 << k)`                     | Sets the k-th bit                                          |
| Unset k-th bit                     | `num & ~(1 << k)`                    | Clears the k-th bit                                        |
| Check k-th bit                     | `if (num & (1 << k))`                | Checks if k-th bit is set                                  |
| Toggle k-th bit                    | `num ^ (1 << k)`                     | Flips the k-th bit                                         |
| Count set bits                     | Use Brian Kernighan’s algo           | Loop: `while(n) { n &= (n-1); count++;}`                   |
| Turn off rightmost 1-bit           | `n & (n - 1)`                        | Same as clear lowest set bit                               |
| Isolate rightmost 1-bit            | `n & -n`                             | Gives only the rightmost set bit                           |
| Swap two numbers                   | `a ^= b; b ^= a; a ^= b;`            | XOR-based swap without temp variable                       |
| Find rightmost different bit       | `(a ^ b) & -(a ^ b)`                 | Finds lowest bit where a and b differ                      |
| Set all bits below k (not including k) | `(1 << k) - 1`                   | Makes a mask with all lower bits set up to k-1             |
| Check if exactly one bit set (nonzero) | `num && !(num & (num - 1))`      | True if num is a power of 2 (and not zero)                 |
| Round up to next power of two      | `n = n-1; n |= n >> 1; n |= n >> 2; n |= n >> 4; n |= n >> 8; n |= n >> 16; n++;` | For 32-bit unsigned ints                                   |
| Find log2 (position of highest set bit) | `31 - __builtin_clz(n)`           | GCC/Clang built-in, returns index of highest set bit       |
| Parity (even/odd number of set bits)   | `__builtin_parity(n)`             | GCC/Clang built-in; 1 if odd, 0 if even number of bits     |
| Absolute value using bits          | `(x ^ (x >> 31)) - (x >> 31)`        | Computes absolute value without branching                  |
| Reverse all bits                   | `__builtin_bitreverse32(n)`          | GCC/Clang built-in for 32-bit integers                     |
| Get lowest zero bit (rightmost 0)  | `~n & (n + 1)`                       | Isolates the lowest unset bit                              |
| Turn on rightmost 0-bit            | `n | (n + 1)`                        | Sets the rightmost 0 bit                                   |                     |

## Example: Toggle k-th Bit
```c
#include <stdio.h>

int main() {
    int num = 42; // 101010
    int k = 1;
    int result = num ^ (1 << k); // Toggles the 1st bit (0-indexed)
    printf("Original: %d, After toggle at %dth bit: %d\n", num, k, result);
    return 0;
}
```

## Pointers

### What is a Pointer?
- A **pointer** is a variable that stores the memory address of another variable.
- Pointers allow direct memory access, dynamic memory management, and efficient array, structure, or function handling.
- Always initialize pointers to `NULL` before use.
- Dereferencing an uninitialized or NULL pointer leads to undefined behavior.
- Prefer using `const` qualifiers to indicate intent and improve code safety.

```c
int *p = NULL; // Safe initial state
```

### Declaration and Access
```c
int a = 10;
int *p = &a; // 'p' holds the address of 'a'
```
- `*p` dereferences the pointer, giving access to the value at the address.
- `&a` gives the memory address of variable `a`.

---

### Pointer Arithmetic
- Pointers can be incremented or decremented.
- **Incrementing a pointer** moves it to the next memory location based on its data type:
  - `p++` moves the pointer by `sizeof(type)` bytes (e.g., 4 bytes for `int` on most systems).
- Example:
  ```c
  int arr[3] = {1, 2, 3};
  int *p = arr;
  p++; // Now points to arr[1]
  ```

---

### Function Pointers
- A **function pointer** holds the memory address of a function.
- Enables callbacks, dynamic function calls, and efficient code.
- Example:
  ```c
  int add(int a, int b) { return a + b; }
  int (*func_ptr)(int, int) = add;
  int sum = func_ptr(2, 3); // Calls add(2, 3)
  ```

---

### Pointers and `const`
| Declaration                | Meaning                                    | Example                       |
|----------------------------|--------------------------------------------|-------------------------------|
| `int *const ptr;`          | **Constant pointer to integer:**           | `ptr` cannot point elsewhere, but value at `*ptr` can change. |
| `int const *ptr;` <br> `const int *ptr;` | **Pointer to constant integer:**                | The value at `*ptr` cannot change, but `ptr` can point elsewhere. |
| `const int *const ptr;`    | **Constant pointer to constant integer:**  | Neither the value at `*ptr` nor the address `ptr` holds can change. |

#### Examples
```c
int x = 10, y = 20;

// Constant pointer to int (can’t point elsewhere)
int *const ptr1 = &x; 
*ptr1 = 15;    // OK
// ptr1 = &y;  // Error

// Pointer to constant int (can point elsewhere, but value can’t change)
const int *ptr2 = &x; 
// *ptr2 = 15; // Error
ptr2 = &y;    // OK

// Constant pointer to constant int (can’t point elsewhere, value can’t change)
const int *const ptr3 = &x; 
// *ptr3 = 15; // Error
// ptr3 = &y;  // Error
```
