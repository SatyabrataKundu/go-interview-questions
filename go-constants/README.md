# Constants
* Go constants are declared with a `const` keyword (e.g. `const x int = 10`)
* Constant value can be _initialized_ only once i.e. at the time of its declaration
* Constants cannot be initialized to a _dynamic(i.e. runtime)_ value
e.g. `const i int = math.Pow10(2)` => _invalid (this will throw a compile time error)_
> **Note:** This rule has following exception:  
we can initialize a constant to a _dynamic_ value by using built-in `len` function; provided; an argument to the `len` function is a constant.
e.g.
```golang
  const i int = len("Hello") => valid  
  var msg string = "Hello"
  const j int = len(msg)  => invalid
```
## Typed Constants
* Constant declaration along with its data type
e.g.
```golang
    func main(){
        const i int = 10
        const f float32 = 3.5
        const str string = "Hello!!"
        const b bool = true
    }
```
* A _typed_ constant can only be used with the variables of the same data type
e.g.
```golang
    const n int = 23

    var i int = n       => valid
    var f float64 = n   => invalid 
    var j int32 = n     => invalid
    var b byte = n      => invalid
```

## Untyped Constants (Tyepeless constants)
* When we declare a constant without a type; it becomes _Untyped_ or _Typeless_ constant
e.g.
```golang
        const i = 10
        const f = 3.5
        const str = "Hello!!"
        const b = true
```
* An _untyped_ constant can be used in an expression with variable of any _compatible_ type
e.g.
```golang
    const n = 23

    var i int = n       => valid
    var f float64 = n   => valid 
    var j int32 = n     => valid
    var b byte = n      => valid
    var t bool = n      => invalid
    var s str = n       => invalid
```

> **Notes:** 
* Literals are fixed values of any type (e.g. `2`, `'A'`, `"hello"`, `false`, `3.08`, etc. )
* All basic literals are `unnamed constant values`

## Declaring multiple constants
* We can declare multiple constants in the same statement
e.g.
```golang
    const i, j int = 1, 11
```
* We can declare multiple constants in a group
e.g.
```golang
    const (
        i int = 23
        f float64 = 3.14
    )
```
* If not explicitly specified; a grouped constant get its `type` and `expression` from the preciding (i.e. previous) constant
e.g. 
```golang
    const (
        i int = 24
        j           => Here, Go infers the type of 'j' as 'int' and value of 'j' as 24
    )
```
> **Note:** 
* To export a constant: Declare it at the package level and make its first letter is capital
e.g. `const Metere int = 100`

## Iota ()
* Iota is a `built-in constant number generator` which generates _ever increasing numbers_
* By default; Iota starts at zero 
e.g.
```golang
    const (
        jan = iota          => Here, value of 'jan' will be 0
        feb = iota          => Here, value of 'feb' will be 1
        march = iota        => Here, value of 'march' will be 2
        april               => Here, value of 'april' will be 3
        may                 => Here, value of 'may' will be 4
        june                => Here, value of 'june' will be 5
    )
```
***
## Potential interview questions: 
* **What will be the output of following program?**
```golang
package main

import "fmt"

const msg string

func main() {
    msg = "I am constant!!"
    fmt.Println(msg)
}
```
   1. `I am constant!!`
   2. Run-time error
   3. Compilation error => Correct  
  
> 3. A constant must be initialized to a value at the time of declaration

* **What will be the output of following program?**
```golang
package main

import "fmt"

const sum int32 = 2

func main() {
    i := 5
    fmt.Println(sum * i)
}
```
   1. `10`
   2. Compilation error => Correct
   3. `7`  
  
> 2. A typed constant can only be used with variables of the same type

* **What will be the output of following program?**
```golang
package main

import "fmt"

const (
    jan = iota + 1
    feb
    march
    _
    may
    june
)

func main() {
    fmt.Println(jan, feb, march, may, june)
}
```
   1. `1, 2, 3, 4, 5`
   2. `0, 1, 2, 4, 5`
   3. `1, 2, 3, 5, 6` => Correct   
  
> 3. Iota starts at zero and generates ever-increasing numbers. A constant repeats an _expression_ of previous constant. Blank identifier swallows the value of an expression. 

***
## Test your knowledge
* **What is true about literals?** 
   1. Literals are fixed values of any type 
   2. All literals are untyped constants
   3. Literals can be used in an expression with variable of any _compatible_ type
   4. All of the above => Correct

* **Which one below is valid?**
   1. `s := "hello golang!!"; const n = len(s)`
   2. `const s = "hello golang!!"; const n = len(s)` => Correct
   3. `const n = utf8.RuneCountInString("hello golang!!");`
> 2. we can initialize a constant to a _dynamic_ value by using built-in `len` function; provided; an argument to the `len` function is a constant.

* **How to fix following code?**
```golang
    const msg string
    msg = "Hello golang!!"
```
   1. `const msg = "hello golang!!"` => Correct
   2. `msg := "hello golang!!"`
   3. Above code is correct already

* **What are the values of following constants?**
```golang
    const(
        On = (iota * 3) + 1
        Off
        Both
    )
```
   1. On = 0; Off = 1; Both = 2  
   2. On = 1; Off = 1; Both = 1
   3. On = 1; Off = 4; Both = 7 => Correct
> 3. Iota starts at zero and generates ever-increasing numbers

* **What will be the output of following code?**
```golang
package main

import "fmt"

const n int = 23

var(
    i int = n 
    f float64 = n   
    j int32 = n     
    b byte = n
)  

func main(){
    fmt.Println(i, f, j, b)
}
```
   1. `23, 23, 23, 23`
   2. Compilation error => Correct
   3. Run-time error
> A _typed_ constant can only be used with the variables of the same data type

* **What will be the output of following code?**
```golang
package main

import "fmt"

const n = 23

var(
    i int = n 
    f float64 = n   
    j int32 = n     
    b byte = n
)  

func main(){
    fmt.Println(i, f, j, b)
}
```
   1. `23, 23, 23, 23` => Correct
   2. Compilation error 
   3. Run-time error
> An _untyped_ constant can be used in an expression with variable of any _compatible_ type

* **What will be the output of following code?**
```golang
package main

import "fmt"

const n = 23

var(
    i int = n 
    f float64 = n   
    j int32 = n     
    b byte = n
    s string = n
)  

func main(){
    fmt.Println(i, f, j, b, s)
}
```
   1. `23, 23, 23, 23, 23` 
   2. Compilation error => Correct
   3. Run-time error
> An _untyped_ constant can be used in an expression with variable of any _compatible_ type
***