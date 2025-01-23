```txt
Метафора: Представь, что ООП — это организация твоей виртуальной команды. Каждый класс — это роль в команде (например, разработчик, дизайнер), объекты — конкретные сотрудники, наследование — обучение новых сотрудников на основе опыта старых, а инкапсуляция — личные навыки, которые они не раскрывают полностью.
```

```txt
Классы и объекты: Класс — это шаблон, по которому создаются объекты с определенными свойствами и методами.
```

```ts
class Person {
  name: string;
  constructor(name: string) {
    this.name = name;
  }
  greet() {
    console.log(`Привет, меня зовут ${this.name}`);
  }
}

const user = new Person("Алексей");
user.greet(); // Вывод: Привет, меня зовут Алексей
```

```txt
 Абстракция: Выделение значимой информации и игнорирование деталей. В TypeScript реализуется через абстрактные классы и интерфейсы.
```

```ts
interface Drawable {
  draw(): void;
}

class Square implements Drawable {
  draw() {
    console.log("Рисуем квадрат");
  }
}

class Triangle implements Drawable {
  draw() {
    console.log("Рисуем треугольник");
  }
}

const figures: Drawable[] = [new Square(), new Triangle()];
figures.forEach((figure) => figure.draw());
// Вывод: Рисуем квадрат
// Вывод: Рисуем треугольник
```

```txt
Инкапсуляция: Сокрытие внутренней реализации класса и предоставление публичного интерфейса для взаимодействия.
```

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

```txt
Полиморфизм: Способность объектов разного класса реагировать на одинаковые сообщения по-разному.
```

```ts
class Shape {
  area(): number {
    return 0;
  }
}

class Circle extends Shape {
  radius: number;
  constructor(radius: number) {
    super();
    this.radius = radius;
  }
  area(): number {
    return Math.PI * this.radius ** 2;
  }
}

class Rectangle extends Shape {
  width: number;
  height: number;
  constructor(width: number, height: number) {
    super();
    this.width = width;
    this.height = height;
  }
  area(): number {
    return this.width * this.height;
  }
}

const shapes: Shape[] = [new Circle(5), new Rectangle(4, 6)];
shapes.forEach((shape) => console.log(shape.area()));
// Вывод: 78.53981633974483 и 24
```

```txt
Наследование: Позволяет создавать новые классы на основе существующих, наследуя их свойства и методы.
```

```ts
class Employee extends Person {
  position: string;
  constructor(name: string, position: string) {
    super(name);
    this.position = position;
  }
  work() {
    console.log(`${this.name} работает как ${this.position}`);
  }
}

const employee = new Employee("Мария", "инженер");
employee.greet(); // Привет, меня зовут Мария
employee.work(); // Мария работает как инженер
```
