### Command (Команда)

###### Инкапсулирует запрос в объект, позволяя параметризовать клиентов с различными запросами и поддерживать операции отмены.

```
Представьте себе официанта в ресторане, 
который принимает заказы у клиентов. 
Каждый заказ записывается на отдельный бланк, 
где указаны все детали: блюда, напитки, особые пожелания. 
Эти бланки можно передавать на кухню, 
где повара готовят заказанные блюда. 
Если клиент решит изменить или отменить заказ, 
официант просто меняет или удаляет соответствующий бланк, 
и повара действуют в соответствии с новыми инструкциями.

Так и в программировании: 
команды инкапсулируют запросы в отдельные объекты, 
что позволяет легко управлять, 
изменять или отменять запросы 
без изменения кода клиента.
```

```ts
class Command {
  execute(): void {}
}

class ConcreteCommand extends Command {
  private receiver: Receiver;

  constructor(receiver: Receiver) {
    super();
    this.receiver = receiver;
  }

  execute(): void {
    this.receiver.action();
  }
}

class Receiver {
  action(): void {
    console.log("Receiver action executed.");
  }
}

class Invoker {
  private command: Command;

  setCommand(command: Command): void {
    this.command = command;
  }

  invoke(): void {
    this.command.execute();
  }
}

// Использование
const receiver = new Receiver();
const command = new ConcreteCommand(receiver);
const invoker = new Invoker();

invoker.setCommand(command);
invoker.invoke(); // Receiver action executed.
```
