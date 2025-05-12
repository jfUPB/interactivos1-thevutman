#### Esta es la solucion de mi actividad ✍️
---

#### **Código Origianal**

- **Enlace**: [https://editor.p5js.org/supervejito80/sketches/5AMEZ4guC](https://editor.p5js.org/supervejito80/sketches/5AMEZ4guC)

---

#### **Código Modificado**

``` js
let port;
let connectBtn;
let microBitConnected = false;

let microBitX = 0;
let microBitY = 0;
let microBitAState = false;
let microBitBState = false;

let rotationX = 0;
let rotationY = 0;

let serialBuffer = [];

function setup() {
  createCanvas(710, 400, WEBGL);
  angleMode(DEGREES);
  strokeWeight(5);
  noFill();
  stroke(32, 8, 64);

  port = createSerial();
  connectBtn = createButton("Connect to micro:bit");
  connectBtn.position(10, 10);
  connectBtn.mousePressed(connectBtnClick);
}

function connectBtnClick() {
  if (!port.opened()) {
    port.open("MicroPython", 115200);
  } else {
    port.close();
  }
}

function draw() {
  background(240, 200, 220);

  // Verifica si el puerto está abierto
  if (!port.opened()) {
    connectBtn.html("Connect to micro:bit");
    return;
  } else {
    connectBtn.html("Disconnect");
    microBitConnected = true;
  }

  readSerialData();

  // Mapear valores del acelerómetro a rotación
  rotationX = map(microBitY, -1024, 1024, -45, 45);
  rotationY = map(microBitX, -1024, 1024, -45, 45);

  rotateX(rotationX);
  rotateY(rotationY);

  box(100);

  // Opcional: visualiza los botones presionados
  if (microBitAState) {
    fill(255, 0, 0, 100);
    sphere(20);
    noFill();
  }
  if (microBitBState) {
    push();
    fill(0, 0, 255, 100);
    translate(0, 0, 60);
    cone(10, 50);
    pop();
    noFill();
  }
}

function readSerialData() {
  let available = port.availableBytes();
  if (available > 0) {
    let newData = port.readBytes(available);
    serialBuffer = serialBuffer.concat(newData);
  }

  while (serialBuffer.length >= 8) {
    if (serialBuffer[0] !== 0xAA) {
      serialBuffer.shift();
      continue;
    }

    if (serialBuffer.length < 8) break;

    let packet = serialBuffer.slice(0, 8);
    serialBuffer.splice(0, 8);

    let dataBytes = packet.slice(1, 7);
    let receivedChecksum = packet[7];
    let computedChecksum = dataBytes.reduce((acc, val) => acc + val, 0) % 256;

    if (computedChecksum !== receivedChecksum) {
      console.log("Checksum error");
      continue;
    }

    let buffer = new Uint8Array(dataBytes).buffer;
    let view = new DataView(buffer);
    microBitX = view.getInt16(0); // bytes 1 y 2
    microBitY = view.getInt16(2); // bytes 3 y 4
    microBitAState = view.getUint8(4) === 1;
    microBitBState = view.getUint8(5) === 1;
  }
}

```

---

#### **Codigo Modificado**

- **Enlace con binario**: [https://editor.p5js.org/supervejito80/sketches/q8UqFtX3c](https://editor.p5js.org/supervejito80/sketches/q8UqFtX3c)

---

#### **Video de Muestra**

- **Enlace con binario**: [https://drive.google.com/file/d/1kFB7KpcBavzjxQaXGtYbFy4wBDXAiEje/view?usp=sharing](https://drive.google.com/file/d/1kFB7KpcBavzjxQaXGtYbFy4wBDXAiEje/view?usp=sharing)
https://drive.google.com/file/d/1kFB7KpcBavzjxQaXGtYbFy4wBDXAiEje/view?usp=sharing