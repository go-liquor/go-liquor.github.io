
# LQArray Helper

## Table of Contents
- [Usage](#usage)
- [Available Functions](#available-functions)
  - [Contains](#contains)
  - [ContainsFunc](#containsfunc)
  - [ContainsBy](#containsby)
  - [Unique](#unique)
  - [Chunk](#chunk)
  - [Map](#map)
  - [Filter](#filter)
  - [Reduce](#reduce)
  - [Reverse](#reverse)
  - [IndexOf](#indexof)
- [Type Safety](#type-safety)
- [Examples](#examples)
  - [Working with Custom Types](#working-with-custom-types)
  - [Working with Strings](#working-with-strings)

Generic array/slice manipulation utilities for Go.



## Usage

```go
import "github.com/go-liquor/liquor-sdk/helpers/lqarray"
```

## Available Functions

### Contains
Check if an element exists in a slice:
```go
numbers := []int{1, 2, 3, 4, 5}
exists := lqarray.Contains(numbers, 3) // true
notExists := lqarray.Contains(numbers, 6) // false
```

### ContainsFunc
Check if an element exists using a custom comparison function:
```go
type Person struct {
    Name string
    Age  int
}

people := []Person{
    {Name: "John", Age: 30},
    {Name: "Jane", Age: 25},
}

exists := lqarray.ContainsFunc(people, Person{Name: "John"}, func(a, b Person) bool {
    return a.Name == b.Name
})
```

### ContainsBy
Check if any element satisfies a condition:
```go
type User struct {
    Age int
}

users := []User{{Age: 25}, {Age: 30}}
hasAdult := lqarray.ContainsBy(users, func(u User) bool {
    return u.Age >= 18
})
```

### Unique
Remove duplicate elements from a slice:
```go
numbers := []int{1, 2, 2, 3, 3, 4}
unique := lqarray.Unique(numbers) // [1, 2, 3, 4]
```

### Chunk
Split a slice into chunks of specified size:
```go
numbers := []int{1, 2, 3, 4, 5}
chunks := lqarray.Chunk(numbers, 2) // [[1, 2], [3, 4], [5]]
```

### Map
Transform each element in a slice:
```go
numbers := []int{1, 2, 3}
doubled := lqarray.Map(numbers, func(x int) int {
    return x * 2
}) // [2, 4, 6]
```

### Filter
Create a new slice with elements that satisfy a condition:
```go
numbers := []int{1, 2, 3, 4, 5}
evenNumbers := lqarray.Filter(numbers, func(x int) bool {
    return x%2 == 0
}) // [2, 4]
```

### Reduce
Reduce a slice to a single value:
```go
numbers := []int{1, 2, 3, 4, 5}
sum := lqarray.Reduce(numbers, func(acc, x int) int {
    return acc + x
}, 0) // 15
```

### Reverse
Reverse the order of elements in a slice:
```go
numbers := []int{1, 2, 3}
reversed := lqarray.Reverse(numbers) // [3, 2, 1]
```

### IndexOf
Find the index of an element:
```go
numbers := []int{1, 2, 3, 4, 5}
index := lqarray.IndexOf(numbers, 3) // 2
notFound := lqarray.IndexOf(numbers, 6) // -1
```

## Type Safety

All functions are implemented using Go generics, providing type safety at compile time. The `Contains` and `IndexOf` functions require the type to be `comparable`, while other functions can work with any type.

## Examples

### Working with Custom Types
```go
type Product struct {
    ID    int
    Name  string
    Price float64
}

products := []Product{
    {ID: 1, Name: "Phone", Price: 999.99},
    {ID: 2, Name: "Laptop", Price: 1499.99},
    {ID: 3, Name: "Tablet", Price: 499.99},
}

// Filter expensive products
expensive := lqarray.Filter(products, func(p Product) bool {
    return p.Price > 1000
})

// Map to names only
names := lqarray.Map(products, func(p Product) string {
    return p.Name
})

// Find product by ID
hasProduct := lqarray.ContainsBy(products, func(p Product) bool {
    return p.ID == 2
})
```

### Working with Strings
```go
words := []string{"hello", "world", "hello", "go"}

// Get unique words
uniqueWords := lqarray.Unique(words)

// Filter words longer than 4 characters
longWords := lqarray.Filter(words, func(w string) bool {
    return len(w) > 4
})

// Transform to uppercase
upper := lqarray.Map(words, func(w string) string {
    return strings.ToUpper(w)
})
```