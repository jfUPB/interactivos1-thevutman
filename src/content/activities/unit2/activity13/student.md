#### Esta es la solucion de mi actividad ✍️
---

El diseño de la máquina de estados para la bomba temporizada fue un ejercicio interesante en la estructuración de la lógica secuencial y la respuesta a eventos en tiempo real. Opté por una estructura con cuatro estados principales: **configuración, armado, cuenta regresiva y explosión**.

Uno de los principales desafios fue gestionar la transición entre estados sin bloqueos, lo que me llevó a utilizar `utime.ticks_ms()` para manejar la temporización sin afectar la capacidad de respuesta a eventos. También noté que la representación visual en la pantalla LED podría mejorarse para hacer más clara la cuenta regresiva, quizá mostrando dígitos más grandes o animaciones.  

Para mejorar el diseño, podría implementar un mecanismo de **desactivación de la bomba** con una secuencia específica de botones, lo que haría el juego más interactivo. Además, podría añadir un efecto visual más impactante en la explosión, como parpadeos rápidos antes del sonido. En general, el diseño funciona bien, pero siempre hay margen para optimización en la experiencia del usuario y la eficiencia del código.  
