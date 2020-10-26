# Create, build and run a go program
## Create a go program: 
**Typical Go program components**
```golang **main.go**
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
