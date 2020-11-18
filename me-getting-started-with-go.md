# Learning Go

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

### truncate fractional digits to int value

By doing this assignment, I learned stdin, number conversion, and Println format.

```go
package main

import "fmt"
import "strconv"

func main() {
	var floatingNumberString string

	fmt.Println("Enter your floating number")
	fmt.Scanln(&floatingNumberString)

	if floatingNumber, err := strconv.ParseFloat(floatingNumberString, 64); err == nil {
		intNumber := int64(floatingNumber)
		fmt.Printf("Your int value is %d\n", intNumber)
	}
}
```

I liked the concise yet powerful if statement that handles nil gracefully.





