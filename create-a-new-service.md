# Create a new service

To create a new service (business logic), you can use the Liquor CLI to simplify the process. Use the following command:

```bash
liquor create service --name <serviceName>
```

eg:

```bash
liquor create service --name order
```

This command will generate the following files in your project:

`internal/app/services/order.go`

```go
package services

import (
        "go.uber.org/zap"
)

type OrderService struct {
        logger *zap.Logger
}

func NewOrderService(logger *zap.Logger) *OrderService {
        return &OrderService{
                logger: logger,
        }
}
```

You need register service in your `cmd/app/main.go`

```go
package main

import (
	"my-pkg/internal/adapters/server/http"
	"my-pkg/internal/app/services"
	"github.com/go-liquor/liquor-sdk/app"
)

func main() {
	app.NewApp(
		http.Server,
		migrate.Migrations,
		app.RegisterService(
			services.NewInitialService,
			services.NewOrderService, // this
		),
	)
}

```

To use the service in your HTTP handler (or elsewhere), simply add it as a parameter in the handler creation function.

```go
package handlers

import (
	"net/http"

	"github.com/gin-gonic/gin"
	"my-pkg/internal/app/services"  // add this
)

type OrderHandler struct {
	svc *services.OrderService // add this
}

func NewOrderHandler(svc *services.OrderService) *OrderHandler {
	return &OrderHandler{
		svc: svc,
	}
}
func (i *OrderHandler) Example(c *gin.Context) {
	c.JSON(http.StatusOK, gin.H{
		"message": i.svc.MyFunction(),
	})
}
```

Liquor uses the [uber/fx](https://github.com/uber-go/fx) dependency injection framework. Therefore, when registering a service, handler, or function, you only need to pass it as an argument to the function that instantiates the object.