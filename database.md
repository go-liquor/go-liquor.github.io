# Database

To avoid importing unnecessary libraries, Liquor only enables the libraries you choose to use. If you need to work with a specific database, you must enable its corresponding library.


- [Available databases drivers](#available-databases-drivers)
    - [MongoDB](#mongodb)
    - [MySQL](#mysql)
    - [Postgres](#postgres)
    - [SQLITE](#sqlite)
- [Configurations](#configurations)


### MongoDB

The MongoDB uses the [mongo-driver](https://www.mongodb.com/pt-br/docs/drivers/go/current/quick-start/)

To enable you need enable module:
```bash
liquor app enable database/mongodb
# or
go get github.com/go-liquor/liquor/sdk/modules/database/mongodb
```

in `cmd/app/main.go` add module:

```go
package main

import (
	"github.com/go-liquor/framework/internal/adapters/server/http"
	"github.com/go-liquor/framework/internal/app/services"
	"github.com/go-liquor/liquor/sdk/app"
    "github.com/go-liquor/liquor/sdk/modules/database/mongodb" // add this
)

func main() {
	app.NewApp(
        mongodb.DatabaseMongoDBModule, // add this
		http.Server,
		app.RegisterService(
			services.NewInitialService,
		),
	)
}
```

## Available databases drivers

Enable only the drivers you are going to use

### MySQL

The MySQL uses the [uptrace/bun](https://bun.uptrace.dev/) 

To enable you need enable module:
```bash
liquor app enable database/mysql
# or
go get github.com/go-liquor/liquor/sdk/modules/database/mysql
```

in `cmd/app/main.go` add module:

```go
package main

import (
	"github.com/go-liquor/framework/internal/adapters/server/http"
	"github.com/go-liquor/framework/internal/app/services"
	"github.com/go-liquor/liquor/sdk/app"
    "github.com/go-liquor/liquor/sdk/modules/database/mysql" // add this
)

func main() {
	app.NewApp(
        mongodb.DatabaseMysqlModule, // add this
		http.Server,
		app.RegisterService(
			services.NewInitialService,
		),
	)
}
```


### Postgres

The Postgres uses the [uptrace/bun](https://bun.uptrace.dev/) 

To enable you need enable module:
```bash
liquor app enable database/postgres
# or
go get github.com/go-liquor/liquor/sdk/modules/database/postgres
```

in `cmd/app/main.go` add module:

```go
package main

import (
	"github.com/go-liquor/framework/internal/adapters/server/http"
	"github.com/go-liquor/framework/internal/app/services"
	"github.com/go-liquor/liquor/sdk/app"
    "github.com/go-liquor/liquor/sdk/modules/database/postgres" // add this
)

func main() {
	app.NewApp(
        mongodb.DatabasePostgresModule, // add this
		http.Server,
		app.RegisterService(
			services.NewInitialService,
		),
	)
}
```

### Sqlite

The SQLite uses the [uptrace/bun](https://bun.uptrace.dev/) 

To enable you need enable module:
```bash
liquor app enable database/sqlite
# or
go get github.com/go-liquor/liquor/sdk/modules/database/sqlite
```

in `cmd/app/main.go` add module:

```go
package main

import (
	"github.com/go-liquor/framework/internal/adapters/server/http"
	"github.com/go-liquor/framework/internal/app/services"
	"github.com/go-liquor/liquor/sdk/app"
    "github.com/go-liquor/liquor/sdk/modules/database/sqlite" // add this
)

func main() {
	app.NewApp(
        mongodb.DatabaseSqliteModule, // add this
		http.Server,
		app.RegisterService(
			services.NewInitialService,
		),
	)
}
```

## Configurations

Your database configurations are stored in the config.yaml file.

```yaml
database:
  sqlite:
    dns: "file::memory:?cache=shared" # you can use :memory: or one file
  mysql:
    dns: "root:password@/test"
    maxConnections: 10
    maxLifetime: 10 # in minutes
  psql:
    dns: "root:password@/test?timeout=5s"
  mongodb:
    dns: "mongodb://localhost:27017"
```