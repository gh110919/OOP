### Pure Fabrication (Чистая фабрикация)

###### Создание класса, который не имеет реального аналога в предметной области, чтобы снизить связанность и повысить абстракцию.

```ts
class Logger {
  log(message: string) {
    console.log(`Log: ${message}`);
  }
}

class Order {
  private logger: Logger;

  constructor(logger: Logger) {
    this.logger = logger;
  }

  placeOrder() {
    this.logger.log("Order placed.");
    // Логика размещения заказа
  }
}

const logger = new Logger();
const order = new Order(logger);
order.placeOrder();

/* Здесь класс Logger создан для улучшения организации кода и уменьшения связанности. */
```
