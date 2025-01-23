### Controller (Контроллер)

###### Присваивание ответственности за обработку системных событий центральному контроллеру, который координирует действия.

```ts
class OrderController {
  placeOrder(order: Order) {
    // Логика размещения заказа
  }
}

const controller = new OrderController();
controller.placeOrder(order);

/* Объект OrderController координирует действия при размещении заказа. */
```
