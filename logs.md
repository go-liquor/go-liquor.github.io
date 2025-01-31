# Logs

Liquor uses [uber/zap](https://github.com/go-uber/zap) as its logging library. To learn more about Zap, check out the official documentation here: [Zap Documentation](https://pkg.go.dev/go.uber.org/zap).

You can configure how logs will work in your application by modifying the settings in the config.yaml file:

```yaml
# config.yaml
log:
  level: "info" # define log level 
  format: "json" # define output log (console, json)
```


## Examples of Usage

```go
type OrderService struct {
        logger *zap.Logger
        repo ports.OrderRepository
}

func NewOrderService(logger *zap.Logger, repo ports.OrderRepository) *OrderService {
        return &OrderService{
                logger: logger,
                repo: repo,
        }
}


func (o *OrderService) Create(ctx context.Context, order *domain.Order) error {
    o.logger.Info("Example logger",zap.String("name", order.Name))
    // Creating a group of logs with param name
    lg := o.logger.With(zap.String("name", order.Name))
    lg.Info("creating an order service")
    if err := o.repo.Create(ctx, order); err != nil {
        lg.Error("error to create order", zap.Error(err))
        return err
    }
    lg.Info("order created")
    return nil
}
```