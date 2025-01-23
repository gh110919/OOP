### Creator (Создатель)

###### Присваивание ответственности за создание экземпляра класса тому классу, который имеет информацию о том, что нужно создать.

```ts
class Order {
  items: Product[] = [];

  addItem(product: Product) {
    this.items.push(product);
  }
}

const order = new Order();
const newProduct = new Product(10, 2);
order.addItem(newProduct);

/* Объект Order является создателем, так как он содержит элементы заказа и отвечает за их создание. */
```
