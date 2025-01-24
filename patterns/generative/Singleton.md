### Singleton(Одиночка)

###### Гарантирует наличие только одного экземпляра класса.

```
Представьте себе президента страны. 
В стране всегда может быть только один действующий президент в любой момент времени. 
Когда новый президент вступает в должность, предыдущий президент уходит. 
Этот механизм обеспечивает уникальность и исключительность роли президента, 
гарантируя, что в любой момент времени у страны будет только один лидер.

В программировании паттерн "Одиночка" (Singleton) работает аналогично: 
он гарантирует, что в системе существует только один экземпляр класса, 
и предоставляет глобальную точку доступа к этому экземпляру. 
Это особенно полезно для управления ресурсами, 
логированием или конфигурационными настройками, 
где требуется один уникальный объект.
```

```ts
class Singleton {
  private static instance: Singleton;

  private constructor() {}

  static getInstance(): Singleton {
    if (!Singleton.instance) {
      Singleton.instance = new Singleton();
    }
    return Singleton.instance;
  }

  showMessage() {
    console.log("Hello, I am a singleton!");
  }
}

const singleton1 = Singleton.getInstance();
const singleton2 = Singleton.getInstance();
console.log(singleton1 === singleton2); // true
singleton1.showMessage();
```
