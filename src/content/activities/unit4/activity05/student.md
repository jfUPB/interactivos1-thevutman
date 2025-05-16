
#### Esta es la solucion de mi actividad ✍️

**Enlace a la aplicación original sin modificar [aqui](https://editor.p5js.org/supervejito80/sketches/5AMEZ4guC)**

#### **Código p5.js de la versión modificada:**
```javascript

let serial;
let rotationX = 0;
let rotationY = 0;
let strokeCol = [32, 8, 64]; // color inicial

function setup() {
  createCanvas(710, 400, WEBGL);
  angleMode(DEGREES);
  strokeWeight(5);
  noFill();
  serial = createSerial();
  serial.open(9600);
  background(240, 200, 220);
}

function draw() {
  background(240, 200, 220);
  orbitControl();

  // Leer datos del micro:bit
  let data = serial.readLine();
  if (data) {
    let values = split(trim(data), ",");
    if (values.length === 4) {
      let xVal = int(values[0]);
      let yVal = int(values[1]);
      let a = int(values[2]);
      let b = int(values[3]);

      // Mapeo de los valores del acelerómetro
      rotationX = map(yVal, -1024, 1024, -90, 90);
      rotationY = map(xVal, -1024, 1024, -90, 90);

      // Cambio de color con los botones
      if (a === 1) {
        strokeCol = [255, 0, 0]; // rojo
      } else if (b === 1) {
        strokeCol = [0, 0, 255]; // azul
      } else {
        strokeCol = [32, 8, 64]; // color original
      }
    }
  }

  rotateX(rotationX);
  rotateY(rotationY);
  stroke(strokeCol);

  for (let zAngle = 0; zAngle < 180; zAngle += 30) {
    for (let xAngle = 0; xAngle < 360; xAngle += 30) {
      push();
      rotateZ(zAngle);
      rotateX(xAngle);
      translate(0, 400, 0);
      box();
      pop();
    }
  }
}
```

#### **Enlace a la aplicación modificada en el editor de p5.js [aqui](https://editor.p5js.org/supervejito80/sketches/SNV0PyAwf)**

#### **Capturas de pantalla del canvas de la aplicación modificada:**
