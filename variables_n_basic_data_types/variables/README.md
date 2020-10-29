# Variables
* A variable(also known as _identifier_) is used to identify a _value with its associated type_ 
e.g. `var i int` => here `i` is a variable of type `int` with value zero
* We must declare a variable before we use it in the program
* Variable name must start with a _letter_ or _underscore_ character
e.g.
    `var str string`, `var _str string` => valid

* Variable name should NOT start with _number_ or _special character_ other than _underscore_
e.g. `var !str string`, `var 1str string` => inavlid

* Variable name should NOT contain _spaces_ or any _special character_ except _underscore_

* We can declare Go variables in multiple ways:
    * **variable declaration:** `var i int`
    * **short variable declaration:** `i := 10` => Go can infer type of variable from context
    * **multiple variables declaration:** 
    ```golang
    ....
    ...
    func main() {
        var i, j, k int
        ....
    }
    ```
    OR
    ```golang
    ....
    ...
    func main() {
        var (
            i int
            j float64
            k string
        )
        ....
    }
    ```
    

* Every _block scoped variable_ should be used otherwise the program won't compile
* It's OK if we declare and don't use _package scoped variable_
* We can initialize Go variables in follwoing ways:
```golang
....
....
//invalid
s := true
func main() {
    //valid
    var s1 bool = true 
    //valid
    var s2 = true
    //valid
    s3 := true
    //valid
    s4,s5 := true, false
    //valid
    s6, x1, y1 := true, 10, 1.23

}
```
***
## Potential interview questions: 
* **Can we change variable's type after its declaration?**
  1. Yes: Go is dynamically typed
  2. No: Go is statically typed => Correct
  3. Yes. Go is both statically as well as dynamically typed

* **Which one is the correct variable name?**
  1. 1name
  2. Na@me
  3. name => Correct

* **What will be the output of following program?**
```golang
package main

import "fmt"

func main(){
    var s = 25
    fmt.Println("Hello golang!!")
}
```
  1. `Hello golang!!`
  2. `25`
  3. Compilation error => Correct
>3. Block scoped variables must be used once declared  

***
## Test your knowledge
* **What will be the output of following program?**
```golang
package main

import "fmt"

var s = 25

func main(){
    fmt.Println("Hello golang!!")
}
```
  1. `Hello golang!!` => Correct
  2. `25`
  3. Compilation error 
> 1. It's OK if we don't use package scoped variable once declared  

* **What will be the output of following program?**
```golang
package main

import "fmt"

func main(){
    var s = 25
    _ = s
    fmt.Println("Hello golang!!")
}
```
  1. `Hello golang!!` => Correct
  2. `25`
  3. Compilation error 
> 1. We can use _blank identifier_ to swallow unused variable

* **Which is correct declaration?**
    1. `var int i := 5`
    2. `var b bool := 3`
    3. `b := true ` => Correct

* **which is correct declaration?**
    1. `a,b,c := 10, 2.5`
    2. `a = 10`
    3. `a,b,c := 10, true, 3.14` => Correct

* **which declaration is equal to `var s string = "hello..."`?**
    1. `var s bool := "hello..."`
    2. `s := "hello..."` => Correct
    3. `var s := "hello..."`

* **what is the type of `i` variable? `i := 10`?**
    1. unit32
    2. int => Correct
    3. float64

* **what is the type of `f` variable? `f := 6.25`?**
    1. int
    2. complex64
    3. float64 => Correct

* **What will be the output of following program?**
```golang
package main

import "fmt"

s := 25

func main(){
    fmt.Println(s)
}
```
  1. `Hello golang!!` 
  2. `25`
  3. Compilation error => Correct
> 3. we can't use short declaration at the package scope   

***
