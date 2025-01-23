### Proxy (Заместитель)

###### Заместитель предоставляет объект, который контролирует доступ к другому объекту, перехватывая все вызовы.

```ts
interface Subject {
  request(): void;
}

class RealSubject implements Subject {
  request(): void {
    console.log("RealSubject: Handling request.");
  }
}

class ProxySubject implements Subject {
  private realSubject: RealSubject;

  constructor(realSubject: RealSubject) {
    this.realSubject = realSubject;
  }

  request(): void {
    console.log("Proxy: Checking access before forwarding request.");
    this.realSubject.request();
    console.log("Proxy: Logging request.");
  }
}

const realSubject = new RealSubject();
const proxy = new ProxySubject(realSubject);
proxy.request();
// "Proxy: Checking access before forwarding request."
// "RealSubject: Handling request."
// "Proxy: Logging request."
```
