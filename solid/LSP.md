### LSP: Liskov Substitution Principle (Принцип подстановки Барбары Лисков)

### Объекты должны быть заменяемы на экземпляры их подтипов без изменения корректности программы.

###### Метафора: Если у тебя есть автомобиль, ты можешь заменить его на другой автомобиль, и он все равно будет выполнять свои функции. Но если ты заменишь его на велосипед, ожидая той же функциональности, возникнут проблемы.

```ts
/* Пример нарушения принципа: */
class Bird {
  fly(): void {
    console.log("Птица летит");
  }
}

class Ostrich extends Bird {
  fly(): void {
    throw new Error("Страусы не умеют летать");
  }
}

function makeBirdFly(bird: Bird) {
  bird.fly();
}

const ostrich = new Ostrich();
makeBirdFly(ostrich); // Ошибка во время выполнения

/* Исправление: */
class Bird {
  // Общие свойства птиц
}

interface FlyingBird {
  fly(): void;
}

class Sparrow extends Bird implements FlyingBird {
  fly(): void {
    console.log("Воробей летит");
  }
}

class Ostrich extends Bird {
  // Страус не реализует интерфейс FlyingBird
}

function makeBirdFly(bird: FlyingBird) {
  bird.fly();
}

const sparrow = new Sparrow();
makeBirdFly(sparrow); // Воробей летит
makeBirdFly(new Ostrich()); // Ошибка на этапе компиляции

/* Теперь невозможно передать нелетающую птицу в функцию, которая ожидает летающую. */
```
