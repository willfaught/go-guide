# Go coding conventions

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119](https://www.ietf.org/rfc/rfc2119.txt).

The examples show what MUST, SHOULD, or MAY be done.

The sections and conventions are ordered alphabetically.

## Documentation

### SHOULD name benchmarks and tests like examples

#### Examples

```go
func BenchmarkT_M_foo() { ...
```

```go
func TestT_M_foo() { ...
```

#### Reasons

- You can run all benchmarks and tests for a package P with `go test -run ^P`
- You can run all benchmarks and tests for a declaration D with `go test -run ^D`
- You can run all benchmarks and tests for a method T.M with `go test -run ^T_M`

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

#### Examples

```go
var (
    foo T

    bar T
)
```

```go
{
    foo()

    bar()
}
```

#### Reason

- Consistent style.

### SHOULD NOT use the built-in functions `make` or `new` unless necessary

#### Examples

```go
make(chan T)
```

```go
make(chan T, n)
```

```go
make(map[T]T, n)
```

```go
new(int)
```

#### Reasons

- 

### SHOULD begin comments with a space and end general comments with a space

#### Examples

```go
// Started earlier
```

```go
/* Started earlier */
```

#### Reasons

- 

### SHOULD capitalize comments

#### Examples

```go
// Started earlier
```

#### Reasons

- 

### SHOULD end comments with multiple sentences with punctuation

#### Examples

```go
// Started earlier. Skip initialization.
```

#### Reasons

- 

### SHOULD group similar kinds of statements and declarations with blank lines

#### Examples

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

#### Reasons

- 

### SHOULD order file declarations like `go doc -u`

#### Examples

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

#### Reasons

- 

### SHOULD separate cases with blank lines

#### Examples

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

#### Reasons

- 

### SHOULD separate multiple-line blocks with blank lines

#### Examples

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

#### Reasons

- 

### SHOULD use long variable declarations instead of short where equivalent

#### Examples

```go
var a, err = ...

b, err := ...
```

#### Reasons

- 

## Testing

### SHOULD NOT use assertion libraries

#### Examples

```go
if actual = Foo(input); actual != expected { ...
```

#### Reasons

- 

### SHOULD call testing.T.Parallel

#### Examples

```go
func TestFoo(t *testing.T) {
    t.Parallel() ...
```

#### Reasons

- 

### SHOULD use the -race flag

#### Examples

```
$ go test -race
```

#### Reasons

- 
