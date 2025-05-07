
#### Esta es la solucion de mi actividad ✍️
---

#### **p5.js**

``` js
let connectBtn;
let serial;
let port;

function setup() {
  createCanvas(400, 400);
  textAlign(CENTER, CENTER);
  textSize(32);

  // Serial
  port = createSerial();
  
  connectBtn = createButton('Connect to micro:bit');
  connectBtn.position(130, 300);
  connectBtn.mousePressed(connectBtnClick);
}

let tiempo = 20;
let estado = "CONFIG";
let seqDesac = ["A", "B", "A", "S"];
let seqPropia = [];
let lastFrameTime = 0;

function draw() {
  background(220);

  if (estado === "CONFIG") {
    text("CONFIGURACIÓN", width / 2, height / 2 - 50);
    text("Tiempo: " + tiempo, width / 2, height / 2);
    if (!port.opened()) {
        connectBtn.html('Connect to micro:bit');
    }
    else {
        connectBtn.html('Disconnect');
    }
  } else if (estado === "ARMADO") {
    text("ARMADO", width / 2, height / 2 - 50);
    text("Tiempo: " + tiempo, width / 2, height / 2);

    if (millis() - lastFrameTime >= 1000 && tiempo > 0) {
      tiempo--;
      lastFrameTime = millis();
    }
    if (tiempo <= 0) {
      estado = "EXPLOSION";
    }
  } else if (estado === "EXPLOSION") {
    text("💀 EXPLOSIÓN 💀", width / 2, height / 2);
  }
  recibirDato()
}

function connectBtnClick() {
    if (!port.opened()) {
        port.open('MicroPython', 115200);
    } else {
        port.close();
    }
}

// Recibe datos del micro:bit
function recibirDato() {
  if(port.availableBytes() > 0){
    let data = port.read(1);
    if (data.length > 0) {
      manejarEvento(data);
    }
  }
}

// Reacciona a evento serial o teclado
function manejarEvento(key) {
  if (estado === "CONFIG") {
    manejarConfig(key);
  } else if (estado === "ARMADO") {
    manejarArmado(key);
  } else if (estado === "EXPLOSION") {
    manejarExplosion(key);
  }
}

function manejarConfig(key) {
  if (key === 'A') {
    tiempo = min(60, tiempo + 1);
  } else if (key === 'B') {
    tiempo = max(10, tiempo - 1);
  } else if (key === 'S') {
    estado = "ARMADO";
    lastFrameTime = millis();
    seqPropia = [];
  }
}

function manejarArmado(key) {
  if (key === 'A' || key === 'B' || key === 'S') {
    if (seqPropia.length >= 4) {
      seqPropia.shift();
    }
    seqPropia.push(key);

    if (seqPropia.length === seqDesac.length) {
      if (JSON.stringify(seqPropia) === JSON.stringify(seqDesac)) {
        estado = "CONFIG";
        tiempo = 20;
      }
    }
  }
}

function manejarExplosion(key) {
  if (key === 'T') {
    estado = "CONFIG";
    tiempo = 20;
  }
}

function keyPressed() {
  manejarEvento(key);
}

```

#### **MicroPython**

``` py
from microbit import *

while True:
    if button_a.was_pressed():
        uart.write("A\n")
    if button_b.was_pressed():
        uart.write("B\n")
    if accelerometer.was_gesture("shake"):
        uart.write("S\n")
    if pin_logo.is_touched():
        uart.write("T\n")

    display.show(Image.HEART)
    sleep(100)

```