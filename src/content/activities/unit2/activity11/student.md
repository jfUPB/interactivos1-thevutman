#### Esta es la solucion de mi actividad ✍️
---

#### Funcionamiento  
1. **Modo Configuración:**  
   - La bomba inicia en este modo sin hacer la cuenta regresiva.  
   - El tiempo inicial de la bomba es de **20 segundos**.  
   - El usuario puede aumentar o disminuir el tiempo con los botones UP y DOWN.  
   - El tiempo programable está entre **10 y 60 segundos**, en incrementos/decrementos de **1 segundo**.  

2. **Modo Armado:**  
   - Se activa al hacer **shake (ARMED)**, iniciando la cuenta regresiva.  
   - La pantalla de LEDs muestra el tiempo restante.  

3. **Explosión:**  
   - Cuando el tiempo llega a **0**, el speaker emite una alarma de explosión.  

4. **Reinicio:**  
   - Para volver al modo de configuración, el usuario debe presionar el **botón TOUCH**.  

##### Estados de la Máquina  
- **CONFIGURACION:** Se ajusta el tiempo con UP/DOWN.  
- **ARMADO:** Se inicia la cuenta regresiva tras el shake.  
- **EXPLOSION:** Cuando el tiempo llega a 0, suena la alarma.  
- **REINICIO:** Se regresa a configuración tras tocar TOUCH.  

1. El sistema inicia en **CONFIGURACION**, permitiendo ajustar el tiempo de la bomba con los botones UP y DOWN.  
2. Al agitar la micro:bit (**Shake/ARMED**), el sistema cambia a **ARMADO** y comienza la cuenta regresiva.  
3. Cuando el tiempo llega a 0, se activa **EXPLOSION**, donde el speaker emite una alarma.  
4. Si el usuario presiona el botón TOUCH, la bomba se **reinicia** y vuelve a **CONFIGURACION**.  
