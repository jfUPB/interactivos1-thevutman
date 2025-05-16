#### Esta es la solucion de mi actividad ✍️
---

#### Codigo p5.js
``` js
let port;
let connectBtn;

function setup() {
    createCanvas(400, 400);
    background(220);
    port = createSerial();
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);
    let sendBtn = createButton('Send Love');
    sendBtn.position(220, 300);
    sendBtn.mousePressed(sendBtnClick);
    fill('white');
    square(200, 200, 55);
}

function draw() {

    if(port.availableBytes() > 0){
        let dataRx = port.read(1);
        if(dataRx == 'A'){
            fill('red');
        }
        background(220);
        noStroke();
        square(200, 200, 55);
        fill('white');
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
    port.write('h');
}

```

Para realizar este ejercicio lo que hice fue usar el código anterior de la actividad que nos permitía conectar con micro:bit y use el mismo código de p5.js anterior y le cambie algunas cosas como cambiar el círculo  por un cuadrado con relleno blanco y borre las funciones que hacían otras interacciones y deje solo la de presionar el botón 'A' cambie de color el cuadrado con un fill.


