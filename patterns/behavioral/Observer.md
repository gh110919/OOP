### Observer (Наблюдатель)

###### Определяет зависимость "один ко многим" между объектами, так что при изменении состояния одного объекта все зависимые уведомляются и обновляются автоматически.

```
Представьте себе группу друзей, 
которые подписаны на новости друг друга в социальных сетях. 
Когда один из друзей публикует новую фотографию или обновляет свой статус, 
все подписчики автоматически получают уведомление об этом событии. 
Каждый из них может сразу увидеть обновление и отреагировать на него.

В программировании паттерн "Наблюдатель" работает аналогично: 
один объект (наблюдаемый) изменяет свое состояние, 
и все зависимые объекты (наблюдатели) автоматически уведомляются 
и обновляются в ответ на это изменение. 
Это позволяет синхронизировать состояние различных частей 
системы без необходимости явного оповещения каждого объекта.
```

```ts
class Subject {
  private observers: Observer[] = [];

  attach(observer: Observer): void {
    this.observers.push(observer);
  }

  detach(observer: Observer): void {
    this.observers = this.observers.filter((obs) => obs !== observer);
  }

  notify(): void {
    for (const observer of this.observers) {
      observer.update();
    }
  }
}

class ConcreteSubject extends Subject {
  private state: number;

  setState(state: number): void {
    this.state = state;
    this.notify();
  }

  getState(): number {
    return this.state;
  }
}

interface Observer {
  update(): void;
}

class ConcreteObserver implements Observer {
  private subject: ConcreteSubject;

  constructor(subject: ConcreteSubject) {
    this.subject = subject;
    this.subject.attach(this);
  }

  update(): void {
    console.log(`Observer updated with state: ${this.subject.getState()}`);
  }
}

// Использование
const subject = new ConcreteSubject();
const observer1 = new ConcreteObserver(subject);
const observer2 = new ConcreteObserver(subject);

subject.setState(1); // Observer updated with state: 1 (два раза)
```
