# Go guide

The guiding principle for these Go coding conventions is:

***Do not write code for yourself; write it for the poor engineer woken in the night to fix it for you.***

The best way to do that is to facilitate working in unfamiliar code.
The best way to do that is to facilitate skimming code.
The best way to do that is to facilitate reading and searching code.
Some of the conventions address these things.

The rest of the conventions describe Go idioms and best practices observed from personal experience.

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119](https://www.ietf.org/rfc/rfc2119.txt).

The examples show what MUST or SHOULD be done, or what is RECOMMENDED to be done.

The sections and conventions are ordered alphabetically.

## Design

- SHOULD NOT export fields of unexported struct types unless necessary

        for _, test := range []struct {
            actual, expected interface{}
        }{ ...

        json.Marshal(struct {
            ID, Name string
        }{ ...

- SHOULD drive libraries with lightweight main packages

        import "github.com/company/foo"

        func main() {
            foo.Foo()
        }

- SHOULD put multiple main packages under cmd

        .../github.com/company/foo/
            cmd/
                foo-start/
                    main.go
                    main_test.go
                foo-stop/
                    main.go
                    main_test.go
            foo.go
            foo_test.go

## Documentation

- SHOULD NOT document simple error results

        // Init initializes t.
        func (t T) Init() error
        
        // Name returns the t name.
        func (t T) Name() (string, error)

- SHOULD name benchmarks and tests like examples

        func BenchmarkFoo_Bar_baz() ...

        func TestFoo_Bar_baz() ...

- SHOULD provide example functions

    foo.go:

        type Foo ...

        func (Foo) Bar() ...

    foo_test.go:

        func ExampleFoo() ...

        func ExampleFoo_baz() ...

        func ExampleFoo_boz() ...

        func ExampleFoo_Bar() ...

        func ExampleFoo_Bar_baz() ...

        func ExampleFoo_Bar_boz() ...

## General

- MUST comply with go test
- MUST comply with go vet
- MUST comply with gofmt -s
- MUST comply with goimports
- MUST comply with golint
- SHOULD comply with https://github.com/golang/go/wiki/CodeReviewComments
- SHOULD comply with https://golang.org/doc/effective_go.html
- SHOULD follow the example of the Go blog
- SHOULD follow the example of the Go standard libraries

## Implementation

- MUST NOT assume conditions that are not explicitly documented

        type T struct {
            ...
            // ID is the identifier. Must not be zero. Must be unique.
            ID string
            ...
            // UpdatedAt is when it was updated. Must be UTC. Must not
            // be less than CreatedAt if not zero. Must not be greater
            // than DeletedAt if DeletedAt is not zero.
            UpdatedAt time.Time
        }

- MUST assert interface implementations with package variable declarations

        var _ fmt.Stringer = Foo{}

        var _ fmt.Stringer = (*Bar)(nil)

        type Foo ...

        func (f Foo) String() string {...}

        type Bar ...

        func (b *Bar) String() string {...}

- MUST commit vendored packages

- MUST name files with a main function main.go

        .../github.com/company/foo/
            cmd/
                foo/
                    main.go
                    main_test.go
            foo.go
            foo_test.go

- MUST use fmt.Print and fmt.Println instead of print and println

        fmt.Print(...)
        fmt.Println(...)

- MUST use lowercase names for package directories and files

        .../github.com/company/foo/
            cmd/
                foo/
                    main.go
                    main_test.go
            foo.go
            foo_test.go

- MUST vendor local and external packages for main packages

- SHOULD implement and export mock implementations of exported interfaces

        type T interface {M()...}

        type TMock struct {
            mock.Mock
        }

        func (t *TMock) M ...

- SHOULD put generate commands in generate.go

## Style

- MUST NOT begin or end blocks with a blank line

        if ... {
            foo()
            ...
            bar()
        }

- MUST name import aliases like packages

        import stdhttp "net/http"
        import foohttp "github.com/company/foo/http"

- MUST name packages the same as their directory

        .../github.com/company/foo-go/
            foo/
                foo.go
        .../github.com/company/bar.go/
            bar/
                bar.go
        ../github.com/company/baz_go/
            baz/
                baz.go

- MUST panic for unrecoverable errors

        type foo struct {
            Name string
        }

        var b, err = json.Marshal(foo{...})

        if err != nil {
            panic(err)
        }

- MUST qualify fields in literals of imported struct types

        foo.Foo{A: 1}
        foo.Foo{A: 1, B: 2}
        Bar{1}
        Bar{1, 2}
        baz{1}
        baz{1, 2}
        struct{A, B int}{1, 2}

- MUST use the type `struct{}` for values of done channels

        var done = make(chan struct{})
        ...
        <-done

- MUST use the type `struct{}` for values of maps that represent sets

        var seen = map[T]struct{}{}

        for _, t := range ts {
            seen[t] = struct{}{}
        }

- RECOMMENDED you abbreviate names with initials or prefixes

        var context ...
        var con ...
        var c ...

        var readWriter ...
        var rw ...
        var r ...
        var w ...

        var template ...
        var temp ...
        var t ...

- RECOMMENDED you prefix standard library import aliases with "std"

        import stdhttp "net/http"
        import foohttp "github.com/company/foo/http"

- RECOMMENDED line comments begin with capitalization

        struct {
            ReadTimeout time.Duration // Maximum duration before timing out read of the request
        }

        if x == nil { // Happens if the database could not be reached
            ...
        }

- RECOMMENDED line comments that are full sentences or contain multiple sentences end with punctuation

        fooaddr.Print() // fooaddr is guaranteed to be valid.

        if !valid { // The scheduler job failed. Retry the job now.

- SHOULD NOT use the functions `make` or `new` unless necessary

        T{...}
        []T{...}
        [N]T{...}
        map[T]T{...}
        make([]T, N)
        make([]T, M, N)
        make(chan T)
        make(map[T]T, N)
        new(int)

- SHOULD NOT use raw string literals unless necessary

        type T struct {
            F int `foo:"bar"`
        }

        regexp.MustCompile(`\{\{.+\}\}`)

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

## Test

- SHOULD NOT fail and stop a test if it is possible to continue

        var id, err = NewFoo()

        if err != nil {
            t.Fatal(err)
        }

        f, err := GetFoo(id)

        if err != nil {
            t.Error(err)
        }

        if err := UpdateFoo(id, Foo{...}); err != nil {
            t.Error(err)
        }

        if err := DeleteFoo(id); err != nil {
            t.Error(err)
        }

- SHOULD NOT use assertion library packages

        if actual.count != expected.count {
            t.Errorf("actual %v, expected %v", actual.count, expected.count)
        }

        if !reflect.DeepEqual(actual.items, expected.items) {
            t.Errorf("actual %v, expected %v", actual.items, expected.items)
        }

- SHOULD NOT use mutable global variables

        func TestFoo(t *testing.T) {
            var s = NewServer()
            ...
        }

- SHOULD call testing.T.Parallel

        func TestFoo(t *testing.T) {
            t.Parallel()
            ...
        }

- SHOULD run tests with the -race flag

        $ go test -race

- SHOULD skip tests rather than comment them

        func TestFoo(t *testing.T) {
            t.SkipNow()
            ...
        }

- SHOULD write table-driven tests

        for _, test := range []struct {
            x, y, expected int
        } {
            {},
            {1, 2, 3},
            ...
        } {
            if actual := add(test.x, test.y); actual != test.expected {
                t.Errorf("x %v, y %v, actual %v, expected %v", test.x, test.y, actual, test.expected)
            }
        }
