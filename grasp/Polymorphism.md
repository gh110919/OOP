### Polymorphism (Полиморфизм)

###### Использование полиморфизма для выполнения различных действий, основанных на типе объекта.

```ts
interface PaymentMethod {
  pay(amount: number): void;
}

class CreditCardPayment implements PaymentMethod {
  pay(amount: number): void {
    console.log(`Оплата кредитной картой: ${amount}`);
  }
}

class PayPalPayment implements PaymentMethod {
  pay(amount: number): void {
    console.log(`Оплата через PayPal: ${amount}`);
  }
}

function processPayment(payment: PaymentMethod, amount: number) {
  payment.pay(amount);
}

const creditCardPayment = new CreditCardPayment();
processPayment(creditCardPayment, 100);

const payPalPayment = new PayPalPayment();
processPayment(payPalPayment, 150);

/* Здесь полиморфизм позволяет обрабатывать различные виды платежей через единый интерфейс PaymentMethod. */
```
