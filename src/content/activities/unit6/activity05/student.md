
#### Esta es la solucion de mi actividad ✍️
---

#### **Idea Creativa: "Duelo de Dibujo en Tiempo Real"**
**Descripción:**
Dos usuarios se conectan y compiten en un reto de dibujo en tiempo real. Uno es el retoador, que propone un dibujo (por ejemplo, una palabra como "gato"), y el otro es el dibujante, que tiene que dibujarlo en 30 segundos. Al final, ambos votan si se logró o no. La comunicación bidireccional sirve para compartir el reto, el dibujo y los votos.

#### **Planificación e Implementación**
**1. Conceptualización**
- **Datos a intercambiar:**
    - Texto del reto (retoador → dibujante).
    - Datos del dibujo (dibujante → retoador).
    - Votos (ambos → servidor).

- **Visualización:**
    - Página del retoador: interfaz para escribir el reto y ver el dibujo en tiempo real.
    - Página del dibujante: canvas para dibujar y ver el reto.
    - Ambos votan al final.

**2. Archivos involucrados**
- **`server.js` — Cambios necesarios:**
    - Evento enviarReto
    - Evento enviarDibujo
    - Evento enviarVoto
- **`page1.js` (Retoador):**
    - Enviar reto.
    - Recibir dibujo.
    - Enviar voto.
- **`page2.js` (Dibujante):**
    - Recibir reto.
    - Enviar dibujo en tiempo real (coordenadas del mouse).
    - Enviar voto.
#### **Código**
**server.js**
``` js
const express = require("express");
const app = express();
const server = require("http").Server(app);
const io = require("socket.io")(server);

app.use(express.static("public"));

io.on("connection", socket => {
  console.log("Cliente conectado");

  socket.on("enviarReto", reto => {
    socket.broadcast.emit("recibirReto", reto);
  });

  socket.on("enviarDibujo", punto => {
    socket.broadcast.emit("recibirDibujo", punto);
  });

  socket.on("enviarVoto", voto => {
    socket.broadcast.emit("recibirVoto", voto);
  });
});

server.listen(3000, () => {
  console.log("Servidor corriendo en puerto 3000");
});
```
**public/page1.js (Retoador)**
``` js
let socket;
let retoInput;
let dibujo = [];

function setup() {
  createCanvas(400, 400);
  background(255);

  retoInput = createInput();
  retoInput.position(10, 420);
  let boton = createButton("Enviar reto");
  boton.position(200, 420);
  boton.mousePressed(() => {
    let texto = retoInput.value();
    socket.emit("enviarReto", texto);
  });

  socket = io();
  socket.on("recibirDibujo", punto => {
    stroke(0);
    strokeWeight(4);
    line(punto.x, punto.y, punto.px, punto.py);
  });

  socket.on("recibirVoto", voto => {
    console.log("Voto recibido:", voto);
  });
}

function keyPressed() {
  if (key === "S") {
    let voto = prompt("¿Logró el dibujo representar el reto? (sí/no)");
    socket.emit("enviarVoto", voto);
  }
}
```
**public/page2.js (Dibujante)**
``` js
let socket;
let reto = "";

function setup() {
  createCanvas(400, 400);
  background(255);

  socket = io();
  socket.on("recibirReto", texto => {
    reto = texto;
  });

  socket.on("recibirVoto", voto => {
    console.log("Voto recibido:", voto);
  });

  let boton = createButton("Votar");
  boton.position(10, 420);
  boton.mousePressed(() => {
    let voto = prompt("¿Te parece que tu dibujo representa bien el reto? (sí/no)");
    socket.emit("enviarVoto", voto);
  });
}

function draw() {
  fill(0);
  noStroke();
  textSize(16);
  text("Reto: " + reto, 10, 20);

  if (mouseIsPressed) {
    stroke(0);
    strokeWeight(4);
    line(mouseX, mouseY, pmouseX, pmouseY);
    socket.emit("enviarDibujo", {
      x: mouseX,
      y: mouseY,
      px: pmouseX,
      py: pmouseY
    });
  }
}
```

#### **Reflexión Final**
- **¿Qué fue fácil?**
    Implementar la lógica de conexión básica con Socket.IO fue sencillo gracias al caso base.
- **¿Qué fue difícil?**
    Coordinar el flujo de datos en tiempo real entre clientes y definir cuándo enviar/recibir los mensajes. La sincronización del dibujo y los votos fue un reto.
- **¿Qué aprendí?**
    A usar eventos personalizados en Socket.IO, a estructurar flujos de interacción creativos entre dos usuarios, y a planificar una aplicación interactiva en tiempo real desde cero.