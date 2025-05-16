#### Esta es la solucion de mi actividad ✍️
---

``` py
# Imports go at the top
from microbit import *

uart.init(baudrate=115200)

# Code in a 'while True:' loop repeats forever
while True:
    display.show(Image.HEART)
    sleep(1000)

    display.scroll("Hi!")
    sleep(1000)

    display.show(Image.HAPPY)
    sleep(1000)

    display.show(Image.SAD)
    sleep(1000)


```

**Explicación del Código**

1. Mostrar imágenes `display.show(Image.X)`

    Se usa `display.show()` para visualizar imágenes predefinidas en la pantalla LED:
- Image.HEART: Un corazón.
- Image.HAPPY: Una cara sonriente.
- Image.SAD: Una cara triste.
2. Mostrar texto `display.scroll("Hi!")`

    Se puede mostrar texto directamente en la pantalla LED de izquierda a derecha.
3. Retraso entre cambios `sleep(1000)`

    sleep(1000) detiene el código durante 1 segundo para que cada imagen o texto sea visible.