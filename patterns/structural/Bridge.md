### Bridge (Мост)

###### Мост разделяет абстракцию и реализацию, позволяя их изменять независимо друг от друга.

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
