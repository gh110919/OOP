### Factory Method(Фабричный Метод)

###### Определяет интерфейс для создания объекта, но позволяет подклассам изменять тип создаваемого объекта.

```
Представьте себе кондитерскую, которая выпускает разные виды тортов: 
шоколадные, фруктовые, сливочные. 
В кондитерской есть общий рецепт (интерфейс) для создания торта, 
который включает в себя базовые этапы: 
приготовление коржей, смешивание крема, сборка и украшение. 
Однако каждый кондитер может использовать этот общий рецепт, 
чтобы создавать свои уникальные виды тортов.

Например, один кондитер может использовать рецепт для создания шоколадного торта, 
добавляя какао и шоколадную глазурь, другой - фруктового торта с клубникой и кремом, 
а третий - сливочного торта с ванильным кремом. Все они следуют одному базовому рецепту, 
но конечный результат отличается в зависимости от творческого подхода каждого кондитера.

В программировании паттерн "Фабричный метод" работает аналогично: 
он определяет общий интерфейс для создания объектов, 
но позволяет подклассам изменять конкретный тип создаваемого объекта, 
предоставляя гибкость и возможность расширения.
```

```ts
interface Document {
  open(): void;
}

class WordDocument implements Document {
  open() {
    console.log("Opening Word document.");
  }
}

class PDFDocument implements Document {
  open() {
    console.log("Opening PDF document.");
  }
}

abstract class Application {
  abstract createDocument(): Document;

  openDocument() {
    const doc = this.createDocument();
    doc.open();
  }
}

class WordApplication extends Application {
  createDocument(): Document {
    return new WordDocument();
  }
}

class PDFApplication extends Application {
  createDocument(): Document {
    return new PDFDocument();
  }
}

const app: Application = new PDFApplication();
app.openDocument();
```
