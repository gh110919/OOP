### Proxy (Заместитель)

###### Заместитель предоставляет объект, который контролирует доступ к другому объекту, перехватывая все вызовы.

```
Представьте себе известного артиста, 
который очень занят и не может лично отвечать на все запросы фанатов и прессы. 
Вместо этого у него есть менеджер, который выполняет роль посредника. 
Менеджер фильтрует все запросы и решает, 
какие из них передать артисту, а какие решить самостоятельно. 
Он также может организовывать встречи 
и давать ответы на часто задаваемые вопросы, 
снимая нагрузку с артиста.

В программировании паттерн "Заместитель" работает аналогично: 
он предоставляет объект, который контролирует доступ к другому объекту, 
перехватывая все вызовы и решая, как их обработать. 
Это позволяет управлять доступом 
и уменьшать нагрузку на основной объект.
```

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
