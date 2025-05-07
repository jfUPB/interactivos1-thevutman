
#### Esta es la solucion de mi actividad ✍️
---

#### **Vectores de prueba**

| Nº | Estado actual | Evento | Fuente | Resultado esperado | Observación |
|----|----------------|--------|--------|---------------------|-------------|
| 1  | CONFIG         | 'A'    | Teclado | Tiempo +1 (máx 60) | Correcto |
| 2  | CONFIG         | 'A'    | micro:bit | Tiempo +1 (máx 60) | Correcto |
| 3  | CONFIG         | 'B'    | Teclado | Tiempo -1 (mín 10) | Correcto |
| 4  | CONFIG         | 'S'    | Teclado o micro:bit | Cambia a ARMADO y reinicia secuencia | Correcto |
| 5  | ARMADO         | 'A'    | Teclado | Agrega a secuencia | Correcto |
| 6  | ARMADO         | 'B'    | micro:bit | Agrega a secuencia | Correcto |
| 7  | ARMADO         | Secuencia ["A", "B", "A", "S"] | Mixto | Cambia a CONFIG | Correcto |
| 8  | ARMADO         | Tiempo llega a 0 | — | Cambia a EXPLOSION | Correcto |
| 9  | EXPLOSION      | 'T'    | Teclado o micro:bit | Cambia a CONFIG y reinicia tiempo | Correcto |
| 10 | CONFIG         | 'Z' (evento no modelado) | Teclado | Sin efecto | Correcto |
| 11 | ARMADO         | 'Z' (evento no modelado) | micro:bit | Sin efecto | Correcto |
| 12 | EXPLOSION      | 'A', 'B', 'S' | Teclado o micro:bit | Sin efecto | Correcto |
| 13 | CONFIG         | 'S' y luego 'A' | Teclado | No afecta, ya está en ARMADO | Correcto |
| 14 | Desconexión serial durante ARMADO | — | Sincronicidad mantenida, sigue funcionando con teclado | Correcto |
| 15 | Reconexión serial en CONFIG | — | Retoma comunicación sin reiniciar estado | Correcto |

#### **Pruebas de regresión**

| Prueba original | ¿Falló luego del cambio? | ¿Por qué falló? | ¿Cómo se corrigió? | Resultado final |
|------------------|--------------------------|------------------|---------------------|------------------|
| Prueba 1         | No                       | —                | —                   | Correcto |
| Prueba 4         | No                       | —                | —                   | Correcto |
| Prueba 7         | No                       | —                | —                   | Correcto |
| Prueba 9         | No                       | —                | —                   | Correcto |
| Prueba 13        | No                       | —                | —                   | Correcto |

