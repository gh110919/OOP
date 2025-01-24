### Fasade (Фасад)

###### Фасад предоставляет упрощённый интерфейс к сложной системе классов, библиотеке или фреймворку.

```
Представьте себе большой театр с множеством залов, сцен и помещений для репетиций. 
Если каждый зритель будет пытаться сам найти нужное помещение, 
это может стать настоящим хаосом. 
Вместо этого у театра есть главный вход с вестибюлем и билетной кассой, 
где вам помогают ориентироваться и направляют в нужное место.

В программировании паттерн "Фасад" работает аналогично: 
он предоставляет упрощённый интерфейс для взаимодействия с комплексной системой, 
скрывая все её внутренние детали и делая использование системы проще и удобнее. 
Театр остаётся сложным и многоуровневым, 
но зрителям предоставляется простой 
и понятный способ получить доступ 
к нужным услугам.
```

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
