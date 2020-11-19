# Control structures in go
* These are the statements (or constructs) which alter the execution flow of the program
* Logical operators play important role in deciding control flow of the program

## Operators in go
|   Operator type       |operator name              |operator symbol    | example 
|---|---|---|---|
|   Equality operators  |equals to                  |   `==`            |   `true == true => true`
|                       |NOT equal to               |   `!=`            |   `true != true => false`
|   Ordering operators  |greater than               |   `>`             |   `1 > 2 => false`
|                       |less than                  |   `<`             |   `1 < 2 => true`
|                       |greater than or equal to   |   `>=`            |   `1 >= 2 => false`
|                       |less than or equal to      |   `<=`            |   `1 <= 2 => true`
|   Logical operators   |Logical NOT                |   `!`             |   `!false => true`
|                       |Logical AND                |   `&&`            |   `true && true => true`
|                       |Logical OR                 |   `||`            |   `true || false => true`

## Logical operators short-circuit
* Go implements `short-circuit evaluation` of the logical operators
e.g.
For a logical `AND` operation; if first operand is `false`; go doesn't evaluate second operand and returns the result as `false`

For a logical `OR` operation; if first operand is `true`; go doesn't evaluate second operand and returns the result as `true`

> **Notes:**  
* Only the values of same type could be compared with each other
* Although, we can compare values of the `compatible types` with each other through the use of `type-casting`
e.g.
```golang
package main

import "fmt"

func main(){
    i, j := 2, 3.14
    if i < j {      //  INVALID comparison as `i` is an `int` while `j` is `float64`
        fmt.Println(i)   
    }

    if j > float64(i) { // VALID as `i` is type casted to `float64`
        fmt.Println(i)
    }
} 
```
## if; if-else; if-else if-else
* The paranthesis in the if statement are optional
* The _condition expression_ in if statement must be a boolean expression
e.g.
```golang
    if 1  {...} // Invalid
    if 1 > 2 {...} // Valid
    if true {...} // valid
```
* In `if-else` clause; `else` clause is _optional_ and can occur only once
* In `if-else if-else` clause; `else if` as well as `else` clause is _optional_ and `else-if` clause can occur any number of times but `else` clause can occur only once 
e.g. 
```golang
    if true {

    } else if {

    } else if {

    } else if {

    } else
```
## short if
* example syntax
```golang
    if n, err := strconv.Atoi("32"); err == nil {
        fmt.Println("String conversion successful. We got:%d", n)
    }
```
* The variables declared in _short if_ statement are visible only inside the _if_ statement and its branches
e.g.
```golang
    if n, err := strconv.Atoi("32"); err != nil {
        // `n` and `err` visible here
        fmt.Println("Error:%v", err)
    } else {
        // `n` and `err` visible here
        fmt.Println("We got:%d", n)
    }
    fmt.Println("The conversion gave us: %d", n) // Compilation error as `n` is not visible here
```

## switch statement
* example syntax
```golang
    fruit := "mango"
    switch fruit {  // switch condition; switch block start
        case "grapes": // case condition; case `grapes` block start
            fmt.Println("sour, tasty")
            //case `grapes` block end
        case "mango": // case condition; case `mango` block start
            fmt.Println("sweet, tasty")
            // case `mango` block end
        default: // default statement i.e. executed when there's no match; 'default' block start
            fmt.Println("tasty")
            // default block end    
    } // switch block end
```
* switch's condition is compared with each case condition and the _case <condition> block_ for the `first match` only is executed 
* switch's condition type determines the type of the _case conditions_
* _case clause_ creates an exclusive code block for itself

* We can use multiple conditions in the same case clause
* Multiple case conditions are treated as `logical or` expression
e.g.
```golang
    fruit := "mango"
    switch fruit {  // switch condition; switch block start
        case "grapes", "lemons": // case condition; case `grapes` OR `lemons` block start
            fmt.Println("sour, tasty")
            //case `grapes` OR `lemons` block end
        case "mango", "banana": // case condition; case `mango` OR `banana` block start
            fmt.Println("sweet, tasty")
            // case `mango` OR `banana` block end
        default: // default statement i.e. executed when there's no match; 'default' block start
            fmt.Println("tasty")
            // default block end    
    } // switch block end
```
* Default condition of the switch block is always _true_
e.g. `switch {...}` <=> `switch true {...}`

* We can use boolean expressions in case clause; provided; switch condition's type is boolean
e.g.
```golang
    switch true {
        case 2 > 1: 
            fmt.Println("2 is greter than 1")
        default:
            fmt.Println("Unknown")
    }
```
* `fallthrough` statement executes next case block without checking it's case condition
```golang
    i := 1
    switch true {
        case  i > 0:
            fmt.Println("positive")
            fallthrough
        default:
            fmt.Println("number") 
    } 
```
The above switch block will output: `positive number`
* `fallthrough` must always be the last statement in the case block
* we cannot `fallthrough` final case in switch

## short switch
* example syntax
```golang
    
    switch i := 1; true { // this is a short switch
        case  i > 0:
            fmt.Println("positive")
        default:
            fmt.Println("number") 
    }
```
> **Notes:**
* Go evaluates switch case conditions from _top to bottom_
* Only the first matching case block within switch block will be executed
* Go adds break statements to case blocks internally; hence no need to add break statements in switch block
* default block will always be executed last
* When number of conditions in _if_ statement become so many that it becomes unreadable; we should replace _if_ with the _switch_

****  
## Potential interview questions: 
* **What will be the output of following program?**
```golang
package main

import "fmt"

const msg string

func main() {
    fmt.Println(2 == false)
}
```
   1. `true`
   2. Run-time error
   3. Compilation error => Correct  
  
> 3. we can only compare compatible types

* **What will be the output of following program?**
```golang
package main

import "fmt"

const msg string

func main() {
    fmt.Println(1.2 > 1.2, 1.2 <= 1.2)
}
```
   1. `true false`
   2. `false true` => Correct
   3. Compilation error

* **What will be the output of following program?**
```golang
package main

import "fmt"

const msg string

func main() {
    var (
        up  = true
        down = !up
    )

    fmt.Println(!up && !down, !up || !down)
}
```
   1. `true true`
   2. `false true` => Correct
   3. Compilation error

> 2. `!up` is `false` => `down` is `false` => `!down` is `true`. Hence, `false && true <=> false`; `false || true <=> true`

* **What will be the output of following program?**
```golang
package main

import "fmt"

const msg string

func main() {
    x := "a" > "b"
    y := "b" <= "c"
    fmt.Println(x || y)
}
```
   1. `true` => Correct
   2. `false` 
   3. Compilation error

> 1. In case of strings; ordering means alphabetical ordering. Hence, `x` is `false` and `y` is `true` => `x || y <=> false || true <=> true`

* **What will be the output of following program?**
```golang
package main

import "fmt"

const msg string

func main() {
    _ = isUp() && isDown()
    _ = isDown() || isUp()
}

func isDown() bool {
    fmt.Print("up ")
    return true
}

func isUp() bool {
    fmt.Print("down ")
    return false
}

```
   1. `down up up down` 
   2. `down up` => Correct 
   3. Compilation error

> 2. remember the short-circuit evaluation of logical expressions 

***

* **What will be the output of following program?**
```golang
package main

import "fmt"

const msg string

func main() {
    taste := "sweet"

    if "sweet" {
        fmt.Println("love it!!")
    }
}
```
   1. `love it` 
   2. nothing 
   3. Compilation error => Correct

> 3. The `if` condition always must be a boolean expression

* **What will be the output of following program?**
```golang
package main

import (
        "fmt"
        "strconv"
)

func main() {

        if i, err := strconv.Atoi("10"); err != nil {
                fmt.Printf("error: %s (n: %d)", err, i)
                return
        }

        fmt.Println(i)
}
```
   1. `10` 
   2. `0` 
   3. Compilation error: undefined i => Correct

> 3. The variables declared in _short if_ statement are visible only inside the _if_ statement and its branches 

* **What will be the output of following program?**
```golang
package main

import (
        "fmt"
)

func main() {

    num := 1.2

    switch n := num; {
    case n < 1:
        fallthrough
    case n >= 1 && n < 2:
        fallthrough
    case n >= 4 && n < 5:
        fmt.Println("whatever")
    case n >= 5 && n < 6:
        fallthrough
    case n >= 6:
        fmt.Println("booom")
    }
}
```
   1. `whatever` => Correct
   2. `boom` 
   3. Compilation error 

> 1. `fallthrough` statement executes next case block without checking it's case condition 

* **What will be the output of following program?**
```golang
package main

import (
        "fmt"
)

func main() {

    num := 1.2

    switch n := num; {
    case n < 1:
        fallthrough
    case n >= 1 && n < 2:
        fallthrough
    case n >= 4 && n < 5:
        fmt.Println("whatever")
    case n >= 5 && n < 6:
        fallthrough
    case n >= 6:
        fmt.Println("booom")
        fallthrough
    }
}
```
   1. `whatever` 
   2. `boom` 
   3. Compilation error => Correct 

> 3. we cannot `fallthrough` final case in switch

* **Which of the switch case block will be executed in the follwoing program?**
```golang
package main

import (
        "fmt"
)

func main() {

    num := 2

    switch n := num; {
    default:
        fmt.Println("n is a number")    
    case n < 1:
        fmt.Println("n is a small number")
    case n > 100:
        fmt.Println("n is a big number")
    }
}
```
   1. `case n < 1` 
   2. `default` => Correct
   3. none of the above
> 2. default statement is executed when there's no match

## Test your knowledge
* **How can you simplify the following if condition?**
```golang
package main

import "fmt"

func main() {
    up := true

    if up == true {...}
}
```
   1. `if up != false {...}` 
   2. `if !up == false {...}` 
   3. `if up {...}` => Correct

* **What's the problem with the following code?**
```golang
package main

import "fmt"

func main() {
    up := true
    on := up

    if up {
        fmt.Println("on!!!")
    } else if !up {
        fmt.Println("off!!")
    } else if on {
        fmt.Println("switch me on!!")
    }
}
```
   1. There's no else branch 
   2. You can't use more than one `else-if` branches
   3. The last `else-if` branch will never be executed => Correct

* **Which one of these types is returned by the comparison operators?**
   1. `bool` => Correct
   2. `int`
   3. `string`

* **Which one below is not one of the ordering operators of Go?**
   1. `<=` 
   2. `>=`
   3. `==` => Correct

* **Which one below is not one of the logical operators of Go?**
   1. `||` 
   2. `!=` => Correct
   3. `&&` 

* **Which expression below equals to the sentence below?**
```
weigth is equal or below 50 and gender is female
```
   1. `weight <= 50 && gender == female` => Correct
   2. `weight < 50 && gender != male`
   3. `weight == 50 || weight > 50 || gender == female`

* **What will be the output of following program?**
```golang
package main

import (
        "fmt"
        "strconv"
)

func main() {
        var i int
        if i, err := strconv.Atoi("10"); err != nil {
                fmt.Printf("error: %s (n: %d)", err, i)
                return
        }

        fmt.Println(i)
}
```
   1. `10` 
   2. `0` => Correct
   3. Compilation error: undefined i 

* **What will be the output of following program?**
```golang
package main

import "fmt"

const msg string

func main() {
    taste := "sweet"

    if taste := "sweet"; taste {
        fmt.Println("love it!!")
    }
}
```
   1. `love it` 
   2. nothing 
   3. Compilation error => Correct

* **What will be the output of the following program?** 
```golang
package main

import (
        "fmt"
)

func main() {

    num := 2

    switch n := num; {
    default:
        fmt.Println("n is a number")    
    case n < 1:
        fallthrough
        fmt.Println("n is a small number")
    case n > 100:
        fmt.Println("n is a big number")
    }
}
```
   1. `n is a small number` 
   2. `n is a number` 
   3. compilation error => Correct
> 3. `fallthrough` statement must be the last statement in the block

* **What will be the output of the following program?**
```golang
   package main

import (
        "fmt"
)

func main() {

    switch 3 {
    case 2:
        fmt.Println("it's not a match ")    
    case 3:
        fmt.Println("it's a match")
    case 2:
        fmt.Println("it's not a match ")
    }
} 
```
   1. `it's a match` 
   2. `it's not a match` 
   3. compilation error => Correct
> 3. duplicate case conditions are not allowed in switch statement

* **What type of values you can use as the case conditions for the following switch statement?**
```golang
    on := false
    switch !on {
    case condition:
        // ...
    }
```
   1. `int` 
   2. `bool` => Correct
   3. `string`
***