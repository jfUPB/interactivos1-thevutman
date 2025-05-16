#### Esta es la solucion de mi actividad ✍️
---

Para permitir la selección de cuatro imágenes en el micro:bit utilizando p5.js, implementé un sistema de comunicación serial entre la computadora y el microcontrolador. La interacción ocurre de la siguiente manera:  

1. **Interfaz en p5.js**  
   - Se creó una interfaz gráfica con cuatro botones, cada uno asociado a una imagen diferente en el micro:bit.  
   - Cuando se presiona un botón, se envía un carácter específico a través del puerto serial.  

2. **Código en micro:bit (MicroPython)**  
   - Se inicializa la comunicación UART para recibir datos desde p5.js.  
   - Dependiendo del carácter recibido ('h', 'g', 'w', 'r'), se muestra una imagen correspondiente en la matriz de LEDs del micro:bit.  
   - También se implementó la detección de botones y gestos en el micro:bit para enviar datos a p5.js. 

**micro:bit**
``` py
let port;
let connectBtn;

function setup() {
    createCanvas(400, 400);
    background(220);
    port = createSerial();
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(130, 260);
    connectBtn.mousePressed(connectBtnClick);
    let sendBtn = createButton('Send happy');
    sendBtn.position(40, 300);
    sendBtn.mousePressed(sendBtnClick2);
    let sendBtn2 = createButton('Send duck');
    sendBtn2.position(135, 300);
    sendBtn2.mousePressed(sendBtnClick3);
    let sendBtn3 = createButton('Send no');
    sendBtn3.position(220, 300);
    sendBtn3.mousePressed(sendBtnClick4);
    let sendBtn4 = createButton('Send sad');
    sendBtn4.position(295, 300);
    sendBtn4.mousePressed(sendBtnClick);
    fill('white');
    ellipse(width / 2, height / 2, 100, 100);
}

function draw() {

    if(port.availableBytes() > 0){
        let dataRx = port.read(1);
        if(dataRx == 'A'){
            fill('red');
        }
        else if(dataRx == 'B'){
            fill('yellow');
        }
        else{
            fill('green');
        }
        background(220);
        ellipse(width / 2, height / 2, 100, 100);
        fill('black');
        text(dataRx, width / 2, height / 2);
    }


    if (!port.opened()) {
        connectBtn.html('Connect to micro:bit');
    }
    else {
        connectBtn.html('Disconnect');
    }
}

function connectBtnClick() {
    if (!port.opened()) {
        port.open('MicroPython', 115200);
    } else {
        port.close();
    }
}

function sendBtnClick() {
    port.write('g');
}
function sendBtnClick2() {
    port.write('h');
}
function sendBtnClick3() {
    port.write('w');
}
function sendBtnClick4() {
    port.write('r');
}
```

**p5.js**
``` js
from microbit import *

uart.init(baudrate=115200)
display.show(Image.BUTTERFLY)

while True:
    if button_a.is_pressed():
        uart.write('A');
        sleep(500);
    if button_b.is_pressed():
        uart.write('B')
        sleep(500)
    if accelerometer.was_gesture('shake'):
        uart.write('C')
        sleep(500)
    if uart.any():
        data = uart.read(1)
        if data:
            if data[0] == ord('h'):
                display.show(Image.HEART)
                sleep(500)
                display.show(Image.HAPPY)
            elif data[0] == ord('g'):
                display.show(Image.SAD)
                sleep(500)
            elif data[0] == ord('w'):
                display.show(Image.DUCK)
                sleep(500)
            elif data[0] == ord('r'):
                display.show(Image.NO)
                sleep(500)
```