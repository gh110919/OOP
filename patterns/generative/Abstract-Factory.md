### Abstract Factory(Абстрактная Фабрика)

###### Создает семейства связанных объектов без указания конкретных классов.

```
Представьте себе компанию, которая производит мебель. 
Вместо того, чтобы каждый раз разрабатывать новый дизайн стула или стола, 
компания создает несколько наборов дизайнов (семейств), 
каждый из которых включает в себя стул, стол, шкаф и так далее. 
Когда заказчик выбирает один из этих наборов, 
компания производит соответствующую мебель, 
не указывая конкретные детали каждого предмета в момент выбора.

Таким образом, клиент выбирает стиль или тему, 
а фабрика (абстрактная фабрика) создаёт все необходимые предметы мебели, 
соответствующие выбранной теме. 
Это позволяет легко добавлять новые семейства продуктов, 
не изменяя существующие.

В программировании паттерн "Абстрактная фабрика" работает аналогично: 
он позволяет создавать семейства связанных объектов 
без необходимости указывать конкретные классы для каждого объекта.
```

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
