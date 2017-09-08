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

- You can run all tests for a package P with `go test -run ^TestP`
- You can run all tests for a declaration D with `go test -run ^TestD`
- You can run all tests for a method T.M with `go test -run ^TestT_M`

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

Consistent style.

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

#### Reason

Consistent style.

### SHOULD begin comments with a space and end general comments with a space

#### Examples

```go
// Started earlier
```

```go
/* Started earlier */
```

#### Reason

Consistent style.

### SHOULD capitalize comments

#### Example

```go
// Started earlier
```

#### Reason

- Consistent style.

### SHOULD end comments with multiple sentences with punctuation

#### Example

```go
// Started earlier. Skip initialization.
```

#### Reason

Consistent style.

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

- Consistent style
- Skimmable

### SHOULD order file declarations like `go doc -u`

#### Example

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

- Find things faster with binary search
- Find things faster with a predictable organization

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

- Consistent style
- Skimmable

### SHOULD separate multiple-line blocks with blank lines

#### Example

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

- Consistent style
- Skimmable

### SHOULD use long variable declarations instead of short where equivalent

#### Example

```go
var foo, err = ...

bar, err := ...
```

#### Reasons

- Consistent style
- Consistent with other kinds of declarations

    ```go
    const c = ...
    var v = ...
    type t = ...
    ```

- Short declarations with multiple variables are context-sensitive: `a, b := f()` can mean declare two new variables, declare a and assign b, or declare b and assign a; and thus cannot always be copied to another place safely
- Avoids unintentional variable shadowing

    ```go
    x := ...

    if ... {
        x, err := ...

    f(x) // X is always unchanged
    ```

- A short declaration indicates that something clever is happening

## Testing

### SHOULD NOT use test frameworks or assertion libraries

#### Examples

```go
if actual = Foo(input); actual != expected { ...
```

#### Reasons

- You don't have to learn test DSLs
- Code is easy to understand
- Third-party code can break or be abandoned

### SHOULD call testing.T.Parallel

#### Examples

```go
func TestFoo(t *testing.T) {
    t.Parallel() ...
```

#### Reasons

- Tests run in parallel finish faster
- Parallelism discourages side effects and singletons

### SHOULD use the -race flag

#### Example

```
$ go test -race
```

#### Reason

Catch data races early.
