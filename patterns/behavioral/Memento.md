### Memento (Хранитель)

###### Позволяет сохранять и восстанавливать внутреннее состояние объекта без нарушения инкапсуляции.

```ts
class Memento {
  private state: string;

  constructor(state: string) {
    this.state = state;
  }

  getState(): string {
    return this.state;
  }
}

class Originator {
  private state: string;

  setState(state: string): void {
    this.state = state;
    console.log(`State set to: ${state}`);
  }

  saveStateToMemento(): Memento {
    return new Memento(this.state);
  }

  getStateFromMemento(memento: Memento): void {
    this.state = memento.getState();
    console.log(`State restored to: ${this.state}`);
  }
}

class Caretaker {
  private mementos: Memento[] = [];

  add(memento: Memento): void {
    this.mementos.push(memento);
  }

  get(index: number): Memento {
    return this.mementos[index];
  }
}

// Использование
const originator = new Originator();
const caretaker = new Caretaker();

originator.setState("State1");
caretaker.add(originator.saveStateToMemento());

originator.setState("State2");
caretaker.add(originator.saveStateToMemento());

originator.setState("State3");

originator.getStateFromMemento(caretaker.get(0)); // State restored to: State1
originator.getStateFromMemento(caretaker.get(1)); // State restored to: State2
```
