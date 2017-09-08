# Go coding conventions

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119](https://www.ietf.org/rfc/rfc2119.txt).

The examples show what MUST, SHOULD, or MAY be done.

The sections and conventions are ordered alphabetically.

## Design

### SHOULD NOT export global variables from libraries

```go
func New() *Foo { ...
```

## Documentation

### SHOULD name benchmarks and tests like examples

```go
func BenchmarkFoo_Bar_baz() { ...
```

```go
func TestFoo_Bar_baz() { ...
```

## General

### MUST comply with go build ./...
### MUST comply with go test ./...
### MUST comply with go vet ./...
### MUST comply with gofmt -s
### MUST comply with goimports
### MUST comply with golint
### SHOULD comply with https://golang.org/blog
### SHOULD comply with https://golang.org/doc/effective_go.html
### SHOULD comply with https://golang.org/wiki
### SHOULD follow the example of the Go standard libraries
### SHOULD follow the example of the Go project

## Implementation

### MUST commit vendored packages

### MUST vendor external packages for main packages

### MUST vendor with dep

## Style

### SHOULD NOT begin or end blocks with a blank line

```go
var (
    foo Foo

    bar Bar
)
```

```go
{
    foo()

    bar()
}
```

### SHOULD NOT use the built-in functions `make` or `new` unless necessary

```go
make(chan Foo)
```

```go
make(chan Foo, bar)
```

```go
make(map[Foo]Bar, baz)
```

```go
new(int)
```

### SHOULD begin comments with a space and end general comments with a space

```go
// Started earlier
```

```go
/* Started earlier */
```

### SHOULD capitalize comments

```go
// Started earlier
```

### SHOULD end comments with multiple sentences with punctuation

```go
// Started earlier. Skip initialization.
```

### SHOULD group similar kinds of statements and declarations with blank lines

```go
const ...
const ...

var ...
var ...

w, x := ...
y, z := ...

func ...
func ...

type ...
type ...

x
x--
x++
x()
<-x
x <- y
x = y
defer x()
go x()

break
continue
fallthrough
goto
return
```

### SHOULD order file declarations like `go doc -u`

```go
const C ...

const c ...

var V ...

var v ...

func F() { ...

func f() { ...

type T ...

func FT(...) *T { ...

func fT(...) *T { ...

func (T) M { ...

func (T) m { ...

type t ...

func Ft(...) *t { ...

func ft(...) *t { ...

func (t) M { ...

func (t) m { ...
```

### SHOULD separate cases with blank lines

```go
select ... {
case ...:
    ...

case ...:
    ...

default:
    ...
}
```

```go
switch ... {
case ...:
    ...

case ...:
    ...

default:
    ...
}
```

### SHOULD separate multiple-line blocks with blank lines

```go
const ...
const ...

const (
    ...
)

const (
    ...
)

if ... {
    ...
}

if ... {
    ...
}

func ... { ... }
func ... { ... }

func ... {
    ...
}

func ... {
    ...
}
```

### SHOULD use long variable declarations instead of short where equivalent

```go
var a, err = ...

b, err := ...
```

## Testing

### SHOULD NOT use assertion libraries

```go
if actual = Foo(input); actual != expected { ...
```

### SHOULD call testing.T.Parallel

```go
func TestFoo(t *testing.T) {
    t.Parallel() ...
```

### SHOULD use the -race flag

```
$ go test -race
```
