
#### Esta es la solucion de mi actividad ✍️
---

#### **Primera visualización en modo Texto en SerialTerminal**

**Resultado observado:** Al ver los datos binarios en modo Texto, se muestra una secuencia de caracteres ilegibles, símbolos raros o letras sin sentido.

**¿Por qué se ve así?**

Porque el formato binario no está hecho para ser leído como texto. Cada byte puede representar cualquier valor entre 0 y 255, y muchos de esos valores no tienen una representación ASCII válida. El programa está mostrando los valores binarios como si fueran caracteres, lo que genera símbolos confusos.

#### **Visualización en modo Hexadecimal**
**Resultado observado:** Ahora se ven valores hexadecimales como ``FF 2A 00 B5 00 01``.

**Relación con el código** ``data = struct.pack('>2h2B', xValue, yValue, int(aState), int(bState))``
Este resultado representa los 6 bytes generados por el ``struct.pack``:

- `>2h2B` indica:

    - `2h`: dos valores **short** de 2 bytes cada uno = 4 bytes

    - `2B`: dos valores **unsigned char** de 1 byte cada uno = 2 bytes

    - Total: **6 bytes**

Por ejemplo, si `xValue = -214`, `yValue = 181`, `aState = 1`, `bState = 0`, el paquete binario codificará esos valores directamente en bytes.

#### **¿Ventajas y desventajas de binario vs ASCII?**
**Ventajas del formato binario:**

- Más compacto (6 bytes frente a ~15-20 bytes en ASCII).
- Más rápido de transmitir y procesar.
- Ideal para dispositivos con memoria limitada o comunicaciones frecuentes.

**Desventajas del formato binario:**

- Difícil de leer sin herramientas especializadas.
- Se requiere una decodificación precisa en el programa receptor (como p5.js).
- Errores de interpretación si hay desincronización en los datos.

#### **Resultado con gesto shake**
**Resultado observado:** Solo se envían datos al agitar el micro:bit. En SerialTerminal (modo hex), se muestran exactamente 6 bytes por evento.

**¿Cuántos bytes se están enviando por mensaje?**
**6 bytes**

**Relación con el formato `>2h2B`:**

- `2h` = 4 bytes (2 por cada short)
- `2B` = 2 bytes (1 por cada botón)
- Total: 6 bytes por mensaje

**¿Qué significa cada byte?**
Depende del valor real:

- Bytes 0-1: eje X (big endian)
- Bytes 2-3: eje Y
- Byte 4: estado de botón A (0 o 1)
- Byte 5: estado de botón B (0 o 1)

#### **¿Cómo se ven los números negativos en binario con `>2h2B`?**
- Los valores `xValue` y `yValue` pueden ser negativos.
- Se codifican usando complemento a dos en 2 bytes (16 bits).
- Ejemplo:
    - -1 = `FF FF`
    - -100 = `FF 9C`
    - 0 = `00 00`
    - 100 = `00 64`

Así, los valores negativos se representan correctamente en binario siempre que el receptor los interprete como `short` con signo.

#### **Experimento con binario y ASCII juntos**
**Resultado observado:**

- Primero se muestran 6 bytes binarios (en modo Hex).
- Luego aparece la palabra `ASCII`: seguida de valores separados por comas (ej. `-214,181,1,0`).

**Diferencias entre binario y ASCII:**

- **Binario:** más compacto y eficiente, pero ilegible a simple vista.
- **ASCII:** legible, útil para depuración o pruebas rápidas, pero más pesado (usa más bytes y más tiempo de transmisión).

**Ventajas del binario:**

- Rápido, ideal para aplicaciones en tiempo real.

**Desventajas del binario:**

- Requiere decodificación y manejo de errores más sofisticado.

**Ventajas del ASCII:**

- Fácil de leer y debuggear.
- Funciona bien con herramientas básicas como Serial Monitor.

**Desventajas del ASCII:**

- Consume más ancho de banda.
- Menor rendimiento en sistemas embebidos.