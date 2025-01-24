### Chain of Responsibility (Цепочка обязанностей)

###### Позволяет передавать запрос последовательно по цепочке обработчиков. Каждый обработчик решает, может ли он обработать запрос или передать его дальше.

```
Представьте себе, что вы находитесь в офисе 
и пытаетесь решить проблему с компьютером. 
Вы сначала обращаетесь к администратору офиса. 
Если он не может помочь, он перенаправляет вас к системному администратору. 
Если системный администратор также не может решить проблему, 
он направляет вас к внешнему техническому специалисту. 
Так создаётся цепочка обязанностей, 
где каждый в этой цепочке проверяет, 
может ли он решить проблему, 
и при необходимости передаёт её дальше.

Эта последовательная передача запроса от одного обработчика 
к другому позволяет эффективно распределять задачи 
и ресурсы, чтобы запрос был обработан тем, 
кто обладает нужными знаниями и навыками.
```

```ts
class Handler {
  private nextHandler: Handler | null = null;

  setNext(handler: Handler): Handler {
    this.nextHandler = handler;
    return handler;
  }

  handle(request: string): void {
    if (this.nextHandler) {
      this.nextHandler.handle(request);
    }
  }
}

class ConcreteHandler1 extends Handler {
  handle(request: string): void {
    if (request === "Request1") {
      console.log("ConcreteHandler1 handled the request.");
    } else {
      super.handle(request);
    }
  }
}

// Использование
const handler1 = new ConcreteHandler1();
const handler2 = new Handler();
handler1.setNext(handler2);

handler1.handle("Request1"); // ConcreteHandler1 handled the request.
```
