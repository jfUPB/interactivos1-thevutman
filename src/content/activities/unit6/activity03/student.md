
#### Esta es la solucion de mi actividad ✍️
---

#### **1. Reflexión sobre el uso de módulos o librerías**
**¿Por qué crees que es útil usar módulos o librerías en lugar de escribir todo desde cero? ¿Qué ventajas aporta?**

Usar módulos o librerías nos ahorra tiempo y esfuerzo, ya que muchas funcionalidades comunes ya están implementadas, probadas y optimizadas. Esto mejora la productividad, facilita el mantenimiento del código y reduce errores. Además, nos permite enfocarnos en la lógica específica de nuestro proyecto sin tener que reinventar la rueda.

#### **4. Experimentación con `express.static`**
**¿Qué ocurre al cambiar la línea a una carpeta que no existe (`archivos_cliente`)? ¿Qué mensaje ves?**

Al cambiar `views` por `archivos_cliente` (una carpeta inexistente), el servidor no encuentra los archivos estáticos como `page1.html`, por lo tanto, al abrir `http://localhost:3000/page1.html` en el navegador, aparece un error 404 (Not Found). En la consola del navegador se puede ver un mensaje como “Failed to load resource”. Al restaurar la línea original con `views`, todo vuelve a funcionar correctamente.

#### **5. Experimentación con rutas**
**¿Qué ocurre al cambiar la ruta `/page1` por `/pagina_uno`?**

Después del cambio, al acceder a `http://localhost:3000/page1`, obtenemos un error 404 porque esa ruta ya no existe. En cambio, al acceder a `http://localhost:3000/pagina_uno`, el navegador muestra correctamente `page1.html`.

**Conclusión:** Las rutas deben coincidir exactamente con lo definido en el código. El servidor solo responde a las URLs que están programadas explícitamente.

#### **6. Observación de conexión y desconexión**
**Preguntas:**
1. ¿Qué mensaje ves al abrir `page1`?
2. ¿Y al abrir `page2`?
3. ¿Los IDs son diferentes?
4. ¿Qué mensaje aparece al cerrar `page1`?
5. ¿Y al cerrar `page2`?

**Respuestas:**
1. Al abrir `http://localhost:3000/page1`, en la terminal se muestra:
    `A user connected - ID: <id_unico>`
2. Al abrir `http://localhost:3000/page2`, se muestra otro mensaje similar con un ID diferente.
3. Sí, los IDs son distintos para cada conexión.
4.  Al cerrar la pestaña de `page1`, aparece:
    `User disconnected - ID: <id_unico_de_page1>`
5. Al cerrar `page2`, aparece un mensaje similar con su respectivo ID.

#### **7. Prueba de recepción de eventos y broadcast**
**Preguntas:**

1. ¿Qué evento se registra al mover page1?
2. ¿Y al mover page2?
3. ¿Qué ocurre si se cambia `broadcast.emit` por `emit`?
4. ¿Se actualiza page2 al mover page1?

**Respuestas:**

1. Al mover `page1`, se registra el evento `win1update` en la terminal con los datos enviados.

2. Al mover `page2`, se registra el evento `win2update` y se muestran los datos correspondientes.

3. Si cambiamos `socket.broadcast.emit('getdata', page1)` por `socket.emit('getdata', page1)`, el mensaje se envía solo al mismo cliente que lo envió, no a los demás.

4. No, `page2` no recibe los datos actualizados cuando `page1` se mueve, porque `emit` no envía datos a los otros sockets conectados. Por eso es importante usar `broadcast.emit`.

#### **8. Cambio de puerto**
**¿Qué ocurre al cambiar el puerto a 3001?**

En la consola aparece el mensaje:
`Server is listening on http://localhost:3001`

Esto indica que el servidor ahora está escuchando en el nuevo puerto. Si tratamos de acceder a `http://localhost:3000`, no funcionará. Debemos acceder a `http://localhost:3001` para ver la aplicación.