### Composite (Компоновщик)

###### Компоновщик позволяет сгруппировать объекты в древовидную структуру и работать с ними так, как с единичными объектами.

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
