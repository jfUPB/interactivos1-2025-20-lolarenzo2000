# Unidad 1

## 🛠 Fase: Apply

### Actividad 05
El microbit al mantener presionado el boton A manda a la computadora "A" el cual es recibido en P5js, que al detectarlo cambia el color del cuadrado a rojo, y cuando no se esta precionando el boton A el cuadrado se pone verde.
### Actividad 06
[Link P5js](https://editor.p5js.org/lolarenzo2000/sketches/_uLAxVe1t)  
Codigo P5js
```js
  let port;
  let connectBtn;
  let connectionInitialized = false;

  function setup() {
    createCanvas(400, 400);
    background(220);
    port = createSerial();
    connectBtn = createButton("Connect to micro:bit");
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);
    x = 200
    speed = 10
  }

  function draw() {
    background(220);

    if (port.opened() && !connectionInitialized) {
      port.clear();
      connectionInitialized = true;
    }

    if (port.availableBytes() > 0) {
      let dataRx = port.read(1);
      if (dataRx == "I") {
        x -= speed;
      } else if (dataRx == "D") {
        x += speed;
      }
    }

    rectMode(CENTER);
    circle(x, height / 2, 50);

    if (!port.opened()) {
      connectBtn.html("Connect to micro:bit");
    } else {
      connectBtn.html("Disconnect");
    }
  }

  function connectBtnClick() {
    if (!port.opened()) {
      port.open("MicroPython", 115200);
      connectionInitialized = false;
    } else {
      port.close();
    }
  }
```
Codigo Micro:Bit
```py
from microbit import *

uart.init(baudrate=115200)

while True :
    if button_a.is_pressed():
        uart.write("I")
    if button_b.is_pressed():
        uart.write("D")

    sleep(100)
```
