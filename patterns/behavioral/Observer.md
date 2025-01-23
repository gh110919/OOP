### Observer (Наблюдатель)

###### Определяет зависимость "один ко многим" между объектами, так что при изменении состояния одного объекта все зависимые уведомляются и обновляются автоматически.

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
