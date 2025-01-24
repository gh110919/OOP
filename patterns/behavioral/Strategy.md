### Strategy (Стратегия)

###### Определяет семейство алгоритмов, инкапсулирует каждый из них и делает их взаимозаменяемыми.

```
Представьте себе шеф-повара, готовящего праздничный ужин. 
У него есть несколько рецептов для приготовления одного и того же блюда: 
один с добавлением специй, 
другой — более классический, 
третий — вегетарианский. 
В зависимости от предпочтений гостей, 
он может выбрать подходящий рецепт 
и приготовить блюдо соответствующим образом. 
Все рецепты относятся к одному и тому же блюду, 
но шеф-повар может легко менять их, 
не изменяя основные принципы приготовления.

В программировании паттерн "Стратегия" работает аналогично: 
он определяет семейство алгоритмов для выполнения задачи, 
инкапсулирует каждый из них 
и позволяет использовать их взаимозаменяемо в зависимости от конкретных условий. 
Это обеспечивает гибкость и адаптивность системы.
```

```ts
class Context {
  private strategy: Strategy;

  setStrategy(strategy: Strategy): void {
    this.strategy = strategy;
  }

  executeStrategy(): void {
    this.strategy.doAlgorithm();
  }
}

interface Strategy {
  doAlgorithm(): void;
}

class ConcreteStrategyA implements Strategy {
  doAlgorithm(): void {
    console.log("Strategy A executed.");
  }
}

class ConcreteStrategyB implements Strategy {
  doAlgorithm(): void {
    console.log("Strategy B executed.");
  }
}

// Использование
const context = new Context();

context.setStrategy(new ConcreteStrategyA());
context.executeStrategy(); // Strategy A executed.

context.setStrategy(new ConcreteStrategyB());
context.executeStrategy(); // Strategy B executed.
```
