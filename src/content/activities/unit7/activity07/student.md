
#### Esta es la solucion de mi actividad ✍️
---

#### **Autoevaluación de Objetivos de Aprendizaje**

|Objetivo de Aprendizaje	|Mi puntuación (2-5)|
|---------------------------|-------------------|
|Configurar y usar VS Code Dev Tunnels	|4|
|Implementar arquitectura cliente-servidor (móvil → servidor)	|5|
|Usar Socket.IO para retransmitir datos (servidor → escritorio)	|4|
|Capturar y procesar eventos en el móvil (p5.js)	|5|
|Modificar el sistema interactivo para crear una experiencia personalizada	|4|
|Analizar y explicar el flujo completo de datos (móvil → servidor → escritorio)	|5|

#### **Reflexión sobre mi proceso de aprendizaje**
**¿Qué fue más fácil?**

La parte más fácil para mí fue capturar eventos táctiles en el móvil usando p5.js, porque ya estaba familiarizado con p5 y su sistema de eventos (`touchStarted`, `mouseDragged`, etc.). La visualización inmediata del canvas ayudó mucho a comprender el comportamiento.

**¿Qué fue más difícil?**

Lo más difícil fue configurar correctamente el túnel con VS Code Dev Tunnels y asegurarme de que el móvil pudiera conectarse al servidor local. Al principio tenía problemas con los puertos y la conexión fallaba. Lo solucioné revisando la documentación y viendo tutoriales.

#### **¿Qué estrategias me ayudaron?**
- Probar el sistema paso por paso (primero el canvas, luego el servidor, después los sockets).
- Imprimir mensajes en consola (`console.log()`) para rastrear si los datos llegaban o no.
- Usar diagramas y mapas mentales para visualizar el flujo de datos.
- Leer ejemplos en la documentación oficial de Socket.IO y p5.js.

#### **Explicación del flujo de información (como si se lo explicara a alguien más)**
El usuario interactúa desde su celular, tocando la pantalla y eligiendo un color o si quiere trazo (`stroke`). Esa información (posición, color y opciones) se envía como un mensaje JSON al servidor (Node.js), usando la tecnología Socket.IO que permite enviar datos en tiempo real.

El servidor está corriendo en mi computador, pero gracias a VS Code Dev Tunnels puede recibir mensajes desde internet. Entonces, el celular se conecta a ese túnel.

Luego, el servidor retransmite los datos al cliente de escritorio (otro navegador), que los recibe y los dibuja en pantalla con p5.js, mostrando las figuras que se controlan desde el móvil.

#### **¿Cómo puedo aplicar esto en otros proyectos?**
Puedo aplicar lo aprendido en varios contextos:
- **Controladores remotos personalizados:** por ejemplo, usar el celular como un control para una instalación interactiva o un videojuego.
- **Visualización en vivo:** conectar sensores o interfaces táctiles móviles para controlar visualizaciones en pantallas grandes.
- **Educación remota:** permitir que los estudiantes interactúen con una pizarra compartida usando sus celulares.
- **Arte interactivo:** controlar una obra visual o sonora en tiempo real desde un dispositivo móvil.