### Inversion of Control (Инверсия управления)

###### Inversion of Control - это принцип, согласно которому управление объектами и зависимостями передается извне. Один из способов реализации IoC - через Dependency Injection.

```ts
interface Service {
  performAction(): void;
}

class ConcreteService implements Service {
  performAction() {
    console.log("Action performed.");
  }
}

class Client {
  private service: Service;

  constructor(service: Service) {
    this.service = service;
  }

  doSomething() {
    this.service.performAction();
  }
}

// Инверсия управления через интерфейс и внедрение зависимости
const service = new ConcreteService();
const client = new Client(service);
client.doSomething();
```
