
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

# Variables de eventos
event_occurred = False
event_value = ""

def tareaEventos():
    """ Captura eventos del micro:bit y del puerto serial """
    global event_occurred, event_value

    if button_a.was_pressed():
        event_occurred = True
        event_value = "A"

    if button_b.was_pressed():
        event_occurred = True
        event_value = "B"

    if accelerometer.was_gesture("shake"):
        event_occurred = True
        event_value = "S"

    if pin_logo.is_touched():
        event_occurred = True
        event_value = "T"

    if uart.any():
        data = uart.read(1)
        if data:
            event_occurred = True
            event_value = chr(data[0])

def tareaBomba():
    global event_occurred, event_value, current_state, time_left, start_time, user_sequence
    if current_state == STATE_CONFIG:
        #display.scroll(str(time_left), delay=100, wait=True)  # Muestra el tiempo en pantalla

        if event_occurred:
            if event_value == "A" and time_left < 60:
                time_left += 1
                display.scroll(str(time_left))
            elif event_value == "B" and time_left > 10:
                time_left -= 1
                display.scroll(str(time_left))
            elif event_value == "S":  # Activar bomba
                current_state = STATE_ARMED
        
            event_occurred = False  # Consumir el evento

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
        if event_occurred:
            if event_value == "A":
                user_sequence.append("A")
            if event_value == "B":
                user_sequence.append("B")
            if event_value == "S":
                user_sequence.append("SHAKE")
            
            print(user_sequence)
        event_occurred = False  # Consumir el evento

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

        if event_occurred:
            if event_value == "T":
                current_state = STATE_CONFIG
                time_left = 20
        event_occurred = False # Consumir el evento
            
def check_deactivation():
    """ Verifica si la secuencia ingresada es correcta """
    return user_sequence == deactivation_sequence

while True:
    tareaBomba()
    tareaEventos()
```

#### **Refactoring con `tareaBomba()` y `tareaEventos()`:**

- **`tareaEventos()`:** Captura eventos del micro:bit y del puerto serial, almacenándolos en las variables `event_occurred` y `event_value`.
- **`tareaBomba()`:** Controla la máquina de estados de la bomba, consumiendo los eventos y ejecutando las acciones correspondientes.

**Uso de UART para comunicación serial:**

La bomba ahora puede recibir eventos desde una aplicación serial en la PC.

Si se envía "A", "B", "S", o "T", el evento se procesa igual que si viniera del micro:bit.

**Consumo de eventos:**

Después de procesar un evento, la variable event_occurred vuelve a False para evitar que se procese repetidamente.