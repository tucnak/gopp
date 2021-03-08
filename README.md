# Go++

![](cover.jpg)

Go++ is a small production-ready experiment that questions the very belief system of
classic Go, we go against the grain and dare do things most wouldn't even think about!

You know what they say that Go is basically improved C? And how they used to say that
C++ was improved C? Well, I guess you could say that in a way, Go++ is improved Go.
Hopefully, we all can appreciate the chic that went into this.

### I. Alternative syntax for Go2 generics
```go
// Instead of (type T) syntax
type T, T1, T2 template

type Vector []T
func Map([]T1) []T2 { ... }

```
We know that certain go-gophers won't like the word `template`, but we frankly love it
and ther's nothing they can do it about.

### II. Shorthand lambda syntax
```go
notEOF := func (err error) : err != io.EOF
```

### III. Pipe operator for error handling
```go
err := pipeline notEOF()
    | resp, err := client.Do()
    | _, err := r.Read(buf)
    | result, err := parser.Parse(buf)
if err != nil {
    // handle err
}
```
The pipe `|` operator indicates that the statement on the right is part of a single
connected pipeline, a simple yet strikingly effective error handling strategy. How it
works: all returned error variables will be automatically checked against nil as well
as the "guard" function, in this case: `notEOF(error) bool`. (The guard is optional!)
If either of the errors isn't nil and the guard function returns true for it, the
pipeline will immediately stop the execution, bind the corresponding error to variable
on the left side of the guard and go to the first statement after the pipeline.

In case if you want to be able to tell which stage of the pipeline failed, there's a
second, optional integer parameter (hereby ignored) which will contain index of the
failed position, starting with 0.

### IV. Go vet, unused imports and variables as warnings

### V. Pattern matching in `switch`
```go
switch err {
case ErrStaticFoobar:
    // handling foobar

case ErrStaticOther:
    // handling some other static

case *TypeError:
    // type cast error handle

default:
    // nil
}
```

### VI. Shorthand slice and map syntax
```go
A := [1, 2, 3, 4, 5] // []int
b := [1, "foobar", 42.01] // []interface{}
M := {0: "hello", 1: "world"} // map[int]string
M := {0: "foobar", 1: 42.01} // map[int]interface{}
```
This doesn't seem like too necessary, but why not?

### VII. Range type and inclusion syntax
```go
var a range
a = 1..5

len(a) // 4
b := a... // b: [1, 2, 3, 4]
```

### VIII. Python-style string interpolation
```go
fmt.Printf("Hello, {}\n", "world") // "Hello, %v\n"
fmt.Printf("A float: {.2f}\n", 42.04) // "A float: %.2f\n"

nine, b := 9, "ball"
fmt.Printf("Hello, {nine} {b}\n") // "Hello, 9 ball"
```

This is one of the features that were lacking _forever_. We are told we need to check
our errors as values, but then when the reality kicks in you usually would have to
either fit all your errors into a set of statics, which will abandon context, or stick
with two separate switches or a `switch` + `if` kind of situation. I mean, it can run
arbitrary code in the `case` clause already, so what the deal?

### TBA...

![Gopher image](doc/gopher/fiveyears.jpg)
*Gopher image by [Renee French][rf], licensed under [Creative Commons 3.0 Attributions license][cc3-by].*

### Contributing

Go++ is the work of a few contributors. We appreciate your help!

To contribute, please read the contribution guidelines:
	https://golang.org/doc/contribute.html

[rf]: https://reneefrench.blogspot.com/
[cc3-by]: https://creativecommons.org/licenses/by/3.0/
