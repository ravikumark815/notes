# GO Notes

Main features:
- Efficient Compilation
- Efficient Execution
- Ease of Programming

> [Official Documentation](https://go.dev/doc/)

> [Go Packages](https://go.dev/pkg)


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

### Go CLI
|   |   |
|---|---|
|`go build` | Compiles go source code |
|`go run`   | Compiles and executes go source code |
|`go fmt`   | Formats all the go code in each file in current directory|
|`go install`| Compiles and "installs" a package|
|`go get`   | Downloads the raw source code of someone else's package|
|`go test`  | Runs any tests associated with current project|

### Variables
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

```go
// Examples
var vName string = "Ravi"
var vName2 = "Ravi"
var v1, v2 = 1, 2.3
v3 := 5.78
var pl = fmt.Println
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
1. Basic Types: Integers, Float, Strings, Boolean
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

```
Runes and Strings:
- Text is represented using the rune type (char in other languages)
- Rune is an alias for int32.
- A rune can represent any symbol - letters, numbers, language characters etc.
- String is the data type for storing multiple runes
- Strings are arrays of bytes and a string length
```

```go
// Printing Data type of a variable
fmt.Printf("Type: %T\n", "hello")   // string
fmt.Println(reflect.TypeOf(25))     // int
fmt.Println(reflect.TypeOf(3.14))   // float64
fmt.Println(reflect.TypeOf(true))   // bool
fmt.Println(reflect.TypeOf(🦍))     // int32
```

> Typecasting:
```go
package main
import "fmt"
func main() {
	// To cast type the type to convert to with the variable to
	// convert in parentheses
	// Doesn't work with bools or strings
	cV1 := 1.5
	cV2 := int(cV1)
	fmt.Println(cV2)

	// Convert string to int (ASCII to Integer)
	cV3 := "50000000"
	cV4, err := strconv.Atoi(cV3)
	fmt.Println(cV4, err, reflect.TypeOf(cV4))

	// Convert int to string (Integer to ASCII)
	cV5 := 50000000
	cV6 := strconv.Itoa(cV5)
	fmt.Println(cV6)

	// Convert string to float
	cV7 := "3.14"
	if cV8, err := strconv.ParseFloat(cV7, 64); err == nil {
		fmt.Println(cV8)
	}

	// Use Sprintf to convert from float to string
	cV9 := fmt.Sprintf("%f", 3.14)
	fmt.Println(cV9)
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
for i, j := range arr { 
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
// Print
import fmt
fmt.Println("Hello Go")
fmt.Printf("value is: %d\n", i);

// Scan
import (
    "bufio"
    "os"
)
reader := bufio.NewReader(os.Stdin)
name, err := reader.ReadString('\n')
```

### Strings
```go
import "strings"

sV1 := "A word"

// Replacer that can be used on multiple strings
// to replace one string with another
replacer := strings.NewReplacer("A", "Another")
sV2 := replacer.Replace(sV1)
fmt.Println(sV2)

// Get length
fmt.Println("Length : ", len(sV2)) // 12

// Contains string
fmt.Println("Contains Another :", strings.Contains(sV2, "Another")) // true

// Get first index match
fmt.Println("o index :", strings.Index(sV2, "o")) // 2

// Replace all matches with 0
// If -1 was 2 it would replace the 1st 2 matches
fmt.Println("Replace :", strings.Replace(sV2, "o", "0", -1)) // An0ther w0rd

// Remove whitespace characters from beginning and end of string
sV3 := "\nSome words\n"
sV3 = strings.TrimSpace(sV3) //Some words

// Split at delimiter
fmt.Println("Split :", strings.Split("a-b-c-d", "-")) //[a b c d]

// Upper and lowercase string
fmt.Println("Lower :", strings.ToLower(sV2)) //another word
fmt.Println("Upper :", strings.ToUpper(sV2)) //ANOTHER WORD

// Prefix or suffix
fmt.Println("Prefix :", strings.HasPrefix("tacocat", "taco")) // true
fmt.Println("Suffix :", strings.HasSuffix("tacocat", "cat")) // true

rStr := "abcdefg"

// Runes in string
fmt.Println("Rune Count :", utf8.RuneCountInString(rStr))

// Print runes in string
for i, runeVal := range rStr {
    // Get index, Rune unicode and character
    fmt.Printf("%d : %#U : %c\n", i, runeVal, runeVal)
}
```

### Times
```go
import time
now := time.Now()
fmt.Println(now.Year(), now.Month(), now.Day(), now.Hour(), now.Minute(), now.Second()) // 2024 December 25 19 4 25
```