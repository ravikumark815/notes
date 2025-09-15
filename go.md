# GO Notes

## Table of Contents

### 1. Exciting Start
- [Main Features](#main-features)
- [Hello World](#hello-world)
- [Go CLI](#go-cli)

### 2. Core Fundamentals
- [Variables](#variables)
- [Data Types](#data-types)
- [Operators](#operators)
- [Comments](#comments)
- [Control and Loop Statements](#control-and-loop-statements)

### 3. Essential Concepts
- [Object-Oriented Programming in Go](#object-oriented-programming-in-go)
- [Functions](#functions)
- [Pointers](#pointers)
- [Structs](#structs)
- [Interfaces](#interfaces)
- [Error Handling](#error-handling)

### 4. Data Structures
- [Arrays](#arrays)
- [Slices](#slices)
- [Maps](#maps)
- [Generics](#generics)
- [Defined Types](#defined-types)

### 5. I/O & Utilities
- [I/O Functions](#io-functions)
- [Strings](#strings)
- [File I/O](#file-io)
- [Time](#time)
- [Math](#math)
- [Command Line Args](#command-line-args)

### 6. Advanced Language Features
- [Packages/Modules](#packagesmodules)
- [Defer, Panic, Recover](#defer-panic-recover)
- [Context Package](#context-package)
- [Concurrency](#concurrency)
- [Channels](#channels)
- [Advanced Concurrency Patterns](#advanced-concurrency-patterns)
- [Struct Embedding and Methods](#struct-embedding-and-methods)

### 7. Development Practices
- [Testing Basics](#testing-basics)
- [Modules and Dependency Management](#modules-and-dependency-management)
- [Common Standard Library Packages](#common-standard-library-packages)
- [Go Tooling](#go-tooling)
- [Closures](#closures)
- [Regular Expressions](#regular-expressions)
- [Keywords](#keywords)

## Main Features
- Efficient Compilation
- Efficient Execution
- Ease of Programming

> [Official Documentation](https://go.dev/doc/)

> [Go Packages](https://go.dev/pkg/)

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
|`go mod init testproj`| Creates a new project named testproj|

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
variable_name := expression
```

```go
// Examples
var vName string = "Ravi"
var vName2 = "Ravi"
var v1, v2 = 1, 2.3
v3 := 5.78
var pl = fmt.Println //Alias for function
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
	fmt.Println(cV2) // 1

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
	fmt.Println("Byte String :", bStr) // abc

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

### Time
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
Slices are arrays that can grow.
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
    fmt.Println(sl1[v]) 
}
sl2.append(sl2, 10)
```

### Functions
*Syntax:*
```go
func funcName(parameters) returnTypes {
    // BODY
}
```
```go
// Example:
func divide(x float64, y float64) (ans float64, err error) {
    if y==0 {
        return 0, fmt.Errorf("Division by 0")
    }
    return x/y, nil
}
func main() {
    divide(5/4)
}

// Voradic Functions: receive unknown number of values:
func getSum(nums ...int) int {
    sum := 0
    for _, num := range nums {
        sum += num
    }
    return sum
}

// Passing Arrays:
func getArraySum(arr[] int) int {
    sum := 0
    for _, v := range arr {
        sum += v
    }
    return sum
}

// Passing Pointer:
func changeVal(numPtr *int) int {
    *numPtr = 12
}
num := 10
changeVal(&num)

// Passing Pointer of an Array
func arrayPtrFunc(arr*[]int) int {
    return 1
}

func main() {
    arr := []int {1,2,3,4}
    fmt.Println(arrayPtrFunc(&arr))
}

// Passing a slice
func sliceFunc(nums ...int) int {
    return len(nums)
}

func main() {
    sSlice := []int{10,20,30}
    fmt.Println(sliceFunc(sSlice...)) // Notice ... in func call
}
```

### Pointers
```go
// Declaration
num := 10
var numPtr *int = &num

// Access
*numPtr = 12

// Address
fmt.Println("Addr:", numPtr)
```

### File I/O
```go
// Create a file
f,err := os.Create("data.txt")
defer f.Close() // Closes the file as soon as we are out of scope

// Write to file
arr := []int{2,3,5,7,11}
for _,num := range arr {
    _,err := f.WriteString(strcov.Itoa(num) + "\n")
}

// Check if file exists
_, err = os.Stat("data.txt")
if errors.Is(err, os.ErrNotExist) {
    fmt.Println("File Doesn't Exist")
}

// Open a file
f,err = os.Open("data.txt")

// Read from file
scan1 := bufio.NewScanner(f)
for scan1.Scan() {
    fmt.Println(scan1.Text())
}

// Append to file
/*
        Exactly one of O_RDONLY, O_WRONLY, or O_RDWR must be specified

    O_RDONLY : open the file read-only
    O_WRONLY : open the file write-only
    O_RDWR   : open the file read-write

    These can be or'ed

    O_APPEND : append data to the file when writing
    O_CREATE : create a new file if none exists
    O_EXCL   : used with O_CREATE, file must not exist
    O_SYNC   : open for synchronous I/O
    O_TRUNC  : truncate regular writable file when opened
*/
_, err = os.Stat("data.txt")
if errors.Is(err, os.ErrNotExist) {
    fmt.Println("File Doesn't Exist")
} else {
    f, err = os.OpenFile("data.txt", os.O_APPEND|os.O_CREATE|os.O_WRONLY, 0644)
    if err != nil {
        log.Fatal(err)
    }
    defer f.Close()
    if _, err := f.WriteString("13\n"); err != nil {
        log.Fatal(err)
    }
}
```

### Command Line Args
```go
func main() {
    fmt.Println(os.Args)
}
/*
go run test.go 24 abc
Output: [test.go, 24, abc]
*/
```

### Packages/Modules
- Packages allow you to keep related together and go looks for packages codes in specific directories. 
- Variables/Functions starting with uppercase letters are accessible outside the package
- To retrieve values or variables for valid authenticated access, we can write getter functions that start with uppercase letters and simply return the variable value.
- `package main` must have `main` function in it. Package names are mostly lowercase
- Example:
```go
// testproj/mypackage/mypackage.go
package test
var GlobalVar := 10 // G uppercase for external access

// main.go
import (
    test "testproj/mypackage"
)
func main() {
    fmt.Println("Var:", test.GlobalVar) // Var: 10
}
```

### Maps
- Maps are collections of k-v pairs.
- Key can be anything that can be compared using `==`

Syntax:
```go
var mapName map [keyType]valueType
mapName := make(map[keyType]valueType)
mapName := map[int]string {1: "a",
    2: "b",
    3: "c"
}
```
Example:
```go
var heroes map[string]string
heroes := make(map[string]string)
mapName := map[int]string {1: "a",
    2: "b",
    3: "c"
}

// Access and Assignment
heroes["Ironman"] = "Tony Stark"
heroes["Batman"] = "Bruce Wayne"
heroes["Superman"] = "Clark Kent"

fmt.Println(mapName) // O/p: map[1:a 2:b 3:c]

// Iterate
for k,v := range mapName {
    fmt.Printf("%d:%s", k, v) // 1:a2:b3:c
}

// Delete
delete(heroes, "Superman")
```

### Generics
- With generics we can specify the data type to be used at a later time. 
- Mainly used when we want to use functions with moldable data types
- Generic type parameter is capitalized and in square brackets

```go
type MyConstraint interface {
    int | float64
}

// T is the generic and can be int/Float64 only
func getSumGen[T MyConstraint] (x T, y T) T {
    return x + y
}

func main() {
    fmt.Println("5 + 4 =", getSumGen(5, 4)) // 9
    fmt.Println("5.6 + 4.7 =", getSumGen(5.6, 4.7)) // 10.3
}
```

### Structs
- Allow you to store values with many different types in a structured manner 
```go
// Define
type customer struct {
    name string
    address string
    balance float64
    id int64
}

// Composition: Struct inside struct
type business struct {
    businessName string
    workaddr string
    contact
}

// Struct Args
func getCustInfo(c customer) {
    fmt.Println("%s owes us %2.f", c.name, c.bal)
}

// Instance and Access
func main() {
    var test customer
    test.name = "John Smith"
    test.address = "9 Main St"
    test.balance = 234.56
    getCustInfo(test) // John Smith owes us 234.56
    
    var bTest business
    bTest.name = "ABC Corp"
    bTest.contact.name = "Jane Doe"
}
```

### Defined Types
- Defined type used previously with structs
- You can use them also to enhance the quality of other data types

```go
	type Tsp float64
    type TBs float64
    type ML float64

    func tspToML (tsp Tsp) ML {
        return ML(tsp * 4.92)
    }

    func TBToML (tsp TBs) ML {
        return ML(tsp * 14.79)
    }

    func (tsp Tsp) ToMLs() ML {
        return ML(tsp * 4.92)
    }
    
    // Convert from tsp to mL
	ml1 := ML(Tsp(3) * 4.92)
	fmt.Printf("3 tsps = %.2f mL\n", ml1)

	// Convert from TBs to mL
	ml2 := ML(TBs(3) * 14.79)
	fmt.Printf("3 TBs = %.2f mL\n", ml2)

	// You can use arithmetic and comparison operators
	fmt.Println("2 tsp + 4 tsp =", Tsp(2) + Tsp(4))
	fmt.Println("2 tsp > 4 tsp =", Tsp(2) > Tsp(4))

	// We can convert with functions
	// Bad Way
	fmt.Printf("3 tsp = %.2f mL\n", tspToML(3))
	fmt.Printf("3 TBs = %.2f mL\n", TBToML(3))

	// We can solve this by using methods which
	// are functions associated with a type
	tsp1 := Tsp(3)
	fmt.Printf("%.2f tsp = %.2f mL\n", tsp1, tsp1.ToMLs())
```

### Interfaces
- Interfaces basically group types together based on their methods
- They allow you to create contracts that say if anything inherits it that they will implement defined methods
- If we had animals and wanted to define that they all perform certain actions, but in their specific way we could use an interface
- With Go you don't have to say a type uses an interface. When your type implements the required methods it is automatic

```go
// Creating interface
type shape interface {
    area() float64
    perimeter() float64
}

type square struct {
    length float64
}

type circle struct {
    radius float64
}

func (s square) area() float64{
    return s.length * s.length
}

func (s square) perimeter() float64{
    return s.length * 4
}

func (c circle) area() string {
    return math.Pi * c.radius * c.radius
}

func (c circle) perimeter() string {
    return 2 * math.Pi * c.radius
}

/* 
Originally square and circle have their own structs and methods.
From here on, the methods are common to both of them and we don't want to write redundant code. Interface groups them together.
So s belongs to a struct that has both area and perimeter functions.
*/

func printShapeInfo(s shape) {
    fmt.Printf("Area: %0.2f", s.area())
    fmt.Printf("Perimeter: %0.2f", s.perimeter())
}

func main() {
    printShapeInfo(square{length: 15.2})
    printShapeInfo(circle{radius: 7.5})
}
```

### Error Handling
Go uses the `error` type for error handling. Functions often return multiple values where the last is an error.

```go
import "errors"

// Custom error
var ErrDivideByZero = errors.New("division by zero")

func divide(a, b float64) (float64, error) {
    if b == 0 {
        return 0, ErrDivideByZero
    }
    return a / b, nil
}

func main() {
    result, err := divide(10, 0)
    if err != nil {
        fmt.Println("Error:", err)
        return
    }
    fmt.Println("Result:", result)
}
```

#### Error Wrapping (Go 1.13+)
```go
import "fmt"

func processFile(filename string) error {
    file, err := os.Open(filename)
    if err != nil {
        return fmt.Errorf("failed to open file %s: %w", filename, err)
    }
    defer file.Close()
    // ... process file
    return nil
}

// Unwrapping errors
func main() {
    err := processFile("nonexistent.txt")
    if err != nil {
        // Check if it's a specific type of error
        if errors.Is(err, os.ErrNotExist) {
            fmt.Println("File does not exist")
        }
        // Get the underlying error
        fmt.Println("Underlying error:", errors.Unwrap(err))
    }
}
```

### Defer, Panic, Recover
#### Defer
- Defers execution of a function until the surrounding function returns
- Useful for cleanup operations
- Deferred functions are executed in LIFO (Last In, First Out) order

```go
func main() {
    defer fmt.Println("This will print last")
    defer fmt.Println("This will print second")
    fmt.Println("This will print first")
}
```

#### Panic and Recover
- `panic` stops normal execution and begins panicking
- `recover` regains control of a panicking goroutine

```go
func mayPanic() {
    panic("Something went wrong!")
}

func safeFunction() {
    defer func() {
        if r := recover(); r != nil {
            fmt.Println("Recovered from panic:", r)
        }
    }()
    mayPanic()
    fmt.Println("This won't print")
}

func main() {
    safeFunction()
    fmt.Println("Program continues")
}
```

### Context Package
The `context` package provides a way to pass cancellation signals and deadlines across API boundaries.

```go
import (
    "context"
    "time"
)

// Function that respects context cancellation
func worker(ctx context.Context) {
    for {
        select {
        case <-ctx.Done():
            fmt.Println("Worker cancelled:", ctx.Err())
            return
        default:
            // Do work
            time.Sleep(100 * time.Millisecond)
        }
    }
}

func main() {
    // Context with timeout
    ctx, cancel := context.WithTimeout(context.Background(), 2*time.Second)
    defer cancel()

    go worker(ctx)

    // Wait for timeout
    time.Sleep(3 * time.Second)
}
```

#### Context with Values
```go
type key string

const userKey key = "user"

func processRequest(ctx context.Context) {
    user := ctx.Value(userKey).(string)
    fmt.Println("Processing request for user:", user)
}

func main() {
    ctx := context.WithValue(context.Background(), userKey, "alice")
    processRequest(ctx)
}
```

### Concurrency
- Concurrency is the concept of executing multiple tasks simultaneously at the same time
- Concurrency allows us to have multiple blocks of code share execution time by pausing their execution. 
- We can also run blocks of codes in parallel at the same time. (Concurrent tasks in Go are called goroutines) 
- To execute multiple functions in new goroutines add the word go in front of the function calls (Those functions can't have return values)

```go
func printTo15() {
	for i := 1; i <= 15; i++ {
		fmt.Println("Func 1 :", i)
	}
}
func printTo10() {
	for i := 1; i <= 10; i++ {
		fmt.Println("Func 2 :", i)
	}
}

func main() {
    go printTo15() // Adding go infront would make them run as go routines (threads)
    go printTo10()
    time.Sleep(2*time.Second)
}

/* O/p
Fun 1: 1
Fun 2: 1
Fun 1 : 3
....
*/
```

### Channels
- We can have go routines communicate using channels. One routine acts a sender another acts as a receiver
- For example, if you want the above `printTo15` and `printTo10` functions to print in order, but execute concurrently

```go
func nums1(channel chan int) {
	channel <- 1
	channel <- 2
}
func nums2(channel chan int) {
	channel <- 3
	channel <- 4
}

func main() {
    // Creating channels
    channel1 := make(chan int)
    channel2 := make(chan int)
    // Running nums1 and nums2 concurrently
    go nums1(channel1)
    go nums2(channel2)
    // Printing them in order using channels
    fmt.Println(<-channel1)
    fmt.Println(<-channel1)
    fmt.Println(<-channel2)
    fmt.Println(<-channel2)
}
```

### Testing Basics
Go has built-in support for testing with the `testing` package.

```go
// calculator.go
package calculator

func Add(a, b int) int {
    return a + b
}

func Divide(a, b float64) (float64, error) {
    if b == 0 {
        return 0, errors.New("division by zero")
    }
    return a / b, nil
}
```

```go
// calculator_test.go
package calculator

import (
    "testing"
)

func TestAdd(t *testing.T) {
    result := Add(2, 3)
    expected := 5

    if result != expected {
        t.Errorf("Add(2, 3) = %d; want %d", result, expected)
    }
}

func TestDivide(t *testing.T) {
    result, err := Divide(10, 2)
    expected := 5.0

    if err != nil {
        t.Errorf("Divide(10, 2) returned error: %v", err)
    }

    if result != expected {
        t.Errorf("Divide(10, 2) = %f; want %f", result, expected)
    }
}

func TestDivideByZero(t *testing.T) {
    _, err := Divide(10, 0)

    if err == nil {
        t.Error("Divide(10, 0) should return error")
    }
}

// Benchmark test
func BenchmarkAdd(b *testing.B) {
    for i := 0; i < b.N; i++ {
        Add(2, 3)
    }
}
```

#### Running Tests
```bash
# Run all tests in current package
go test

# Run tests with verbose output
go test -v

# Run benchmark tests
go test -bench=.

# Run specific test
go test -run TestAdd

# Generate coverage report
go test -cover
go test -coverprofile=coverage.out
go tool cover -html=coverage.out
```

### Modules and Dependency Management
Go modules were introduced in Go 1.11 to manage dependencies.

#### Creating a Module
```bash
# Initialize a new module
go mod init example.com/myproject

# This creates go.mod file
module example.com/myproject

go 1.21
```

#### Adding Dependencies
```bash
# Add a dependency
go get github.com/gin-gonic/gin

# Update all dependencies
go get -u

# Remove unused dependencies
go mod tidy
```

#### go.mod and go.sum
- `go.mod`: Defines module path, Go version, and dependencies
- `go.sum`: Contains cryptographic hashes of dependencies for security

```go
// Example go.mod
module example.com/myproject

go 1.21

require (
    github.com/gin-gonic/gin v1.9.1
    github.com/go-playground/validator/v10 v10.14.0
)

require (
    github.com/bytedance/sonic v1.9.1 // indirect
    github.com/chenzhuoyu/base64x v0.0.0-20221115062448-fe3a3abad311 // indirect
    // ... more indirect dependencies
)
```

### Advanced Concurrency Patterns
#### Worker Pools
```go
func worker(id int, jobs <-chan int, results chan<- int) {
    for j := range jobs {
        fmt.Println("worker", id, "started job", j)
        time.Sleep(time.Second)
        fmt.Println("worker", id, "finished job", j)
        results <- j * 2
    }
}

func main() {
    const numJobs = 5
    jobs := make(chan int, numJobs)
    results := make(chan int, numJobs)

    // Start 3 workers
    for w := 1; w <= 3; w++ {
        go worker(w, jobs, results)
    }

    // Send jobs
    for j := 1; j <= numJobs; j++ {
        jobs <- j
    }
    close(jobs)

    // Collect results
    for a := 1; a <= numJobs; a++ {
        <-results
    }
}
```

#### Select with Timeout
```go
func main() {
    c1 := make(chan string, 1)
    go func() {
        time.Sleep(2 * time.Second)
        c1 <- "result 1"
    }()

    select {
    case res := <-c1:
        fmt.Println(res)
    case <-time.After(1 * time.Second):
        fmt.Println("timeout 1")
    }

    // Second example with default
    select {
    case msg := <-c1:
        fmt.Println("received", msg)
    default:
        fmt.Println("no message received")
    }
}
```

### Struct Embedding and Methods
Struct embedding allows one struct to include another struct as an anonymous field.

```go
type Person struct {
    Name string
    Age  int
}

func (p Person) Introduce() {
    fmt.Printf("Hi, I'm %s and I'm %d years old\n", p.Name, p.Age)
}

type Employee struct {
    Person  // Embedded struct
    Company string
    Salary  float64
}

func main() {
    emp := Employee{
        Person: Person{
            Name: "Alice",
            Age:  30,
        },
        Company: "Tech Corp",
        Salary:  75000,
    }

    // Can access embedded fields directly
    fmt.Println(emp.Name)  // Alice
    fmt.Println(emp.Age)   // 30

    // Can call embedded methods
    emp.Introduce()  // Hi, I'm Alice and I'm 30 years old

    // Can also access through embedded struct
    fmt.Println(emp.Person.Name)  // Alice
}
```

#### Method Overriding
```go
func (e Employee) Introduce() {
    fmt.Printf("Hi, I'm %s, I work at %s\n", e.Name, e.Company)
}

func main() {
    emp := Employee{
        Person: Person{Name: "Bob", Age: 25},
        Company: "Dev Inc",
    }

    emp.Introduce()  // Hi, I'm Bob, I work at Dev Inc (overridden method)
    emp.Person.Introduce()  // Hi, I'm Bob and I'm 25 years old (original method)
}
```

### Common Standard Library Packages
#### fmt Package
```go
import "fmt"

// Printing
fmt.Print("Hello")           // No newline
fmt.Println("Hello")         // With newline
fmt.Printf("Name: %s\n", name) // Formatted

// Scanning
var name string
fmt.Scan(&name)              // Read from stdin
fmt.Scanf("%s", &name)       // Formatted scan
fmt.Scanln(&name)            // Read line
```

#### io Package
```go
import "io"

// Copy data between readers and writers
io.Copy(dst, src)

// Read all data from reader
data, err := io.ReadAll(reader)

// Create multi-reader
multiReader := io.MultiReader(reader1, reader2)
```

#### os Package
```go
import "os"

// File operations
file, err := os.Open("file.txt")
file, err := os.Create("newfile.txt")

// Environment variables
os.Getenv("PATH")
os.Setenv("MY_VAR", "value")

// Command line arguments
os.Args  // []string of command line args

// Exit program
os.Exit(1)
```

#### net/http Package
```go
import "net/http"

// Simple HTTP server
http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintf(w, "Hello, %s!", r.URL.Path[1:])
})

http.ListenAndServe(":8080", nil)

// HTTP client
resp, err := http.Get("http://example.com")
if err != nil {
    log.Fatal(err)
}
defer resp.Body.Close()

body, err := io.ReadAll(resp.Body)
```

### Go Tooling
#### go vet
Static analysis tool that finds potential errors in Go code.

```bash
# Run go vet on current package
go vet

# Run go vet on specific files
go vet file1.go file2.go

# Common issues go vet catches:
# - Unused variables
# - Incorrect printf format strings
# - Unreachable code
# - Incorrect lock usage
```

#### go fmt
Automatically formats Go source code.

```bash
# Format all files in current directory
go fmt

# Format specific files
go fmt file1.go file2.go

# Check if files need formatting (returns exit code)
go fmt -d .
```

#### go doc
Shows documentation for packages and symbols.

```bash
# Show package documentation
go doc fmt

# Show function documentation
go doc fmt.Println

# Show method documentation
go doc os.File.Read

# Start local documentation server
go doc -http=:6060
```

---

### Closures
- Closures are functions that don't have to be associated with an identifier (Anonymous)
```go
import "fmt"

// Pass a function to a function
func useFunc(f func(int, int) int, x, y int) {
	fmt.Println("Answer :", (f(x, y)))
}

func sumVals(x, y int) int {
    // Create a closure that sums values
	intSum := func(x, y int) int {
        return x + y 
    }
	fmt.Println("5 + 4 =", intSum(5, 4)) // 9

	// Closures can change values outside the function
	samp1 := 1
	changeVar := func() { 
        samp1 += 1 
    }
	changeVar() // Changing value of a var outside of the function
	fmt.Println("samp1 =", samp1) // sampl = 2

	// Pass a function to a function
	useFunc(sumVals, 5, 8)
}
```

### Regular Expressions
```go
import regexp
func main() {
    reStr := "The ape was at the apex"
    match,_ := regexp.MatchString("ape[^ ]", reStr) // ape not followed by a space
    fmt.Println(match) // true

    reStr2 := "Cat rat mat fat pat"
	r, _ := regexp.Compile("([crmfp]at)")

    // Did you find any matches?
	fmt.Println("MatchString :", r.MatchString(reStr2)) // true

	// Return first match
	fmt.Println("FindString :", r.FindString(reStr2)) // rat

	// Starting and ending index for 1st match
	fmt.Println("Index :", r.FindStringIndex(reStr2)) // [4 7]

	// Return all matches
	fmt.Println("All Matches :", r.FindAllString(reStr2, -1)) // [rat mat fat pat]

	// Get 1st 2 matches
	fmt.Println("First 2 Matches :", r.FindAllString(reStr2, 2)) // [rat mat]

	// Get indexes for all matches
	fmt.Println("Indexes for all matches :", r.FindAllStringSubmatchIndex(reStr2, -1)) //[[4 7 4 7][8 11 8 11][12 15 12 15][16 19 16 19]]

	// Replace all matches with Dog
	fmt.Println(r.ReplaceAllString(reStr2, "Dog")) // Cat Dog Dog Dog Dog
}
```

## Bitwise Operations
Go supports bitwise operations on integer types.

```go
// Bitwise AND
fmt.Println(5 & 3) // 1 (0101 & 0011 = 0001)

// Bitwise OR
fmt.Println(5 | 3) // 7 (0101 | 0011 = 0111)

// Bitwise XOR
fmt.Println(5 ^ 3) // 6 (0101 ^ 0011 = 0110)

// Bitwise NOT (complement)
fmt.Println(^5) // -6 (in two's complement)

// Left shift
fmt.Println(5 << 1) // 10 (0101 << 1 = 1010)

// Right shift
fmt.Println(5 >> 1) // 2 (0101 >> 1 = 0010)

// Check if even/odd
func isEven(n int) bool {
    return n&1 == 0
}

// Count set bits (Hamming weight)
func countBits(n uint) int {
    count := 0
    for n > 0 {
        count += int(n & 1)
        n >>= 1
    }
    return count
}

// Check if power of 2
func isPowerOfTwo(n int) bool {
    return n > 0 && (n&(n-1)) == 0
}

// Swap two numbers without temp
func swap(a, b *int) {
    *a = *a ^ *b
    *b = *a ^ *b
    *a = *a ^ *b
}
```

## Sorting and Searching
### Custom Sorting
Implement `sort.Interface` for custom types.

```go
import "sort"

type Person struct {
    Name string
    Age  int
}

type ByAge []Person

func (a ByAge) Len() int           { return len(a) }
func (a ByAge) Swap(i, j int)      { a[i], a[j] = a[j], a[i] }
func (a ByAge) Less(i, j int) bool { return a[i].Age < a[j].Age }

func main() {
    people := []Person{
        {"Alice", 25},
        {"Bob", 20},
        {"Charlie", 30},
    }
    sort.Sort(ByAge(people))
    fmt.Println(people) // [{Bob 20} {Alice 25} {Charlie 30}]
}

// Sort strings by length, then alphabetically
type ByLengthThenAlpha []string

func (s ByLengthThenAlpha) Len() int { return len(s) }
func (s ByLengthThenAlpha) Swap(i, j int) { s[i], s[j] = s[j], s[i] }
func (s ByLengthThenAlpha) Less(i, j int) bool {
    if len(s[i]) != len(s[j]) {
        return len(s[i]) < len(s[j])
    }
    return s[i] < s[j]
}

func main() {
    strs := []string{"apple", "fig", "banana", "date"}
    sort.Sort(ByLengthThenAlpha(strs))
    fmt.Println(strs) // [fig date apple banana]
}
```

### Binary Search
```go
func binarySearch(arr []int, target int) int {
    low, high := 0, len(arr)-1
    for low <= high {
        mid := low + (high-low)/2
        if arr[mid] == target {
            return mid
        } else if arr[mid] < target {
            low = mid + 1
        } else {
            high = mid - 1
        }
    }
    return -1
}
```

## Implementing Data Structures
### Stack
```go
type Stack []interface{}

func (s *Stack) Push(v interface{}) {
    *s = append(*s, v)
}

func (s *Stack) Pop() interface{} {
    if len(*s) == 0 {
        return nil
    }
    v := (*s)[len(*s)-1]
    *s = (*s)[:len(*s)-1]
    return v
}

func (s *Stack) Peek() interface{} {
    if len(*s) == 0 {
        return nil
    }
    return (*s)[len(*s)-1]
}
```

### Queue
```go
type Queue []interface{}

func (q *Queue) Enqueue(v interface{}) {
    *q = append(*q, v)
}

func (q *Queue) Dequeue() interface{} {
    if len(*q) == 0 {
        return nil
    }
    v := (*q)[0]
    *q = (*q)[1:]
    return v
}

func (q *Queue) Front() interface{} {
    if len(*q) == 0 {
        return nil
    }
    return (*q)[0]
}
```

### Linked List
```go
type Node struct {
    Val  int
    Next *Node
}

type LinkedList struct {
    Head *Node
}

func (l *LinkedList) Insert(val int) {
    node := &Node{Val: val}
    if l.Head == nil {
        l.Head = node
        return
    }
    current := l.Head
    for current.Next != nil {
        current = current.Next
    }
    current.Next = node
}

func (l *LinkedList) Display() {
    current := l.Head
    for current != nil {
        fmt.Printf("%d -> ", current.Val)
        current = current.Next
    }
    fmt.Println("nil")
}
```

### Binary Tree
```go
type TreeNode struct {
    Val   int
    Left  *TreeNode
    Right *TreeNode
}

func inorderTraversal(root *TreeNode) []int {
    var result []int
    if root == nil {
        return result
    }
    result = append(result, inorderTraversal(root.Left)...)
    result = append(result, root.Val)
    result = append(result, inorderTraversal(root.Right)...)
    return result
}
```

### Heap (Min-Heap)
```go
import "container/heap"

type MinHeap []int

func (h MinHeap) Len() int           { return len(h) }
func (h MinHeap) Less(i, j int) bool { return h[i] < h[j] }
func (h MinHeap) Swap(i, j int)      { h[i], h[j] = h[j], h[i] }

func (h *MinHeap) Push(x interface{}) {
    *h = append(*h, x.(int))
}

func (h *MinHeap) Pop() interface{} {
    old := *h
    n := len(old)
    x := old[n-1]
    *h = old[0 : n-1]
    return x
}

func main() {
    h := &MinHeap{3, 1, 4, 1, 5}
    heap.Init(h)
    heap.Push(h, 9)
    fmt.Println(heap.Pop(h)) // 1
}
```

## Algorithms
### Bubble Sort
```go
func bubbleSort(arr []int) {
    n := len(arr)
    for i := 0; i < n-1; i++ {
        for j := 0; j < n-i-1; j++ {
            if arr[j] > arr[j+1] {
                arr[j], arr[j+1] = arr[j+1], arr[j]
            }
        }
    }
}
```

### Quick Sort
```go
func quickSort(arr []int, low, high int) {
    if low < high {
        pi := partition(arr, low, high)
        quickSort(arr, low, pi-1)
        quickSort(arr, pi+1, high)
    }
}

func partition(arr []int, low, high int) int {
    pivot := arr[high]
    i := low - 1
    for j := low; j < high; j++ {
        if arr[j] < pivot {
            i++
            arr[i], arr[j] = arr[j], arr[i]
        }
    }
    arr[i+1], arr[high] = arr[high], arr[i+1]
    return i + 1
}
```

### Merge Sort
```go
func mergeSort(arr []int) []int {
    if len(arr) <= 1 {
        return arr
    }
    mid := len(arr) / 2
    left := mergeSort(arr[:mid])
    right := mergeSort(arr[mid:])
    return merge(left, right)
}

func merge(left, right []int) []int {
    result := make([]int, 0, len(left)+len(right))
    i, j := 0, 0
    for i < len(left) && j < len(right) {
        if left[i] < right[j] {
            result = append(result, left[i])
            i++
        } else {
            result = append(result, right[j])
            j++
        }
    }
    result = append(result, left[i:]...)
    result = append(result, right[j:]...)
    return result
}
```

### Fibonacci (DP)
```go
func fibonacci(n int) int {
    if n <= 1 {
        return n
    }
    dp := make([]int, n+1)
    dp[0], dp[1] = 0, 1
    for i := 2; i <= n; i++ {
        dp[i] = dp[i-1] + dp[i-2]
    }
    return dp[n]
}
```

## Advanced Error Handling
### Custom Errors
```go
type MyError struct {
    Msg  string
    Code int
}

func (e *MyError) Error() string {
    return fmt.Sprintf("Error %d: %s", e.Code, e.Msg)
}

func doSomething() error {
    return &MyError{"Something went wrong", 500}
}
```

### Panic and Recover in Production
```go
func safeDivide(a, b float64) (float64, error) {
    if b == 0 {
        return 0, errors.New("division by zero")
    }
    return a / b, nil
}

func handlePanic() {
    if r := recover(); r != nil {
        fmt.Println("Recovered from panic:", r)
    }
}

func riskyFunction() {
    defer handlePanic()
    // Some risky code
    panic("Something bad happened")
}
```

## Go Idioms and Best Practices
- Use `make` for slices/maps/channels when you know the size.
- Prefer `for range` for iteration.
- Use `defer` for cleanup.
- Handle errors immediately.
- Use interfaces for polymorphism.
- Keep functions small and focused.
- Use goroutines and channels for concurrency.
- Follow naming conventions: exported names start with capital.
- Use `context` for cancellation.
- Write tests and benchmarks.

## Networking Basics in Go
### HTTP Server
```go
import (
    "fmt"
    "net/http"
)

func handler(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintf(w, "Hello, %s!", r.URL.Path[1:])
}

func main() {
    http.HandleFunc("/", handler)
    http.ListenAndServe(":8080", nil)
}
```

### HTTP Client
```go
import (
    "fmt"
    "io"
    "net/http"
)

func main() {
    resp, err := http.Get("https://api.github.com/users/octocat")
    if err != nil {
        panic(err)
    }
    defer resp.Body.Close()
    body, err := io.ReadAll(resp.Body)
    if err != nil {
        panic(err)
    }
    fmt.Println(string(body))
}
```

### TCP Server
```go
import (
    "bufio"
    "fmt"
    "net"
)

func handleConnection(conn net.Conn) {
    defer conn.Close()
    scanner := bufio.NewScanner(conn)
    for scanner.Scan() {
        fmt.Println("Received:", scanner.Text())
        conn.Write([]byte("Echo: " + scanner.Text() + "\n"))
    }
}

func main() {
    ln, err := net.Listen("tcp", ":8080")
    if err != nil {
        panic(err)
    }
    for {
        conn, err := ln.Accept()
        if err != nil {
            continue
        }
        go handleConnection(conn)
    }
}
```
