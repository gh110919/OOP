### Interpreter (Интерпретатор)

###### Определяет грамматику представления и интерпретатор для обработки запросов.

```
Представьте себе переводчика, 
который работает с двумя людьми, 
говорящими на разных языках. 
Один человек говорит на английском, а другой на русском. 
Переводчик должен понимать грамматику и лексику обоих языков, 
чтобы правильно интерпретировать и передавать сообщения. 
Он принимает фразы на одном языке, 
обрабатывает их и переводит на другой, 
сохраняя смысл и контекст.

В программировании интерпретатор работает аналогично: 
он принимает команды на языке высокого уровня (например, код), 
интерпретирует их согласно правилам и грамматике (синтаксису) этого языка 
и выполняет соответствующие действия. 
Это позволяет системе обрабатывать запросы и команды, 
даже если они поступают на разных языках 
или в разных форматах.
```

```ts
interface Expression {
  interpret(context: string): boolean;
}

class TerminalExpression implements Expression {
  private data: string;

  constructor(data: string) {
    this.data = data;
  }

  interpret(context: string): boolean {
    return context.includes(this.data);
  }
}

class OrExpression implements Expression {
  private expr1: Expression;
  private expr2: Expression;

  constructor(expr1: Expression, expr2: Expression) {
    this.expr1 = expr1;
    this.expr2 = expr2;
  }

  interpret(context: string): boolean {
    return this.expr1.interpret(context) || this.expr2.interpret(context);
  }
}

// Использование
const expr1 = new TerminalExpression("Hello");
const expr2 = new TerminalExpression("World");
const orExpr = new OrExpression(expr1, expr2);

console.log(orExpr.interpret("Hello there!")); // true
```
