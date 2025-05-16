#### Esta es la solucion de mi actividad ✍️
---

#### **Entradas y salidas del micro:bit**  

**Entradas:**  
1. **Botón A**: Botón físico en el lado izquierdo del micro:bit, usado para interacciones.  
2. **Botón B**: Botón físico en el lado derecho del micro:bit, similar a A, pero independiente.  
3. **Sensor de luz**: Usa los LED de la pantalla para detectar cambios en la iluminación ambiental.  
4. **Acelerómetro**: Detecta la inclinación, sacudidas y movimiento en tres ejes (x, y, z).  

**Salidas:**  
1. **25 Led light**: Pantalla de 25 LEDs que permite mostrar imágenes y texto.  
2. **Speaker**: Genera sonidos con diferentes frecuencias.  
3. **Pines de salida**: Se pueden usar para controlar LEDs, motores y otros dispositivos electrónicos.  
4. **Comunicación serial**: Envía datos a través de la interfaz USB o Bluetooth.  

---

#### **Funciones de Micropython para Entradas y Salidas**  

**Funciones para Entradas:**  
1. **`button_a.is_pressed()`** - Verifica si el botón A está presionado.  

   ```python
   from microbit import *
   if button_a.is_pressed():
       display.show("A")
    ```
2. **`accelerometer.get_x()`** - Obtiene la aceleración en el eje X.

   ```python
    from microbit import *
    while True:
        x = accelerometer.get_x()
        print(x)
        sleep(100)
    ```
3. **`pin1.read_analog()`** - Lee un valor analógico de un sensor conectado al pin 1.

   ```python
    from microbit import *
    valor = pin1.read_analog()
    print(valor)
    ```

**Funciones para Salidas:**  
1. **`display.show(Image.HEART)`** - Muestra un ícono en la matriz de LEDs.

   ```python
    from microbit import *
    display.show(Image.HEART)
    ```
2. **`pin0.write_digital(1)`** - Envía un valor digital (1 o 0) a un pin para encender o apagar un dispositivo.

   ```python
    from microbit import *
    pin0.write_digital(1)
    ```
3. **`music.play(music.BA_DING)`** - Reproduce un sonido.

   ```python
    from microbit import *
    import music
    music.play(music.BA_DING)
    ```
