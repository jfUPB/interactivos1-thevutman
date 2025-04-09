#### Esta es la solucion de mi actividad ✍️
---

``` py
# Imports go at the top
from microbit import *
import music
import speech

# Code in a 'while True:' loop repeats forever
while True:
    if button_a.is_pressed():
        music.play(music.BA_DING)
        sleep(500)

    if button_b.is_pressed():
        music.play(['C4:4', 'E4:4', 'G4:4'])
        sleep(500)
    if pin_logo.is_touched():
        speech.say('hola mundo')
```

1. Si se presiona el botón B, se reproduce una melodía personalizada:
- C4:4 → Nota Do en la 4ta octava, duración 4.
- E4:4 → Nota Mi en la 4ta octava, duración 4.
- G4:4 → Nota Sol en la 4ta octava, duración 4.
- sleep(500) para evitar repeticiones continuas.


`music.play([])` permite tocar secuencias de notas.

2- Si se toca el logo, el micro:bit dice "Hola mundo" en voz sintetizada.

- `speech.say('hola mundo')` usa el módulo de síntesis de voz del micro:bit.