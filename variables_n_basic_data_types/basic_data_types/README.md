# Basic data types in go
## Numeric types
* **Integer types:**  
    * uint8, uint16, uint32, uint64
    * int8, int16, int32, int64

* **Floating Types:**
    * float32, float64
    * complex64 (Complex numbers with float32 real and imaginary parts)
    * complex128 (Complex numbers with float64 real and imaginary parts)

* **Other numeric Types:**
    * byte (same as uint8)
    * rune (same as int32)
    * uint (32 bits on 32-bit systems & 64 bits on 64-bit systems)
    * int (32 bits on 32-bit systems & 64 bits on 64-bit systems)
    * uintptr:  
        * This is an unsigned integer type which is large enough to hold any pointer address
        * It is just an integer representation of an address
        * Its size is platform dependent (32 bits on 32-bit systems & 64 bits on 64-bit systems)
        * It's not recommended to actively use this data type unless you need to perform unsafe memory accesses

## Boolean Types:
* true
* false

## String Types:
* A string type represents the set of string values
* Its value is a sequence of bytes
* Strings are immutable types

### Type Summary:
|Type name  | Zero value| example literals  |
|---        |---        |---                |
|int        |0          |-3, 0, 34          |
|float64    |0          |-.4, 0., 1.        |
|bool       |false      |true, false        |
|string     |""         |"Hi there!!"       |

> **Notes:** 
> * A zero value is value that an uninitialized variable gets by default
> * Zero value of all numeric data types is zero
***
## Potential interview questions: 
* **What will be the output of following program?**
```golang
package main

import "fmt"

func main() {
    var x float
    fmt.Println(x) 
}

```
  1. garbage value
  2. compilation error => Correct
  3. `0`
>2. There's no such type as _float_ in go. There's _float32_ and _float64_

* **What will be the output of following program?**
```golang
package main

import "fmt"

func main() {
    var x float64
    fmt.Println(x) 
}

```
  1. garbage value
  2. compilation error
  3. `0` => Correct
>3. All numeric types in go have zero value of zero

***
## Test your knowledge
* **What will be the output of following program?**
```golang
package main

import "fmt"
var str string
func main() {
    fmt.Println(str+"Hello golang!!") 
}

```
  1. garbage value
  2. `Hello golang!!` => Correct
  3. no output 

* **Which one of below is float literal?**
    1. `2,32`
    2. `,32`
    3. `.28` => Correct

* **Which one of below is a bool constant?**
    1. `-32`
    2. `false` => Correct
    3. `"false"`

* **What is the size of a _rune_ type?**
    1. 32 bits on 32-bit systems & 64 bits on 64-bit systems
    2. same as int32 => Correct
    3. same as uint32

* **What is the size of _int_ type?**
    1. 32 bits on 32-bit systems & 64 bits on 64-bit systems => Correct
    2. same as int64
    3. same as uint32

***