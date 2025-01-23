### Абстракция: Выделение значимой информации и игнорирование деталей. В TypeScript реализуется через абстрактные классы и интерфейсы.

```ts
interface Drawable {
  draw(): void;
}

class Square implements Drawable {
  draw() {
    console.log("Рисуем квадрат");
  }
}

class Triangle implements Drawable {
  draw() {
    console.log("Рисуем треугольник");
  }
}

const figures: Drawable[] = [new Square(), new Triangle()];
figures.forEach((figure) => figure.draw());
// Вывод: Рисуем квадрат
// Вывод: Рисуем треугольник
```
