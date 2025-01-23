### Dependency Injection (Внедрение зависимостей)

###### Dependency Injection - это способ предоставления зависимостей объектам. Он позволяет улучшить тестируемость и уменьшить связанность кода.

```ts
class Engine {
  start() {
    console.log("Engine started.");
  }
}

class Car {
  private engine: Engine;

  constructor(engine: Engine) {
    this.engine = engine;
  }

  drive() {
    this.engine.start();
    console.log("Car is driving.");
  }
}

// Внедрение зависимости через конструктор
const engine = new Engine();
const car = new Car(engine);
car.drive();
```
