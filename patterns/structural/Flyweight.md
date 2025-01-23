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
