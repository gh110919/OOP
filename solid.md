```txt
SRP: Single Responsibility Principle (Принцип единственной ответственности)
```

```txt
Класс должен иметь только одну причину для изменения.
```

```txt
Метафора: Представь, что у тебя есть швейцарский нож с множеством инструментов. Он удобен, но если тебе нужно починить только отвертку, придется разбирать весь нож. Гораздо эффективнее иметь отдельные инструменты для каждой задачи.
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

```txt
OCP: Open-Closed Principle (Принцип открытости/закрытости)
```

```txt
Код должен быть открыт для расширения, но закрыт для изменения.
```

```txt
Метафора: Подумай о розетке в стене. Она позволяет подключать разные устройства без изменения самой розетки. Мы можем расширять функциональность, не трогая исходный код.
```

```ts
/* Базовый класс: */
abstract class Shape {
  abstract area(): number;
}

/* Расширение функционала: */
class Circle extends Shape {
  constructor(private radius: number) {
    super();
  }

  area(): number {
    return Math.PI * this.radius ** 2;
  }
}

class Rectangle extends Shape {
  constructor(private width: number, private height: number) {
    super();
  }

  area(): number {
    return this.width * this.height;
  }
}

/* Мы можем добавлять новые фигуры, не изменяя базовый класс Shape. */
```

```txt
LSP: Liskov Substitution Principle (Принцип подстановки Барбары Лисков)
```

```txt
Объекты должны быть заменяемы на экземпляры их подтипов без изменения корректности программы.
```

```txt
Метафора: Если у тебя есть автомобиль, ты можешь заменить его на другой автомобиль, и он все равно будет выполнять свои функции. Но если ты заменишь его на велосипед, ожидая той же функциональности, возникнут проблемы.
```

```ts
/* Пример нарушения принципа: */
class Bird {
  fly(): void {
    console.log("Птица летит");
  }
}

class Ostrich extends Bird {
  fly(): void {
    throw new Error("Страусы не умеют летать");
  }
}

function makeBirdFly(bird: Bird) {
  bird.fly();
}

const ostrich = new Ostrich();
makeBirdFly(ostrich); // Ошибка во время выполнения

/* Исправление: */
class Bird {
  // Общие свойства птиц
}

interface FlyingBird {
  fly(): void;
}

class Sparrow extends Bird implements FlyingBird {
  fly(): void {
    console.log("Воробей летит");
  }
}

class Ostrich extends Bird {
  // Страус не реализует интерфейс FlyingBird
}

function makeBirdFly(bird: FlyingBird) {
  bird.fly();
}

const sparrow = new Sparrow();
makeBirdFly(sparrow); // Воробей летит
makeBirdFly(new Ostrich()); // Ошибка на этапе компиляции

/* Теперь невозможно передать нелетающую птицу в функцию, которая ожидает летающую. */
```

```txt
ISP: Interface Segregation Principle (Принцип разделения интерфейса)
```

```txt
Многие специализированные интерфейсы лучше, чем один универсальный.
```

```txt
Метафора: В ресторане для клиентов предлагается меню, а для поваров — рецепт. Нет смысла заставлять клиента читать рецепт приготовления блюда.
```

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

```txt
DIP: Dependency Inversion Principle (Принцип инверсии зависимостей)
```

```txt
Модули верхнего уровня не должны зависеть от модулей нижнего уровня. Оба должны зависеть от абстракций.
```

```txt
Метафора: Строя дом, мы используем чертежи (абстракции), а не привязываемся к конкретным материалам. Это позволяет нам выбирать разные материалы, не меняя сам проект.
```

```ts
/* Пример зависимости от конкретного класса: */
class MySQLDatabase {
  connect(): void {
    // Подключение к MySQL
  }
}

class UserService {
  private db: MySQLDatabase;

  constructor() {
    this.db = new MySQLDatabase();
  }

  getUser(id: number): void {
    this.db.connect();
    // Получение пользователя из базы данных
  }
}

/* Исправленный пример с инверсией зависимостей: */
interface Database {
  connect(): void;
}

class MySQLDatabase implements Database {
  connect(): void {
    // Подключение к MySQL
  }
}

class PostgreSQLDatabase implements Database {
  connect(): void {
    // Подключение к PostgreSQL
  }
}

class UserService {
  constructor(private db: Database) {}

  getUser(id: number): void {
    this.db.connect();
    // Получение пользователя из базы данных
  }
}

const userService = new UserService(new MySQLDatabase());
userService.getUser(1);

/* Теперь UserService не зависит от конкретной реализации базы данных и может работать с любой, соответствующей интерфейсу Database. */
```
