#### Esta es la solucion de mi actividad ✍️
---

**Codigo micro:bit**
``` py
# Imports go at the top
from microbit import *

uart.init(baudrate=115200)

# Code in a 'while True:' loop repeats forever
while True:
    if uart.any():
        data = uart.read(1)
        if data:
            display.show(str(data, 'utf-8'))
```

**Codigo p5.js**
``` js
let port;
let connectBtn;
let sendBtnA, sendBtnB;

function setup() {
    createCanvas(400, 200);
    background(220);
    port = createSerial();
    connectBtn = createButton('Conectar a micro:bit');
    connectBtn.position(130, 50);
    connectBtn.mousePressed(connectToMicrobit);

    // Botón para enviar 'A'
    sendBtnA = createButton('Enviar A');
    sendBtnA.position(100, 100);
    sendBtnA.mousePressed(() => sendData('A'));

    // Botón para enviar 'B'
    sendBtnB = createButton('Enviar B');
    sendBtnB.position(200, 100);
    sendBtnB.mousePressed(() => sendData('B'));
}

function connectToMicrobit() {
    if (!port.opened()) {
        port.open('MicroPython', 115200);
    } else {
        port.close();
    }
}

function sendData(data) {
    if (port.opened()) {
        port.write(data); // Enviar el carácter al micro:bit
    } else {
        console.log("Micro:bit no conectado");
    }
}

```

#### Explicación del Código
**p5.js:**

- Se crea un puerto serial con `createSerial()`.
- Se implementa un botón para conectar/desconectar el micro:bit.
- Se crean botones para enviar los caracteres 'A' y 'B' al - micro:bit.
- Se usa `port.write(data)` para enviar datos.
**Micro:bit:**

- Se configura la UART con `uart.init()`.
- Si hay datos disponibles, se leen y se muestran en la pantalla LED.