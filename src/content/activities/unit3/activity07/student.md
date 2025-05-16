
#### Esta es la solucion de mi actividad ✍️
---

``` js
function setup() {
  createCanvas(400, 400);
  textAlign(CENTER, CENTER);
  textSize(32);
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
  if (key === 'A' || key === 'B') {
    if (seqPropia.length >= 4) {
      seqPropia.shift(); // Elimina el primer elemento si ya hay 4
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
  if (estado === "CONFIG") {
    manejarConfig(key);
  } else if (estado === "ARMADO") {
    manejarArmado(key);
  } else if (estado === "EXPLOSION") {
    manejarExplosion(key);
  }
}
```