### Наследование: Позволяет создавать новые классы на основе существующих, наследуя их свойства и методы.

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
