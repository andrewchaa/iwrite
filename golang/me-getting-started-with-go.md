# Learning Go through a course in Coursera

Not the game of Go, but golang. 

Recently, my friend, Eduard, suggested learning Golang. Go is an interesting language with powerful low-level features like pointer but also with modern language support like garbage collection. 

I used brew to install Go, as I'm on mac. 

```bash
brew install golang
```

### Hello world

```go
package main

import "fmt"

func main() {
	fmt.Println("Hello world")
}
```

`import` bring in package. In go, everything is package. `fmt` is like Console in `c#` 

To run it, do `go run hello.go` 

### Module

A module is a collection of [Go packages](https://golang.org/ref/spec#Packages) stored in a file tree with a `go.mod` file at its root. The `go.mod` file defines the module’s _module path_, which is also the import path used for the root directory, and its _dependency requirements_, which are the other modules needed for a successful build. Each dependency requirement is written as a module path and a specific [semantic version](http://semver.org/).

```go
go mod init github.com/andrewchaa/gowebclient
```

### conditionals

```go
// if else
func NewName(fname string, lname string) *Name {
	name := new(Name)
	if len(fname) > 20 {
		name.fname = fname[:20]
	} else {
		name.fname = fname
	}

	if len(lname) > 20 {
		name.lname = lname[:20]
	} else {
		name.lname = lname
	}

	return name
}

```

### handling strings

```go
package main

import (
	"bufio"
	"fmt"
	"os"
	"strings"
)

func main() {

	fmt.Println("Enter your string input")
	scanner := bufio.NewScanner(os.Stdin)
	scanner.Scan()
	input := scanner.Text()

	var inputLowercase = strings.ToLower(input)
	var userInputBody = inputLowercase[1:len(inputLowercase)-1]

	if strings.HasPrefix(inputLowercase, "i") &&
		strings.HasSuffix(inputLowercase, "n") &&
		strings.Contains(userInputBody, "a") {

		fmt.Println("Found!")
	} else {
		fmt.Println("Not Found!")
	}

}

```

bufio is to receive user input that includes space. string is a collection of character. \[0:10\] syntax was really powerful.

### iterations

```go
// for range
var names []Name
for fileScanner.Scan() {
	nameArr := strings.Split(fileScanner.Text(), " ")
	name := NewName(nameArr[0], nameArr[1])
	names = append(names, *name)
}

for _, name := range names {
	fmt.Printf("%s %s\n", name.fname, name.lname)
}

```

### json

```go
	scanner := bufio.NewScanner(os.Stdin)
	user := make(map[string]string)

	fmt.Println("Enter your name")
	scanner.Scan()
	user["name"] = scanner.Text()

	fmt.Println("Enter your address")
	scanner.Scan()
	user["address"] = scanner.Text()

	jsonString, _ := json.Marshal(user)
	fmt.Println(string(jsonString))

```

### map

```go
scanner := bufio.NewScanner(os.Stdin)
user := make(map[string]string)

fmt.Println("Enter your name")
scanner.Scan()
user["name"] = scanner.Text()

fmt.Println("Enter your address")
scanner.Scan()
user["address"] = scanner.Text()

```

### slice

a dynamically-sized flexible view into the elements of an array

```go
var names []Name
for fileScanner.Scan() {
	nameArr := strings.Split(fileScanner.Text(), " ")
	name := NewName(nameArr[0], nameArr[1])
	names = append(names, *name)
}

```

### string

```go
// cut up to the length
func NewName(fname string, lname string) *Name {
	name := new(Name)
	name.fname = fname[:20]
	name.lname = lname[:20]

	return name
}

// split
nameArr := strings.Split(fileScanner.Text(), " ")
name := NewName(nameArr[0], nameArr[1])

```

### struct

`struct` is a typed collection of fields, usefl for grouping data together to form records

```go
type person struct {
    name string
    age  int
}

s := person{name: "Sean", age: 50}
```

### truncate fractional digits to int value

By doing this assignment, I learned stdin, number conversion, and Println format.

```go
package main

import "fmt"

func main() {
	var input float64
	var number int

	fmt.Println("Enter your floating number")
	fmt.Scanln(&input)

	number = int(input)
	fmt.Printf("Your int value is %d\n", number)
}

```

Scanln accepts user input. Yet it can't handle space so you need to use bufio if the input has any space in it. 

### user input

simple string without space

```go
var firstname string
fmt.Println("your firstname: ")
fmt.Scanln(&firstname)
```

If you the input has space in the middle, use Scanner

```go
import (
	"bufio"
	"fmt"
	"os"
)

func main() {
	scanner := bufio.NewScanner(os.Stdin)

	fmt.Println("Enter your name")
	scanner.Scan()
	name := scanner.Text()
}
```

