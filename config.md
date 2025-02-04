# Config

All application configurations should be stored in the config.yaml file.

> This file should not be committed to your repository, as it contains sensitive information. Instead, store it as a secret in your CI/CD provider to ensure security.

- [Access settings](#access-settings)
    - [Example](#example)
- [Reference](#reference)
    - [App](#app)
    - [Server HTTP](#serverhttp)
    - [Password](#password)
    - [Log](#log)
    - [Database](#database)

## Access settings

To access the configurations directly from your services or other functions, simply pass the config reference to the service.

```go
package services

import (
        "go.uber.org/zap"
        "github.com/go-liquor/liquor-sdk/config"
)

type OrderService struct {
        logger *zap.Logger
        cfg *config.Config
}

func NewOrderService(logger *zap.Logger, cfg *config.Config) *OrderService {
        return &OrderService{
                logger: logger,
                cfg: cfg
        }
}

func (o *OrderService) Run(ctx context.Context) {
    fmt.Println(o.cfg.GetString("app.name")) // My App
}
```

You can use functions like `GetString`, `GetInt`, `GetBool`, etc., to retrieve information from your configuration file. This allows you to create custom configurations and access them using helper methods.

To access a configuration value, navigate through the YAML nodes using "." as a separator.

### Example

```go
appName := config.GetString("app.name")
debugMode := config.GetBool("app.debug")
dbHost := config.GetString("my-redis.host")
dbPort := config.GetInt("my-redis.port")
current := config.GetString("my-redis.db.current")
```


```yaml
# config.yaml
app:
  name: "LiquorApp"
  debug: true

my-redis:
  host: "localhost"
  port: 5432
  db:
    current: yes
```



## Reference


```yaml
app:
  name: "My App"
  debug: true
  timezone: UTC
server:
  http:
    port: 8000
    cors:
      default: true
      origin:
        - "*"
      methods:
        - "GET"
        - "POST"
        - "PUT"
        - "DELETE"
        - "OPTIONS"
      headers:
        - "Origin"
        - "Authorization
        - "Content-Type"
      credentials: true
password:
  bcryptCost: 10
log:
  level: "info"
  format: "json"
database:
  sqlite:
    dns: "file::memory:?cache=shared"
  mysql:
    dns: "root:password@/test"
    maxConnections: 10
    maxLifetime: 10 # in minutes
  psql:
    dns: "root:password@/test?timeout=5s"
  mongodb:
    dns: "mongodb://localhost:27017"
```



### App

| Config | Type | Description |
|--------|--------|--------|
| app.name | `string` | The app name |
| app.debug | `bool` | Enable debug mode |
| app.timezone | `string` | Timezone |

### Server.Http

Here, you define your HTTP server configurations

| Config | Type | Description |
|--------|--------|--------|
| server.http.port | `int` |  Define the port where the HTTP server will start |
| server.http.cors.default | `bool` | When enabled, this setting defines the default CORS configuration (allows all origins, accepts all methods, and permits standard headers). **This configuration is not recommended for production.** |
| server.http.cors.origin | `[]string` | Define the list of origins allowed to make requests. |
| server.http.cors.methods | `[]string` | Define the list of methods http allowed to make requests. |
| server.http.cors.headers | `[]string` | Define the list of headers http allowed to make requests. |
| server.http.cors.credentials | `bool` | Define if allowed credentials |

### Password

Here, you define your Password configurations

| Config | Type | Description |
|--------|--------|--------|
| password.bcryptCost | `int` | Define the bcrypt cost to use methos bcrypt |


### Log

Here, you define the log configurations

| Config | Type | Description |
|--------|--------|--------|
| log.level | `string` | Define log level (debug, info, warn, error, panic, dpanic) |
| log.format | `string` | Define log output format (console, json). To production we recommendate `json` |

### Database

Here, you define the database configurations

| Config | Type | Description |
|--------|--------|--------|
| database.sqlite.dns | `string` | DNS to access sqlite |
| database.mysql.dns | `string` | DNS connection mysql |
| database.mysql.maxConnections | `int` |  Is highly recommended to limit the number of connection used by the application. There is no recommended limit number because it depends on application and MySQL server. |
| database.mysql.maxLifetime | `int` | Is required to ensure connections are closed by the driver safely before connection is closed by MySQL server, OS, or other middlewares. The value is in minutes |
| database.postgres.dns | `string` | DNS connection postgres |
| database.mongodb.dns | `string` | DNS connection mongodb | 

