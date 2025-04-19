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
> Prefer using multi line comments everytime

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
| `fgets()`    | Reads a string from a file stream, safe and bounded by size. |
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

| Directive       | Description |
|----------------|-------------|
| `#include`      | Inserts the contents of a file. `<...>` searches standard system directories; `"..."` searches current directory first. |
| `#define`       | Defines a macro or constant. The preprocessor replaces all matching tokens with the expression. |
| `#undef`        | Undefines a macro. |
| `#if`, `#elif`, `#else`, `#endif` | Used for conditional compilation. |
| `#ifdef`, `#ifndef` | Used to check if a macro is defined or not. |

---

## Macros

- **Simple Macros**: Replace tokens with text.
```c
#define PI 3.14
```

- **Function-like Macros**: Accept arguments but perform **no type checking**.
```c
#define SQUARE(x) ((x) * (x))
```

- **Arguments Are Not Evaluated Before Expansion**: Macros substitute tokens as-is.

- **Token Pasting (`##`)**: Concatenate macro parameters.
```c
#define COMBINE(a, b) a##b
// COMBINE(hello, world) -> helloworld
```

- **Stringizing (`#`)**: Convert macro parameter to string literal.
```c
#define TO_STRING(x) #x
// TO_STRING(123) -> "123"
```

- **Multi-line Macros:** Use a backslash (`\`) to continue a macro definition on the next line:
```c
#define DEBUG_PRINT(msg) \    printf("Debug: %s\n", msg); \    log_to_file(msg)
```


- **Predefined Macros in C:**

| Macro         | Description                       |
|---------------|-----------------------------------|
| `__FILE__`    | Name of the current source file   |
| `__LINE__`    | Current line number in the source file |
| `__DATE__`    | Compilation date (string)         |
| `__TIME__`    | Compilation time (string)         |
| `__STDC__`    | Defined if the compiler conforms to ANSI C |

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
```

---

### Output

```
File 'sample.txt' written successfully.

Reading from file 'sample.txt':
Hello, World!
This is a sample file.

File 'sample.txt' appended successfully.
```

