# Create, build and run a go program
## Create a go program:
 
**Typical Go program components**
Following is the typical go program i.e. `$GOPATH/src/myproject/main.go`
```golang 
    package main

    import "fmt"

    func main() {
        fmt.Println("Hello Golang!!")
    }
```
* The `package` clause (non-optional):  
    * This must be the first statement in any go source code file e.g. `package main`
    * Without this clause your go program won't compile

* The `import` clause (optional):
    * The `import` keyword makes an external package available to the current .go file (e.g. `import fmt` makes `fmt` package available to the current .go file)

* The `main` function (non-optional):
    * This is the entry point of any go program
    * Without `main` function your go program won't be able to run
***

## Build a go program (go build):
* `go build` command compiles packages and dependencies required for the go program
* This command should always be run inside the program directory 
e.g.
```shell
cd $GOPATH/src/myproject/
go build
##This will generate an executable named `$GOPATH/src/myproject/myproject` 
``` 
* `go build` generates a compiled executable go program file inside the program directory

> **Note**: `go install` generates a compiled executable go program file inside the `$GOPATH/bin/` directory
***
## Executing a go program:
A go program can be executed in two ways
1. Running the executable go program file i.e. generated using `go build` command
e.g. On linux:
```shell
$cd $GOPATH/src/myproject/
$go build
$ls
myproject main.go
$./myproject 
Hello Golang!!

```
2. Using `go run` command:  
```shell
$cd $GOPATH/src/myproject/
$go run main.go 
Hello Golang!!
```
> `go run` command both compiles and runs a go program
***

## Potential interview questions:
* **What must be the first statement any go source file?**
    1. An `import` statement
    2. A `func` declaration
    3. A `package` clause => correct

* **What will be the output of the following program?** 
```golang
import  "fmt"

func main() {
    fmt.Println("Hello golang!!")
}
```
   1. `Hello golang!!`
   2. A compilation error => Correct
   3. No output

***
## Test your knowledge
* **How will you fix following program?** 
```golang
import  "fmt"

func main() {
    fmt.Println("Hello golang!!")
}
```
   1. Add `package main` at the beginning => Correct
   2. Add `package main`after the `import` statement
   3. There is nothing wrong with the program

* **What does `import fmt` do in the following program?** 
```golang
package main

import "fmt"

func main() {
    fmt.Println("Hello golang!!")
}
```
   1. It makes the `fmt` package available inside current .go file => correct 
   2. It prints `Hello golang` to the console
   3. It defines a new package called `fmt`

* **What will be the output of the following program?** 
```golang
package main

func main() {

}
```
   1. `Hello golang!!`
   2. It's an incorrect program
   3. It's a correct program but it doesn't give any output => Correct

* **What does `go build` do when it's run inside a program directory?**
    1. It runs a go program
    2. It compiles a go program
    3. It compiles a go program and generates a compiled executable go program file inside the program directory => Correct

* **What does `go run` do when it's run inside a program directory?**
    1. It compiles and runs a go program
    2. It compiles a go program
    3. It will give an error as: `go run: no go files listed` => Correct

* **What does `go build` do when it's run inside a program directory?**
    1. It runs a go program
    2. It generates a compiled executable go program file inside the program directory
    3. It generates a compiled executable go program file inside the `$GOPATH/bin/` directory => Correct

* **What is the purpose of `main` function in the following program?**
```golang
package main

import "fmt"

func main() {
    fmt.Println("Hello golang!!")
}
```
   1. It identifies package `main`
   2. It is used to print message to the console
   3. It defines the starting point of this go program => Correct

* **Where should we call the `main` function in a go program?**
    1. Inside any function
    2. After `import` statement
    3. We should not call the `main` function; Go calls it automatically => Correct
***