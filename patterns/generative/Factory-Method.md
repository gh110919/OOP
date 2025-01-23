### Factory Method

###### Определяет интерфейс для создания объекта, но позволяет подклассам изменять тип создаваемого объекта.

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
