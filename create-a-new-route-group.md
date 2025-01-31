# Create a new route group

To create a new route group, you can use the Liquor CLI to simplify the process. Use the following command:

```bash
liquor create route --name <grupName> --group <GroupPathAPI>
```

eg:

```bash
liquor create route --name order --group /api/orders
```

This command will generate the following files in your project:

`internal/adapters/server/http/routes/order.go`

```go
package routes

import (
	"github.com/gin-gonic/gin"
	"my-pkj/internal/adapters/server/http/handlers"
)

func OrderRoutes(r *gin.Engine, handler *handlers.OrderHandler) {
	group := r.Group("/api/orders")
	{
		group.GET("/", handler.Example)
	}
}
```

`internal/adapters/server/http/handlers/order.go`

```go
package handlers

import (
	"net/http"

	"github.com/gin-gonic/gin"
)

type OrderHandler struct {
}

func NewOrderHandler() *OrderHandler {
	return &OrderHandler{
	}
}
func (i *OrderHandler) Example(c *gin.Context) {
	c.JSON(http.StatusOK, gin.H{
		"message": "this is an example",
	})
}
```

**If you want, you can automatically generate CRUD routes.**

```bash
liquor create route --name order --group /api/orders --crud
```

This command will generate the following files in your project:


`internal/adapters/server/http/routes/order.go`

```go
package routes

import (
	"github.com/gin-gonic/gin"
	"my-pkg/internal/adapters/server/http/handlers"
)

func OrderRoutes(r *gin.Engine, handler *handlers.OrderHandler) {
	group := r.Group("/api/orders")
	{
        group.GET("/", handler.List)
        group.POST("/", handler.Create)
        group.GET("/:id", handler.Get)
        group.PATCH("/:id", handler.Update)
        group.DELETE("/:id", handler.Delete)
	}
}

```

`internal/adapters/server/http/handlers/order.go`

```go
package handlers

import (
	"net/http"

	"github.com/gin-gonic/gin"
)

type OrderHandler struct {
}

func NewOrderHandler() *OrderHandler {
	return &OrderHandler{
	}
}
func (i *OrderHandler) List(c *gin.Context) {
	c.Status(http.StatusOK)
}

func (i *OrderHandler) Create(c *gin.Context) {
	c.Status(http.StatusOK)
}

func (i *OrderHandler) Get(c *gin.Context) {
	c.Status(http.StatusOK)
}

func (i *OrderHandler) Update(c *gin.Context) {
	c.Status(http.StatusOK)
}

func (i *OrderHandler) Delete(c *gin.Context) {
	c.Status(http.StatusOK)
}
```