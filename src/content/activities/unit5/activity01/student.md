
#### Esta es la solucion de mi actividad ✍️
---

#### **Descripción de la Comunicación entre el Micro:bit y el Sketch de p5.js**
El **micro:bit** se comunica con el **sketch de p5.js** a través de un puerto serie, enviando datos de los sensores del micro:bit al navegador mediante un protocolo de comunicación en formato ASCII.

**Datos que Envía el Micro:bit**
El micro:bit envía información sobre el estado del acelerómetro y los botones. Los datos enviados son:

**1. xValue:** Valor de la aceleración en el eje X del acelerómetro.

**2. yValue:** Valor de la aceleración en el eje Y del acelerómetro.

**3. aState:** Estado del botón A (si está presionado o no).

**4. bState:** Estado del botón B (si está presionado o no).

Estos datos se envían en el siguiente formato CSV (Comma Separated Values) y son transmitidos a través de la comunicación serial a una frecuencia de 10 Hz:

```python
xValue, yValue, aState, bState
```

**Estructura del Protocolo ASCII Usado**

El protocolo ASCII es muy simple: se utilizan caracteres legibles para el ser humano para representar los valores de los sensores y botones. La estructura es la siguiente:

```python
"{},{},{},{}\n".format(xValue, yValue, aState, bState)
```

Donde:

- **xValue y yValue** son números enteros que representan los valores de aceleración en los ejes X y Y, respectivamente.

- **aState y bState** son valores booleanos que indican si los botones A y B están presionados (`True` o `False`).

- El carácter de salto de línea (`\n`) indica el final de cada conjunto de datos.

Este formato permite que el navegador reciba y procese fácilmente los datos del micro:bit.

#### **Código en p5.js para Leer los Datos del Micro:bit y Transformarlos en Coordenadas de la Pantalla**
En p5.js, los datos del micro:bit se leen desde el puerto serie mediante el siguiente bloque de código:

```javascript
if (port.availableBytes() > 0) {
  let data = port.readUntil("\n");
  if (data) {
    data = data.trim();
    let values = data.split(",");
    if (values.length == 4) {
      microBitX = int(values[0]) + windowWidth / 2;
      microBitY = int(values[1]) + windowHeight / 2;
      microBitAState = values[2].toLowerCase() === "true";
      microBitBState = values[3].toLowerCase() === "true";
      updateButtonStates(microBitAState, microBitBState);
    } else {
      print("No se están recibiendo 4 datos del micro:bit");
    }
  }
}
```

**1. Lectura de los Datos:** Se utiliza `port.readUntil("\n")` para leer los datos del micro:bit hasta encontrar el salto de línea (`\n`).

**2. Procesamiento de los Datos:** Los datos recibidos se separan usando `split(",")`, lo que da como resultado un arreglo de 4 elementos. Estos elementos corresponden a:

- `values[0]`: El valor de aceleración en el eje X.
- `values[1]`: El valor de aceleración en el eje Y.
- `values[2]`: El estado del botón A.
- `values[3]`: El estado del botón B.

** 3. Transformación en Coordenadas de la Pantalla:** Se asignan los valores de los ejes X y Y a las variables `microBitX` y `microBitY`, respectivamente. Estos valores son desplazados por el centro de la pantalla para asegurar que el micro:bit se mueva en el espacio visible del lienzo (`windowWidth / 2` y `windowHeight / 2`).

#### **Generación de los Eventos "A Pressed" y "B Released"**
En p5.js, los eventos "A Pressed" y "B Released" se generan al detectar cambios en el estado de los botones A y B enviados por el micro:bit. La función `updateButtonStates()` realiza esta tarea:

```javascript
function updateButtonStates(newAState, newBState) {
  // Evento A Pressed
  if (newAState === true && prevmicroBitAState === false) {
    lineModuleSize = random(50, 160);
    clickPosX = microBitX;
    clickPosY = microBitY;
    print("A pressed");
  }

  // Evento B Released
  if (newBState === false && prevmicroBitBState === true) {
    c = color(random(255), random(255), random(255), random(80, 100));
    print("B released");
  }

  prevmicroBitAState = newAState;
  prevmicroBitBState = newBState;
}
```

** 1. A Pressed:** Si el estado del botón A cambia de `false` a `true`, se considera que el botón A ha sido presionado. Se genera un evento que:

- Cambia el tamaño de la línea (`lineModuleSize`) a un valor aleatorio.
- Registra las coordenadas actuales del micro:bit (`clickPosX`, `clickPosY`).

** 2. B Released:** Si el estado del botón B cambia de `true` a `false`, se considera que el botón B ha sido liberado. Se genera un evento que:

- Cambia el color `c` a un valor aleatorio.