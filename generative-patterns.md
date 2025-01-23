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

### Builder

###### Разделяет создание сложного объекта на шаги, чтобы можно было создавать разные представления объекта.

```ts
class House {
  windows: number;
  doors: number;
  hasGarage: boolean;

  constructor() {
    this.windows = 0;
    this.doors = 0;
    this.hasGarage = false;
  }
}

class HouseBuilder {
  private house: House;

  constructor() {
    this.house = new House();
  }

  setWindows(windows: number): this {
    this.house.windows = windows;
    return this;
  }

  setDoors(doors: number): this {
    this.house.doors = doors;
    return this;
  }

  setGarage(hasGarage: boolean): this {
    this.house.hasGarage = hasGarage;
    return this;
  }

  build(): House {
    return this.house;
  }
}

const builder = new HouseBuilder();
const house = builder.setWindows(4).setDoors(2).setGarage(true).build();
console.log(house);
```

### Factory Method

###### Определяет интерфейс для создания объекта, но позволяет подклассам изменять тип создаваемого объекта.

```ts
interface Document {
  open(): void;
}

class WordDocument implements Document {
  open() {
    console.log("Opening Word document.");
  }
}

class PDFDocument implements Document {
  open() {
    console.log("Opening PDF document.");
  }
}

abstract class Application {
  abstract createDocument(): Document;

  openDocument() {
    const doc = this.createDocument();
    doc.open();
  }
}

class WordApplication extends Application {
  createDocument(): Document {
    return new WordDocument();
  }
}

class PDFApplication extends Application {
  createDocument(): Document {
    return new PDFDocument();
  }
}

const app: Application = new PDFApplication();
app.openDocument();
```

### Prototype

###### Создает объекты на основе шаблона (прототипа) путем клонирования.

```ts
interface Prototype {
  clone(): this;
}

class Sheep implements Prototype {
  public name: string;
  public category: string;

  constructor(name: string, category: string) {
    this.name = name;
    this.category = category;
  }

  clone(): this {
    const clone = Object.create(this);
    clone.name = this.name;
    clone.category = this.category;
    return clone;
  }
}

const originalSheep = new Sheep("Dolly", "Mountain");
const clonedSheep = originalSheep.clone();
console.log(clonedSheep);
```

### Singleton

###### Гарантирует наличие только одного экземпляра класса.

```ts
class Singleton {
  private static instance: Singleton;

  private constructor() {}

  static getInstance(): Singleton {
    if (!Singleton.instance) {
      Singleton.instance = new Singleton();
    }
    return Singleton.instance;
  }

  showMessage() {
    console.log("Hello, I am a singleton!");
  }
}

const singleton1 = Singleton.getInstance();
const singleton2 = Singleton.getInstance();
console.log(singleton1 === singleton2); // true
singleton1.showMessage();
```

### Simple Factory

###### Создает объекты без предоставления конкретного класса.

```ts
class Car {
  drive() {
    console.log("Driving a car.");
  }
}

class Truck {
  drive() {
    console.log("Driving a truck.");
  }
}

class VehicleFactory {
  static createVehicle(type: string): Car | Truck {
    if (type === "car") {
      return new Car();
    } else if (type === "truck") {
      return new Truck();
    } else {
      throw new Error("Unknown vehicle type.");
    }
  }
}

const vehicle = VehicleFactory.createVehicle("car");
vehicle.drive();
```
