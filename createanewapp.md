# Create a new app

To create your first app, you can use the following command: 

```bash
liquor app create --name <app-name> --pkg <app-package>
```

When you create a new app, you get a fully prepared boilerplate for a web application, including a server, logger, and configuration file ready to use.

Copy the config.example.yaml file to config.yaml to set up the initial configuration for your application.

> Important: The config.yaml file should not be included in your repository, as it contains sensitive information about your application.

```bash
cp config.example.yaml config.yaml
```

Run your application using the initial configurations.

```bash
go run cmd/app/main.go
```
