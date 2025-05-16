#### Esta es la solucion de mi actividad ✍️
---

#### **Tabla comparativa: Protocolo ASCII vs Protocolo Binario**

|Aspecto	|Protocolo ASCII	|Protocolo Binario|
|--------|-----------------|-----------------|
|Eficiencia	|Menos eficiente: se enviaban más caracteres por cada valor (por ejemplo, "123,45\n")	|Más eficiente: se enviaban directamente los bytes en binario (por ejemplo, 8 bytes totales)|
|Velocidad	|Más lento por la conversión de texto y separación de caracteres	|Más rápido al enviar datos crudos sin caracteres intermedios|
|Facilidad	|Más fácil de entender y depurar, ya que los datos eran legibles	|Más difícil de interpretar, se necesitaba framing y verificación con checksum|
|Uso de recursos	|Usaba menos memoria y menos código |Usaba más memoria y código por el manejo del buffer, framing, y checksum|

En la aplicación con ASCII, los datos llegaban como texto separado por comas y se podían leer directamente (`split(",")`). En la versión binaria tuvimos que buscar un byte de sincronización (`0xaa`), verificar el checksum y convertir los bytes a enteros con `DataView`.

#### **Preguntas de consolidación**
**¿Por qué fue necesario introducir framing en el protocolo binario?**

Porque los datos binarios no tienen separadores visibles como comas o saltos de línea. El framing nos permite reconocer el inicio de un paquete de datos válido y asegurarnos de leer exactamente la cantidad necesaria de bytes.

**¿Cómo funciona el framing?**

Funciona usando un byte de sincronización (en este caso `0xaa`) al inicio del paquete. Luego se verifica que haya al menos 8 bytes disponibles, se leen y se valida su integridad con un checksum antes de procesarlos.

**¿Qué es un carácter de sincronización?**

Es un byte especial (por ejemplo, `0xaa`) que indica el inicio de un paquete de datos. Nos ayuda a sincronizar correctamente la lectura del buffer.

**¿Qué es el checksum y para qué sirve?**

El checksum es un valor calculado sumando los bytes del paquete (excepto el checksum recibido) y tomando el módulo 256. Sirve para detectar si los datos llegaron corruptos. Si el checksum calculado no coincide con el recibido, el paquete se descarta.

#### **Análisis del código en `readSerialData()` en p5.js**
``` js
function readSerialData() {
    let available = port.availableBytes();
    if (available > 0) {
        let newData = port.readBytes(available);
        serialBuffer = serialBuffer.concat(newData);
    }
```
**¿Qué hace `concat` y por qué?**
Concat une los datos nuevos (`newData`) al buffer actual (`serialBuffer`). Esto es necesario porque los datos pueden llegar en fragmentos, y debemos acumularlos hasta tener un paquete completo.

```js
while (serialBuffer.length >= 8) {
    if (serialBuffer[0] !== 0xaa) {
        serialBuffer.shift();
        continue;
    }
```

**¿Por qué se recorre el buffer solo si tiene 8 o más bytes?**

Porque cada paquete tiene 8 bytes exactos. Si hay menos, no se puede procesar un paquete completo y se debe esperar.

**¿Qué significa 0xaa?**

Es el byte de sincronización, equivalente a 170 en decimal. Nos dice que puede empezar un paquete válido.

**¿Qué hace `shift` y la instrucción `continue`? ¿Por qué?**

`shift()` elimina el primer byte del buffer porque no es el byte de sincronización esperado. `continue` salta al siguiente ciclo del bucle para volver a intentar sincronizar con el siguiente byte.

**¿Qué hace break si hay menos de 8 bytes?**

Sale del bucle porque no hay datos suficientes para formar un paquete. Se espera a que lleguen más datos en el siguiente ciclo.

```js
let packet = serialBuffer.slice(0, 8);
serialBuffer.splice(0, 8);
```

**¿Cuál es la diferencia entre `slice` y `splice`? ¿Por qué se usan así?**

`slice` copia los primeros 8 bytes para analizarlos. `splice` elimina esos bytes del buffer porque ya fueron procesados. Se usan juntos para trabajar sobre una copia segura y luego limpiar el buffer.

```js
let computedChecksum = dataBytes.reduce((acc, val) => acc + val, 0) % 256;
```

**¿Cómo opera `reduce`?**

Reduce recorre todos los valores (`val`) del arreglo `dataBytes`, acumulando su suma (`acc`). Luego se aplica `% 256` para que el resultado esté en el rango de un byte.

**¿Por qué se compara el checksum enviado con el calculado?**

Para asegurarnos de que el paquete no se corrompió durante la transmisión. Si no coinciden, significa que hubo un error y se descarta el paquete con `continue`.

**¿Qué hace `continue` aquí?**

Salta el resto del bucle y evita procesar un paquete con error de checksum. Así no se actualiza la interfaz con datos erróneos.

#### **Lectura de datos binarios con DataView**
```js
let buffer = new Uint8Array(dataBytes).buffer;
let view = new DataView(buffer);
```

**¿Qué es un `DataView` y para qué se usa?**

`DataView` permite leer datos binarios desde un buffer con precisión en cuanto a tipo y orden (por ejemplo, enteros de 16 bits, sin signo, etc.).

**¿Por qué se hacen estas conversiones?**

Porque los datos binarios deben interpretarse correctamente. Por ejemplo, dos bytes consecutivos pueden representar un entero de 16 bits con signo, y no se pueden leer directamente como texto o números individuales.

```js
microBitX = view.getInt16(0) + windowWidth / 2;
microBitY = view.getInt16(2) + windowHeight / 2;
microBitAState = view.getUint8(4) === 1;
microBitBState = view.getUint8(5) === 1;
```

Aquí se interpretan correctamente las posiciones X e Y y los estados de los botones A y B usando `getInt16` y `getUint8`.