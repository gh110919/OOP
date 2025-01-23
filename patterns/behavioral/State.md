### State (Состояние)

###### Позволяет объекту изменять своё поведение в зависимости от его внутреннего состояния.

```ts
class Context {
  private state: State;

  constructor(state: State) {
    this.transitionTo(state);
  }

  transitionTo(state: State): void {
    console.log(`Transition to ${state.constructor.name}.`);
    this.state = state;
    this.state.setContext(this);
  }

  request(): void {
    this.state.handle();
  }
}

abstract class State {
  protected context: Context;

  setContext(context: Context): void {
    this.context = context;
  }

  abstract handle(): void;
}

class ConcreteStateA extends State {
  handle(): void {
    console.log("ConcreteStateA handles request.");
    this.context.transitionTo(new ConcreteStateB());
  }
}

class ConcreteStateB extends State {
  handle(): void {
    console.log("ConcreteStateB handles request.");
    this.context.transitionTo(new ConcreteStateA());
  }
}

// Использование
const context = new Context(new ConcreteStateA());
context.request(); // ConcreteStateA handles request.
context.request(); // ConcreteStateB handles request.
```
