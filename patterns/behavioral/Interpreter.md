### Interpreter (Интерпретатор)

###### Определяет грамматику представления и интерпретатор для обработки запросов.

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
