### Инкапсуляция: Сокрытие внутренней реализации класса и предоставление публичного интерфейса для взаимодействия.

```ts
class BankAccount {
  private balance: number;
  constructor(initialBalance: number) {
    this.balance = initialBalance;
  }
  deposit(amount: number) {
    this.balance += amount;
  }
  getBalance(): number {
    return this.balance;
  }
}

const account = new BankAccount(1000);
account.deposit(500);
console.log(account.getBalance()); // Вывод: 1500
// account.balance; // Ошибка: свойство 'balance' приватное
```
