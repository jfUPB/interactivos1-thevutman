
#### Esta es la solucion de mi actividad ✍️
---

#### **COMPONENTES CLAVE DEL SISTEMA**
**1. Aplicación Cliente Móvil (`mobile/sketch.js`)**
- Captura los eventos táctiles del usuario.
- Permite elegir color y activar/desactivar `stroke`.
- Envía los datos por `socket.emit()` al servidor.

**2. Servidor Node.js (`server.js`)**
- Recibe los datos desde el móvil por `socket.on()`.
- Usa `socket.broadcast.emit()` para enviar los datos al cliente de escritorio.
- Es el "puente" de comunicación entre el móvil y el escritorio.

**3. VS Code Dev Tunnels**
- Hace accesible el servidor local en internet mediante un URL público.
- Permite que el móvil (fuera de la red local) se conecte al servidor.

**4. Aplicación Cliente de Escritorio (`desktop/sketch.js`)**
- Escucha los datos enviados por el servidor.
- Dibuja las partículas en base a esos datos (posición, color, stroke).
- El canvas se actualiza en tiempo real.

**5. El Usuario**
- Interactúa desde el móvil (toques, selección de color y stroke).

#### **DIAGRAMA**
``` less
[ Usuario ]
     |
     v
[ Móvil: mobile/sketch.js ]
     |
     |  --> Evento touch (x, y)
     |  --> Color seleccionado
     |  --> Stroke ON/OFF
     v
[ Servidor Node.js (server.js) ]
     ^                            ^
     |                            |
     |  socket.emit('message', {x, y, color, stroke})
     |                            |
     |----------------------------|
     |
     v
[ Escritorio: desktop/sketch.js ]
     |
     v
Dibujo en canvas con p5.js
     ^
     |
     |  Datos: { x, y, color, stroke }
     |
[ Dev Tunnels ]
(Intermediario público entre móvil y servidor)
```

#### **EXPLICACIÓN DEL ROL DE CADA COMPONENTE**
**1. Móvil**
- Captura el input del usuario (posición del toque, color, y si se usa `stroke`).
- Envia esos datos en formato JSON usando `socket.emit()`.

**2. Servidor Node.js**
- Recibe los datos del móvil.
- Los retransmite al cliente de escritorio usando `socket.broadcast.emit()`.
- Es el canal de comunicación principal.

**3. VS Code Dev Tunnels**
- Hace público el servidor en localhost para que sea accesible desde el móvil.
- Funciona como una "puerta de entrada" para que el móvil se conecte a tu máquina local.

**4. Escritorio**
- Recibe la información desde el servidor.
- Dibuja las partículas en canvas usando los datos recibidos.

**5. Usuario**
- Controla toda la experiencia desde el móvil (es el input principal del sistema).