# lesiw.io/dataer

An experimental package to add metadata to types.

Specify a type with `-t T` and the data to extend it with as `-d D`. The type
will be made to fulfill the interface:

``` go
type Dataer interface {
    Data() D // Return value is the type chosen to extend T.
}
```

## Example: Struct
``` go
//go:generate go run lesiw.io/dataer@latest -t superstring -d stringdata

package main

import "fmt"
    
type superstring string

type stringdata struct {
    String string
    Int int
}

func main() {
    x := superstring("a string")
    y := superstring("a string")
    x.Data().String = "x"
    x.Data().Int = 42
    y.Data().String = "y"
    fmt.Println(x)
    fmt.Println("x == y?", x == y)
    fmt.Println("x str:", x.Data().String)
    fmt.Println("y str:", y.Data().String)
    fmt.Println("x int:", x.Data().Int)
    fmt.Println("y int:", y.Data().Int)
}
```

## Example: Basic type
``` go
//go:generate go run lesiw.io/dataer@latest -t superstring -d int

package main

import "fmt"

type superstring string

func main() {
	x := superstring("a string")
	y := superstring("a string")
	*x.Data() = 42
	*y.Data() = -1
	fmt.Println(x)
	fmt.Println("x == y?", x == y)
	fmt.Println("x int:", *x.Data())
	fmt.Println("y int:", *y.Data())
}
```
