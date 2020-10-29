# Go type system
## Built-in types (Pre-declared types)
* A built-in type (or predeclared type) can be used anywhere in the program without importing any library package

|Type name| value range|
|---|---|
|`bool`|`true` or `false`|
|`string`(i.e.`[]byte)`|Any string value of any size|
|`int`|same as `int32` or `int64`|
|`uint`|same as `uint32` or `uint64`|
|`int8`| `-128` to `127`|
|`int16`| `-32768` to `32767`|
|`int32`| `-2` to `+2` billions|
|`int64`| `-9` to `+9` quintillions|
|`uint8`| `0` to `255`|
|`uint16`| `0` to `65535`|
|`uint32`| `0` to `4` billions|
|`uint64`| `0` to `0` quintillions|
|`float32`| `8 digit` precision |
|`float64`| `16 digit` precision|
|complex64| `two float32s`|
|complex128| `two float64s`|

* **Overflows:**
    * When we try to store larger number than a size can accomodate; overflow happens  
        e.g. if we try to store `256` value into an `uin8` type variable; overflow happens
    * **Overflow in signed types:**
        `min value - 1` -> `max positive`
        `max value + 1` -> `min negative`  
        e.g. 
        ```golang
           var x int8 = -127
           x-- => 128

           var y int8 = 128
           y++ => -127 
        ```
    * **Overflow in unsigned types:**
        `min value - 1` -> `max positive`
        `max value + 1` -> `zero`  
        e.g. 
        ```golang
           var x uint8 = 0
           x-- => 255

           var y uint8 = 255
           y++ => 0 
        ```
## Aliased types
* Aliased types are `exactly the same` types but with `different names`
e.g. 
    * `uint8` = `byte` 
    * `int32` = `rune` 
* Following is the syntax to create a new aliased type
    `type tyep = alias`
    e.g. 
    ```
        // Deprecated: Use github.com/docker/cli/cli/streams.In instead
        type InStream = streams.In
    ```
    Existing code that was using `InStream` do not break and now use the new type `streams.In`

* Type aliasing used mostly in refactoring of the large code bases

## Defined types (Named types)
* A `new type` declared using an another `existing type`
e.g. 
`type Duration int64` => Here, `Duration` is a Defined type
`type newDuration Duration` => Here, `newDuration` is a Defined type

## Underlying types
* A `Defined type` gets its size and properties from `a type that has real structure`. Hence, such `type with a real strucure` becomes an `Underlying type` for the `Defined type`
e.g.
`type Duration int64` => Here, `Duration` is a Defined type
`type newDuration Duration` => Here, `newDuration` is a Defined type
Here, for both `Defined types`(i.e. `Duration` and `newDuration`); the `Underlying type` is `int64`
* A `Defined type` and its `source type` share the same `Underlying type`

* A `Defined type` and the corresponding `Underlying type` are `different` types

* A type can be converted to another type iff they share the same `Underlying type`
e.g. 
```golang
    var s int64 = 500
    var ms Duration

    ms = Duration(s)
    s = int64(ms)
``` 
* `Defined type` methods can only be attached to that `Defined type`
e.g.
```golang
    type Duration int64
    func (d Duartion) Hours() float64 {...} => correct
    
    func main(){
        var d Duration
        d.Hours() => valid
        var t int64
        t.Hours() => invalid
    }
```
***
## Potential interview questions: 
* **What will be the output of following program?**
```golang
package main

import "fmt"

func main() {
    var ch uint8 = 255
    fmt.Println(ch+3)
}
```
   1. 0
   2. 258
   3. 2 => Correct  
  
> 3. for unsigned types; `max value + 1` -> `zero`

* **What will be the output of following program?**
```golang
package main

import "fmt"

func main() {
    var ch int8 = -128
    fmt.Println(ch - 5)
}
```
   1. -133
   2. 123 => Correct
   3. 133
  
> 3. for signed types; `min value - 1` -> `max positive`

* **What is the underlying type of the `Century` type?**
```golang
package main

type (
    Duration int64
    Year Duration
    Decade Year
    Century Decade
)

func main() {
    ...
}
```
   1. Decade
   2. Duration 
   3. int64 => Correct
  
> 3. A `Defined type` gets its size and properties from `a type that has real structure`. Hence, such `type with a real strucure` becomes an `Underlying type` for the `Defined type`

***
## Test your knowledge
* **Which type need not be converted between each other?** 
   1. `byte` and `rune` 
   2. `rune` and `uint32`
   3. `byte` and `uint8` => Correct

* **How to fix the following code?**
```golang
package main

import "fmt"

type Distance int

var (
    v Distance = 50
    c = 100
)

func main(){
    fmt.Print(v + c)
}
```
   1. v + Distance(c) => Correct
   2. v + int(c)
   3. int(v+c)

* **How to define a new type using int32?**
   1. type Age int32 => Correct
   2. type int32 Age
   3. Age = type int32

* **How to create an Aliased type using float32?**
   1. type fraction float32
   2. type float32 = fraction => Correct
   3. fraction = type float32

* **Which property doesn't the `Decade` type get from its underlying type?**
```golang
    type Decade time.Duration
```
   1. size
   2. methods => Correct
   3. range of values

* **What is the size of the `int` data type?**
   1. 32-bits
   2. 64-bits
   3. 32-bits or 64-bits depending upon the underlying architecture

* **Which one of the following is NOT a built-in data type?**
   1. byte
   2. rune
   3. duration => Correct
   4. complex64

* **Which types you might want to define for the following program?**
```golang
package main

import "fmt"

func main() {
	celsius := 35.
	fahrenheit := (9*celsius + 160) / 5
	fmt.Printf("%g ºC is %g ºF\n", celsius, fahrenheit)
}
```
   1. Celsius and Fahrenheit using float64 => CORRECT
   2. Temperature using int64
   3. Celsius and Fahrenheit using int64

* **Why do we want to define new types?**
   1. To declare new methods
   2. For type-safety
   3. For readability and conveying meaning
   4. All of the options above CORRECT
***