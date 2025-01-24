### Iterator (Итератор)

###### Предоставляет способ последовательного доступа ко всем элементам коллекции без раскрытия её внутреннего представления.

```
Представьте себе кассира в магазине, 
который сканирует товары на кассе. 
У кассира есть лента, на которой лежат все покупки, 
и он последовательно берет один товар за другим, 
сканирует его и передает дальше, 
не раскрывая покупателю внутреннее устройство кассового аппарата 
или системы учета.

В программировании итератор работает аналогично: 
он предоставляет способ последовательного доступа 
ко всем элементам коллекции (товарам на ленте) 
без раскрытия её внутреннего представления (работы кассового аппарата). 
Это позволяет обходить все элементы коллекции, 
не зная её внутренней структуры.
```

```ts
interface Iterator<T> {
  next(): T | null;
  hasNext(): boolean;
}

class ConcreteIterator<T> implements Iterator<T> {
  private collection: T[];
  private position: number = 0;

  constructor(collection: T[]) {
    this.collection = collection;
  }

  next(): T | null {
    if (this.hasNext()) {
      return this.collection[this.position++];
    }
    return null;
  }

  hasNext(): boolean {
    return this.position < this.collection.length;
  }
}

// Использование
const collection = [1, 2, 3];
const iterator = new ConcreteIterator(collection);

while (iterator.hasNext()) {
  console.log(iterator.next()); // 1 2 3
}
```
