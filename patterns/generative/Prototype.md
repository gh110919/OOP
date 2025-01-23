### Prototype

###### Создает объекты на основе шаблона (прототипа) путем клонирования.

```ts
interface Prototype {
  clone(): this;
}

class Sheep implements Prototype {
  public name: string;
  public category: string;

  constructor(name: string, category: string) {
    this.name = name;
    this.category = category;
  }

  clone(): this {
    const clone = Object.create(this);
    clone.name = this.name;
    clone.category = this.category;
    return clone;
  }
}

const originalSheep = new Sheep("Dolly", "Mountain");
const clonedSheep = originalSheep.clone();
console.log(clonedSheep);
```
