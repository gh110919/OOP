### Strategy (Стратегия)

###### Определяет семейство алгоритмов, инкапсулирует каждый из них и делает их взаимозаменяемыми.

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
