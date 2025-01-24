### Visitor (Посетитель)

###### Позволяет добавлять в класс новые операции, не изменяя его.

```
Представьте себе музей, 
который периодически приглашает различных экскурсоводов для проведения экскурсий. 
Каждый экскурсовод имеет свою уникальную программу 
и рассказывает о выставке по-своему, 
добавляя новые интересные детали и истории, 
не меняя саму экспозицию. 
То есть, сам музей (класс) остается неизменным, 
но каждый экскурсовод (посетитель) 
добавляет свою уникальную экскурсию (операцию).

В программировании паттерн "Посетитель" работает аналогично: 
вы можете добавлять новые операции к классам 
без изменения их исходного кода, 
просто создавая новые "посетители", 
которые выполняют дополнительные действия.
```

```ts
interface Visitor {
  visitConcreteElementA(element: ConcreteElementA): void;
  visitConcreteElementB(element: ConcreteElementB): void;
}

interface Element {
  accept(visitor: Visitor): void;
}

class ConcreteElementA implements Element {
  accept(visitor: Visitor): void {
    visitor.visitConcreteElementA(this);
  }

  operationA(): void {
    console.log("ConcreteElementA operation.");
  }
}

class ConcreteElementB implements Element {
  accept(visitor: Visitor): void {
    visitor.visitConcreteElementB(this);
  }

  operationB(): void {
    console.log("ConcreteElementB operation.");
  }
}

class ConcreteVisitor implements Visitor {
  visitConcreteElementA(element: ConcreteElementA): void {
    console.log("Visitor is processing ConcreteElementA.");
    element.operationA();
  }

  visitConcreteElementB(element: ConcreteElementB): void {
    console.log("Visitor is processing ConcreteElementB.");
    element.operationB();
  }
}

// Использование
const elements: Element[] = [new ConcreteElementA(), new ConcreteElementB()];
const visitor = new ConcreteVisitor();

for (const element of elements) {
  element.accept(visitor);
}
```
