### Decorator (Декоратор)

###### Декоратор динамически добавляет новое поведение объектам, оборачивая их.

```ts
interface Coffee {
  cost(): number;
  description(): string;
}

class SimpleCoffee implements Coffee {
  cost(): number {
    return 5;
  }
  description(): string {
    return "Simple coffee";
  }
}

class MilkDecorator implements Coffee {
  private coffee: Coffee;

  constructor(coffee: Coffee) {
    this.coffee = coffee;
  }

  cost(): number {
    return this.coffee.cost() + 2;
  }

  description(): string {
    return this.coffee.description() + ", milk";
  }
}

let myCoffee = new SimpleCoffee();
myCoffee = new MilkDecorator(myCoffee);
console.log(myCoffee.description()); // "Simple coffee, milk"
console.log(myCoffee.cost()); // 7
```
