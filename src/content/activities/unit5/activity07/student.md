#### Esta es la solucion de mi actividad ✍️
---

Esta unidad me pareció muy valiosa porque me permitió enfrentarme a una situación real de comunicación entre un microcontrolador y una interfaz visual. Sentí que no solo aprendí conceptos técnicos como protocolos binarios, framing, checksum o buffers, sino también a tener paciencia para depurar errores que no siempre eran fáciles de detectar. Me gustó ver cómo todo lo aprendido en código tenía un efecto tangible: una coordenada que cambia, un botón que responde, un dato que llega bien o llega mal. Eso me ayudó a mantenerme motivado.

Me pareció especialmente interesante que trabajáramos primero con protocolo ASCII y luego con binario. Esa comparación me ayudó a entender por qué es importante la eficiencia en sistemas donde cada byte cuenta. Aunque el protocolo binario fue más complejo de implementar, también fue el que más me enseñó. Me hizo pensar en detalles que antes no habría considerado, como cuántos bytes tiene un entero o por qué necesitamos sincronización en un flujo de datos.

**¿Qué creo que se podría mejorar en esta unidad para los próximos semestres?**

Creo que algo que se podría mejorar es que haya una explicación visual o animada del proceso de framing y verificación del paquete binario. Tal vez una animación paso a paso que muestre cómo llega el buffer, cómo se buscan los bytes de sincronización, cómo se corta el paquete y cómo se calcula el checksum. Eso ayudaría mucho a los que somos más visuales y nos cuesta entender todo solo leyendo código.

También considero que sería útil tener un ejemplo completo funcionando al inicio, como una referencia segura, y luego desmontarlo poco a poco para entender cómo se construyó. A veces ver todo junto desde el principio ayuda a reducir la ansiedad de no entender.

Por último, podría incluirse una breve introducción sobre cómo funcionan los buffers en general y cómo se gestionan los datos que llegan en trozos, porque al principio eso fue un poco confuso.
