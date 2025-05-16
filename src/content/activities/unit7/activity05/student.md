
#### Esta es la solucion de mi actividad ✍️
---

#### **mobile/sketch.js**
``` js
let socket;
let rSlider, gSlider, bSlider;
let strokeCheckbox;

function setup() {
    createCanvas(windowWidth, windowHeight);
    background(220);

    // Conectar al servidor de Socket.IO
    //let socketUrl = 'http://localhost:3000';
    socket = io();

    socket.on('connect', () => {
        console.log('Connected to server');
    });

    socket.on('message', (data) => {
        console.log(`Received message: ${data}`);
    });

    socket.on('disconnect', () => {
        console.log('Disconnected from server');
    });

    socket.on('connect_error', (error) => {
        console.error('Socket.IO error:', error);
    });

    // Sliders de color
    rSlider = createSlider(0, 255, 150);
    rSlider.position(10, 10);
    gSlider = createSlider(0, 255, 100);
    gSlider.position(10, 40);
    bSlider = createSlider(0, 255, 255);
    bSlider.position(10, 70);

    // Checkbox de stroke
    strokeCheckbox = createCheckbox('Stroke', true);
    strokeCheckbox.position(10, 100);
}

function touchMoved() {
  let data = {
    x: mouseX,
    y: mouseY,
    color: {
      r: rSlider.value(),
      g: gSlider.value(),
      b: bSlider.value()
    },
    useStroke: strokeCheckbox.checked()
  };

  socket.emit('message', JSON.stringify(data));
  return false; // Evita el scroll
}
```

#### **desktop/sketch.js**

``` js
let socket;
let particles = [];

function setup() {
  createCanvas(windowWidth, windowHeight);
  background(0);

    //let socketUrl = 'http://localhost:3000';
    socket = io(); 

    // Evento de conexión exitosa
    socket.on('connect', () => {
        console.log('Connected to server');
    });

    // Recibir mensaje del servidor
    socket.on('message', (data) => {
        console.log(`Received message: ${data}`);
        try {
            let parsedData = JSON.parse(data);
            console.log(`Received data: ${parsedData.x}`);
            // if (parsedData && parsedData.type === 'touch') {
            //     circleX = parsedData.x;
            //     circleY = parsedData.y;
            // }
            particles.push(new Particle(parsedData.x, parsedData.y, parsedData.color, parsedData.useStroke));
        } catch (e) {
            console.error("Error parsing received JSON:", e);
        }
    });    

    // Evento de desconexión
    socket.on('disconnect', () => {
        console.log('Disconnected from server');
    });

    socket.on('connect_error', (error) => {
        console.error('Socket.IO error:', error);
    });

  // Escuchar datos del móvil
}

function draw() {
  for (let i = particles.length - 1; i >= 0; i--) {
    particles[i].update();
    particles[i].display();
    if (particles[i].isDead()) {
      particles.splice(i, 1);
    }
  }

  if (particles.length === 0) background(0, 20);
}

class Particle {
  constructor(x, y, color, useStroke) {
    this.pos = createVector(x, y);
    this.vel = p5.Vector.random2D();
    this.lifespan = 255;
    this.size = random(5, 20);
    this.color = color;
    this.useStroke = useStroke;
    this.noiseOffset = random(1000);
  }

  update() {
    let angle = noise(this.pos.x * 0.005, this.pos.y * 0.005, this.noiseOffset) * TWO_PI * 2;
    let force = p5.Vector.fromAngle(angle);
    force.mult(0.5);
    this.vel.add(force);
    this.vel.limit(4);
    this.pos.add(this.vel);
    this.lifespan -= 3;
  }

  display() {
    fill(this.color.r, this.color.g, this.color.b, this.lifespan);
    if (this.useStroke) {
      stroke(255, this.lifespan);
    } else {
      noStroke();
    }
    ellipse(this.pos.x, this.pos.y, this.size);
  }

  isDead() {
    return this.lifespan < 0;
  }
}
```
#### **server.js**
``` js
const express = require('express');
const http = require('http');
const socketIO = require('socket.io');

const app = express();
const server = http.createServer(app); 
const io = socketIO(server); 
const port = 3000;

app.use(express.static('public'));

io.on('connection', (socket) => {
    console.log('New client connected');
    console.log("hola")
    socket.on('message', (message) => {
        console.log("hola")
        console.log(`Received message => ${message}`);
        socket.broadcast.emit('message', message);
    });

    socket.on('disconnect', () => {
        console.log('Client disconnected');
    });
});

server.listen(port, () => {
    console.log(`Server is listening on http://localhost:${port}`);
});
```

#### **Cambios en `mobile/sketch.js`**
Agregué sliders de color (R, G, B) y una casilla de verificación para activar/desactivar el stroke. En cada `touchMoved()` se envían estos datos al servidor:

```js
socket.emit('touchData', {
  x: mouseX,
  y: mouseY,
  color: { r: rSlider.value(), g: gSlider.value(), b: bSlider.value() },
  useStroke: strokeCheckbox.checked()
});
```
#### **Cambios en `desktop/sketch.js`**
Se agregaron las siguientes funciones:

``` js
socket.on('touchData', (data) => {
  particles.push(new Particle(data.x, data.y, data.color, data.useStroke));
});
```
La clase `Particle` fue modificada para recibir el color y si usa stroke. En `display()` se aplica `fill` con el color recibido y se activa/desactiva el `stroke()`.