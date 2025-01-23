### Low Coupling (Низкая связанность)

###### Минимизировать зависимость одного класса от другого, чтобы изменения в одном классе не затрагивали другие.

```ts
class Payment {
  processPayment(amount: number) {
    // Логика обработки платежа
  }
}

class Order {
  payment: Payment;

  constructor(payment: Payment) {
    this.payment = payment;
  }

  checkout(amount: number) {
    this.payment.processPayment(amount);
  }
}

const payment = new Payment();
const order = new Order(payment);
order.checkout(100);

/* Здесь класс Order зависит от абстракции Payment, что уменьшает связанность. */
```
