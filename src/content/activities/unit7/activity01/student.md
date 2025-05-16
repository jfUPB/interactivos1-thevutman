
#### Esta es la solucion de mi actividad ✍️
---

#### **¿Por qué usamos esta URL en lugar de localhost?**
Usamos la URL de Dev Tunnels porque `localhost:3000` solo funciona en el mismo computador donde corre el servidor. Como el celular no está ejecutando el servidor localmente, necesita acceder al servidor a través de Internet, y Dev Tunnels crea una URL pública temporal que expone el servidor de manera segura hacia afuera.

#### **¿Qué hacen `npm install` y `npm start`?**
- `npm install` descarga e instala todas las dependencias definidas en el archivo `package.json`, necesarias para ejecutar el servidor.
- `npm start` ejecuta el script definido para iniciar el servidor (en este caso, probablemente corre `node server.js`).

#### **Mensajes en la terminal del servidor**
Cuando conecté los clientes, en la terminal del servidor observé:
- `New client connected`
- `Received message => {"x": 157, "y": 283}`
- `Client disconnected`

Cada cliente conectado tenía un identificador único. Aunque los mensajes eran similares, estaban asociados a diferentes `socket.id`, lo que permitía al servidor diferenciarlos.

#### **Observaciones sobre la interacción**
- Funcionó correctamente: al tocar la pantalla del celular, el círculo en la pantalla del computador se movía de forma fluida.
- Latencia: mínima, apenas perceptible. La comunicación fue casi en tiempo real.
- Interacción intuitiva y fácil de probar.

#### **¿Cerré el puerto?**
Sí, cerré el puerto al finalizar las pruebas.

**¿Por qué es importante hacerlo?**

Porque mantener el puerto abierto expone el servidor a posibles accesos no autorizados desde Internet. Cerrar el túnel garantiza mayor seguridad y evita consumo innecesario de recursos.