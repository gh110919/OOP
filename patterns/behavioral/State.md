### State (Состояние)

###### Позволяет объекту изменять своё поведение в зависимости от его внутреннего состояния.

```
Представьте себе светофор на перекрестке. 
В зависимости от текущего состояния (красный, желтый или зелёный свет) 
он изменяет своё поведение, регулируя движение транспорта. 
Когда горит красный свет, машины стоят; 
когда зелёный — едут; 
а когда желтый, они готовятся к остановке. 
Светофор меняет своё поведение в зависимости от своего состояния, 
обеспечивая порядок и безопасность на дороге.

В программировании паттерн "Состояние" работает аналогично: 
объект изменяет своё поведение в зависимости от его внутреннего состояния, 
обеспечивая гибкость и упрощая управление различными режимами работы
```

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
