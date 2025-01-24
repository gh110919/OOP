### Полиморфизм

###### Способность объектов разного класса реагировать на одинаковые сообщения по-разному.

```
Представьте себе, что вы идёте по улице и видите двух собак. 
Вы бросаете палку, и обе собаки бегут за ней, 
но одна приносит её обратно, а другая начинает жевать её. 
Одна и та же команда ("принеси палку") вызывает разные реакции у разных собак. 
В программировании полиморфизм работает аналогично: 
разные объекты могут по-разному реагировать 
на одни и те же сообщения (методы), 
в зависимости от их типа.
```

```ts
class Shape {
  area(): number {
    return 0;
  }
}

class Circle extends Shape {
  radius: number;
  constructor(radius: number) {
    super();
    this.radius = radius;
  }
  area(): number {
    return Math.PI * this.radius ** 2;
  }
}

class Rectangle extends Shape {
  width: number;
  height: number;
  constructor(width: number, height: number) {
    super();
    this.width = width;
    this.height = height;
  }
  area(): number {
    return this.width * this.height;
  }
}

const shapes: Shape[] = [new Circle(5), new Rectangle(4, 6)];
shapes.forEach((shape) => console.log(shape.area()));
// Вывод: 78.53981633974483 и 24
```
