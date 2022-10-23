# corset

A spec-compliant CORS middleware.

## Setup

```go
c := corset.NewCorset(corset.CorsetOptions{
  AllowedOrigins:   origins,
  AllowedMethods:   methods,
  AllowedHeaders:   headers,
  ExposeHeaders:    []string{"X-Powered-By"},
  AllowCredentials: true,
})

r := NewRouter() // implements `ServeHTTP`

if err := http.ListenAndServe(":3000", c.Handler(r)); err != nil {
  log.Fatal(err)
}
```

## Usage

#### type Corset

```go
type Corset struct {
}
```

Corset represents a Corset middleware object.

#### func  NewCorset

```go
func NewCorset(opts CorsetOptions) *Corset
```
NewCorset initializes a new Corset middleware object.

#### func  NewCorsetSensibleDefaults

```go
func NewCorsetSensibleDefaults() *Corset
```

#### func (*Corset) Handler

```go
func (c *Corset) Handler(h http.Handler) http.Handler
```
Handler initializes the Corset middleware and applies the CORS spec, as
configured by the consumer, on the request.

#### type CorsetOptions

```go
type CorsetOptions struct {
	AllowedOrigins        []string
	AllowedMethods        []string
	AllowedHeaders        []string
	AllowCredentials      bool
	UseOptionsPassthrough bool
	MaxAge                int
	ExposeHeaders         []string
}
```

CorsetOptions represents configurable options that are available to the
consumer.
