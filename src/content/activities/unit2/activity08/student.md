#### Esta es la solucion de mi actividad ✍️
---
**Descripción**

Este programa utiliza una máquina de estados para controlar el parpadeo de dos píxeles en la pantalla LED del micro:bit. Cada píxel alterna entre encendido y apagado en intervalos de tiempo específicos.

**Estado**

`Init`	Se ejecuta al crear el objeto Pixel. Inicializa el tiempo y enciende el píxel. Luego, cambia a `WaitTimeout`.`

`WaitTimeout`	Espera a que pase un tiempo `interval` antes de cambiar el estado del píxel y actualizar la pantalla.

**Evento**

`"¿Ha pasado el tiempo de espera?"`	Si el tiempo transcurrido es mayor que `interval`, cambia el estado del píxel.

**Acción**

`display.set_pixel(x, y, valor)`	Enciende o apaga un píxel en la pantalla del micro:bit.

`utime.ticks_ms()`	Obtiene el tiempo actual en milisegundos.

`utime.ticks_diff()`	Calcula la diferencia de tiempo entre dos momentos.

**Resultados y Conclusiones**

- El código implementa una máquina de estados finitos que alterna entre dos estados (`Init` y `WaitTimeout`).

- Cada píxel parpadea a su propio ritmo:

  - `pixel1` en la posición `(0,0)` cambia cada **1000 ms** (1s).

  - `pixel2` en la posición `(4,4)` cambia cada **500 ms** (0.5s).

- Se utiliza `utime.ticks_ms()` para controlar los intervalos sin necesidad de `sleep()`, lo que permite mantener el programa no bloqueante.