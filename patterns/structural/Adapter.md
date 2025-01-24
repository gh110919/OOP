### Adapter (Адаптер)

###### Адаптер позволяет объектам с несовместимыми интерфейсами работать вместе. Он оборачивает один из объектов, адаптируя его интерфейс к нужному.

```
Представьте себе, что вы путешествуете по разным странам 
и у вас есть множество различных электронных устройств. 
Каждое устройство имеет свою вилку, 
а розетки в каждой стране отличаются. 
Вместо того чтобы менять вилку на каждом устройстве, 
вы используете адаптер, 
который позволяет подключить ваше устройство к любой розетке, 
независимо от её формы.

В программировании паттерн "Адаптер" работает аналогично: 
он позволяет объектам с несовместимыми интерфейсами работать вместе, 
оборачивая один объект и предоставляя интерфейс, 
который другой объект может использовать. 
Это обеспечивает гибкость и совместимость 
между различными компонентами системы.
```

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
