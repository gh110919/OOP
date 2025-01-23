### Template Method (Шаблонный метод)

###### Определяет скелет алгоритма, позволяя подклассам переопределять отдельные шаги алгоритма без изменения его структуры.

```ts
abstract class AbstractClass {
  templateMethod(): void {
    this.baseOperation1();
    this.requiredOperations1();
    this.baseOperation2();
    this.hook1();
    this.requiredOperations2();
    this.baseOperation3();
    this.hook2();
  }

  baseOperation1(): void {
    console.log("AbstractClass says: I am doing the bulk of the work.");
  }

  baseOperation2(): void {
    console.log(
      "AbstractClass says: But I let subclasses override some operations."
    );
  }

  baseOperation3(): void {
    console.log("AbstractClass says: And I am doing the rest of the work.");
  }

  protected abstract requiredOperations1(): void;
  protected abstract requiredOperations2(): void;

  hook1(): void {}
  hook2(): void {}
}

class ConcreteClass extends AbstractClass {
  requiredOperations1(): void {
    console.log("ConcreteClass says: Implemented Operation1.");
  }

  requiredOperations2(): void {
    console.log("ConcreteClass says: Implemented Operation2.");
  }

  hook1(): void {
    console.log("ConcreteClass says: Overridden Hook1.");
  }
}

// Использование
const concreteClass = new ConcreteClass();
concreteClass.templateMethod();
```
