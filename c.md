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