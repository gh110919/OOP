### OCP: Open-Closed Principle (Принцип открытости/закрытости)

### Код должен быть открыт для расширения, но закрыт для изменения.

###### Метафора: Подумай о розетке в стене. Она позволяет подключать разные устройства без изменения самой розетки. Мы можем расширять функциональность, не трогая исходный код.

```ts
/* Базовый класс: */
abstract class Shape {
  abstract area(): number;
}

/* Расширение функционала: */
class Circle extends Shape {
  constructor(private radius: number) {
    super();
  }

  area(): number {
    return Math.PI * this.radius ** 2;
  }
}

class Rectangle extends Shape {
  constructor(private width: number, private height: number) {
    super();
  }

  area(): number {
    return this.width * this.height;
  }
}

/* Мы можем добавлять новые фигуры, не изменяя базовый класс Shape. */
```
