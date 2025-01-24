### Prototype(Прототип)

###### Создает объекты на основе шаблона (прототипа) путем клонирования.

```
Представьте себе художника, который создаёт уникальные скульптуры из глины. 
Каждая скульптура является оригинальным произведением искусства. 
Затем он делает силиконовую форму с этой оригинальной скульптуры (прототип). 
С помощью этой формы он может делать множество точных копий оригинальной скульптуры, 
каждая из которых будет иметь те же детали и особенности, что и оригинал.

В программировании паттерн "Прототип" работает аналогично: 
он позволяет создавать новые объекты 
на основе существующего объекта (прототипа) путем клонирования, 
сохраняя все его свойства и характеристики. Это полезно, 
когда нужно быстро создавать множество одинаковых объектов с минимальными усилиями.
```

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
