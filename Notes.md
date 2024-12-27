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

    // Convert Byte arr into string
    byteArr := []byte{'a', 'b', 'c'}
	bStr := string(byteArr[:])
	pl("Byte String :", bStr) // abc

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

|Placeholder|Purpose|
|---|---|
%d | Integer
%c | Character
%f | Float
%t | Boolean
%s | String
%o | Base 8
%x | Base 16
%v | Guesses based on data type
%T | Type of supplied value


```go
// Print
import fmt
fmt.Println("Hello Go")

fmt.Printf("%s %d %c %f %t %o %x\n", "String", 1, 'A', 3.14, true, 1, 1)
fmt.Printf("%9f\n", 3.14)      // Width 9
fmt.Printf("%.2f\n", 3.141592) // Decimal precision 3.14

sp := fmt.Sprintf("%9.f\n", 3.141592) // Returns a formatted string
fmt.Println(sp) // Width 9 no precision  3

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
import "time"
now := time.Now()
fmt.Println(now.Year(), now.Month(), now.Day(), now.Hour(), now.Minute(), now.Second()) // 2024 December 25 19 4 25

```

### Math
```go
import "math"
randNum := rand.Intn(50) // Generate a rand int between 0 and 50
fmt.Println(randNum)
fmt.Println("Abs(-10) =", math.Abs(-10)) // 10
fmt.Println("Pow(4, 2) =", math.Pow(4, 2)) // 16
fmt.Println("Sqrt(16) =", math.Sqrt(16)) // 4
fmt.Println("Cbrt(8) =", math.Cbrt(8)) // 2
fmt.Println("Ceil(4.4) =", math.Ceil(4.4)) // 5
fmt.Println("Floor(4.4) =", math.Floor(4.4)) // 4
fmt.Println("Round(4.4) =", math.Round(4.4)) // 4
fmt.Println("Log2(8) =", math.Log2(8)) // 3
fmt.Println("Log10(100) =", math.Log10(100)) // 2
// Get the log of e to the power of 2
fmt.Println("Log(7.389) =", math.Log(math.Exp(2))) // 2
fmt.Println("Max(5,4) =", math.Max(5, 4)) // 5
fmt.Println("Min(5,4) =", math.Min(5, 4)) // 4
// Convert 90 degrees to radians
r90 := 90 * math.Pi / 180
// Convert 1.5708 radians to degrees
d90 := r90 * (180 / math.Pi)
fmt.Printf("%f radians = %f degrees\n", r90, d90) // 1.57096 radians = 90 degrees
fmt.Println("Sin(90): ", math.Sin(90 * math.Pi / 180)) // 1
fmt.Println("Cos(0): ", math.Cos(0 * math.Pi / 180)) // 1
fmt.Println("Tan(45): ", math.Tan(45 * math.Pi / 180)) // 1
fmt.Println("Hypot: ", math.Hypot(3,4)) // 5
```

### Arrays
```go
var arr1 [5] int //Declare
arr2 := [5] int {1, 2, 3, 4, 5} // Declare and Initialize
arr1[0] = 10 // Assign
fmt.Println (arr1[0]) // Access
fmt.Println (len(arr2)) // Length
arr3 := [][]int {} // Multidimension array
fmt.Println(arr1[:3]) // Slice from beginning
fmt.Println(arr1[2:]) // Slice to the end

//  Iterate: 
for i:=0; i<len(arr2); i++ {
    fmt.Println(arr2[i])
}

for k,v := range arr2 {
    fmt.Printf("%d : %d\n", k, v)
}

// Slices of Array
str1 := "abcdef"
rArr := [] rune(str1) // Convert to array of runes
for _,v := range rArr {
    fmt.Printf("%d", v) // 97 98 99 100 101
}
```

### Slices
Slices are like array that can grow. It points to an array.
```go
// Create
sl1 := make([]string, 3) // size 3
sl1[0] = "Ravi"
sl1[1] = "Kumar"
sl1[2] = "Reddy"

// Length
fmt.Println(len(sl1)) // 3

// Iterate
for i:=0; i<len(sl1); i++ {
    fmt.Println(sl1[i])
}
for _,v := range sl1 {
    fmt.Println(sl1[v])
}

// Creating slice from an arry. Slice changes when the array it points to, changes and vice versa.
sArr := [5] int {10,20,30,40,50}
sl2 := sArr[0:2] // Creating Slice for range 0-2
fmt.Println(s)
for _,v := range sl2 {
    fmt.Println(sl1[v]) // 
}
```