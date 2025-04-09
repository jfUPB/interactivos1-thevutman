
#### Esta es la solucion de mi actividad ✍️
---

``` js
let port;
let botonA, botonB, botonS, botonT;

function setup() {
  createCanvas(400, 200);
  background(220);
  
  port = createSerial();

  botonA = createButton('Botón A');
  botonA.position(30, 30);
  botonA.mousePressed(() => enviarEvento('A'));

  botonB = createButton('Botón B');
  botonB.position(120, 30);
  botonB.mousePressed(() => enviarEvento('B'));

  botonS = createButton('Shake');
  botonS.position(210, 30);
  botonS.mousePressed(() => enviarEvento('S'));

  botonT = createButton('Touch');
  botonT.position(300, 30);
  botonT.mousePressed(() => enviarEvento('T'));

  // Botón para conectar al puerto serial
  let botonConectar = createButton('Conectar micro:bit');
  botonConectar.position(30, 100);
  botonConectar.mousePressed(connectBtnClick);
}

function connectBtnClick() {
    if (!port.opened()) {
        port.open('MicroPython', 115200);
    } else {
        port.close();
    }
}

function enviarEvento(valor) {
    port.write(valor + '\n');
    console.log('Enviado: ' + valor);
}

```