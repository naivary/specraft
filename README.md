# JSON Schema

JSON Schema is a Go package for generating JSON Schema based upon defined marker
comments. There are already tools which are generating JSON Schema based upon
struct tags. This approach is kinda clumsy because it will amount to a lot of
tags to be set and at the same time the generate go-doc will not include those.
Marker comments on the otherside a normal Go comments which will be generated by
go doc. The concept is (as I know) originated by Kubernetes and Kubebuilder. If
you which to read more about it see [here](https://pkg.go.dev/sigs.k8s.io/controller-tools/pkg/markers).

## Example
```go
type AuthenticationRequest struct {
    // +jsonschema:validation:format=email
    // +jsonschema:validation:required
    //
    // Email is the email of the user who
    // wants to login
    Email string `json:"email"`

    // +jsonschema:validation:required
    //
    // Password is raw password of the user
    Password string `json:"password"`
}
```

The "normal" documentation string of the struct field will be used for the
`description` field of the JSON Schema. The type will be infered from the
choosen Go datatype.

## Supported validation keywords
- enum (const=enum with one item)
- multipleOf
- maximum
- exclusiveMaximum
- minimum
- exclusiveMinimum
- maxLength
- minLength
- pattern
- maxItems
- minItems
- uniqueItems
- maxContains
- minContains
- dependentRequired
- format
- regex
- contentEncoding
- contentMediaType
- deprecated
- title
- description (take the documentaitn written on the field)
- default: enforce defaults?
- readOnly/writeOnly (JUST FOR DOCS)
- examples

## Further planned features
- [ ] Code generation for specified defaults based upon a common `Defaulter`
  interface
- [ ] deprecated msg?
