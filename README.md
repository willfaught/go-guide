# Go coding conventions

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED",  "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119](https://www.ietf.org/rfc/rfc2119.txt).

The sections and conventions are ordered alphabetically.

## General

These conventions closely follow Go idioms, Go best practicies, and the Go Way. They are the consensus of the Go community on how best to write Go. Most who write Go already do these things. Aside from the obvious benefits, it is important to write Go like the Go community so new engineers can more easily understand it.

### MUST comply with go build ./...
### MUST comply with go test ./...
### MUST comply with go vet ./...
### MUST comply with gofmt -s
### MUST comply with goimports
### MUST comply with golint
### MUST support go doc
### MUST support go generate
### MUST support go get
### MUST support go install
### MUST support go mod
### SHOULD comply with https://golang.org/blog
### SHOULD comply with https://golang.org/doc/effective_go.html
### SHOULD comply with https://golang.org/doc/faq
### SHOULD comply with https://golang.org/wiki/CodeReviewComments
### SHOULD follow the example of the Go project
### SHOULD follow the example of the Go standard libraries

## Style

### SHOULD begin one-line comments and end one-line general comments with a space

#### Examples

Good:

```go
// Started earlier
```

```go
/* Started earlier */
```

Bad:

```go
//Started earlier
```

```go
/*Started earlier*/
```

### SHOULD capitalize comments

#### Examples

Good:

```go
// Started earlier
```

Bad:

```go
// started earlier
```

### SHOULD end comments with multiple sentences with punctuation

#### Examples

Good:

```go
// Started earlier. Skip initialization.
```

Bad:

```go
// Started earlier. Skip initialization
```

## Testing

### SHOULD NOT use other test frameworks
