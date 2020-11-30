# Loop statements in Go
* _for_ is the only loop statement in go
e.g. 
```golang
package main

import "fmt"

func main(){
    for i := 0; i < 4; i++ {
            fmt.Println(i)
        }
}    
```
* In a _for_ statement; other than the keyword _for_ and the _curly braces_; all other parts are optional
e.g. 
```golang
package main

func main(){
    for {    }
} 
```
* We can exit out of the for loop using _break_ statement
e.g.
```golang
package main

func main(){
    var i, sum int

    for {
        if i >= 5 {
            break
        }
        sum += i
    }
} 
```
* We can exit out of the _specific_ for loop using _labeled break_ statement
e.g.
```golang
package main

func main(){
outer:
    for i:=0; i< 10; i++ {
        for j:= 0; j < 10; j++ {
                if j == 5 {
                    break // this will only break inner for loop
                }
                if i == 4 {
                    break outer // this will break from outer for loop
                }
            }
        }       
    }
} 
```

* We can skip current iteration of the for loop using _continue_ statement
e.g.
```golang
package main

func main(){
    var i, sum int
    for {
        if i == 5 {
            continue
        }
        sum += i
    }
}  
```
* We can skip current iteration of the _specific_ for loop using _labeled continue_ statement
e.g.
```golang
package main

func main(){
outer:
    for i:=0; i< 10; i++ {
        for j:= 0; j < 10; j++ {
                if j == 5 {
                    continue // this will only continue to the next iteration of the inner for loop
                }
                if i == 3 {
                    continue outer // this will continue to the next iteration of the outer for loop
                }
            }
        }       
    }
} 
```
> **Note**: We can move execution of the program to a specific location using _goto_ statement; provided the _goto_ statement doesn't jump over the declarations of the variable(s) in the labeled block
e.g.
```golang
package main

import "fmt"

func main(){
        var i int
        fmt.Println("I am going to loop using goto")
        loop:
        fmt.Println("i:",i)
        i++
        if i < 5 {
                goto loop // takes control to `loop:` statement
        }
}

```

## The _for-range_ clause
* The _range_ keyword is used in the _for_ loop to iterate over the _items_ of an array, slice, channel or map
* With array and slices; it returns the index of the item as an integer.
* With maps; it returns the `key` of the next `key-value` pair
* _range_ always returns one or two values depending upon number of variables used on the LHS of the expression. Out of those two values; first value is _index_ and second value is the _item_ and it's use in the expression is optional
e.g.
```golang
package main

import "fmt"

func main(){
    for i, v := range os.Args { // os.Args is an array of the command line arguments passed to the go program
        fmt.Printf("The argument %d is: %s", i, v)
    }
}    
```
* Following table indicates meaning of values returned by _range_ expression

|Range expression       |1st value      | 2nd value(optional)
|---                    |---            |---                
|Array or slice a[n]    | index i int   | a[i]
|String s string type   | index i int	| rune int
|map m map[K]V          | key k K       | value m[k] V
|channel c chan E       | element e E   | none

***
## Potential interview questions: 
* **What will be the output of following program?**
```golang
package main

import "fmt"

func main() {
    for i := 3; i > 0; {
        i--
        fmt.Println(i)
    }
}
```
   1. `2 1 0` => Correct
   2. `1 2 3`
   3. `0 1 2` 
  
* **What will be the output of following program?**
```golang
package main

import "fmt"

func main() {
    for i := 2; i <= 9; i++ {
        if i % 3 != 0 {
            continue
        }

        fmt.Println(i)
    }
```
   1. `3 6 9` => Correct
   2. `9 6 3`
   3. `2 3 6 9`

* **What will be the output of following program if you run it using following command?**
```golang
    go run main.go go is great
```
```golang
package main

import "fmt"

func main() {
    var i int

    for range os.Args {
        i++
    }

    fmt.Println(i)
```
   1. `2` 
   2. `4` => Correct
   3. `go is great`

* **Will this loop ever terminate?**
```golang
package main

func main() {
	flag := "A"

main:
	for {
		switch flag {
		case "A":
			flag = "B"
			break
		case "B":
			break main
		}
	}
}
```
   1. `No, this loop will loop to infinity` 
   2. `Yes, the second break will terminate the loop` => Correct
   3. `Yes, the first break will terminate the loop`

***

* **What will be the output of the following program?**
```golang
package main

import "fmt"

func main(){
        goto loop
        var i int
        fmt.Println("I am going to loop using goto")
        loop:
        fmt.Println(i)
        i++
        if i < 3 {
                goto loop // takes control to `loop:` statement
        }
}
```
   1. `0 1 2` 
   2. `1 2 3` 
   3. `syntax error: goto loop jumps over declaration of i` => Correct
> 3. The _goto_ statement should not jump over any variable(s) declaration in _<label>_ block

## Test your knowledge
* **What will be the output of following program?**
```golang
package main

import "fmt"

func main(){
        var i int
        fmt.Println("I am going to loop using goto")
        loop:
        fmt.Println(i)
        i++
        if i < 3 {
                goto loop // takes control to `loop:` statement
        }
}
```
   1. `0 1 2` => Correct
   2. `1 2 3` 
   3. `syntax error` 

* **Will this loop terminate after the `break`?**
```golang
package main

func main() {
main:
	for {
		switch "A" {
        case "A":
            break // <- here!
        case "B":
            continue main
        }
	}
}
```
   1. `Yes, the break will terminate the loop` 
   2. `No, the break will only terminate the switch but the loop will continue` => Correct
   3. `Yes, the break will terminate the switch`

* **What is wrong with the following program?**
```golang
    package main

func main() {
	for {
	switcher:
		switch {
		case true:
			switch {
			case false:
				continue switcher
			}
		}
	}
}
```
   1. `continue statement cannot be used within a switch statement` 
   2. `It will loop to infinity` 
   3. `continue statement can only continue a loop ` => Correct

* **Which scope a label belongs to?**
   1. `To the body of the function that it is in` => Correct 
   2. `To the scope of the statement that it is in` 
   3. `To the package scope that it is in` 

* **How can you simplify following code block?**
```golang
    for ; true ; {...}
```
   1. `for true; {...}` 
   2. `for {...}` => Correct
   3. `for ; true {...} ` 

* **Which one of these is a valid loop statement in Go?**
   1. `while {...}` 
   2. `for {...}` => Correct
   3. `repeat {...} until `