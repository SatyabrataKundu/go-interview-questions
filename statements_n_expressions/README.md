# Statements and Expressions

## Key concepts
### **Statements:**
```golang
package main

import "fmt"

func main(){
    fmt.Println("Hello!!")
}
```
* Any instruction in go program is a statement (e.g. `import "fmt"`)
* Statements control the execution flow of the go program
e.g. The statement `fmt.Println("Hello")` in above program takes control of execution to the `Println` function of `fmt` package which is an external package

> **Note:** Idiomatically, we seperate two or more go statements with a _newline_. Although, implicitly, go compiler treats _newline_ as a _semicolon(;)_
e.g. 
```golang
package main

import "fmt"

func main(){
    fmt.Println("Hello!!")
    fmt.Println("World!!")
}
```
is equivalent to:
```golang
package main

import "fmt"

func main(){
    fmt.Println("Hello!!"); fmt.Println("World!!")
}
```
***
### **Expressions:**
```golang
package main

import (
    "fmt"
    "runtime"
)

func main(){
    // this will print number of CPUs
    fmt.Println(runtime.NumCPU())
}

```
* An expression returns one or more values
* Expressions should be used _with_ or _within_ a statement 
e.g. `runtime.NumCPU()` is an expression which is used within the `fmt.Println(..)` statement
* A function call that returns one or more values is an expression
* An operator can combine expressions
e.g. `fmt.Println(runtime.NumCPU()+1)` => The `+` operator will add 1 to the return value of `runtime.NumCPU()` call

***

## Potential interview questions: 
* **What will be the output of following program?**
```golang
package main

func main() {
    "Hello!!"
}
```
  1. `Hello!!`
  2. An error as: "Hello!!" evaluated but not used => Correct (reason: an expression must be used _with_ or _within_ a statement )
  3. An error as: syntax error: "Hello"  

* **Will the following program work?**
```golang
package main

import "fmt"

func main(){
    fmt.Println("Will "); fmt.Println("this "); fmt.Println("work?")
}
```
   1. No. Each statement should be on newline
   2. Yes. Expressions can be seperated with semicolon
   3. Yes. Go implicitly adds semicolon for each statement already => Correct

***
## Test your knowledge
* **Which one is the correct description for a statement?** 
    1. A statement produces value
    2. A statement contains an expression
    3. A statement is an instruction which controls the execution flow => Correct

* **Which one is the correct description for an expression?** 
    1. An expression produces one or more values => Correct
    2. An expression contains a statement
    3. An expression is an instruction which controls the execution flow

* **Which of the following is true about the operators?** 
    1. An operator is an expression
    2. An Operator contains an expression
    3. An operator can combine expressions => Correct

* **What is true about `add(1,2)` in the following program?**
```golang
package main

import "fmt"

func add(a int, b int) int {
    return a+b
}

func main(){
    fmt.Println(add(1,2))
}
```
   1. `add(1,2)` is an expression => Correct
   2. `add(1,2)` is a statement
   3. `add(1,2)` is an operator

* **What is true about `add(1,2)` in the following program?**
```golang
package main

import "fmt"

func add(a int, b int) {
    fmt.Println(a+b)
}

func main(){
    add(1,2)
}
```
   1. `add(1,2)` is an expression 
   2. `add(1,2)` is a statement => Correct
   3. `add(1,2)` is an operator
***