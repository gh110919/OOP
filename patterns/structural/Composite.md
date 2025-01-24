### Composite (Компоновщик)

###### Компоновщик позволяет сгруппировать объекты в древовидную структуру и работать с ними так, как с единичными объектами.

```
Представьте себе дерево с ветвями, листьями и плодами.
Дерево как целое представляет собой композицию:
у него есть основной ствол (корень), от которого отходят ветви,
каждая из которых имеет листья и плоды.
Несмотря на то, что дерево состоит из множества отдельных элементов,
мы воспринимаем его как единое целое.

В программировании паттерн "Компоновщик" работает аналогично:
он позволяет сгруппировать объекты в древовидную структуру
и работать с этой группой как с единичным объектом.
Например, вы можете создать структуру меню,
где каждое подменю может содержать пункты меню,
и работать с меню как с единым объектом,
независимо от его внутренней структуры.
```

```ts
interface Component {
  operation(): string;
}

class Leaf implements Component {
  operation(): string {
    return "Leaf";
  }
}

class Composite implements Component {
  private children: Component[] = [];

  public add(component: Component): void {
    this.children.push(component);
  }

  public operation(): string {
    return `Branch(${this.children
      .map((child) => child.operation())
      .join("+")})`;
  }
}

const leaf = new Leaf();
const tree = new Composite();
tree.add(leaf);
tree.add(leaf);
console.log(tree.operation()); // "Branch(Leaf+Leaf)"
```
