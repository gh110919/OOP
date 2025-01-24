### Interface Polymorphism (Полиморфизм интерфейсов)

###### Использование полиморфизма для выполнения различных действий, основанных на типе объекта.

```
Представьте себе универсального мастера на все руки. 
Он может быть плотником, электриком, сантехником, 
и всё зависит от того, какие инструменты он берет в руки. 
Когда мастер берёт молоток, он становится плотником; 
когда берет разводной ключ, он становится сантехником; 
а если берет тестер, то становится электриком. 
В зависимости от ситуации он выполняет различные задачи, 
адаптируясь к нуждам. В программировании это аналогично полиморфизму, 
когда объект может изменять свое поведение 
в зависимости от используемого метода или интерфейса.
```

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
