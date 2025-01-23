### Inversion of Control (Инверсия управления)

###### Inversion of Control - это принцип, согласно которому управление объектами и зависимостями передается извне. Один из способов реализации IoC - через Dependency Injection.

```
Inversion of Control (IoC) — это принцип проектирования 
в разработке программного обеспечения,
который перенимает контроль над выполнением программы 
от традиционного потока управления
и передает его структурам высокого уровня.
Основная цель IoC заключается в повышении модульности 
и тестируемости кода
путем устранения жестких связей между компонентами системы.

Суть IoC заключается в изменении порядка управления: 
не программа управляет процессом выполнения,
а контейнер или фреймворк управляет созданием 
и жизненным циклом объектов,
предоставлением зависимостей и вызовом методов.
Это достигается через внедрение зависимостей,
событийную обработку и использование контейнеров IoC.
```

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
