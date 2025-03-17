
#### Esta es la solucion de mi actividad ✍️
---

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

# Secuencia de desactivación esperada
deactivation_sequence = ["A", "B", "A", "SHAKE"]
user_sequence = []

def check_deactivation():
    """ Verifica si la secuencia ingresada es correcta """
    return user_sequence == deactivation_sequence

while True:
    if current_state == STATE_CONFIG:
        display.scroll(str(time_left))  # Muestra el tiempo en pantalla

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

        # Capturar secuencia de desactivación
        if button_a.was_pressed():
            user_sequence.append("A")
        if button_b.was_pressed():
            user_sequence.append("B")
        if accelerometer.was_gesture("shake"):
            user_sequence.append("SHAKE")

        # Si se ingresa una secuencia errónea, se borra
        if len(user_sequence) > len(deactivation_sequence) or user_sequence != deactivation_sequence[:len(user_sequence)]:
            user_sequence = []

        # Si la secuencia es correcta, se desactiva la bomba
        if check_deactivation():
            display.show(Image.HAPPY)
            utime.sleep_ms(2000)
            current_state = STATE_CONFIG
            time_left = 20
            user_sequence = []  # Reiniciar secuencia

    elif current_state == STATE_EXPLODED:
        display.show(Image.SKULL)  # Representa la explosión
        music.play(music.WAWAWAWAA)
        utime.sleep(2)

        if pin_logo.is_touched():
            current_state = STATE_CONFIG
            time_left = 20
```

- Lista user_sequence: Guarda los botones presionados en orden.
- Lista deactivation_sequence: Contiene la secuencia correcta (["A", "B", "A", "SHAKE"]).
- Validación: Se compara la secuencia ingresada con la esperada en cada paso.
- Si el usuario se equivoca, la secuencia se reinicia y la cuenta regresiva sigue.
- Si la secuencia es correcta, la bomba vuelve al estado de configuración y muestra una carita feliz.