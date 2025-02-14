# Create a new resource

The Liquor framework provides a CLI command to automatically generate all the necessary files for a new resource.

## Table of Contents
- [Command Structure](#command-structure)
- [Example Usage](#example-usage)
- [Generated Files](#generated-files)
- [File Descriptions](#file-descriptions)
  - [Database Layer](#database-layer)
  - [HTTP Layer](#http-layer)
  - [Domain Layer](#domain-layer)
  - [Service Layer](#service-layer)
  - [Application Layer](#application-layer)



## Command Structure

```bash
liquor create resource --name <name> --group <api_group>
```


## Example Usage

```bash
liquor create resource --name users
```

This command will automatically generate:

```plaintext
├── app/
│   ├── adapters/
│   │   └── database/
│   │   │   └── migrations/
│   │   │   │   └── user_migration.go         # Database schema and migrations
│   │   │   └── repositories/
│   │   │   │   └── users_repository.go       # Database operations implementation
│   │   └── server/
│   │   │   └── rest/
│   │   │   │   └── middleware.go             # HTTP middleware functions
│   │   │   │   └── module.go                 # Module configuration and setup
│   │   │   │   └── users_handler.go          # HTTP request handlers
│   │   │   │   └── users_route.go            # Route definitions and configurations
│   ├── domain/
│   │   └── entity/
│   │   │   │   └── users.go                  # Domain model and business rules
│   │   └── ports/
│   │   │   │   └── users_repository.go       # Repository interface definition
│   ├── services/
│   │   └── users.go                          # Business logic implementation
│   ├── users_app.go                          # Application setup and initialization
```


## File Descriptions

### Database Layer
- **user_migration.go**: Contains database schema definitions and migrations for the users table. This file defines the structure of your data in the database.

- **users_repository.go**: Implements the actual database operations. This includes methods for creating, reading, updating, and deleting user records in the database.

### HTTP Layer
- **middleware.go**: Contains HTTP middleware functions for request processing, such as authentication, logging, and error handling.

- **module.go**: Configures and sets up the module, including dependency injection and module initialization.

- **users_handler.go**: Implements HTTP request handlers that process incoming requests and return responses. This includes input validation and response formatting.

- **users_route.go**: Defines API routes and their corresponding handlers, including HTTP methods and URL patterns.

### Domain Layer
- **users.go**: Defines the user entity and its behavior, including validation rules and business logic specific to the user domain.

- **users_repository.go** (in ports): Defines the interface for the repository layer, specifying what operations are available for user data manipulation.

### Service Layer
- **users.go**: Implements the business logic for user-related operations, coordinating between the repository and domain layers.

### Application Layer
- **users_app.go**: Sets up and initializes the user module, including dependency injection and configuration.
