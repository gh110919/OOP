### Flyweight (Приспособленец)

###### Приспособленец уменьшает затраты на создание большого количества однотипных объектов, делая их разделяемыми.

```
Представьте себе библиотеку, в которой хранится огромное количество книг. 
Вместо того чтобы каждый читатель брал книгу домой и хранил её у себя, 
библиотека предоставляет возможность всем читателям пользоваться одной 
и той же книгой. Когда кто-то хочет почитать книгу, 
он просто берет её из библиотеки, а после прочтения возвращает обратно, 
чтобы её мог использовать следующий читатель. 
Это позволяет библиотеке обслуживать множество людей, 
экономя место и ресурсы.

В программировании паттерн "Приспособленец" работает аналогично: 
он уменьшает затраты на создание большого количества однотипных объектов, 
делая их разделяемыми. Вместо создания нового объекта каждый раз, 
когда он нужен, объекты могут быть повторно использованы, 
что значительно снижает затраты на хранение и управление.
```

```ts
class Flyweight {
  private sharedState: string;

  constructor(sharedState: string) {
    this.sharedState = sharedState;
  }

  operation(uniqueState: string): void {
    console.log(
      `Flyweight: Displaying shared (${this.sharedState}) and unique (${uniqueState}) state.`
    );
  }
}

class FlyweightFactory {
  private flyweights: { [key: string]: Flyweight } = {};

  getFlyweight(sharedState: string): Flyweight {
    if (!(sharedState in this.flyweights)) {
      this.flyweights[sharedState] = new Flyweight(sharedState);
    }
    return this.flyweights[sharedState];
  }
}

const factory = new FlyweightFactory();
const flyweight1 = factory.getFlyweight("shared");
flyweight1.operation("unique1");

const flyweight2 = factory.getFlyweight("shared");
flyweight2.operation("unique2");
```
