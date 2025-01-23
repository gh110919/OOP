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
