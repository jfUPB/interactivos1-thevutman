
#### Esta es la solucion de mi actividad ✍️
---

#### **1. Pausa activa: Conectividad**
**¿Cómo te conectas a Internet? ¿Qué pasa si la rampa se corta?**

En casa y en la universidad, normalmente me conecto a Internet mediante Wi-Fi, aunque en algunos casos también se usan cables Ethernet. Si esa "rampa" se corta —por ejemplo, si el router se apaga o falla el proveedor de Internet— no puedo acceder a ningún servicio online: no cargan las páginas web, no hay videollamadas, ni se puede usar mensajería. Es como si mi vehículo quedara atrapado sin salida a la red de carreteras digitales.

#### **2. Pausa activa: Cliente y servidor**
**¿Ejemplos de relaciones cliente-servidor en la vida diaria?**

Un restaurante es un excelente ejemplo:
- **Cliente:** la persona que ordena comida.
- **Servidor:** el mesero o sistema de pedidos.
- **Petición:** el cliente pide un plato específico.
- **Respuesta:** el servidor entrega la comida solicitada.

También en una biblioteca, el lector (cliente) solicita un libro al bibliotecario (servidor), quien se lo proporciona si está disponible.

#### **3. Pausa activa: Componentes de una URL**
Ejemplo con URL de sitio favorito:

Supongamos: `https://www.youtube.com/watch?v=dQw4w9WgXcQ`
- **Protocolo:** `https://`
- **Dominio:** `www.youtube.com`
- **Ruta:** `/watch?v=dQw4w9WgXcQ`

Si solo escribo` www.youtube.com`, el servidor probablemente me envía la página principal como respuesta por defecto (`/index.html` o `/home`), ya que así está configurado para visitantes sin una ruta específica.

#### **4. Pausa activa: Comparación de protocolos**
**Similitudes con protocolos seriales (como con micro:bit):**
- Ambos usan un formato estandarizado de comunicación.
- Tienen un emisor y un receptor que entienden ese protocolo.

**Diferencias clave:**

- HTTP tiene estructuras más complejas (códigos de estado, encabezados, contenido tipo MIME).
- Es diseñado para la web, con múltiples capas de seguridad, formato y estructura.

**¿Por qué HTTP es más complejo?**

Porque necesita manejar muchas más situaciones: tipos de archivos, estados de error, múltiples dispositivos, y garantizar una experiencia coherente para millones de usuarios simultáneamente.

#### **5. Pausa activa: HTML, CSS, JS en una página web**
**Formulario de login:**
- **HTML:** campos de texto para usuario y contraseña, y el botón “Iniciar sesión”.
- **CSS:** el estilo del botón, colores, espaciado y fuente.
- **JavaScript:** comprobar que los campos no estén vacíos, y mostrar mensajes como “contraseña incorrecta” sin necesidad de recargar la página.

#### **6. Pausa activa: ¿Cómo y cuándo se ejecuta JavaScript?**
Normalmente, el navegador ejecuta JS:
- En cuanto lo encuentra si está en la parte superior del HTML.
- Después de construir todo el DOM si está al final o marcado con `defer`.

El JavaScript entra en acción una vez que los elementos de la página ya están cargados y se puede interactuar con ellos.

#### **7. Pausa activa: Eventos vs draw()**
**Ventajas del modelo basado en eventos:**
- Es más eficiente: solo se ejecuta código cuando realmente ocurre algo.
- Ahorra recursos del navegador y la batería del dispositivo.
- Permite reacciones específicas a interacciones del usuario o mensajes del servidor.

**¿Un bucle draw() para toda la página web?**

No sería eficiente. Redibujar todo constantemente, cuando la mayoría del tiempo no hay cambios, desperdicia recursos. Para interfaces web, esperar a eventos es mejor.

#### **8. Pausa activa: ¿Por qué usar JavaScript en cliente y servidor?**
**Ventajas:**
- **Un solo lenguaje:** Los desarrolladores no necesitan aprender dos lenguajes distintos para frontend y backend.
- **Reutilización de lógica:** Algunas validaciones o estructuras se pueden compartir entre cliente y servidor.
- **Flujo de trabajo más ágil:** Equipos más pequeños y eficientes pueden trabajar en todo el sistema web.

#### **9. Pausa activa: ¿Por qué usar WebSockets y Socket.IO?**
Porque permiten una comunicación en tiempo real, continua y eficiente. A diferencia de las peticiones HTTP que son lentas y pesadas para intercambios rápidos, los WebSockets mantienen una conexión abierta entre el cliente y el servidor, lo cual es ideal para:
- Juegos en línea
- Aplicaciones colaborativas (como Google Docs)
- Seguimiento de cursores o chat en tiempo real