#### Esta es la solucion de mi actividad ✍️
---

#### 💻 Código en MicroPython

``` py
from microbit import *

class Semaforo:
    def __init__(self):
        self.state = "ROJO"
        self.startTime = running_time()
        self.interval = 4000 

    def update(self):
        currentTime = running_time()
        
        if self.state == "ROJO":
            self.mostrar_rojo()
            if currentTime - self.startTime > self.interval:
                self.state = "AMARILLO1"
                self.startTime = currentTime
                self.interval = 800 
        
        elif self.state == "VERDE":
            self.mostrar_verde()
            if currentTime - self.startTime > self.interval:
                self.state = "AMARILLO2"
                self.startTime = currentTime
                self.interval = 800
        
        elif self.state == "AMARILLO1":
            self.mostrar_amarillo()
            if currentTime - self.startTime > self.interval:
                self.state = "VERDE"
                self.startTime = currentTime
                self.interval =3000  
                
        elif self.state == "AMARILLO2":
            self.mostrar_amarillo()
            if currentTime - self.startTime > self.interval:
                self.state = "ROJO"
                self.startTime = currentTime
                self.interval = 4000
    
    def mostrar_rojo(self):
        display.clear()
        for y in range(2):  # Las dos primeras filas
            for x in range(1, 4):
                display.set_pixel(x, y, 9)
    
    def mostrar_amarillo(self):
        display.clear()
        for x in range(1, 4):
            display.set_pixel(x, 2, 9)  # Tercera fila
    
    def mostrar_verde(self):
        display.clear()
        for y in range(3, 5):  # Últimas dos filas
            for x in range(1, 4):
                display.set_pixel(x, y, 9)

semaforo = Semaforo()

while True:
    semaforo.update()
    sleep(100)
```

#### Análisis del Código

#### 🔄 Estados de la Máquina  
1. **ROJO** → El semáforo se encuentra en rojo, impidiendo el paso.  
2. **VERDE** → El semáforo cambia a verde, permitiendo el paso.  
3. **AMARILLO** → Indica advertencia para pasar a verde y antes de volver a rojo.  

#### ⚡ Eventos Evaluados  
- **ROJO → AMARILLO1:** Ocurre después de 4 segundos.  
- **VERDE → AMARILLO2:** Ocurre después de 3 segundos.  
- **AMARILLO1 → ROJO:** Ocurre después de 80 milisegundos. 
- **AMARILLO2 → VERDE:** Ocurre después de 80 milisegundos.  

#### 🎬 Acciones en cada Evento  
- **En ROJO:** Se encienden los LEDs de las dos primeras filas.  
- **En VERDE:** Se encienden los LEDs de las dos últimas filas.  
- **En AMARILLO:** Se encienden los LEDs de la tercera fila.  

