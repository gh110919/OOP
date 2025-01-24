### Builder(Строитель)

###### Разделяет создание сложного объекта на шаги, чтобы можно было создавать разные представления объекта.

```
Представьте себе строительную компанию, которая занимается возведением домов. 
У каждой семьи, заказывающей дом, есть свои уникальные пожелания: 
одни хотят большой дом с несколькими спальнями, другие предпочитают компактный коттедж. 
Вместо того чтобы строить все дома одинаковыми, 
строительная компания использует пошаговый процесс.

Каждый этап строительства — закладка фундамента, 
возведение стен, установка крыши 
и внутренняя отделка — позволяет адаптировать 
и изменять дом в соответствии с пожеланиями заказчика. 
Так, один заказчик может выбрать больше окон, другой — просторную кухню, 
а третий — дополнительный этаж. 
Проектировщик (Builder) координирует каждый шаг, 
чтобы создать дом, точно соответствующий ожиданиям клиента.

В программировании паттерн "Строитель" работает аналогично: 
он разделяет процесс создания сложного объекта на пошаговые этапы, 
позволяя легко адаптировать и изменять конечный результат 
в зависимости от требований.
```

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
