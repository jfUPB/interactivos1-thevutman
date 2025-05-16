
#### Esta es la solucion de mi actividad ✍️
---

#### **Análisis del Código:**
**1. Setup inicial**
``` js
const express = require('express');
const http = require('http');
const socketIO = require('socket.io');

const app = express();
const server = http.createServer(app);
const io = socketIO(server);
const port = 3000;
```
- `express`: framework que facilita la creación del servidor web.
- `http`: módulo básico de Node.js para crear el servidor HTTP.
- `socket.io`: permite comunicación en tiempo real usando WebSockets.
- Se crea una aplicación Express, se monta un servidor HTTP sobre ella, y se enlaza Socket.IO para gestionar las conexiones WebSocket.

**2. Servir archivos estáticos**
``` js
app.use(express.static('public'));
```
- Esta línea configura el servidor para servir automáticamente archivos estáticos desde la carpeta `public`.
- Por ejemplo: si el navegador pide `/mobile/index.html`, el servidor lo busca en `public/mobile/index.html`.

**3. Manejo de conexiones y eventos**
``` js
io.on('connection', (socket) => {
    console.log('New client connected - ID:', socket.id);

    socket.on('message', (message) => {
        console.log(`Received message => ${message} from ID: ${socket.id}`);
        socket.broadcast.emit('message', message);
    });

    socket.on('disconnect', () => {
        console.log('Client disconnected - ID:', socket.id);
    });
});
```
- `io.on('connection', callback)`: se ejecuta cada vez que un cliente se conecta.

- `socket.on('message')`: escucha el evento 'message' que puede provenir del móvil.

- `socket.broadcast.emit('message')`: retransmite ese mensaje a todos los demás clientes, excepto al que lo envió.

- `socket.on('disconnect')`: avisa cuando un cliente se desconecta.

**4. Inicio del servidor**
``` js
server.listen(port, () => {
    console.log(`Server is listening on http://localhost:${port}`);
});
```
- El servidor empieza a escuchar conexiones en el puerto 3000.
- Se imprime en consola que el servidor está activo.

#### **Preguntas de Reflexión**
**1. ¿Cuál es la función principal de `express.static('public')`?**
- Sirve automáticamente todos los archivos estáticos dentro de la carpeta `public`.
- Es más eficiente y flexible que usar `app.get('/ruta', handler)` como en la Unidad 6, ya que no requiere definir manualmente cada ruta. Simplemente se accede mediante la estructura de carpetas y nombres de archivo.

**2. Explica detalladamente el flujo de un mensaje táctil:**
- Cliente móvil detecta un toque y emite un evento `'message'` con los datos (por ejemplo, posición X/Y del dedo en JSON).
- Servidor (server.js) recibe este evento con `socket.on('message')`.
- El servidor retransmite el mensaje a todos los demás clientes conectados usando `socket.broadcast.emit('message', message)`.
- Cliente escritorio escucha el evento `'message'` y actualiza la interfaz según los datos recibidos.

**¿Por qué `socket.broadcast.emit`?**
- Porque solo queremos que los demás clientes reciban el mensaje, no el que lo envió (el móvil).
- Si se usara `io.emit`, todos los clientes, incluido el móvil, recibirían el mensaje.
- Si se usara `socket.emit`, solo el móvil se enviaría el mensaje a sí mismo (lo cual no tiene sentido).

**3. Si conectaras dos computadores de escritorio y un móvil, ¿quién recibiría el mensaje?**
- Ambos computadores de escritorio recibirían el mensaje que envía el móvil.
- El móvil no lo recibe, ya que el servidor usa `socket.broadcast.emit`.
- Esto permite que los escritorios reaccionen al movimiento táctil del móvil en tiempo real, sin que el móvil se vea afectado por sus propios mensajes.

**4. ¿Qué información útil proporcionan los `console.log` del servidor?**
- Identifican cuándo un cliente se conecta o se desconecta, y muestran su ID único.
- Muestran el contenido de cada mensaje recibido y el ID del cliente que lo envió.
- Esto es útil para depurar el sistema y confirmar que los eventos están ocurriendo correctamente.