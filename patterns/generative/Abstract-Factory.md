### Abstract Factory

###### Создает семейства связанных объектов без указания конкретных классов.

```ts
interface Chair {
  sitOn(): void;
}

class VictorianChair implements Chair {
  sitOn() {
    console.log("Sitting on a Victorian chair.");
  }
}

class ModernChair implements Chair {
  sitOn() {
    console.log("Sitting on a modern chair.");
  }
}

interface FurnitureFactory {
  createChair(): Chair;
}

class VictorianFurnitureFactory implements FurnitureFactory {
  createChair(): Chair {
    return new VictorianChair();
  }
}

class ModernFurnitureFactory implements FurnitureFactory {
  createChair(): Chair {
    return new ModernChair();
  }
}

const factory: FurnitureFactory = new ModernFurnitureFactory();
const chair: Chair = factory.createChair();
chair.sitOn();
```
