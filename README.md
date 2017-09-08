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

        &Foo{}
        []Foo{}
        make([]Foo, bar)
        make([]Foo, bar, baz)
        make(chan Foo)
        make(chan Foo, bar)
        make(map[Foo]Bar, baz)
        map[Foo]Bar{...}
        new(int)

- SHOULD abbreviate names with initials or prefixes

        var context ...
        var con ...
        var c ...

        var readWriter ...
        var rw ...
        var r ...

        var template ...
        var temp ...
        var t ...

- SHOULD begin comments with a space and end general comments with a space

        // Only if out of date

        /* Only if out of date */

- SHOULD capitalize comments

        // Only if out of date

- SHOULD end line comments that are full sentences or contain multiple sentences end with punctuation

        fooaddr.Print() // fooaddr is guaranteed to be valid.

        if !valid { // The scheduler job failed. Retry the job now.

- SHOULD alias all imports with conflicting names

        import stdhttp "net/http"
        import foohttp "github.com/company/foo/http"

- SHOULD generate code that looks hand-written

- SHOULD group adjacent statements of the same kind together and separate groups with a blank line

        const ...
        const ...

        var ...
        var ...
        x := ...
        y := ...

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

        if ... {...}
        if ... {...}

        for ... {...}
        for ... {...}

- SHOULD order constants, variables, functions, and types like `go doc -u`

        const (
            C1 ...
            c1 ...
        )

        const (
            C2 ...
            c2 ...
        )

        const C3 ...

        const C4 ...

        const c3 ...

        const c4 ...

        var V1 ...

        var (
            V4 ...
            v4 ...
        )

        var V2 ...

        var (
            V3 ...
            v3 ...
        )

        var v1 ...

        var v2 ...

        func F1 ...

        func F2 ...

        func f1 ...

        func f2 ...

        type T1 ...

        func F3(...) (T1 ...) {...}

        func F4(...) (*T1 ...) {...}

        func f3(...) (T1 ...) {...}

        func f4(...) (*T1 ...) {...}

        func (T1) M1 ...

        func (*T1) M2 ...

        func (T1) m1 ...

        func (*T1) m2 ...

        type T2 ...

        type t1 ...

        type t2 ...

- SHOULD panic with the problematic value if the panic output is sufficient to understand the problem

        switch n {
        case 0:
            ...
        ...
        default:
            panic(n)
        }

- SHOULD prefix standard library import aliases with "std"

        import stdio "io"

- SHOULD separate cases with a blank line

        switch t {
        case TypeAnimal:
            ...

        case TypeMineral:
            ...

        case TypeVegetable:
            ...

        default:
            panic(t)
        }

- SHOULD separate file declarations not in a declaration block with a blank line

        const C1 ...

        const (
            C2 ...
            C3 ...
        )

        const C4 ...

        var V1 ...

        var (
            V2 ...
            V3 ...
        )

        var V4 ...

        func F1 ...

        func F2 ...

        type T1 ...

        type (
            T2 ...
            T3 ...
        )

        type T4 ...

        func (T4) M1 ...

        func (T4) M2 ...

- SHOULD separate multiple-line curly and round bracket blocks from other statements with a blank line

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

- SHOULD use line comments instead of general comments

        // Package p ...
        package p

        // F ...
        func F ...

        if ... { // Happens when ...
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
