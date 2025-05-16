
#### Esta es la solucion de mi actividad ✍️
---

#### **¿Qué ocurrió en la terminal cuando ejecutaste `npm install`?**
Cuando ejecuté `npm install`, la terminal comenzó a descargar e instalar varios módulos necesarios para el funcionamiento del proyecto. Estos incluyen Express y Socket.IO, que están listados en el archivo `package.json`. El propósito de este comando es instalar todas las dependencias que el servidor necesita para funcionar correctamente. Es un paso esencial para preparar el entorno de ejecución.

#### **¿Qué mensaje específico apareció en la terminal después de ejecutar `npm start`? ¿Qué indica este mensaje?**
Después de ejecutar `npm start`, apareció el siguiente mensaje en la terminal:

``` bash
Servidor escuchando en http://localhost:3000
```
Este mensaje indica que el servidor Node.js está corriendo y está listo para aceptar conexiones entrantes desde el navegador en el puerto 3000. Es una señal de que el entorno está correctamente configurado.

#### **Describe lo que ves inicialmente en `page1` y `page2` en tu navegador.**
Al abrir `http://localhost:3000/page1` y `http://localhost:3000/page2`, en ambas páginas aparece un lienzo con un fondo blanco y dos círculos. Cada página muestra un círculo negro (que representa al usuario local) y un círculo rojo (que representa al usuario remoto).

Inicialmente, ambos círculos están en el centro de la pantalla. No se mueven hasta que se interactúa con la ventana.

#### **¿Qué mensajes aparecieron en la terminal del servidor cuando abriste `page1` y `page2`?**
Cuando abrí cada página, la terminal mostró algo como:

``` bash
Un cliente se ha conectado
cliente conectado desde: /page1
Un cliente se ha conectado
cliente conectado desde: /page2
```

Esto indica que el servidor está registrando correctamente cada cliente que se conecta, y puede identificar desde qué página está llegando la conexión.

#### **Describe qué sucede en ambas páginas del navegador cuando mueves una de las ventanas.**
Cuando se mueve una de las ventanas del navegador, el círculo negro en esa página se desplaza de acuerdo con el movimiento del mouse (en eje X). Lo interesante es que en la otra ventana también se mueve el círculo rojo, que representa al cliente remoto.

Esto significa que el movimiento del mouse se está enviando en tiempo real al servidor, y luego al otro cliente, gracias a la comunicación con Socket.IO.

#### **¿Qué mensajes aparecen en la consola del navegador (F12 > Consola) y en la terminal del servidor durante esa interacción?**
- En la consola del navegador, aparecen mensajes como:

    ``` js
    hhGNFRdi8gQPOAs4AAAF

    {x: -7, y: 0, width: 500, height: 958}
    height:958
    width:500
    x:-7
    y:0
    [[Prototype]]:Object
    ```
    Estos indican que el sketch local está emitiendo datos (posición X del mouse) y está recibiendo datos del otro cliente.
- En la terminal del servidor, los mensajes son similares a:

    ``` css
    Received win2update from ID: hhGNFRdi8gQPOAs4AAAF Data: { x: 787, y: 99, width: 397, height: 958 }

    ```
    Esto confirma que el servidor recibe los datos de un cliente y los reenvía al otro, cumpliendo su función de "puente" entre ambos navegadores.