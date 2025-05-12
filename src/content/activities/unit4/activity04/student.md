
#### Esta es la solucion de mi actividad ✍️

#### **Compara el código original del caso de estudio con el anterior. ¿Qué notas de diferente?**

El uso de p5.webserial.js indica una orientación hacia comunicación con hardware.

#### **¿Para qué se usan estas imágenes? ¿Qué representan?**

funcionan como pinceles personalizados. En lugar de simplemente dibujar líneas o círculos, el usuario puede “pintar” en la pantalla con formas gráficas complejas contenidas en los archivos SVG.

#### **¿Por qué solo se leen datos del micro:bit si el puerto está abierto?**
Porque el puerto serial (`port`) debe estar activo para que pueda recibir datos. Si el puerto no está abierto, no hay canal de comunicación entre la computadora y el micro:bit, por lo tanto:

- `port.readUntil("\n")` no puede recibir nada.
- `port.availableBytes()` será siempre `0`.
- El micro:bit puede estar enviando datos, pero no hay nadie "escuchando".

#### **¿Se podrían leer datos si el puerto está cerrado?**
No, no es posible. Si el puerto serial no está abierto:

- No hay flujo de información entre el micro:bit y tu sketch.
- Cualquier dato que el micro:bit envíe será ignorado o descartado por el sistema operativo si no hay un proceso receptivo.

#### **¿Qué pasa si el micro:bit sigue enviando datos pero el puerto está cerrado?**
- El micro:bit sigue transmitiendo normalmente (como un radio que emite constantemente).
- Pero esos datos no llegan a p5.js porque el puerto no está abierto.
- En algunos casos, si el puerto se abre más tarde, no se reciben los datos anteriores (se pierden).

#### **¿Qué pasaría si el micro:bit no envía el “\n”?**

Va a generar un error en la lectura.

- Al sumar windowWidth / 2 y windowHeight / 2, estamos trasladando el punto de referencia al centro de la pantalla.
- Así, cuando xValue = 0 y yValue = 0, el objeto estará en el centro del lienzo en (windowWidth / 2, windowHeight / 2).

#### **Verificación de eventos keyPressed y keyReleased**
Para verificar que los eventos de keyPressed y keyReleased se están generando correctamente:

- Usar print() en la consola:

    El código ya incluye print(“A pressed”) y print(“B released”), lo que permite ver en la consola cuándo se detecta un evento.
- Mostrar en pantalla un cambio de color o dibujo

#### **Análisis del algoritmo updateButtonStates()**
La función updateButtonStates() tiene el propósito de detectar cambios en el estado de los botones del micro:bit y responder a estos eventos.

#### **¿Qué hace?**
- Comprueba si el botón A ha pasado de no presionado (false) a presionado (true).
- Comprueba si el botón B ha pasado de presionado (true) a no presionado (false).

#### **¿Por qué es necesario almacenar el estado anterior de los botones?**
- Al comparar el estado actual con el anterior, se detecta solo la transición, asegurando que la acción ocurre una única vez por pulsación.

#### **¿Qué pasaría si no se almacenara el estado anterior?**
- Se generaría un evento cada vez que se ejecuta draw(), en lugar de detectar solo la transición de estado.
- El cambio de color, la posición del clic y otros efectos se actualizarían de forma incontrolada, causando comportamiento no deseado.

#### **Diferencias entre los códigos**
Comparando los dos códigos, se pueden notar 2 diferencias:

- **Interacción con el micro:bit:**

        1. El nuevo código está diseñado para recibir datos del micro:bit a través de   serial y utilizar la inclinación y botones del dispositivo.
        2. En el código original, la interacción dependía del mouse y del teclado.
- **Eventos del mouse:**

        1. En el código original, el usuario podía interactuar directamente con el mouse para dibujar en la pantalla.
        2. En el nuevo código, el mousePressed() y otros eventos del mouse parecen haber sido eliminados o modificados para depender del micro:bit.

#### **Análisis del mensaje en la consola: “No se están recibiendo 4 datos del micro:bit”**
- Este mensaje significa que la aplicación esperaba recibir cuatro valores separados por comas desde el micro:bit (x, y, a, b), pero no está recibiendo los cuatro valores correctamente.

**Causa:**
Problema con la lectura del puerto serial:
La función `port.readUntil(“\n”)` puede estar recibiendo líneas de datos incompletas en algunos frames.

#### **¿El mensaje ocurre en varios frames o solo en uno?**
- aparece ocasionalmente, indica que en algunos momentos el micro:bit no está enviando datos completos.

#### **Posibles soluciones al problema**
- Agregar un control de lectura
Antes de procesar los datos, asegurarse de que port.availableBytes() > 0 y que data tiene el formato correcto.
- Modificar el código del micro:bit
Revisar si el micro:bit está enviando datos correctamente sin cortes ni valores faltantes.