# Create migrations

You can use migrations to prepare your project’s tables and indexes. **Ensure that these operations can be executed multiple times since they run along with the application.**

To create a migrations, you can use the Liquor CLI to simplify the process. Use the following command:

```bash
liquor create migrate --name <migrateName>
```

eg:

```bash
liquor create migrate --name createUserTable
```

This command will generate the following files in your project:

`internal/adapters/database/migrations/create_user_table_migrate.go`

```go
package migrations

import (
    "github.com/uptrace/bun"
)
func createUserTableMigrate(db *bun.DB) {

}
```

and update the `internal/adapters/database/migrations/migrations.go` with registration

```go
package migrations

import "github.com/go-liquor/liquor/sdk/app"

var Migrations = app.RegisterMigrations(
    createUserTableMigrate,
//go:liquor:migrations
)
```

> The format of your migration file depends on the database driver you are using.
