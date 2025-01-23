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
