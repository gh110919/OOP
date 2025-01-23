### Information Expert (Информационный эксперт)

###### Присваивание ответственности тому объекту, который имеет наибольшие знания, необходимые для выполнения этой ответственности.

```ts
class Product {
  price: number;
  quantity: number;

  constructor(price: number, quantity: number) {
    this.price = price;
    this.quantity = quantity;
  }

  getTotalPrice(): number {
    return this.price * this.quantity;
  }
}

const product = new Product(10, 5);
console.log(product.getTotalPrice()); // Вывод: 50

/* Здесь объект Product является информационным экспертом для вычисления общей стоимости, так как он владеет всей необходимой информацией. */
```

### Creator (Создатель)

###### Присваивание ответственности за создание экземпляра класса тому классу, который имеет информацию о том, что нужно создать.

```ts
class Order {
  items: Product[] = [];

  addItem(product: Product) {
    this.items.push(product);
  }
}

const order = new Order();
const newProduct = new Product(10, 2);
order.addItem(newProduct);

/* Объект Order является создателем, так как он содержит элементы заказа и отвечает за их создание. */
```

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

### Pure Fabrication (Чистая фабрикация)

###### Создание класса, который не имеет реального аналога в предметной области, чтобы снизить связанность и повысить абстракцию.

```ts
class Logger {
  log(message: string) {
    console.log(`Log: ${message}`);
  }
}

class Order {
  private logger: Logger;

  constructor(logger: Logger) {
    this.logger = logger;
  }

  placeOrder() {
    this.logger.log("Order placed.");
    // Логика размещения заказа
  }
}

const logger = new Logger();
const order = new Order(logger);
order.placeOrder();

/* Здесь класс Logger создан для улучшения организации кода и уменьшения связанности. */
```

### Indirection (Опосредствование)

###### Введение посредника для уменьшения прямой связанности между классами или компонентами.

```ts
class Database {
  query(sql: string) {
    // Выполнение запроса
  }
}

class DataAccessLayer {
  private database: Database;

  constructor(database: Database) {
    this.database = database;
  }

  executeQuery(sql: string) {
    this.database.query(sql);
  }
}

const database = new Database();
const dataAccessLayer = new DataAccessLayer(database);
dataAccessLayer.executeQuery("SELECT * FROM users");

/* Здесь DataAccessLayer служит посредником между кодом и базой данных, уменьшая прямую связанность. */
```

### Protected Variations (Защищенные вариации)

###### Защита от изменений с помощью создания стабильных интерфейсов, которые изолируют части системы.

```ts
interface Database {
  query(sql: string): void;
}

class MySQLDatabase implements Database {
  query(sql: string): void {
    // Логика MySQL-запроса
  }
}

class PostgreSQLDatabase implements Database {
  query(sql: string): void {
    // Логика PostgreSQL-запроса
  }
}

class DataAccessLayer {
  private database: Database;

  constructor(database: Database) {
    this.database = database;
  }

  executeQuery(sql: string): void {
    this.database.query(sql);
  }
}

const mysqlDatabase = new MySQLDatabase();
const dataAccessLayer = new DataAccessLayer(mysqlDatabase);
dataAccessLayer.executeQuery("SELECT * FROM users");

// Позднее можем заменить MySQL на PostgreSQL, не изменяя DataAccessLayer
const postgreSQLDatabase = new PostgreSQLDatabase();
const newDataAccessLayer = new DataAccessLayer(postgreSQLDatabase);
newDataAccessLayer.executeQuery("SELECT * FROM products");

/* Здесь интерфейс Database защищает DataAccessLayer от изменений конкретных реализаций базы данных. */
```
