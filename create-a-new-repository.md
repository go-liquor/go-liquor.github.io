# Create a new repository

To create a new repository, you can use the Liquor CLI to simplify the process. Use the following command:

```bash
liquor create repository --name <repositoryName>
```

eg:

```bash
liquor create repository --name order
```

This command will generate the following files in your project:

`internal/adapters/database/repository/order_repository.go`

```go
package repository

import (
    "github.com/uptrace/bun"

    "lucas/internal/app/ports"
)

type OrderRepository struct {
    db *bun.DB

}
func NewOrderRepository(db *bun.DB) ports.OrderRepository {
    return  &OrderRepository{
        db: db,
    }
}
```

`internal/app/ports/order_repository.go`


```go
package ports


type OrderRepository interface {
}
```


You need register repository in your `cmd/app/main.go`


```go
package main

import (
	"my-pkg/internal/adapters/server/http"
    "my-pkg/internal/adapters/database/repository"
	"github.com/go-liquor/liquor-sdk/app"
)

func main() {
	app.NewApp(
		http.Server,
		migrate.Migrations,
        app.RegisterRepository(
            repository.NewOrderRepository, // this
        )
	)
}
```

> Remember that the functions created in the repository need to be updated in ports, as the repository is an implementation of the interface in ports.