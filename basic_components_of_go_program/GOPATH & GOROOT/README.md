# GOPATH & GOROOT

## key concepts:
### **GOPATH:**
* GOPATH is an environmental variable
* The value of the GOPATH defines the location of your `go workspace` or your `go source code`
* By default, the `go workspace` is a directory named `go` and is located under user's home directory:
    * For linux and MacOS, it's `~/go`
    * For windows, it's `%USERPROFILE%/go`
* GOPATH is a **root** of your `go workspace`.

> **Note**: Although, you can set the GOPATH manually, it's not recommended

* Typical structure of a `go workspace`:  
It contains following folders -
    * **src/**:
        * This is where your source code files are located (i.e. *.go files)
    * **pkg/**:
        * This where the compiled package files are located (i.e. *.a files)
        * Go uses these files to make compilation and linking (i.e. the build process) faster
    * **bin/**
        * This is where compiled and executable programs built by go are located
        * When we run `go install` command inside program directory (i.e. a directory of the `main` package); go will put the executable under this folder

### **GOROOT**:
* GOROOT is an environmental variable
* The value of GOROOT defines the location of your `go SDK` (e.g. /usr/local/go)
* You do not need to change this variable, unless you plan to use different `go verisons`

***  
## Potential interview questions: 
* **What is GOPATH?**
    1. It's a path of the GO folder
    2. An environment variable used by go determine location of the `go workspace` => CORRECT
    3. It's the root of GO SDK

* **How can I print value of the GOPATH?**
    1. Using `ls` command 
    2. Using `go environment` command
    3. Using `go env GOPATH` command => Correct

* **How can I print value of the GOROOT?**
    1. Using `ls` command 
    2. Using `go environment` command
    3. Using `go env GOROOT` command => Correct
***
## Test your knowledge
* **Where should I save my go source code?** 
    1. Under `$GOPATH`
    2. Under my home directory
    3. Under `$GOPATH/src` => Correct

* **Is it mandatory to set a GOPATH?**
    1. Yes.
    2. No: By default, it's under `root` directory of my computer
    3. No: By default, it's located under user's home directory => Correct

* **Where are the executable go program files located?**
    1. Under `$GOPATH/` directory
    2. Under `~/go/bin` direcory
    3. Under `$GOPATH/bin` directory => Correct

* **Where are the compiled go package files loacted?**
    1. Under `$GOPATH/` directory
    2. Under `~/go/pkg` direcory
    3. Under `$GOPATH/pkg` directory => Correct

* **How can I print the current go version?**
    1. Using `ls` command 
    2. Using `go version` command => Correct
    3. Using `go env version` command
***