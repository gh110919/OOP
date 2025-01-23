### Fasade (Фасад)

###### Фасад предоставляет упрощённый интерфейс к сложной системе классов, библиотеке или фреймворку.

```ts
class Subsystem1 {
  operation1(): string {
    return "Subsystem1: Ready!";
  }
}

class Subsystem2 {
  operation2(): string {
    return "Subsystem2: Go!";
  }
}

class Facade {
  private subsystem1: Subsystem1;
  private subsystem2: Subsystem2;

  constructor() {
    this.subsystem1 = new Subsystem1();
    this.subsystem2 = new Subsystem2();
  }

  operation(): string {
    return `${this.subsystem1.operation1()} ${this.subsystem2.operation2()}`;
  }
}

const facade = new Facade();
console.log(facade.operation()); // "Subsystem1: Ready! Subsystem2: Go!"
```
