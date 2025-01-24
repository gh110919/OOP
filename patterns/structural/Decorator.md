### Decorator (Декоратор)

###### Декоратор динамически добавляет новое поведение объектам, оборачивая их.

```
Представьте себе новогоднюю ёлку. 
Вначале это просто зелёное дерево, 
но когда вы начинаете украшать её, 
вы добавляете гирлянды, шары, мишуру и прочие украшения. 
Каждое новое украшение добавляет ёлке дополнительную красоту и сияние, 
но само дерево остаётся неизменным под всеми этими слоями декораций.

В программировании паттерн "Декоратор" работает аналогично: 
он позволяет динамически добавлять новое поведение объектам, 
оборачивая их дополнительными классами-декораторами. 
Это позволяет гибко изменять и расширять функциональность объекта 
без изменения его исходного кода.
```

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
