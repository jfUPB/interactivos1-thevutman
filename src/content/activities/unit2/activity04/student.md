#### Esta es la solucion de mi actividad ✍️
---

Para esta actividad, realicé experimentos con los botones A, B y el logo táctil del micro:bit, siguiendo el método de planteamiento de hipótesis, experimentación y análisis de resultados.  


#### **Experimento 1: Combinación de botones A y B** 

**¿Qué quería comprobar?**  
Si al presionar ambos botones simultáneamente se puede activar una acción diferente en el micro:bit.

**Hipótesis**  
Si presiono A y B al mismo tiempo, el micro:bit debería mostrar una imagen distinta en la pantalla.

**Código del experimento**  

```python
# Imports go at the top
from microbit import *


# Code in a 'while True:' loop repeats forever
while True:
    if button_a.is_pressed() and button_b.is_pressed():
        display.show(Image.YES)
    else:
        display.clear()

```

**Resultados obtenidos**

Cuando se presionan A y B al mismo tiempo, la pantalla muestra la imagen "YES". Si solo se presiona uno de los dos, la pantalla se mantiene apagada.

**Análisis de los resultados**

El micro:bit puede detectar la pulsación simultánea de A y B porque `is_pressed()` verifica cada botón de manera independiente. La condición lógica `and` permite que la acción solo ocurra cuando ambos botones están activos.

**Conclusión**

Es posible usar la combinación de botones para generar más interacciones, como un tercer estado adicional a los botones individuales.

#### **Experimento 2: Uso del logo táctil como botón virtual** 

**¿Qué quería comprobar?**  
Si el logo táctil en la parte superior del micro:bit puede ser utilizado como un botón.

**Hipótesis**  
Si toco el logo del micro:bit, debería encenderse un icono en la pantalla.

**Código del experimento**  

```python
# Imports go at the top
from microbit import *


# Code in a 'while True:' loop repeats forever
while True:
    if pin_logo.is_touched():
        display.show(Image.HAPPY)
    else:
        display.clear()

```

**Resultados obtenidos**

Al tocar el logo, aparece una cara feliz en la pantalla. Cuando se deja de tocar, la pantalla se apaga.

**Análisis de los resultados**

El logo del micro:bit funciona como una entrada capacitiva, detectando el contacto con la piel. La función `is_touched()` evalúa si hay suficiente cambio en la capacitancia para activar el evento.

**Conclusión**

El logo táctil puede ser usado como un botón adicional, permitiendo ampliar las opciones de interacción sin necesidad de botones físicos.