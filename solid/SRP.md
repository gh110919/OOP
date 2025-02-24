### SRP: Single Responsibility Principle (Принцип единственной ответственности)

###### Каждый класс должен иметь только одну причину для изменения.

```
Представьте себе библиотеку, 
где каждый книжный шкаф предназначен только для одного жанра: 
один для детективов, другой для фантастики, третий для научной литературы и так далее. 
Когда нужно пополнить коллекцию, 
добавляется новый раздел в соответствующий шкаф, 
не затрагивая другие. 
Например, добавление новой книги в раздел детективов 
не повлияет на полки с фантастикой или научной литературой. 
Так и в программировании: каждый класс должен отвечать только за одну задачу, 
и изменения должны касаться только этой задачи, 
не затрагивая другие части системы.
```

```ts
/* Плохой подход: */
class Employee {
  calculatePay(): number {
    // Логика расчета зарплаты
  }

  saveToDatabase(): void {
    // Логика сохранения в базу данных
  }

  generateReport(): string {
    // Логика генерации отчета
  }
}

/* Хороший подход: */
class Employee {
  // Свойства сотрудника
}

class PaymentCalculator {
  calculate(employee: Employee): number {
    // Логика расчета зарплаты
  }
}

class EmployeeRepository {
  save(employee: Employee): void {
    // Логика сохранения в базу данных
  }
}

class ReportGenerator {
  generate(employee: Employee): string {
    // Логика генерации отчета
  }
}

/* Теперь каждый класс отвечает за свою задачу, и изменения в одном классе не затронут другие. */
```
