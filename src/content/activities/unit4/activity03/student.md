
#### Esta es la solucion de mi actividad ✍️
---

#### **¿Qué información se está enviando?**

Se envían cuatro valores:
- `xValue`: aceleración en el eje X.
- `yValue`: aceleración en el eje Y.
- `aState`: estado del botón A (`True` o `False`).
- `bState`: estado del botón B (`True` o `False`).

#### **¿Cómo se está enviando?**

A través del puerto serial UART, con los datos organizados como texto, separados por comas y terminados con salto de línea.

#### **Análisis del formato:**
```python
"{},{},{},{}\n".format(xValue, yValue, aState, bState)
```

Este formato crea una cadena como:
```
512,-100,True,False\n
```
Se usa `\n` para indicar el final de cada grupo de datos.

#### **Observación en SerialTerminal**

Los datos se ven como líneas de texto que cambian en tiempo real, por ejemplo:
```
120,345,False,False
88,300,True,False
```
#### **¿Por qué usar comas y salto de línea?**

- **Comas (`,`)**: permiten identificar y separar cada valor individual.
- **Salto de línea (`\n`)**: indica cuándo termina un conjunto de datos, ideal para leer línea por línea.

#### **¿Qué pasa si no se usan comas ni salto de línea?**

- Los datos estarían pegados y serían difíciles de interpretar:  
  `512-100TrueFalse`
- Sin salto de línea, todos los datos aparecerían como una única cadena continua.

#### ¿Para qué sirve `sleep(100)`?

- Pausa de 100 milisegundos entre cada envío.
- Permite que los datos se envíen a **10 Hz**.
- Sin esta pausa, el envío sería demasiado rápido y podría causar saturación del canal serial.

#### **Comportamiento del acelerómetro (`xValue` y `yValue`):**

- **xValue:**
  - Positivo → micro:bit inclinado a la **derecha**.
  - Negativo → micro:bit inclinado a la **izquierda**.
- **yValue:**
  - Positivo → inclinado hacia **atrás**.
  - Negativo → inclinado hacia **adelante**.

Valores comunes: entre -1024 y +1024.

#### **Comportamiento de los botones:**

- `aState` y `bState`:
  - `True` cuando el botón está presionado.
  - `False` cuando no lo está.

#### **Diferencia entre `is_pressed()` y `was_pressed()`:**

- `is_pressed()`: devuelve `True` mientras el botón está presionado.
- `was_pressed()`: devuelve `True` solo una vez, tras haber sido presionado.

#### **Análisis de bytes enviados**

Si los datos son:

```
xValue = 969  
yValue = 652  
aState = True  
bState = False
```

La cadena enviada sería:
```
969,652,True,False\n
```

En formato hexadecimal (ASCII):
```
39 36 39 2C 36 35 32 2C 54 72 75 65 2C 46 61 6C 73 65 0A
```
