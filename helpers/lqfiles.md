# LQFiles Helper

File system operations helper for Go applications.


## Usage

To use it you need to instantiate the provider in your `cmd/app/main.go`:

```go
package main

import (
	"github.com/go-liquor/framework/internal/adapters/server/http"
	"github.com/go-liquor/framework/internal/app/services"
	"github.com/go-liquor/liquor-sdk/app"
    "github.com/go-liquor/liquor-sdk/helpers/lqfiles" // add this
)

func main() {
	app.NewApp(
        lqfiles.FilesProvider, // add this
		http.Server,
		app.RegisterService(
			services.NewInitialService,
		),
	)
}
```

in you service or provider you can use it like this:

```go
type Service struct {
    files lqfiles.Files // add this
}

func NewService(
    files lqfiles.Files
) *Service {
    return &Service{
        files: files,
    }
}
```

## Features

- File reading and writing
- Directory operations
- File copying and moving
- File existence checking
- Directory listing

## Examples

### Initialize the Helper


### File Operations

```go
// Write data to file
data := []byte("Hello, World!")
err := files.Write("example.txt", data)
if err != nil {
    // Handle error
}

// Read file content
content, err := files.Read("example.txt")
if err != nil {
    // Handle error
}

// Copy file
err = files.Copy("source.txt", "destination.txt")
if err != nil {
    // Handle error
}

// Move/Rename file
err = files.Move("old.txt", "new.txt")
if err != nil {
    // Handle error
}
```

### Directory Operations

```go
// Create directory (and parent directories if needed)
err := files.CreateDir("path/to/new/directory")
if err != nil {
    // Handle error
}

// Check if path exists
exists := files.Exists("path/to/check")

// Check if path is a directory
isDir := files.IsDir("path/to/check")

// List directory contents
entries, err := files.ListDir("path/to/directory")
if err != nil {
    // Handle error
}

for _, entry := range entries {
    fmt.Printf("Name: %s, IsDir: %v\n", entry.Name(), entry.IsDir())
}
```

### Common Use Cases

1. Working with Configuration Files
```go
// Save configuration
config := []byte(`{"setting": "value"}`)
err := files.Write("config.json", config)

// Read configuration
configData, err := files.Read("config.json")
```

2. Managing Temporary Files
```go
// Create temp directory
err := files.CreateDir("temp")
if err != nil {
    // Handle error
}

// Clean up when done
defer files.Remove("temp")
```

3. File Processing
```go
// Process files in directory
entries, err := files.ListDir("data")
if err != nil {
    // Handle error
}

for _, entry := range entries {
    if !entry.IsDir() {
        // Process file
        data, err := files.Read("data/" + entry.Name())
        if err != nil {
            continue
        }
        // Process data...
    }
}
```

## File Permissions

- Written files: 0644 (rw-r--r--)
- Created directories: 0755 (rwxr-xr-x)

## Error Handling

The package provides standard Go error handling:

```go
// Handle file operations errors
if err := files.Write("file.txt", data); err != nil {
    switch {
    case os.IsPermission(err):
        // Handle permission error
    case os.IsNotExist(err):
        // Handle not found error
    default:
        // Handle other errors
    }
}
```

## Thread Safety

The Files interface implementation is safe for concurrent use by multiple goroutines.

## Best Practices

1. Always check for errors
```go
if err := files.Write("file.txt", data); err != nil {
    // Handle error
}
```

2. Use deferred cleanup
```go
tempDir := "temp"
files.CreateDir(tempDir)
defer files.Remove(tempDir)
```

3. Validate paths before operations
```go
if !files.Exists(path) {
    // Handle missing file/directory
}
```
