### DIP: Dependency Inversion Principle (Принцип инверсии зависимостей)

### Модули верхнего уровня не должны зависеть от модулей нижнего уровня. Оба должны зависеть от абстракций.

###### Метафора: Строя дом, мы используем чертежи (абстракции), а не привязываемся к конкретным материалам. Это позволяет нам выбирать разные материалы, не меняя сам проект.

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
