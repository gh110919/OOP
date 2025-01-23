### Information Expert (Информационный эксперт)

###### Присваивание ответственности тому объекту, который имеет наибольшие знания, необходимые для выполнения этой ответственности.

```ts
class Product {
  price: number;
  quantity: number;

  constructor(price: number, quantity: number) {
    this.price = price;
    this.quantity = quantity;
  }

  getTotalPrice(): number {
    return this.price * this.quantity;
  }
}

const product = new Product(10, 5);
console.log(product.getTotalPrice()); // Вывод: 50

/* Здесь объект Product является информационным экспертом для вычисления общей стоимости, так как он владеет всей необходимой информацией. */
```
