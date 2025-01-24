### Mediator (Посредник)

###### Определяет объект, инкапсулирующий способ взаимодействия множества объектов.

```
Представьте себе дирижёра оркестра. 
У каждого музыканта есть своё место и партия, 
которую он должен исполнять, 
но они не взаимодействуют напрямую друг с другом. 
Вместо этого, дирижёр управляет каждым музыкантом, 
задавая темп, ритм и динамику исполнения. 
Дирижёр координирует работу всего оркестра, 
обеспечивая гармоничное звучание всех инструментов.

В программировании посредник (mediator) выполняет аналогичную роль: 
он управляет взаимодействием между различными объектами, 
чтобы они работали согласованно, но не напрямую друг с другом. 
Это упрощает структуру системы 
и снижает связанность между её частями.
```

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
