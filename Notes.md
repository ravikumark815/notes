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

> Declaring a variable:
- Using `var` keyword: Can be used anywhere
- Using `:=` short declaration operator: Can be used inside functions only.
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


> Runes and Strings:
- Text is represented using the rune type (char in other languages)
- Rune is an alias for int32.
- A rune can represent any symbol - letters, numbers, language characters etc.
- String is the data type for storing multiple runes
- Strings are arrays of bytes and a string length

> To print data type of a variable:
```go
var a = 20
fmt.Printf("Type: %T\n", a) // int
```

> Typecasting:
```go
package main
import "fmt"
func main() {
	var totalsum int = 846
	var number int = 19
	var avg float32
	avg = float32(totalsum) / float32(number)
}
```

### Operators
| Category | Operators |
|---|---|
Arithmetic | `+ - * / %`
Relational | `== != > < >= <=`
Logical | `&&` &#124;&#124; `!`
Bitwise | `&` &#124; `^ << >> &^`
Assignment | `= += -= *= /= %= &= ^= <<= >>=` &#124;= 
Unary | `+ - ! & * ^ ++ --`
Misc | `&:`(Address) `*:`(Pointer) `<-`(Receive) `:=` (Declaration)

### Comments:
```go
// Single Line Comment
/*
Multi 
Line
Comment
*/
```

### Control and Loop Statements
**if-else-if:**
```go
if v1 == 100 {
    fmt.Printf("100\n")
} else if v1 == 200 {
    fmt.Printf("200\n")
} else if v1 == 300 {
    fmt.Printf("300\n")
} else {
    fmt.Printf("No Matches\n")
}
```
**for:**
```go
for i := 0; i < 5; i++{ 
    fmt.Printf("%d",i)   
}
```
```go
// Infinite loop 
for { 
    fmt.Printf("GeeksforGeeks\n")   
}
```
```go
// for loop as while
i:= 0 
for i < 3 { 
    i += 2 
}
```
```go
// Range Loop
arr := []string{"a", "b"}
for i, j := range rvariable { 
    fmt.Println(i, j)  
}
/* Output:
0 a
1 b
*/
```
```go
// Strings
for i,j := range "abc" {
    fmt.Printf("%d: %c\n", i, j)
}
```
```go
// Maps
mmap := map[int]string {
    1:"a",
    2:"b",
    3:"c",
}
for k, v := range mmap {
    fmt.Println(k, v)
}
```
**Switch:**
```go
func main() {
    day := 1
    switch day {
    case 1:
        fmt.Println("Monday")
    case 2:
        fmt.Println("Tuesday")
    default:
        fmt.Println("Invalid")
    }
}
```
```go
// Type Switch
func main() {
    var day interface{} = 2
    switch v := day.(type) {
    case int:
        switch v {
        case 1:
            fmt.Println("Monday")
        case 2:
            fmt.Println("Tuesday")
        default:
            fmt.Println("Invalid day")
        }
    default:
        fmt.Printf("Unknown type: %T\n", v)
    }
}
```

**Loop Control:**
```go
// break
for i:=0; i<5; i++ { 
    fmt.Println(i) 
    if i == 3{ 
         break; 
    } 
}
```
```go
// continue
for i < 8 {
    if i == 5 {
        i = i + 2;
        continue;
    }
    fmt.Printf("value is: %d\n", i);
    i++;
} 
```
```go
// goto
label: for x < 8 {
    if x == 5 {
        x = x + 1; 
        goto label
    }
    x++;
}
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