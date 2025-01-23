### Adapter (Адаптер)

###### Адаптер позволяет объектам с несовместимыми интерфейсами работать вместе. Он оборачивает один из объектов, адаптируя его интерфейс к нужному.

```ts
class OldSystem {
  public specificRequest(): string {
    return "Old system behavior";
  }
}

class NewSystem {
  request(): string {
    return "New system behavior";
  }
}

class Adapter implements NewSystem {
  private oldSystem: OldSystem;

  constructor(oldSystem: OldSystem) {
    this.oldSystem = oldSystem;
  }

  public request(): string {
    return this.oldSystem.specificRequest();
  }
}

const oldSystem = new OldSystem();
const adapter = new Adapter(oldSystem);
console.log(adapter.request()); // "Old system behavior"
```

### Bridge (Мост)

###### Мост разделяет абстракцию и реализацию, позволяя их изменять независимо друг от друга.

```ts
interface Device {
  isEnabled(): boolean;
  enable(): void;
  disable(): void;
}

class TV implements Device {
  private on = false;

  isEnabled(): boolean {
    return this.on;
  }

  enable(): void {
    this.on = true;
  }

  disable(): void {
    this.on = false;
  }
}

class Remote {
  protected device: Device;

  constructor(device: Device) {
    this.device = device;
  }

  togglePower(): void {
    if (this.device.isEnabled()) {
      this.device.disable();
    } else {
      this.device.enable();
    }
  }
}

const tv = new TV();
const remote = new Remote(tv);
remote.togglePower();
console.log(tv.isEnabled()); // true
```

### Composite (Компоновщик)

###### Компоновщик позволяет сгруппировать объекты в древовидную структуру и работать с ними так, как с единичными объектами.

```ts
interface Component {
  operation(): string;
}

class Leaf implements Component {
  operation(): string {
    return "Leaf";
  }
}

class Composite implements Component {
  private children: Component[] = [];

  public add(component: Component): void {
    this.children.push(component);
  }

  public operation(): string {
    return `Branch(${this.children
      .map((child) => child.operation())
      .join("+")})`;
  }
}

const leaf = new Leaf();
const tree = new Composite();
tree.add(leaf);
tree.add(leaf);
console.log(tree.operation()); // "Branch(Leaf+Leaf)"
```

### Decorator (Декоратор)

###### Декоратор динамически добавляет новое поведение объектам, оборачивая их.

```ts
interface Coffee {
  cost(): number;
  description(): string;
}

class SimpleCoffee implements Coffee {
  cost(): number {
    return 5;
  }
  description(): string {
    return "Simple coffee";
  }
}

class MilkDecorator implements Coffee {
  private coffee: Coffee;

  constructor(coffee: Coffee) {
    this.coffee = coffee;
  }

  cost(): number {
    return this.coffee.cost() + 2;
  }

  description(): string {
    return this.coffee.description() + ", milk";
  }
}

let myCoffee = new SimpleCoffee();
myCoffee = new MilkDecorator(myCoffee);
console.log(myCoffee.description()); // "Simple coffee, milk"
console.log(myCoffee.cost()); // 7
```

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

### Flyweight (Приспособленец)

###### Приспособленец уменьшает затраты на создание большого количества однотипных объектов, делая их разделяемыми.

```ts
class Flyweight {
  private sharedState: string;

  constructor(sharedState: string) {
    this.sharedState = sharedState;
  }

  operation(uniqueState: string): void {
    console.log(
      `Flyweight: Displaying shared (${this.sharedState}) and unique (${uniqueState}) state.`
    );
  }
}

class FlyweightFactory {
  private flyweights: { [key: string]: Flyweight } = {};

  getFlyweight(sharedState: string): Flyweight {
    if (!(sharedState in this.flyweights)) {
      this.flyweights[sharedState] = new Flyweight(sharedState);
    }
    return this.flyweights[sharedState];
  }
}

const factory = new FlyweightFactory();
const flyweight1 = factory.getFlyweight("shared");
flyweight1.operation("unique1");

const flyweight2 = factory.getFlyweight("shared");
flyweight2.operation("unique2");
```

### Proxy (Заместитель)

###### Заместитель предоставляет объект, который контролирует доступ к другому объекту, перехватывая все вызовы.

```ts
interface Subject {
  request(): void;
}

class RealSubject implements Subject {
  request(): void {
    console.log("RealSubject: Handling request.");
  }
}

class ProxySubject implements Subject {
  private realSubject: RealSubject;

  constructor(realSubject: RealSubject) {
    this.realSubject = realSubject;
  }

  request(): void {
    console.log("Proxy: Checking access before forwarding request.");
    this.realSubject.request();
    console.log("Proxy: Logging request.");
  }
}

const realSubject = new RealSubject();
const proxy = new ProxySubject(realSubject);
proxy.request();
// "Proxy: Checking access before forwarding request."
// "RealSubject: Handling request."
// "Proxy: Logging request."
```
