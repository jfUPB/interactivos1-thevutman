
#### Esta es la solucion de mi actividad ✍️
---

#### **Propósito principal de `mobile/sketch.js` y `desktop/sketch.js`**
- `mobile/sketch.js`: Este script funciona como cliente emisor. Su propósito es capturar el movimiento del dedo sobre una pantalla táctil y enviar las coordenadas del toque al servidor en tiempo real usando Socket.IO, optimizando la cantidad de datos enviados mediante un umbral (threshold).
- `desktop/sketch.js`: Este script es el cliente receptor. Se encarga de escuchar los mensajes reenviados por el servidor, decodificarlos y actualizar la posición de un círculo en el canvas según los datos recibidos del cliente móvil.

#### **Explicación de `touchMoved()` en el cliente móvil**
La función touchMoved() se activa automáticamente cada vez que el usuario arrastra el dedo sobre el canvas. Aquí está el desglose:
- **Threshold:** Se utiliza un umbral (por ejemplo, 5 píxeles) para evitar enviar demasiados datos cuando el movimiento es mínimo. Esto mejora el rendimiento y reduce la sobrecarga de la red.
- **Detección de movimiento:** Se calcula la diferencia entre la posición actual (`mouseX`, `mouseY`) y la última posición enviada (`lastTouchX`, `lastTouchY`). Solo si esta diferencia supera el threshold se envía un nuevo mensaje.
- **Formato de datos:** Se crea un objeto `touchData` con tres propiedades:

``` javascript
{
  type: 'touch',
  x: mouseX,
  y: mouseY
}
```
Este objeto se convierte en texto con `JSON.stringify(touchData)` para transmitirlo por Socket.IO.

- Emisión del mensaje:

``` javascript
socket.emit('message', JSON.stringify(touchData));
```
- Prevención del comportamiento por defecto: `return false` evita efectos no deseados del navegador, como hacer scroll al mover el dedo.

#### **Procesamiento de datos en el cliente de escritorio**
El cliente de escritorio realiza los siguientes pasos:
- Se conecta al servidor mediante `socket = io();`.
- Escucha eventos de tipo `'message'`:

``` javascript
socket.on('message', (data) => { ... });
```
- Convierte el texto JSON en un objeto con `JSON.parse(data)` dentro de un bloque `try...catch` para evitar errores en caso de datos mal formateados.
- Verifica si el objeto recibido es del tipo `'touch'`:

``` javascript
if (parsedData && parsedData.type === 'touch') { ... }
```
- Si es así, actualiza las variables `circleX` y `circleY` con las coordenadas enviadas desde el móvil.
- Finalmente, en `draw()`, se dibuja un círculo en la nueva posición.

#### **Respuestas a las preguntas de reflexión**
**Reflexión (Móvil)**

**1. ¿Por qué es útil enviar los datos como un objeto JSON en lugar de una cadena como “mouseX,mouseY”?**

- JSON permite estructurar la información, incluyendo más detalles (por ejemplo, tipo de evento, usuario, color, etc.). Es más escalable y mantenible.
- Facilita la lectura, validación y extensión del código, especialmente cuando hay varios tipos de mensajes.

**2. ¿Qué pasaría si quitaras la comprobación del threshold?**
- El cliente enviaría demasiados mensajes (uno por cada pequeño movimiento), lo que podría:
    - Saturar la red con datos innecesarios.
    - Hacer que la experiencia se vuelva lenta o que haya retrasos en el cliente receptor.
    - Aumentar el consumo de batería en dispositivos móviles.

**3. ¿Cómo adaptarías este código para que también respondiera al clic del ratón en un computador?**

Agregaría una función `mouseMoved()` que replique la lógica de `touchMoved()`:

``` javascript
function mouseMoved() {
    if (socket && socket.connected) {
        let dx = abs(mouseX - lastTouchX);
        let dy = abs(mouseY - lastTouchY);

        if (dx > threshold || dy > threshold || lastTouchX === null) {
            let mouseData = {
                type: 'touch',
                x: mouseX,
                y: mouseY
            };
            socket.emit('message', JSON.stringify(mouseData));
            lastTouchX = mouseX;
            lastTouchY = mouseY;
        }
    }
}
```
**Reflexión (Escritorio)**

**1. ¿Por qué es importante usar JSON.parse() dentro de un bloque try…catch?**
- Porque si los datos no están bien formateados como JSON, el método `JSON.parse()` lanzará un error que podría detener la ejecución del script.
- `try…catch` garantiza que el código siga funcionando incluso si llega un mensaje malformado.

**2. Si los canvas del móvil y escritorio tienen tamaños diferentes (ej. 300x300 vs 600x600), ¿cómo mapearías las coordenadas correctamente?**

Usaría la función` map()` de p5.js para escalar las coordenadas:

``` javascript
let mappedX = map(parsedData.x, 0, 300, 0, 600);
let mappedY = map(parsedData.y, 0, 300, 0, 600);

circleX = mappedX;
circleY = mappedY;
```
Esto asegura que las coordenadas del móvil se adapten proporcionalmente al tamaño del canvas del escritorio.

**3. ¿Qué cambiarías si el servidor enviara el evento como ‘updateDesktop’ en vez de ‘message’?**

Solo se necesita cambiar el nombre del listener:

``` javascript
socket.on('updateDesktop', (data) => {
    // misma lógica de parseo y actualización
});
```
