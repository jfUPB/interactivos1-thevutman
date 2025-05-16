
#### Esta es la solucion de mi actividad ✍️

``` py
from microbit import *
import utime
import music

# Definir estados de la máquina
STATE_CONFIG = 0
STATE_ARMED = 1
STATE_COUNTDOWN = 2
STATE_EXPLODED = 3

# Variables de control
current_state = STATE_CONFIG
time_left = 20  # Tiempo inicial en segundos
start_time = 0

while True:
    if current_state == STATE_CONFIG:
        display.scroll(str(time_left))  # Muestra el tiempo en la pantalla
        
        if button_a.was_pressed() and time_left < 60:
            time_left += 1
        if button_b.was_pressed() and time_left > 10:
            time_left -= 1
        if accelerometer.was_gesture("shake"):  # Activar bomba
            current_state = STATE_ARMED

    elif current_state == STATE_ARMED:
        display.show(Image.YES)
        utime.sleep_ms(1000)
        start_time = utime.ticks_ms()
        current_state = STATE_COUNTDOWN

    elif current_state == STATE_COUNTDOWN:
        elapsed_time = (utime.ticks_ms() - start_time) // 1000
        remaining_time = time_left - elapsed_time

        if remaining_time > 0:
            display.scroll(str(remaining_time))
        else:
            current_state = STATE_EXPLODED

        if pin_logo.is_touched():
            current_state = STATE_CONFIG
            time_left = 20

    elif current_state == STATE_EXPLODED:
        display.show(Image.SKULL)  # Representa la explosión
        music.play(music.WAWAWAWAA)
        
        if pin_logo.is_touched():
            current_state = STATE_CONFIG
            time_left = 20

```