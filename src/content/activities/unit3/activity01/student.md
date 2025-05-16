
#### Esta es la solucion de mi actividad ✍️
---

``` py
from microbit import *
import utime

class Semaforo:
    def __init__(self, rojo, amarillo, verde, posicion):
        self.tiempos = {'rojo': rojo, 'amarillo': amarillo, 'verde': verde}
        self.estado = 'rojo'
        self.tiempo_restante = rojo
        self.posicion = posicion  # Posición en el display
        self.ultimo_cambio = utime.ticks_ms()  # Marca de tiempo inicial
        self.dibujar()

    def actualizar_estado(self):
        ahora = utime.ticks_ms()
        if utime.ticks_diff(ahora, self.ultimo_cambio) >= 1000:  # 1 segundo
            self.tiempo_restante -= 1
            self.ultimo_cambio = ahora
            
            if self.tiempo_restante <= 0:
                if self.estado == 'rojo':
                    self.estado = 'verde'
                    self.tiempo_restante = self.tiempos['verde']
                    self.borrar()
                    self.dibujar()
                elif self.estado == 'verde':
                    self.estado = 'amarillo'
                    self.tiempo_restante = self.tiempos['amarillo']
                    self.borrar()
                    self.dibujar()
                elif self.estado == 'amarillo':
                    self.estado = 'rojo'
                    self.tiempo_restante = self.tiempos['rojo']
                    self.borrar()
                    self.dibujar()

    def dibujar(self):
        # display.clear()
        if self.estado == 'rojo':
            display.set_pixel(self.posicion, 0, 9)  # Representación del rojo
        elif self.estado == 'amarillo':
            display.set_pixel(self.posicion, 2, 9)  # Representación del amarillo (brillo medio)
        elif self.estado == 'verde':
            display.set_pixel(self.posicion, 4, 9)  # Representación del verde (brillo bajo)
            
    def borrar(self):
        # display.clear()
        if self.estado == 'verde':
            display.set_pixel(self.posicion, 0, 0)  # Representación del rojo
        elif self.estado == 'rojo':
            display.set_pixel(self.posicion, 2, 0)  # Representación del amarillo (brillo medio)
        elif self.estado == 'amarillo':
            display.set_pixel(self.posicion, 4, 0)  # Representación del verde (brillo bajo)

semaforo1 = Semaforo(5, 2, 3, 0)
semaforo2 = Semaforo(3, 1, 2, 2)
semaforo3 = Semaforo(4, 3, 2, 4)

while True:
    # display.clear()
    semaforo1.actualizar_estado()
    semaforo2.actualizar_estado()
    semaforo3.actualizar_estado()
```

#### **Reflexión**

- Reutilización de código: Definir un semáforo como una clase nos permite crear múltiples instancias sin necesidad de escribir código repetitivo.
- Modularidad: Cada semáforo funciona de manera independiente con sus propios atributos y métodos, facilitando la depuración y mantenimiento.
- Escalabilidad: Si en el futuro necesitamos más semáforos o cambiar sus tiempos, solo debemos modificar los valores de las instancias sin alterar la lógica principal.
- Organización del código: La programación orientada a objetos permite estructurar el código de manera más clara y fácil de entender.
Además, el uso de una máquina de estados dentro de la clase es fundamental para modelar correctamente el comportamiento del semáforo. En este caso, cada semáforo pasa por tres estados (rojo, amarillo, verde), cambiando según el tiempo programado. Este enfoque es eficiente porque separa la lógica de cambio de estados del código principal, asegurando que cada semáforo sigue su propio ciclo sin interferencias.🚦