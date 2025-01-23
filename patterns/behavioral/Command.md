### Command (Команда)

###### Инкапсулирует запрос в объект, позволяя параметризовать клиентов с различными запросами и поддерживать операции отмены.

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
