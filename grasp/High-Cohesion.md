### High Cohesion (Высокая связность)

###### Поддерживать классы с высоким уровнем связности, что означает выполнение тесно связанных задач.

```ts
class Product {
  price: number;
  quantity: number;

  constructor(price: number, quantity: number) {
    this.price = price;
    this.quantity = quantity;
  }

  calculateTotalPrice(): number {
    return this.price * this.quantity;
  }
}

/* Здесь класс Product имеет высокую связность, выполняя только задачи, связанные с продуктом. */
```
