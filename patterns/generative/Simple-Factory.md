### Simple Factory(Простая фабрика)

###### Создает объекты без предоставления конкретного класса.

```
Представьте себе автомат по продаже напитков. 
Когда вы подходите к автомату, вы видите кнопки с различными видами напитков: 
газировка, сок, вода и т.д. 
Вы нажимаете на кнопку с выбранным напитком, 
и автомат выдает вам именно то, что вы заказали, 
без необходимости знать, 
как именно внутри автомата хранится 
или смешивается этот напиток.

В программировании паттерн "Простая фабрика" работает аналогично: 
он создает объекты различных классов по запросу, 
не предоставляя конкретного класса в момент создания. 
Пользователь просто делает запрос на создание объекта, 
а фабрика автоматически создает 
и возвращает нужный объект.
```

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
