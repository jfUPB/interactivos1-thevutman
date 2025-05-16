
#### Esta es la solucion de mi actividad ✍️
---

#### **1. ¿Por qué es necesario Dev Tunnels en este escenario y cómo funciona conceptualmente?**
Dev Tunnels es necesario porque cuando ejecuto el servidor con `npm start`, este se queda escuchando en `localhost:3000`, lo cual solo es accesible desde mi propia computadora. Si abro esa dirección en el navegador de mi celular, no funciona, porque el celular interpreta `localhost` como su propio dispositivo, no el mío.

Usar Dev Tunnels resuelve este problema: crea una URL pública y segura (por ejemplo, `https://mi-tunnel.use2.devtunnels.ms`) que redirige todas las solicitudes a `localhost:3000` en mi PC. Así, desde el celular puedo conectarme a esa dirección pública y llegar directamente al servidor que está corriendo en mi máquina, aunque esté en otra red. Es como un puente entre mi celular y mi servidor local, sin tener que preocuparme por configuraciones complicadas de red.

#### **2. ¿Por qué usamos `JSON.stringify()` en el emisor (móvil) y `JSON.parse()` en el receptor (escritorio)? ¿Qué problema resuelve JSON aquí?**
En JavaScript, un objeto como `{ x: 120, y: 250 }` no se puede enviar directamente a través de la red. Necesitamos convertirlo en una cadena de texto. Ahí entra `JSON.stringify()`, que convierte el objeto en un string con formato JSON: `"{\"x\":120,\"y\":250}"`.

Cuando el escritorio recibe ese mensaje, es simplemente texto. Para volver a trabajar con los datos como objeto, usamos `JSON.parse()`, que transforma el texto JSON en un objeto JavaScript otra vez.

JSON resuelve el problema de estructurar y transportar datos complejos (no solo texto plano) entre dos dispositivos que se comunican por red.

#### **3. Describe la función de `touchMoved()` y por qué se usa la variable `threshold` en el cliente móvil.**
`touchMoved()` es una función de p5.js que se ejecuta cada vez que el usuario mueve el dedo sobre el canvas en un dispositivo táctil. Es muy útil para detectar y seguir el movimiento del dedo en tiempo real.

Sin embargo, como esta función puede activarse muchísimas veces por segundo, se usa una variable llamada `threshold` para evitar enviar mensajes a cada pequeño temblor o movimiento. El código compara la distancia actual del toque con la última enviada, y solo envía datos si la diferencia es suficientemente grande. Esto optimiza la red y evita sobrecargar el sistema con información innecesaria.

#### **4. ¿Qué otros eventos táctiles existen en p5.js y para qué tipo de interacciones podrían ser útiles?**
- `touchStarted()`: se ejecuta cuando el usuario toca la pantalla por primera vez. Es útil para detectar taps o toques iniciales, por ejemplo, presionar un botón virtual o iniciar una animación.
- `touchEnded()`: se ejecuta cuando el usuario levanta el dedo. Sirve para detectar cuando una interacción termina, como soltar un botón o detener una acción.
- `touchMoved()` (ya usado): para hacer dibujos, controlar objetos o enviar la posición continua del dedo.

Estos eventos permiten crear interfaces interactivas como juegos, sliders, botones y menús táctiles que responden de forma intuitiva al comportamiento del usuario.

#### **5. Compara brevemente Dev Tunnels con simplemente usar la IP local. ¿Cuáles son las ventajas y desventajas de cada uno?**
|Método	|Ventajas	|Desventajas|
|-------|-----------|-----------|
|IP local	|Rápido si estás en la misma red Wi-Fi	|No funciona si los dispositivos están en redes diferentes o si hay firewalls bloqueando.|
|Dev Tunnels	|Funciona desde cualquier red o ubicación. No requiere configuración de red. Seguro.	|Necesita estar conectado a Internet. A veces puede tener más latencia que la IP local.|

En resumen, la IP local es útil solo en entornos cerrados, mientras que Dev Tunnels ofrece una solución más universal y escalable para acceder al servidor desde cualquier lugar.