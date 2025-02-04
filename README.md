# Liquor framework

> Liquor is a framework for backend development in web applications. It provides a boilerplate to kickstart your application without worrying about the HTTP server, dependency injection, or database connection.


```go
package main

import (
	"github.com/my-project/my-project/internal/adapters/database/migrations"
	"github.com/my-project/my-project/internal/adapters/server/http"
	"github.com/my-project/my-project/internal/app/services"

	"github.com/go-liquor/liquor-sdk/app"
)

func main() {
	app.NewApp(
		http.Server,
		migrations.Migrations,
		app.RegisterService(
			services.NewInitialService,
		),
	)
}

```