### Bridge (Мост)

###### Мост разделяет абстракцию и реализацию, позволяя их изменять независимо друг от друга.

```
Представьте себе пульт дистанционного управления и телевизор. 
Пульт дистанционного управления позволяет вам изменять каналы, 
регулировать громкость и выполнять другие действия. 
Вы можете заменить пульт на новый, 
и он все равно будет работать с вашим телевизором, 
потому что пульт и телевизор связаны 
через стандартный интерфейс (ИК-сигнал или Bluetooth).

В программировании паттерн "Мост" работает аналогично: 
он разделяет абстракцию (пульт дистанционного управления) 
и реализацию (телевизор), позволяя изменять их независимо друг от друга. 
Это обеспечивает гибкость и возможность изменять одну часть системы, 
не затрагивая другую.
```

```ts
interface Device {
  isEnabled(): boolean;
  enable(): void;
  disable(): void;
}

class TV implements Device {
  private on = false;

  isEnabled(): boolean {
    return this.on;
  }

  enable(): void {
    this.on = true;
  }

  disable(): void {
    this.on = false;
  }
}

class Remote {
  protected device: Device;

  constructor(device: Device) {
    this.device = device;
  }

  togglePower(): void {
    if (this.device.isEnabled()) {
      this.device.disable();
    } else {
      this.device.enable();
    }
  }
}

const tv = new TV();
const remote = new Remote(tv);
remote.togglePower();
console.log(tv.isEnabled()); // true
```
