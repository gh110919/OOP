### ISP: Interface Segregation Principle (Принцип разделения интерфейса)

### Многие специализированные интерфейсы лучше, чем один универсальный.

###### Метафора: В ресторане для клиентов предлагается меню, а для поваров — рецепт. Нет смысла заставлять клиента читать рецепт приготовления блюда.

```ts
/* Плохой пример: */
interface MultifunctionalDevice {
  print(): void;
  scan(): void;
  fax(): void;
}

class OldPrinter implements MultifunctionalDevice {
  print(): void {
    // Печать
  }

  scan(): void {
    throw new Error("Сканирование не поддерживается");
  }

  fax(): void {
    throw new Error("Факс не поддерживается");
  }
}

/* Хороший пример: */
interface Printer {
  print(): void;
}

interface Scanner {
  scan(): void;
}

interface Fax {
  fax(): void;
}

class SimplePrinter implements Printer {
  print(): void {
    // Печать
  }
}

/* Теперь SimplePrinter реализует только необходимые ему методы. */
```
