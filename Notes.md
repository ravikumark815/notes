# GO Notes

Main features:
- Efficient Compilation
- Efficient Execution
- Ease of Programming

> [Official Documentation](https://go.dev/doc/)

### Hello World:
```go
package main // Packages used to organize and reuse code

import "fmt" // Package of formatted I/O functions

func main() { // execution starts here
    fmt.Println("Hello World!") // Print Line
}
```
```sh
terminal@linux$ go run helloworld.go
Hello World!
terminal@linux$ 
```

### Identifiers
- Start with `[a-z][A-Z][_]`
- Contains `[a-z][A-Z][0-9][_]`
- No Keywords
- Identifier with only `_` is a blank identifier and used as a placeholder
- Exported identiers start with **Upper** Case Letter and are accessed across files
- Two types of declaring a variable:
```go
var variable_name type = expression
variable_name:= expression
```

### Keywords
|   |   |   |   |   |
|---|---|---|---|---|
| break | case | chan | const | continue | 
default | defer | else | fallthrough | for | 
func | go | goto | if | import | 
interface | map | package | range | return | 
select | struct | switch |  type | var

### Data Types
1. Basic Types: Integers, Strings, Boolean
2. Aggregate Types: Arrays, Structs
3. Reference Types: Pointers, Slices, Maps, Functions, Channels
4. Interface Types

| Data Type | Description |
|---|---|
int8 | 8-bit signed integer
int16 | 16-bit signed integer
int32 | 32-bit signed integer
int64 | 64-bit signed integer
uint8 | 8-bit unsigned integer
uint16 | 16-bit unsigned integer
uint32 | 32-bit unsigned integer
uint64 | 64-bit unsigned integer
int | Both int and uint contain same size, either 32 or 64 bit.
uint | Both int and uint contain same size, either 32 or 64 bit.
rune | It is a synonym of int32 and also represent Unicode code points.
byte | It is a synonym of uint8.
uintptr | It is an unsigned integer type. Its width is not defined, but its can hold all the bits of a pointer value.
float32 | 32-bit IEEE 754 floating-point number
float64	| 64-bit IEEE 754 floating-point number
complex64 | Complex numbers which contain float32 as a real and imaginary component.
complex128 | Complex numbers which contain float64 as a real and imaginary component

> To print type of a variable:
```go
package main 
import "fmt"
func main() { 
var a = 20
fmt.Printf("Type: %T\n", a) // int
```

### Runes and Strings:
- Text is represented using the rune type (char in other languages)
- Rune is an alias for int32.
- A rune can represent any symbol - letters, numbers, language characters etc.
- String is the data type for storing multiple runes
- Strings are arrays of bytes and a string length

### Operators
| Category | Operators |
|---|---|
Arithmetic | `+ - * / %`
Relational | `== != > < >= <=`
Logical | `&&` &#124;&#124; `!`
Bitwise | `&` &#124; `^ << >> &^`
Assignment | `= += -= *= /= %= &= ^= <<= >>=` &#124;= 
Unary | `+ - ! & * ^ ++ --`
Misc | `&:`(Address) `*:`(Pointer) `<-`(Receive)

### Comments:
```go
// Single Line Comment
/*
Multi 
Line
Comment
*/
```

### I/O functions

```go
func Printf(format string, a ...any) (n int, err error)
/*
func        : Keyword for function
Printf      : Name of function
format, a   : Arguments
n, err      : Returns
*/
```