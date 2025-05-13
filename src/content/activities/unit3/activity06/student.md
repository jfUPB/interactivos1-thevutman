#### Esta es la solucion de mi actividad ✍️
---

#### **Vectores de prueba**

|#	|Estado inicial	|Evento (tecla)	|Resultado esperado	|Estado final esperado	|¿Pasó?	|Observación|
|---|-------------------------------|-------------------|----------------|---|--|-----------|
|1	|CONFIG	|A	|Aumenta el tiempo a 21	|CONFIG	|[ ]	|Verifica que el tiempo aumente sin pasar de 60.|
|2	|CONFIG	|B	|Disminuye el tiempo a 19	|CONFIG	|[ ]	|Verifica que no baje de 10.
|3	|CONFIG	|S	|Cambia al estado ARMADO y comienza conteo regresivo	|ARMADO	|[ ]	|Reinicia seqPropia y empieza el temporizador.|
|4	|ARMADO	|A, B, A, S	|Desactiva bomba (secuencia correcta)	|CONFIG	|[ ]	|Debe reiniciar el tiempo a 20.|
|5	|ARMADO	|A, A, A, A	|No se desactiva bomba	|ARMADO	|[ ]	|La secuencia es incorrecta.|
|6	|ARMADO	|Esperar 20 seg	|Explosión automática	|EXPLOSION	|[ ]	|Después de 20 seg, cambia a EXPLOSION.|
|7	|EXPLOSION	|T	|Reinicia todo	|CONFIG	|[ ]	|Estado vuelve a CONFIG y tiempo a 20.|
|8	|ARMADO	|A, B	|Acumula secuencia parcial	|ARMADO	|[ ]	|No cambia de estado aún.|
|9	|ARMADO	|A, B, A, A	|No se desactiva	|ARMADO	|[ ]	|Solo secuencia exacta desactiva.|
|10	|EXPLOSION	|A	|No hace nada	|EXPLOSION	|[ ]	|Solo tecla T tiene efecto.
