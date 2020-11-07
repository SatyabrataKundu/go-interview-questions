# Strings
* Strings declaration syntax:
```golang
package main

import "fmt"

func main(){
    s1 := "Hello!!"             => This(s1) is called a `string literal`
    s2 := `{                    => This(s2) is called a  `raw string literal`
        "message": "Hello!!"
    }`
    
    fmt.Println(s1,s2)
}
```
* Normally, `string literals` are used to declare _single line_ strings whereas `raw string literals` are used to declare _multiline strings_

* If you want to use `string literals` for declaring _multiline strings_; you need to make use of _escape sequences_ 
e.g. 
```golang
package main

import "fmt"

func main() {
        s := "{\n\"message\": \"Hello!!\"\n}"
        fmt.Println(s)
}
```
* There's no need to use _escape characters_ to declare _multiline strings_ with `raw string literals`
* In Go, all string literals are `utf-8` encoded

## strings, runes and []byte
* The `Unicode code points` are represented in go using _rune_ data type (i.e. an alias of _int32_ type)
* The `Unicode code points` is nothing but a _numerical representation of any unicode character_
e.g.  The `Unicode code point` for the english letter 'A' is number `65` 

* A _rune_ can represent any unicode character of size upto 4-bytes
e.g. 
A rune literal 'A' represents a unicode character of size 1-byte as its `Unicode code point` is number `65`
whereas
A rune literal 'ü' represents a unicode character of size 2-bytes as its `Unicode code point` is number `252`

* Thus, a _rune_ is a sequence of upto 4-bytes i.e. _slice of bytes_
* As a _rune_ represents a character and a string is a _sequence of characters_; a _string_ is a _sequence of runes_
* `string = sequence of runes`; `rune = sequence of bytes` => `string = sequence of bytes`

> **Notes**: 
> * In Go, String is not only a `sequence of bytes` but a `read-only sequence of bytes` i.e. in go, `strings are immutable` 
e.g. Internally, A string `hey` means `[]byte{104, 101, 121}` => In unicode; `'H'<=> 104`; `'e'<=> 101`; `'y'<=> 121` 
> * As a _rune literal_ is a typeless constant; it can be converted into a byte, a rune or any other numeric type
> * As _string is a read-only byte slice_; following statements are valid: `b := []byte("hey")`; `msg := string([]byte{104, 101, 121})`

## string concatenation operator (+)
* We can concatenate strings with `+` operator as:
```golang
    str := "Good" + " " + "bye!!"   => `str` becomes "Good bye!!"
    str1 := "Good" + " " + `bye!!`   => `str1` becomes "Good bye!!"
    str2 := `Good` + ` bye!!`   => `str2` becomes "Good bye!!"
```
## string conversions
* Package _strconv_ implements conversions to and from string representations of basic data types
    e.g.
    * The most common numeric conversions are Atoi (string to int) and Itoa (int to string)
    ```golang
        i, err := strconv.Atoi("-42")
        s := strconv.Itoa(-42)
    ```
    * ParseBool, ParseFloat, ParseInt, and ParseUint convert strings to values
    ```golang
        b, err := strconv.ParseBool("true")
        f, err := strconv.ParseFloat("3.1415", 64)
        i, err := strconv.ParseInt("-42", 10, 64)
        u, err := strconv.ParseUint("42", 10, 64)
    ```

## string length
* The in-built `len` function returns `number of bytes in a given string`
e.g. `lb := len("len("útil")")` => Here, `lb` will be evaluated to `5` as size of the character `ú` is 2-bytes

* To count the number of characters in a string; the function `utf8.RuneCountInString` should be used
e.g. `ln := utf8.RuneCountInString("útil")` => Here, `ln` will be evaluated to `4`

***
## Potential interview questions: 
* **What will be the output of following program?**
```golang
package main

import "fmt"

func main() {
    str := "\"Hello\"" + ` \"golang!!\"`
    fmt.Println(str)
}
```
   1. `"Hello golang!!"`
   2. \"Hello\" \"golang!!\"
   3. `"Hello" \"golang!!\"` => Correct  
  
> 3. Go interprets the escape sequence inside _string literals_ whereas it doesn't interpret the escape sequence inside _raw string literals_

* **What will be the output of following program?**
> Hint: Size of the unicode character `ş` is 2-bytes
```golang
package main

import "fmt"

func main() {
    fmt.Println(len("gitmişmişsin"))
}
```
   1. 12
   2. 14  => Correct
   3. compilation error  
  
> 2. The in-built `len` function returns `number of bytes in a given string`

* **How to find number of characters in the word `gitmişmişsin`?**
   1. `utf8.RuneCountInString("gitmişmişsin")` => Correct
   2. `len("gitmişmişsin")`  
   3. `len(gitmişmişsin)`  
  
> 1. To count the number of characters in a string; the function `utf8.RuneCountInString` can be used

## Test your knowledge
* **What will be the output of following program?**
```golang
package main

import "fmt"

func main() {
    n := len("Hello") + len(`\"golang!!\"`)
    fmt.Println(n)
}
```
   1. 13
   2. 17  => Correct
   3. 11  
  
> 2. The in-built `len` function returns `number of bytes in a given string`.Go interprets the escape sequence inside _string literals_ whereas it doesn't interpret the escape sequence inside _raw string literals_

* **What will be the output of following program?**
> Hint: Size of the unicode character `ş` is 2-bytes
```golang
package main

import "fmt"

func main() {
    n := utf8.RuneCountInString("gitmişmişsin")
    fmt.Println(n)
}
```
   1. 13
   2. 17  
   3. compilation error  => Correct
  
> 3. The import of package `unicode/utf8` is missing

* **Which implements conversions to and from string representations of basic data types?**
   1. `strings`
   2. `strconv`  => Correct
   3. `unicode/utf8`

* **Which one of the follwoing is true?**
   1. In go, _string literals_ are `utf-32` encoded
   2. In go, _string literals_ are `rune` encoded  
   3. In go, _string literals_ are `utf-8` encoded => Correct

* **Which one of the follwoing is true?**
   1. In go, _rune_ can be converted into a byte, a rune or any other numeric type
   2. In go, _rune literal_ can be converted into a byte, a rune or any other numeric type => Correct
   3. In go, _rune literal_ can be converted into an `int32` type only 
> 2. As a _rune literal_ is a typeless constant; it can be converted into a byte, a rune or any other numeric type

* **What will be the output of following program?**
> Hint: Size of the unicode character `ş` is 2-bytes
```golang
package main

import (
    "fmt"
    "unicode/utf8"
)

func main() {
    n := utf8.RuneCountInString("gitmişmişsin")
    fmt.Println(n)
}
```
   1. 13
   2. 12  => Correct
   3. compilation error  
  
> 2. To count the number of characters in a string; the function `utf8.RuneCountInString` can be used

* **What will be the output of following program?**
> Hint: Size of the unicode character `ş` is 2-bytes
```golang
package main

import (
    "fmt"
    "unicode/utf8"
)

func main() {
    word := "gitmişmişsin"
    b := []byte(word)
    fmt.Println(utf8.RuneCountInString(b))
}
```
   1. 13
   2. 12  
   3. compilation error => Correct 
  
> 3. The function `utf8.RuneCountInString` gives the rune count(i.e. character count) in the _string_ and not the rune count in _byte slice_

* **What will be the output of following program?**
> Hints: 
>    * Size of the unicode character `ş` is 2-bytes
>    * The function `utf8.RuneCount` gives rune count in a _byte slice_
```golang
package main

import (
    "fmt"
    "unicode/utf8"
)

func main() {
    word := "gitmişmişsin"
    b := []byte(word)
    fmt.Println(utf8.RuneCount(b), len(word), len(string(word[1])))
}
```
   1. `12 14 1` => Correct
   2. `17 14 1`  
   3. compilation error  
  
> 1. As _string is a read-only byte slice_; `string` to `[]byte` conversion is valid and vice versa. Slice index starts at `zero`.

* **What will be the output of following program?**
> Hints: 
>    * Size of the unicode character `ş` is 2-bytes
>    * The function `utf8.RuneCount` gives rune count in a _byte slice_
```golang
package main

import (
    "fmt"
    "unicode/utf8"
)

func main() {
    word := "gitmişmişsin"
    word[1] = "x"
    fmt.Println(word)
}
```
   1. `xitmişmişsin` 
   2. `gxtmişmişsin`  
   3. compilation error => Correct  
> 3. In Go, String is not only a `sequence of bytes` but a `read-only sequence of bytes` i.e. in go, `strings are immutable`

* **What will be the output of following program?**
> Hints: 
>    * Size of the unicode character `ş` is 2-bytes
>    * _for range_ loops over the runes of a string
>    * Unicode code poits: `'a' = 97` `'ş' = 351` `'k' = 107`
```golang
package main

import (
    "fmt"
)

func main() {
    word := "aşk"
    for w := range word {
        fmt.Printf("%v\t", w)
    }
}
```
   1. `a ş k` 
   2. `0 1 3` => Correct 
   3. `97 351 107`  
  
> 1. String is a `ut-8 encoded`, read-only _byte slice_. Slice index starts at `zero`. _runes_ may start and end in different indexes

* **What will be the output of following program?**
> Hints: 
>    * Size of the unicode character `ş` is 2-bytes
>    * _for range_ loops over the runes of a string
>    * Unicode code poits: `'a' = 97` `'ş' = 351` `'k' = 107`
```golang
package main

import (
    "fmt"
)

func main() {
    word := "aşk"
    for _, w := range word {
        fmt.Printf("%v\t", w)
    }
}
```
   1. `a ş k` 
   2. `0 1 3`  
   3. `97 351 107` => Correct 
  
> 1. String is a read-only _byte slice_. Slice index starts at `zero`.

* **Which one below is true?**
    1. _for range_ loops over the bytes of a string 
    2. _for range_ loops over the runes of a string  => Correct
    3. Both 1 and 2

* **For go strings, which one below is true?**
    1. runes always start and end in the same indexes
    2. bytes may start and end in different indexes  
    3. runes may start and end in different indexes => Correct

* **Which byte slice below equals to the string `"kaskas"`? Hint: Unicode code poits: `'a' = 97` `'s' = 115` `'k' = 107`**  
    1. []byte{107, 97, 115, 107, 97, 115 } => Correct
    2. []byte{107, 97, 115, 107, 97 }  
    3. []byte{107, 97, 115, 107, 97, 107 }

***