# Go guide

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119](https://www.ietf.org/rfc/rfc2119.txt).

The examples show what MUST, SHOULD, or MAY be done.

The sections and conventions are ordered alphabetically.

## Design

- SHOULD NOT export global variables from libraries

        func New() *Foo { ...

## Documentation

- SHOULD name benchmarks and tests like examples

        func BenchmarkFoo_Bar_baz() ...

        func TestFoo_Bar_baz() ...

## General

- MUST comply with go build ./...
- MUST comply with go test ./...
- MUST comply with go vet ./...
- MUST comply with gofmt -s
- MUST comply with goimports
- MUST comply with golint
- SHOULD comply with https://golang.org/doc/effective_go.html
- SHOULD comply with the Go blog
- SHOULD comply with the Go wiki
- SHOULD follow the example of the Go standard libraries
- SHOULD follow the example of the Go project

## Implementation

- MUST commit vendored packages

- MUST vendor external packages for main packages

- MUST vendor with dep

## Style

- SHOULD NOT begin or end blocks and groups with a blank line

        var (
            foo Foo

            bar Bar
        )

        {
            foo()

            bar()
        }

- SHOULD NOT use the built-in functions `make` or `new` unless necessary

        make(chan Foo)
        make(chan Foo, bar)
        make(map[Foo]Bar, baz)
        new(int)

- SHOULD begin comments with a space and end general comments with a space

        // Started earlier

        /* Started earlier */

- SHOULD capitalize comments

        // Started earlier

- SHOULD end comments with multiple sentences with punctuation

        // Started earlier. Skip initialization.

- SHOULD group similar statements and declarations and separate different ones with a blank line

        const ...
        const ...

        var ...
        var ...

        func ...
        func ...

        type ...
        type ...

        w, x := ...
        y, z := ...

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

- SHOULD order file declarations like `go doc -u`

        const C ...
        
        const c ...

        var V ...

        var v ...

        func F ...

        func f ...

        type T ...

        func FT(...) *T ...

        func fT(...) *T ...

        func (T) M ...

        func (T) m ...

        type t ...

        func Ft(...) *t ...

        func ft(...) *t ...

        func (t) M ...

        func (t) m ...

- SHOULD separate cases with a blank line

        select ... {
        case ...:
            ...

        case ...:
            ...

        default:
            ...
        }

        switch ... {
        case ...:
            ...

        case ...:
            ...

        default:
            ...
        }

- SHOULD separate multiple-line curly and round bracket blocks with a blank line

        const ...

        const (
            ...
        )

        if ... {
            ...
        }

        var ...

        var (
            ...
        )

        func ... { ... }

        func ... {
            ...
        }

- SHOULD use long variable declarations instead of short where equivalent

        var a, err = ...
        b, err := ...

        if err := f(a, b); err != nil {...}

## Testing

- SHOULD NOT use assertion libraries

        if actual = Foo(input); actual != expected { ...

- SHOULD call testing.T.Parallel

        func TestFoo(t *testing.T) {
            t.Parallel() ...

- SHOULD use the -race flag

        $ go test -race
