# Package and Scopes
## **Package:**
```golang
package main

import "fmt"

func main(){
    fmt.Println("Hello golang!!")
}
```
* Conceptually, a _package_ is a collection of go source files &/or other go packages 
* The `package <package_name>` clause lets the Go compiler know which package the current file belongs to
* The `package <package_name>` clause _must_ be the first statement in any go source file; otherwise the program won't compile
* There are mainly two types of packages in Go:  
    1. **Executable package**: The package which contains the main function (e.g. `package main`)
    2. **Library package**: These packages are created for importing them into other packages (`package fmt`)  

| Library Package       | Executable Package     |
|---                    |---                     |
| created for the reuse | created for execution  |
| can be imported       | shouldn't be imported  |
| can have any name     | name should be main    |
| no func main          | must contain func main |                      | 

***
## **Scope**
* The scope is nothing but the visibilty of the declared names
* The location of a statement/expression in a go source code defines its _scope_ within the program
```golang
package main

// file scope
import "fmt"

//package scope
const subject = "golang!!" 

// package scope
func main(){ // begin block scope 

    var hello = "hello "

    fmt.Println(hello, subject)
} // block scope end

```
> **Notes:** 
> We cannot redeclare a package scope variable but we can redeclare block scope variable
> Importing happens in the file scope
***
## Potential interview questions: 
* **Which name below is _package scoped_?**
```golang
package main

import "fmt"

var sw bool 

func main(){ 
    var hello = "hello "
    fmt.Println(hello)
} 
```
  1. `hello`
  2. `fmt`
  3. `sw` => Correct 

* **What is the scope of the `main` function in following code?**
```golang
package main

import "fmt"

var sw bool 

func main(){ 
    var hello = "hello "
    fmt.Println(hello)
} 
```
  1. file scope
  2. package scope => Correct
  3. block scope 

* **How many times you can use `package <name>` clause in single go source code file?**
  1. Once => Correct
  2. Twice 
  3. Any number of times

***
## Test your knowledge
* **Why is `package <name>` clause used in go source code file?**
    1. to import a package
    2. to declare a new function
    3. to let Go compiler know which package this file belongs to => Correct

* **Where should we save multiple source code files that belongs to same package?**
    1. inside same directory => Correct
    2. across multiple directories
    3. inside GOPATH

* **Which of the follwoing statement is correct?**
    1. main package
    2. package main => Correct
    3. my package

* **Which of the following package types `go run` can execute?**
    1. Library package
    2. Executable package => Correct
    3. Imported package

* **Which of the following package types `go build` can compile?**
    1. Library package
    2. Executable package 
    3. Both 1 and 2 => Correct

* **Which one is an executable package?**
    1. `package Main` with `func Main`
    2. `package exec` with `func exec`
    3. `package main` with `func main` => Correct

* **which package is created for reuse and can be imported?**
    1. Importable package
    2. Library package => Correct
    3. Exec package

* **What is a scope?**
    1. A self contained block of code
    2. The visibility of declared names => Correct
    3. A control structure that decides address binding of the variables

* **Can other files in main package see `fmt` name?**
```golang
package main

import "fmt"

var sw bool 

func main(){ 
    var hello = "hello "
    fmt.Println(hello)
} 
```
  1. Yes. 
  2. No: It's in the file scope => Correct
  3. No: It's in the block scope 
>2. Importing happens in the file scope 

* **What will be the output of following program?**
```golang
package main

import "fmt"

var sw = "hi" 
var sw = true

func main(){ 
    fmt.Println(sw)
} 
```
  1. Compilation error => Correct 
  2. `hello`
  3. `true`
>1. We cannot redeclare a package scoped variable 

* **What will be the output of following program?**
```golang
package main

import "fmt"

var sw = "hi" 

func main(){ 
    var sw = "hello"
    fmt.Println(sw)
} 
```
  1. Compilation error 
  2. `hi`
  3. `hello` => Correct
>Here, the `sw` name outside _main_ function is package scoped and `sw` name inside the _main_ funcion is block scoped. The block scoped declaration prevails within the block. Also, for Go compiler they are two different _identifiers_

