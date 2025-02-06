# Liquor String

## Table of Contents
- [Case Conversion Functions](#case-conversion-functions)
  - [ToSnakeCase](#tosnakecase)
  - [ToCamelCase](#tocamelcase)
  - [ToKebabCase](#tokebabcase)
- [Pluralization Functions](#pluralization-functions)
  - [ToPlural](#toplural)
  - [ToSingular](#tosingular)
  - [IsPlural](#isplural)
  - [IsSingular](#issingular)
- [Validation Functions](#validation-functions)
  - [IsEmail](#isemail)
  - [IsURL](#isurl)
  - [IsNumeric](#isnumeric)
  - [IsAlphanumeric](#isalphanumeric)
- [Generation Functions](#generation-functions)
  - [RandomString](#randomstring)
  - [UUID](#uuid)



## Case Conversion Functions

### ToSnakeCase

Converts a sting to snake_case format

```go
result := lqstring.ToSnakeCase("helloWorld") // returns "hello_world"
```

### ToCamelCase

Converts a string to camelCase format.

```go
result := lqstring.ToCamelCase("hello_world") // returns "helloWorld"
```

## ToKebabCase

Converts a string to kebab-case format.

```go
result := lqstring.ToKebabCase("helloWorld") // returns "hello-world"
```

## Pluralization Functions

## ToPlural

Converts a singular word to its plural form.

```go
result := lqstring.ToPlural("book") // returns "books"
```

## ToSingular
Converts a plural word to its singular form.

```go
result := lqstring.ToSingular("books") // returns "book"
```

## IsPlural

Checks if a word is in plural form.

```go
result := lqstring.IsPlural("books") // returns true
```

## IsSingular

Checks if a word is in singular form.
```go
result := lqstring.IsSingular("book") // returns true
```

## Validation Functions

### IsEmail
Checks if a string is a valid email address.

```go
result := lqstring.IsEmail("user@example.com") // returns true
```

### IsURL
Checks if a string is a valid URL.

```go
result := lqstring.IsEmail("user@example.com") // returns true
```

### IsNumeric

```go
result := lqstring.IsNumeric("12345") // returns true
```

### IsAlphanumeric

```go
result := lqstring.IsAlphanumeric("abc123") // returns true
```

## Generation Functions

### RandomString

Generates a random string of the specified length.

```go
result := lqstring.RandomString(10) // returns a random string of length 10
```

### UUID

Generates a new UUID v4

```go
result := lqstring.UUID() // returns a UUID string like "550e8400-e29b-41d4-a716-446655440000"
```
