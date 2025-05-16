
#### Esta es la solucion de mi actividad ✍️
---

#### **1. Conexión inicial**
**¿Ves algún error relacionado con la conexión cuando detienes el servidor y recargas page2.html? ¿Qué indica?**

Sí. En la consola aparece un error que dice algo como:

``` pgsql
WebSocket connection to 'ws://localhost:3000/socket.io/…' failed.
```
Esto indica que el navegador intentó conectarse al servidor mediante WebSockets, pero no había ningún servidor ejecutándose en ese momento. Por lo tanto, la conexión falla.

**¿Desaparecen los errores al reiniciar el servidor y recargar la página?**

Sí. Al reiniciar el servidor y recargar `page2.html`, el cliente se conecta correctamente y ya no aparecen errores. Se imprime en consola algo como:

``` css
Connected to server - My ID: D3fsj2kL0...
```

#### **2. Manejando la conexión establecida**
**¿Qué pasó en page1 antes de que movieras page2, si comentamos `socket.emit('win2update', currentPageData, socket.id)`?**

Page1 no tenía información sobre page2 hasta que se detectó un movimiento o cambio en la ventana de page2. Esto se debe a que sin esa línea, page2 no envía su estado inicial al servidor al conectarse.

**¿Por qué es útil enviar el estado inicial al conectarse?**

Porque permite que la otra página (page1) tenga acceso inmediato a la información sobre page2, sin necesidad de esperar un cambio. Esto mejora la sincronización y la representación visual desde el inicio.

#### **3. Recibiendo datos del servidor**
**¿Se dispara el log “Page 2 received data…” al mover la ventana de page1? ¿Qué datos muestra?**

Sí. En la consola de `page2` se imprime:

``` yaml
Page 2 received data about the other window: { x: ..., y: ..., width: ..., height: ... }
```

Esto confirma que está recibiendo correctamente los datos enviados por el servidor después de que page1 los emite.

**¿Se dispara este log al mover la ventana de page2?**

No. Porque `page2` no se está enviando datos a sí misma. El servidor emite la información recibida de un cliente a los demás clientes conectados (broadcast), pero no de vuelta al mismo que envió.

#### **4. Detectando cambios y enviando actualizaciones**
**¿Cuándo aparece el mensaje “Page 2 detected change…”?**

Cuando muevo la ventana de page2, ya sea su posición o su tamaño, el mensaje aparece en consola justo después del cambio.

**¿Aparece el mensaje si la ventana no se mueve?**

No. El mensaje solo aparece si hay una diferencia entre el estado actual (`currentPageData`) y el anterior (`previousPageData`).

**¿Por qué es eficiente esta estrategia de comparar con el estado anterior antes de enviar datos por la red?**

Porque evita enviar información innecesaria. Solo se transmite cuando hay un cambio real. Esto reduce la carga de la red, mejora el rendimiento y hace el sistema más escalable y eficiente.

#### **5. Visualización y creatividad**
**Modificación 1 – Color de fondo depende de la distancia entre ventanas:**

``` javascript
let distancia = resultingVector.mag();
background(map(distancia, 0, 1000, 255, 0)); // entre blanco y negro
```
A medida que las ventanas se alejan entre sí, el fondo se vuelve más oscuro. Esto da una idea visual clara de la “proximidad” entre las ventanas.

**Modificación 2 – Tamaño del círculo depende del ancho de la ventana remota:**

```javascript
drawCircle(point2[0], point2[1], remotePageData.width / 4); // se pasa el tamaño
```
Y la función `drawCircle` se modificó para aceptar el tamaño:

``` javascript
function drawCircle(x, y, size = 150) {
    ellipse(x, y, size, size);
}
```
Si la otra ventana se redimensiona, el círculo en esta ventana cambia de tamaño dinámicamente. Ayuda a visualizar el estado del otro cliente.

**Modificación 3 – Color de línea depende de la posición:**

``` javascript
if (resultingVector.x < 0) {
    stroke('red'); // si está a la izquierda
} else {
    stroke('green'); // si está a la derecha
}
```
Es fácil ver de un vistazo si la otra ventana está a la izquierda o derecha. Es una buena forma de usar visualización contextual.

#### **Reflexión final:**

Esta actividad me ayudó a comprender cómo los clientes interactúan entre sí a través de un servidor usando Socket.IO. Aprendí que:
- El `emit` permite a los clientes enviar datos.
- El `on` permite reaccionar a eventos de entrada.
- La comparación entre estado actual y anterior es clave para optimizar la comunicación.
- Los datos recibidos se pueden usar para representaciones gráficas creativas e interactivas.

También noté que la visualización puede volverse muy expresiva si se combinan conceptos como vectores, color y geometría. Esto tiene mucho potencial en proyectos colaborativos, visualización de datos o juegos interactivos en red.