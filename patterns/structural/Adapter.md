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
