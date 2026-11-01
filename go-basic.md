## Go

---

# 1. BASICS

## 1.1 Packages

Every Go program belongs to a package.

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, Go!")
}
```

- `package main`: Executable application.
- `import`: Import another package.
- `func main()`: Application entry point.
- `fmt`: Standard formatting package.

Java comparison: Similar to Java packages, imports, and the `main()` entry point.

## 1.2 Imports

```go
import (
    "fmt"
    "math"
    "strings"
)

func main() {
    fmt.Println(math.Sqrt(16))
    fmt.Println(strings.ToUpper("go"))
}
```

## 1.3 Exported Names

Go uses capitalization to control visibility.

```go
var Name = "Deepak"  // Exported
var age = 35         // Package-private
```

- Uppercase first letter = exported.
- Lowercase first letter = unexported.

This applies to functions, types, variables, and constants.

## 1.4 Functions

```go
func add(x int, y int) int {
    return x + y
}
```

When consecutive parameters have the same type:

```go
func add(x, y int) int {
    return x + y
}
```

Multiple return values:

```go
func calculate(a, b int) (int, int) {
    return a + b, a * b
}

sum, product := calculate(5, 3)
```

Go commonly returns an error as the last return value.

```go
func divide(a, b float64) (float64, error) {
    if b == 0 {
        return 0, fmt.Errorf("division by zero")
    }

    return a / b, nil
}
```

## 1.5 Named Return Values

```go
func calculate(a, b int) (sum int) {
    sum = a + b
    return
}
```

Named return values are initialized to their zero values.

## 1.6 Variables

Three common declaration styles:

```go
var name string = "Go"

var age int
age = 35

city := "Chicago"
```

Important:

- `var` works inside and outside functions.
- `:=` is shorthand and only works inside functions.
- Go requires variables to be used once declared.

Multiple declarations:

```go
var (
    name = "Go"
    age  = 10
)
```

## 1.7 Basic Data Types

| Type | Description |
|---|---|
| bool | Boolean |
| string | Text |
| int | Integer |
| int8/int16/int32/int64 | Signed integers |
| uint | Unsigned integer |
| float32/float64 | Floating point |
| byte | Alias for uint8 |
| rune | Alias for int32, Unicode code point |
| complex64/complex128 | Complex numbers |

```go
var isActive bool = true
var age int = 35
var price float64 = 99.99
var name string = "Go"
var character rune = 'A'
```

## 1.8 Zero Values

Go automatically initializes variables.

| Type | Zero Value |
|---|---|
| int | 0 |
| float64 | 0 |
| bool | false |
| string | "" |
| pointer | nil |
| slice | nil |
| map | nil |
| interface | nil |

```go
var count int
var active bool
var name string

fmt.Println(count)  // 0
fmt.Println(active) // false
fmt.Println(name)   // ""
```

## 1.9 Type Conversion

Go does not automatically convert between different numeric types.

```go
var x int = 10
var y float64 = float64(x)

var a float64 = 10.5
var b int = int(a) // 10
```

String conversion:

```go
import "strconv"

number := 123

text := strconv.Itoa(number)

value, err := strconv.Atoi("123")
```

## 1.10 Constants

```go
const Pi = 3.14159

const (
    StatusActive = "ACTIVE"
    StatusFailed = "FAILED"
)
```

`iota` generates sequential constants.

```go
const (
    Sunday = iota
    Monday
    Tuesday
    Wednesday
)
```

Values: 0, 1, 2, 3.

## 1.11 Numeric Constants

Go constants can have arbitrary precision until assigned a concrete type.

```go
const (
    Big   = 1 << 100
    Small = Big >> 99
)
```

---

# 2. FLOW CONTROL

## 2.1 For Loop

Go has only one looping keyword: `for`.

Traditional loop:

```go
for i := 0; i < 5; i++ {
    fmt.Println(i)
}
```

While-style loop:

```go
i := 0

for i < 5 {
    fmt.Println(i)
    i++
}
```

Infinite loop:

```go
for {
    fmt.Println("Running")
}
```

## 2.2 If / Else

```go
age := 20

if age >= 18 {
    fmt.Println("Adult")
} else {
    fmt.Println("Minor")
}
```

Go supports initialization inside an if statement.

```go
if age := 20; age >= 18 {
    fmt.Println("Adult")
}
```

The variable is scoped to the if/else statement.

## 2.3 Switch

```go
day := "Monday"

switch day {
case "Monday":
    fmt.Println("Start of week")
case "Friday":
    fmt.Println("Almost weekend")
default:
    fmt.Println("Regular day")
}
```

Multiple conditions:

```go
switch day {
case "Saturday", "Sunday":
    fmt.Println("Weekend")
default:
    fmt.Println("Weekday")
}
```

Switch without an expression:

```go
score := 85

switch {
case score >= 90:
    fmt.Println("A")
case score >= 80:
    fmt.Println("B")
default:
    fmt.Println("C")
}
```

Unlike traditional C-style switches, Go automatically stops after a matching case. Use `fallthrough` when explicitly needed.

## 2.4 Defer

`defer` schedules a function call to execute when the surrounding function returns.

```go
func main() {
    defer fmt.Println("Third")
    fmt.Println("First")
    fmt.Println("Second")
}
```

Output:

```text
First
Second
Third
```

Multiple defers execute in LIFO order.

```go
defer fmt.Println("A")
defer fmt.Println("B")
defer fmt.Println("C")
```

Output: C, B, A.

Common use: Resource cleanup.

```go
file, err := os.Open("data.txt")
if err != nil {
    return
}
defer file.Close()
```

---

# 3. MORE TYPES

## 3.1 Pointers

A pointer stores the memory address of a value.

```go
x := 42

p := &x

fmt.Println(*p) // 42

*p = 100

fmt.Println(x) // 100
```

Operators:

- `&x`: Address of x.
- `*p`: Value stored at the address.
- `*int`: Pointer to an integer.

Go does not support pointer arithmetic.

## 3.2 Structs

Structs group related fields.

```go
type Employee struct {
    Name   string
    Age    int
    Salary float64
}
```

Create a struct:

```go
employee := Employee{
    Name:   "John",
    Age:    30,
    Salary: 90000,
}
```

Access fields:

```go
fmt.Println(employee.Name)
employee.Age = 31
```

Java comparison: Similar to a class containing fields, but structs do not automatically provide inheritance or class behavior.

## 3.3 Struct Literals

```go
type Point struct {
    X, Y int
}

p1 := Point{10, 20}

p2 := Point{
    X: 10,
    Y: 20,
}
```

Prefer named fields when initialization readability matters.

## 3.4 Struct Pointers

```go
p := &Point{10, 20}

fmt.Println(p.X)

p.X = 100
```

Go automatically dereferences struct pointers when accessing fields.

## 3.5 Arrays

Arrays have a fixed length.

```go
var numbers [5]int

numbers[0] = 10
numbers[1] = 20
```

Array initialization:

```go
numbers := [3]int{10, 20, 30}
```

Length:

```go
fmt.Println(len(numbers))
```

Important: Arrays are values. Assigning an array copies its contents.

## 3.6 Slices

Slices are dynamically sized views of arrays.

```go
numbers := []int{10, 20, 30, 40, 50}
```

Access elements:

```go
fmt.Println(numbers[0])
```

Slice an existing slice:

```go
fmt.Println(numbers[1:4]) // [20 30 40]
fmt.Println(numbers[:3])  // [10 20 30]
fmt.Println(numbers[2:])  // [30 40 50]
```

## 3.7 Slice Length and Capacity

```go
numbers := []int{10, 20, 30, 40, 50}

fmt.Println(len(numbers)) // 5
fmt.Println(cap(numbers)) // 5
```

- `len()`: Number of elements currently accessible.
- `cap()`: Maximum length before a new underlying array is needed.

## 3.8 Nil Slices

```go
var numbers []int

fmt.Println(numbers == nil) // true
fmt.Println(len(numbers))   // 0
```

A nil slice is valid and can be appended to.

## 3.9 Make

Use `make()` to create initialized slices, maps, and channels.

```go
numbers := make([]int, 5)

fmt.Println(len(numbers)) // 5
```

Specify capacity:

```go
numbers := make([]int, 3, 10)

fmt.Println(len(numbers)) // 3
fmt.Println(cap(numbers)) // 10
```

## 3.10 Append

```go
numbers := []int{1, 2, 3}

numbers = append(numbers, 4)

numbers = append(numbers, 5, 6)
```

Append another slice:

```go
more := []int{7, 8}

numbers = append(numbers, more...)
```

The `...` expands a slice into individual arguments.

## 3.11 Range

Iterate over slices and arrays:

```go
numbers := []int{10, 20, 30}

for index, value := range numbers {
    fmt.Println(index, value)
}
```

Only values:

```go
for _, value := range numbers {
    fmt.Println(value)
}
```

Only indexes:

```go
for index := range numbers {
    fmt.Println(index)
}
```

## 3.12 Maps

Maps store key-value pairs.

```go
ages := map[string]int{
    "John": 30,
    "Mary": 25,
}
```

Access:

```go
fmt.Println(ages["John"])
```

Insert/update:

```go
ages["David"] = 40
```

Delete:

```go
delete(ages, "Mary")
```

Check if key exists:

```go
age, exists := ages["John"]

if exists {
    fmt.Println(age)
}
```

Map iteration:

```go
for key, value := range ages {
    fmt.Println(key, value)
}
```

Important:
- Map iteration order is unspecified.
- Maps are reference-like data structures.
- A nil map can be read but cannot accept new entries.
- Use `make()` or a map literal before writing.

## 3.13 Function Values

Functions are first-class values in Go.

```go
func add(a, b int) int {
    return a + b
}

operation := add

result := operation(10, 20)
```

Functions can be passed as arguments.

```go
func calculate(a, b int, operation func(int, int) int) int {
    return operation(a, b)
}
```

## 3.14 Function Closures

A closure captures variables from its surrounding scope.

```go
func counter() func() int {
    count := 0

    return func() int {
        count++
        return count
    }
}

c := counter()

fmt.Println(c()) // 1
fmt.Println(c()) // 2
fmt.Println(c()) // 3
```

Closures are useful for maintaining state without defining a separate struct.

---

# 4. METHODS AND INTERFACES

## 4.1 Methods

Go does not have classes. You can attach methods to named types.

```go
type Rectangle struct {
    Width  float64
    Height float64
}

func (r Rectangle) Area() float64 {
    return r.Width * r.Height
}
```

Usage:

```go
r := Rectangle{10, 5}

fmt.Println(r.Area()) // 50
```

The receiver `(r Rectangle)` connects the method to the type.

## 4.2 Pointer Receivers

Use pointer receivers when modifying the original value.

```go
func (r *Rectangle) Resize(width, height float64) {
    r.Width = width
    r.Height = height
}
```

Usage:

```go
r := Rectangle{10, 5}

r.Resize(20, 10)
```

Remember:
- Value receiver: Operates on a copy.
- Pointer receiver: Can modify the original value.

## 4.3 Methods on Non-Struct Types

Methods can be attached to user-defined named types.

```go
type MyInt int

func (n MyInt) Double() MyInt {
    return n * 2
}
```

The receiver type must be defined in the same package.

## 4.4 Interfaces

An interface defines behavior through method signatures.

```go
type Shape interface {
    Area() float64
}
```

Implementing an interface requires no explicit declaration.

```go
type Circle struct {
    Radius float64
}

func (c Circle) Area() float64 {
    return 3.14 * c.Radius * c.Radius
}
```

The Circle type automatically satisfies Shape.

```go
func printArea(s Shape) {
    fmt.Println(s.Area())
}
```

Usage:

```go
circle := Circle{Radius: 5}

printArea(circle)
```

This is called implicit interface implementation.

## 4.5 Empty Interface

```go
var value any

value = 10
value = "Hello"
value = true
```

`any` is an alias for `interface{}`.

It can hold values of any type.

## 4.6 Type Assertions

Extract a concrete value from an interface.

```go
var value any = "Hello"

text := value.(string)

fmt.Println(text)
```

Safer approach:

```go
text, ok := value.(string)

if ok {
    fmt.Println(text)
}
```

## 4.7 Type Switch

Identify the concrete type dynamically.

```go
func checkType(value any) {
    switch v := value.(type) {
    case int:
        fmt.Println("Integer:", v)
    case string:
        fmt.Println("String:", v)
    case bool:
        fmt.Println("Boolean:", v)
    default:
        fmt.Println("Unknown type")
    }
}
```

## 4.8 Stringer Interface

The `fmt.Stringer` interface requires a `String()` method.

```go
type Person struct {
    Name string
    Age  int
}

func (p Person) String() string {
    return fmt.Sprintf("%s (%d)", p.Name, p.Age)
}
```

Usage:

```go
p := Person{"John", 30}

fmt.Println(p)
```

## 4.9 Error Interface

Errors are values in Go.

```go
type error interface {
    Error() string
}
```

Create an error:

```go
err := errors.New("something went wrong")
```

Return errors from functions:

```go
func validate(age int) error {
    if age < 18 {
        return errors.New("underage")
    }

    return nil
}
```

Check errors:

```go
if err := validate(15); err != nil {
    fmt.Println(err)
}
```

## 4.10 Readers

The `io.Reader` interface is one of the most important Go interfaces.

```go
type Reader interface {
    Read(p []byte) (n int, err error)
}
```

Example:

```go
reader := strings.NewReader("Hello Go")

buffer := make([]byte, 5)

n, err := reader.Read(buffer)

if err != nil && err != io.EOF {
    panic(err)
}

fmt.Println(string(buffer[:n]))
```

## 4.11 Images

The `image.Image` interface represents an image.

Important methods:

```go
type Image interface {
    ColorModel() color.Model
    Bounds() Rectangle
    At(x, y int) color.Color
}
```

The Go Tour uses this to demonstrate how different concrete types can satisfy the same interface.

---

# 5. GENERICS

Generics allow functions and types to work with multiple data types while maintaining compile-time type safety.

## 5.1 Generic Functions

```go
func Print[T any](value T) {
    fmt.Println(value)
}
```

Usage:

```go
Print[int](10)
Print[string]("Hello")
Print[float64](10.5)
```

Go can often infer the type:

```go
Print(10)
Print("Hello")
```

## 5.2 Type Parameters

`T` is a type parameter.

```go
func First[T any](items []T) T {
    return items[0]
}
```

Usage:

```go
numbers := []int{10, 20, 30}
names := []string{"John", "Mary"}

fmt.Println(First(numbers))
fmt.Println(First(names))
```

## 5.3 Constraints

Constraints define which types are allowed.

```go
func Add[T int | float64](a, b T) T {
    return a + b
}
```

This function accepts integers or float64 values.

## 5.4 Any Constraint

```go
func Display[T any](value T) {
    fmt.Println(value)
}
```

`any` permits all types.

## 5.5 Comparable Constraint

Use `comparable` when a generic value needs equality operators.

```go
func Contains[T comparable](items []T, target T) bool {
    for _, item := range items {
        if item == target {
            return true
        }
    }

    return false
}
```

Usage:

```go
fmt.Println(Contains([]int{1, 2, 3}, 2))
fmt.Println(Contains([]string{"Go", "Java"}, "Go"))
```

## 5.6 Generic Types

Types can also have type parameters.

```go
type Stack[T any] struct {
    Items []T
}

func (s *Stack[T]) Push(value T) {
    s.Items = append(s.Items, value)
}
```

Usage:

```go
stack := Stack[int]{}

stack.Push(10)
stack.Push(20)
```

Key takeaway: Generics reduce duplicate code while preserving type safety.

---

# 6. CONCURRENCY

Concurrency is one of Go's biggest strengths.

## 6.1 Goroutines

A goroutine is a lightweight concurrent execution unit.

```go
func sayHello() {
    fmt.Println("Hello")
}

func main() {
    go sayHello()

    time.Sleep(time.Second)
}
```

The `go` keyword starts a goroutine.

Important: Do not use `time.Sleep()` as production synchronization. Use channels, WaitGroups, or other synchronization mechanisms.

## 6.2 Channels

Channels allow goroutines to communicate.

Create a channel:

```go
ch := make(chan int)
```

Send data:

```go
ch <- 10
```

Receive data:

```go
value := <-ch
```

Example:

```go
func worker(ch chan int) {
    ch <- 100
}

func main() {
    ch := make(chan int)

    go worker(ch)

    result := <-ch

    fmt.Println(result)
}
```

An unbuffered channel synchronizes sender and receiver.

## 6.3 Buffered Channels

Buffered channels allow a limited number of values without an immediate receiver.

```go
ch := make(chan int, 2)

ch <- 10
ch <- 20

fmt.Println(<-ch)
fmt.Println(<-ch)
```

Capacity is two.

## 6.4 Channel Blocking

- Sending blocks until a receiver is ready or buffer space is available.
- Receiving blocks until data is available.
- Sending on a closed channel panics.
- Receiving from a closed channel returns the zero value immediately.

## 6.5 Closing Channels

```go
ch := make(chan int, 2)

ch <- 10
ch <- 20

close(ch)

for value := range ch {
    fmt.Println(value)
}
```

Important:
- The sender normally closes the channel.
- Never close a channel from a receiver just because it has finished receiving.
- Closing indicates no more values will be sent.

## 6.6 Range Over Channels

```go
for value := range ch {
    fmt.Println(value)
}
```

The loop continues until the channel is closed and drained.

## 6.7 Select

`select` waits on multiple channel operations.

```go
select {
case value := <-ch1:
    fmt.Println("Channel 1:", value)

case value := <-ch2:
    fmt.Println("Channel 2:", value)

default:
    fmt.Println("No channel ready")
}
```

If multiple cases are ready, Go chooses one pseudo-randomly.

## 6.8 Timeout Pattern

```go
select {
case result := <-ch:
    fmt.Println(result)

case <-time.After(2 * time.Second):
    fmt.Println("Timeout")
}
```

## 6.9 Sync Package

The `sync` package provides synchronization primitives.

### WaitGroup

Wait for multiple goroutines to finish.

```go
var wg sync.WaitGroup

for i := 0; i < 3; i++ {
    wg.Add(1)

    go func(id int) {
        defer wg.Done()
        fmt.Println("Worker", id)
    }(i)
}

wg.Wait()
```

### Mutex

Protect shared data.

```go
var (
    counter int
    mu      sync.Mutex
)

func increment() {
    mu.Lock()
    counter++
    mu.Unlock()
}
```

Use `defer mu.Unlock()` when appropriate to ensure unlocking happens on every return path.

### RWMutex

Allows multiple readers or one writer.

```go
var mu sync.RWMutex

mu.RLock()
fmt.Println("Read operation")
mu.RUnlock()

mu.Lock()
fmt.Println("Write operation")
mu.Unlock()
```

---

# 7. IMPORTANT GO SYNTAX QUICK REFERENCE

| Operation | Syntax |
|---|---|
| Print | `fmt.Println()` |
| Print formatted | `fmt.Printf()` |
| String formatting | `fmt.Sprintf()` |
| Length | `len()` |
| Capacity | `cap()` |
| Append | `append()` |
| Create slice/map/channel | `make()` |
| Address | `&variable` |
| Dereference | `*pointer` |
| Error check | `if err != nil` |
| Start goroutine | `go function()` |
| Channel send | `ch <- value` |
| Channel receive | `value := <-ch` |
| Defer execution | `defer function()` |
| Type assertion | `value.(Type)` |
| Type switch | `switch v := x.(type)` |

# 8. GO COMMANDS

```bash
# Check Go version
go version

# Create a module
go mod init myproject

# Run application
go run main.go

# Compile application
go build

# Run tests
go test ./...

# Run tests with coverage
go test -cover ./...

# Format code
go fmt ./...

# Download dependencies
go mod tidy

# List dependencies
go list -m all

# Run static analysis
go vet ./...

# Race detector
go test -race ./...
```

# 9. JAVA VS GO QUICK COMPARISON

| Concept | Java | Go |
|---|---|---|
| Entry point | `public static void main` | `func main()` |
| Class | `class` | Struct + methods |
| Interface | Explicit `implements` | Implicit implementation |
| Inheritance | Supported | Composition |
| Generics | Generics | Type parameters |
| Exception handling | try/catch | Error returns |
| Null | null | nil |
| Loops | for, while, do-while | for |
| Concurrency | Threads, ExecutorService | Goroutines |
| Communication | BlockingQueue, etc. | Channels |
| Resource cleanup | try-with-resources | defer |
| Collections | List, Map, Set | Slices, maps |
| Access modifiers | public/private/protected | Uppercase/lowercase |
| Constructors | Constructors | Functions returning values |

# 10. MOST IMPORTANT GO CONCEPTS TO MASTER

1. Slices vs arrays.
2. Maps and their initialization.
3. Pointers and pointer receivers.
4. Structs and composition.
5. Interfaces and implicit implementation.
6. Error handling without exceptions.
7. Defer and resource cleanup.
8. Goroutines and channels.
9. Select and channel synchronization.
10. Mutex and WaitGroup.
11. Generics and type constraints.
12. Go modules and package organization.

**Learning recommendation:** Do not just memorize the syntax. Write small programs for each concept and understand how Go handles memory, errors, types, and concurrency.
