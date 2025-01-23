### Chain of Responsibility (Цепочка обязанностей)

###### Позволяет передавать запрос последовательно по цепочке обработчиков. Каждый обработчик решает, может ли он обработать запрос или передать его дальше.

```ts
class Handler {
  private nextHandler: Handler | null = null;

  setNext(handler: Handler): Handler {
    this.nextHandler = handler;
    return handler;
  }

  handle(request: string): void {
    if (this.nextHandler) {
      this.nextHandler.handle(request);
    }
  }
}

class ConcreteHandler1 extends Handler {
  handle(request: string): void {
    if (request === "Request1") {
      console.log("ConcreteHandler1 handled the request.");
    } else {
      super.handle(request);
    }
  }
}

// Использование
const handler1 = new ConcreteHandler1();
const handler2 = new Handler();
handler1.setNext(handler2);

handler1.handle("Request1"); // ConcreteHandler1 handled the request.
```

### Command (Команда)

###### Инкапсулирует запрос в объект, позволяя параметризовать клиентов с различными запросами и поддерживать операции отмены.

```ts
class Command {
  execute(): void {}
}

class ConcreteCommand extends Command {
  private receiver: Receiver;

  constructor(receiver: Receiver) {
    super();
    this.receiver = receiver;
  }

  execute(): void {
    this.receiver.action();
  }
}

class Receiver {
  action(): void {
    console.log("Receiver action executed.");
  }
}

class Invoker {
  private command: Command;

  setCommand(command: Command): void {
    this.command = command;
  }

  invoke(): void {
    this.command.execute();
  }
}

// Использование
const receiver = new Receiver();
const command = new ConcreteCommand(receiver);
const invoker = new Invoker();

invoker.setCommand(command);
invoker.invoke(); // Receiver action executed.
```

### Iterator (Итератор)

###### Предоставляет способ последовательного доступа ко всем элементам коллекции без раскрытия её внутреннего представления.

```ts
interface Iterator<T> {
  next(): T | null;
  hasNext(): boolean;
}

class ConcreteIterator<T> implements Iterator<T> {
  private collection: T[];
  private position: number = 0;

  constructor(collection: T[]) {
    this.collection = collection;
  }

  next(): T | null {
    if (this.hasNext()) {
      return this.collection[this.position++];
    }
    return null;
  }

  hasNext(): boolean {
    return this.position < this.collection.length;
  }
}

// Использование
const collection = [1, 2, 3];
const iterator = new ConcreteIterator(collection);

while (iterator.hasNext()) {
  console.log(iterator.next()); // 1 2 3
}
```

### Interpreter (Интерпретатор)

###### Определяет грамматику представления и интерпретатор для обработки запросов.

```ts
interface Expression {
  interpret(context: string): boolean;
}

class TerminalExpression implements Expression {
  private data: string;

  constructor(data: string) {
    this.data = data;
  }

  interpret(context: string): boolean {
    return context.includes(this.data);
  }
}

class OrExpression implements Expression {
  private expr1: Expression;
  private expr2: Expression;

  constructor(expr1: Expression, expr2: Expression) {
    this.expr1 = expr1;
    this.expr2 = expr2;
  }

  interpret(context: string): boolean {
    return this.expr1.interpret(context) || this.expr2.interpret(context);
  }
}

// Использование
const expr1 = new TerminalExpression("Hello");
const expr2 = new TerminalExpression("World");
const orExpr = new OrExpression(expr1, expr2);

console.log(orExpr.interpret("Hello there!")); // true
```

### Mediator (Посредник)

###### Определяет объект, инкапсулирующий способ взаимодействия множества объектов.

```ts
class Mediator {
  notify(sender: object, event: string): void {}
}

class ConcreteMediator extends Mediator {
  private component1: Component1;
  private component2: Component2;

  constructor(c1: Component1, c2: Component2) {
    super();
    this.component1 = c1;
    this.component1.setMediator(this);
    this.component2 = c2;
    this.component2.setMediator(this);
  }

  notify(sender: object, event: string): void {
    if (event === "A") {
      this.component2.doC();
    }
  }
}

class Component {
  protected mediator: Mediator;

  setMediator(mediator: Mediator): void {
    this.mediator = mediator;
  }
}

class Component1 extends Component {
  doA(): void {
    this.mediator.notify(this, "A");
  }
}

class Component2 extends Component {
  doC(): void {
    console.log("Component2 does C.");
  }
}

// Использование
const c1 = new Component1();
const c2 = new Component2();
const mediator = new ConcreteMediator(c1, c2);

c1.doA(); // Component2 does C.
```

### Memento (Хранитель)

###### Позволяет сохранять и восстанавливать внутреннее состояние объекта без нарушения инкапсуляции.

```ts
class Memento {
  private state: string;

  constructor(state: string) {
    this.state = state;
  }

  getState(): string {
    return this.state;
  }
}

class Originator {
  private state: string;

  setState(state: string): void {
    this.state = state;
    console.log(`State set to: ${state}`);
  }

  saveStateToMemento(): Memento {
    return new Memento(this.state);
  }

  getStateFromMemento(memento: Memento): void {
    this.state = memento.getState();
    console.log(`State restored to: ${this.state}`);
  }
}

class Caretaker {
  private mementos: Memento[] = [];

  add(memento: Memento): void {
    this.mementos.push(memento);
  }

  get(index: number): Memento {
    return this.mementos[index];
  }
}

// Использование
const originator = new Originator();
const caretaker = new Caretaker();

originator.setState("State1");
caretaker.add(originator.saveStateToMemento());

originator.setState("State2");
caretaker.add(originator.saveStateToMemento());

originator.setState("State3");

originator.getStateFromMemento(caretaker.get(0)); // State restored to: State1
originator.getStateFromMemento(caretaker.get(1)); // State restored to: State2
```

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

### Strategy (Стратегия)

###### Определяет семейство алгоритмов, инкапсулирует каждый из них и делает их взаимозаменяемыми.

```ts
class Context {
  private strategy: Strategy;

  setStrategy(strategy: Strategy): void {
    this.strategy = strategy;
  }

  executeStrategy(): void {
    this.strategy.doAlgorithm();
  }
}

interface Strategy {
  doAlgorithm(): void;
}

class ConcreteStrategyA implements Strategy {
  doAlgorithm(): void {
    console.log("Strategy A executed.");
  }
}

class ConcreteStrategyB implements Strategy {
  doAlgorithm(): void {
    console.log("Strategy B executed.");
  }
}

// Использование
const context = new Context();

context.setStrategy(new ConcreteStrategyA());
context.executeStrategy(); // Strategy A executed.

context.setStrategy(new ConcreteStrategyB());
context.executeStrategy(); // Strategy B executed.
```

### Template Method (Шаблонный метод)

###### Определяет скелет алгоритма, позволяя подклассам переопределять отдельные шаги алгоритма без изменения его структуры.

```ts
abstract class AbstractClass {
  templateMethod(): void {
    this.baseOperation1();
    this.requiredOperations1();
    this.baseOperation2();
    this.hook1();
    this.requiredOperations2();
    this.baseOperation3();
    this.hook2();
  }

  baseOperation1(): void {
    console.log("AbstractClass says: I am doing the bulk of the work.");
  }

  baseOperation2(): void {
    console.log(
      "AbstractClass says: But I let subclasses override some operations."
    );
  }

  baseOperation3(): void {
    console.log("AbstractClass says: And I am doing the rest of the work.");
  }

  protected abstract requiredOperations1(): void;
  protected abstract requiredOperations2(): void;

  hook1(): void {}
  hook2(): void {}
}

class ConcreteClass extends AbstractClass {
  requiredOperations1(): void {
    console.log("ConcreteClass says: Implemented Operation1.");
  }

  requiredOperations2(): void {
    console.log("ConcreteClass says: Implemented Operation2.");
  }

  hook1(): void {
    console.log("ConcreteClass says: Overridden Hook1.");
  }
}

// Использование
const concreteClass = new ConcreteClass();
concreteClass.templateMethod();
```

### Visitor (Посетитель)

###### Позволяет добавлять в класс новые операции, не изменяя его.

```ts
interface Visitor {
  visitConcreteElementA(element: ConcreteElementA): void;
  visitConcreteElementB(element: ConcreteElementB): void;
}

interface Element {
  accept(visitor: Visitor): void;
}

class ConcreteElementA implements Element {
  accept(visitor: Visitor): void {
    visitor.visitConcreteElementA(this);
  }

  operationA(): void {
    console.log("ConcreteElementA operation.");
  }
}

class ConcreteElementB implements Element {
  accept(visitor: Visitor): void {
    visitor.visitConcreteElementB(this);
  }

  operationB(): void {
    console.log("ConcreteElementB operation.");
  }
}

class ConcreteVisitor implements Visitor {
  visitConcreteElementA(element: ConcreteElementA): void {
    console.log("Visitor is processing ConcreteElementA.");
    element.operationA();
  }

  visitConcreteElementB(element: ConcreteElementB): void {
    console.log("Visitor is processing ConcreteElementB.");
    element.operationB();
  }
}

// Использование
const elements: Element[] = [new ConcreteElementA(), new ConcreteElementB()];
const visitor = new ConcreteVisitor();

for (const element of elements) {
  element.accept(visitor);
}
```
