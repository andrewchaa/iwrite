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

## Organising Go code

Go programs are organised into packages. 

* Package: a collection of source files in the same directory
* Module: a collection of related Go packages. 
* Repository: contains one or more modules

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



