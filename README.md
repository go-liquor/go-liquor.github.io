# Liquor framework

> Liquor is a framework for backend development in web applications. It provides a boilerplate to kickstart your application without worrying about the HTTP server, dependency injection, or database connection.


```go
package main

import (
	"github.com/go-liquor/liquor-sdk/app"
)

func main() {
	app.NewApp(
		// put here the modules and applications resources
	)
}

```