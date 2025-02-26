#### Esta es la solucion de mi actividad ✍️
---


#### Descripción del Problema  
El micro:bit sigue esta secuencia de imágenes en pantalla:  
1. **Cara Feliz** → 1.5 segundos  
2. **Cara Sonriente** → 1 segundo  
3. **Cara Triste** → 2 segundos  
4. **Repetir ciclo**  

Si el usuario presiona el botón A en cualquier momento:  
- **Feliz → Triste**  
- **Sonriente → Feliz**  
- **Triste → Sonriente**  

#### Concurrencia en el Programa  
El programa logra la concurrencia al:  
- **Separar el control del tiempo de la detección de eventos**, verificando constantemente si ha pasado el tiempo de cada estado sin bloquear la ejecución.  
- **Usar `utime.ticks_ms()` para medir el tiempo sin detener el flujo del programa con `sleep()`**, permitiendo que se capturen eventos de botones en cualquier momento.  
- **Cambiar el estado inmediatamente cuando se detecta un evento de botón**, interrumpiendo la secuencia normal si es necesario.  

#### Análisis del Código  
El código implementa una **máquina de estados** con cuatro estados:  
1. `STATE_INIT`: Configura el sistema y muestra la cara feliz.  
2. `STATE_HAPPY`: Muestra la cara feliz y espera 1.5 segundos.  
3. `STATE_SMILE`: Muestra la cara sonriente y espera 1 segundo.  
4. `STATE_SAD`: Muestra la cara triste y espera 2 segundos.  

Cada estado tiene **eventos** que lo llevan a otro estado:  
- **Tiempo transcurrido** → Cambia al siguiente estado.  
- **Presión del botón A** → Cambia a un estado alternativo.  

#### Vectores de Prueba  
Para comprobar la correcta ejecución del programa, se aplicaron los siguientes vectores de prueba:  

##### 🔹 **Vector de Prueba 1 - Secuencia Normal**  
- **Condición Inicial:** El programa inicia en `STATE_HAPPY`.  
- **Eventos Generados:** No se presiona ningún botón, se deja correr el tiempo.  
- **Resultado Esperado:**  
  1. `STATE_HAPPY` → `STATE_SMILE` (después de 1.5s).  
  2. `STATE_SMILE` → `STATE_SAD` (después de 1s).  
  3. `STATE_SAD` → `STATE_HAPPY` (después de 2s).  
- **Resultado Obtenido:** Secuencia correcta. 

##### 🔹 **Vector de Prueba 2 - Interrupción en `STATE_HAPPY`**  
- **Condición Inicial:** El programa está en `STATE_HAPPY`.  
- **Eventos Generados:** Se presiona el botón A antes de que pase 1.5s.  
- **Resultado Esperado:**  
  - Inmediatamente cambia a `STATE_SAD`, sin esperar 1.5s.  
  - Luego sigue la secuencia normal (`STATE_SAD → STATE_HAPPY`).  
- **Resultado Obtenido:** Interrupción correcta. 

##### 🔹 **Vector de Prueba 3 - Interrupción en `STATE_SAD`**  
- **Condición Inicial:** El programa está en `STATE_SAD`.  
- **Eventos Generados:** Se presiona el botón A antes de que pasen 2s.  
- **Resultado Esperado:**  
  - Inmediatamente cambia a `STATE_SMILE`.  
  - Luego sigue la secuencia normal (`STATE_SMILE → STATE_SAD`).  
- **Resultado Obtenido:** Interrupción correcta. 
