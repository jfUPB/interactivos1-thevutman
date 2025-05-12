
#### Esta es la solucion de mi actividad ✍️

#### **1. ¿Qué es un protocolo de comunicación y por qué es importante en la comunicación serial?**

Un protocolo de comunicación es un conjunto de reglas que definen cómo se intercambian los datos entre dispositivos. En la comunicación serial, es importante porque asegura que tanto el micro:bit como p5.js entiendan el orden, tipo y formato de los datos que se están enviando y recibiendo. Sin un protocolo, sería imposible sincronizar la lectura de datos correctamente.

 *Fragmento de código relacionado:*
```python
uart.init(115200)
```

#### **2. ¿Por qué se separan los datos con comas en el protocolo ASCII que exploramos?**
Porque al usar comas podemos separar cada dato de forma clara para luego dividirlos fácilmente con la función `split()` en p5.js. Esto nos ayuda a identificar cada valor (x, y, botón A, botón B) de forma independiente.

*Fragmento de código relacionado:*
```python
data = "{},{},{},{}\n".format(xValue, yValue, aState, bState)
```

#### **3. ¿Por qué es necesario terminar los datos con un carácter que marque el fin del mensaje?**
Porque p5.js necesita saber cuándo termina un paquete de datos para leerlo completo y no quedarse esperando más información. El salto de línea `\n` es un buen delimitador para leer hasta ahí con `readLine()`.
*Fragmento de código relacionado:*
```python
data = "{},{},{},{}\n".format(xValue, yValue, aState, bState)
```

#### **4. ¿Por qué fue necesario usar una máquina de estados en la aplicación modificada de p5.js?**
Porque necesitábamos que la lectura y visualización de los datos funcionara de forma ordenada, dependiendo de si el puerto estaba conectado, si había datos disponibles, etc. Así evitamos errores o que la interfaz se bloquee por intentar leer datos cuando no hay conexión.

*Fragmento de código relacionado (simulado):*
```javascript
if (serial.available()) {
  let data = serial.readLine();
  // estado cambia según datos recibidos
}
```

#### **5. ¿Cómo se formatean los datos en el micro:bit para ser enviados por el puerto serial?**
Se convierten a una cadena de texto en formato CSV (valores separados por comas), incluyendo `\n` al final para marcar el fin del mensaje. Se usa `format()` para hacerlo más limpio.

*Fragmento de código relacionado:*

```python
data = "{},{},{},{}\n".format(xValue, yValue, aState, bState)
uart.write(data)
```

#### **6. ¿Qué significa que los datos enviados por el micro:bit están codificados en ASCII?**
Significa que se envían como texto legible por humanos, donde cada carácter (como “1”, “2”, “,”) corresponde a un byte del estándar ASCII. Esto facilita su lectura en p5.js y otros entornos que trabajen con texto.

*Ejemplo de dato enviado:*

`"123,756,0,1\n"` → caracteres ASCII

#### **7. ¿Por qué es necesario en la aplicación de p5.js preguntar si hay bytes disponibles en el puerto serial antes de leerlos?**
Porque si no hay datos disponibles y tratamos de leer, puede devolver `null` o provocar errores. Es como preguntar “¿hay algo en la bandeja?” antes de sacar una carta.

#### **Fragmento de código:**
```javascript
if (serial.available()) {
  let data = serial.readLine();
}
```

#### **8. ¿Qué pasa si esto no se hace?**
Si no preguntamos primero y tratamos de leer, p5.js puede fallar, leer datos incompletos o incluso trabarse, ya que estaría esperando información que aún no ha llegado.

#### **9. ¿Cómo se elimina el retorno de carro o salto de línea de un string en p5.js?**
Usando `trim()`, que limpia los espacios en blanco al inicio y al final del string, incluyendo `\n` o `\r`.

*Fragmento de código:*
```javascript
let cleanData = trim(data);
```

#### **10. Si una cadena tiene información separada por espacios y quieres dividir dicha información en varias cadenas individuales ¿Qué función de p5.js usarías?**
Usaría la función `split()`, indicando el espacio como separador.

*Fragmento de código:*
```javascript
let partes = split(data, " ");
```

#### **11. ¿Por qué es necesario en la aplicación del caso de estudio convertir las cadenas a números enteros antes de usarlas en el sketch de p5.js?**
Porque los datos leídos desde el puerto llegan como texto (strings) y para usar esos valores en condiciones, rotaciones, posiciones, etc., se necesitan como números (`int` o `float`).

*Fragmento de código:*
```javascript
let xVal = int(values[0]);
let yVal = int(values[1]);
```

#### **12. Si el micro:bit tiene los siguientes datos:**
`xValue: 123, yValue: 756, aState: False, bState: True`

**¿Qué bytes se enviarían por el puerto serial?**

Se enviarían los siguientes caracteres (en ASCII):
`"123,756,0,1\n"`

#### **13. ¿Qué aprendiste nuevo del micro:bit que no sabías antes?**
Aprendí cómo usar el acelerómetro para obtener datos en tiempo real y cómo enviar esa información al computador por el puerto serial usando `uart.write()`. También comprendí cómo estructurar los datos en formato legible (ASCII).

#### **14. ¿Qué aprendiste nuevo de p5.js que no sabías antes?**
Aprendí cómo conectarlo con hardware externo como el micro:bit a través del puerto serial, cómo leer los datos y procesarlos, y cómo usarlos para interactuar con visualizaciones dinámicas, como la esfera de cubos 3D que gira según la aceleración.