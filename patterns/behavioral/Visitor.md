### Visitor (Посетитель)

###### Позволяет добавлять в класс новые операции, не изменяя его.

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
