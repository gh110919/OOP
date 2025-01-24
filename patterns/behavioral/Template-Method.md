### Template Method (Шаблонный метод)

###### Определяет скелет алгоритма, позволяя подклассам переопределять отдельные шаги алгоритма без изменения его структуры.

```
Представьте себе организацию большого праздничного ужина. 
У вас есть базовый план мероприятия: сначала приветственный напиток, 
затем закуски, основное блюдо, десерт и, наконец, кофе. 
Этот план можно считать "шаблонным методом". 
Вы приглашаете несколько шеф-поваров, 
и каждый из них может вносить свои изменения в конкретные шаги: 
один шеф готовит закуски по своему рецепту, 
другой — основное блюдо, 
третий — десерт.

Однако структура мероприятия остаётся неизменной: 
последовательность подачи блюд сохраняется. 
Таким образом, каждый шеф-повар может переопределить отдельные шаги процесса, 
не изменяя общую структуру мероприятия. 

В программировании паттерн "Шаблонный метод" работает аналогично: 
он задаёт общий скелет алгоритма, 
а подклассы могут переопределять конкретные шаги, 
не нарушая основной структуры.
```

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
