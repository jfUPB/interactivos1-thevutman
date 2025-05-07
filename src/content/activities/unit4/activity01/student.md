
#### Esta es la solucion de mi actividad ✍️
---

#### **Sitios explorados:**
- OpenProcessing
- Generative Design
- p5.js Examples

---

#### **Ejemplo 1: OpenProcessing**

- **Enlace al ejemplo**: [2D Complex Exponents](https://openprocessing.org/sketch/2604831)

- **¿Qué me llamó la atención?**  
  El movimiento de las lineas y cómo se comportan de forma orgánica dependiendo del movimiento del mouse.

- **¿Cómo está hecho?**  
  - Tiene dibididas las secciones, para: `math`, `visual`, `grid`
    - **math:** Tiene adentro funciones con operaciones para calcular vectores
    - **visual:** Tiene adentro el `setUp()` y `draw()` y aqui esta toda la configuracion del proyecto
    - **grid:** Tiene adentro funciones que permite hacer el grid de fondo  


- **Modificación realizada**:  
  Cambié los colores de las lineas y el fondo, y aumenté el número de vectores para darle más densidad al efecto visual.

- **Enlace a mi versión modificada**: [Mi versión modificada en p5.js](https://editor.p5js.org/supervejito80/sketches/Q-I02MQtL)

---

#### **Ejemplo 2: Generative Design**

- **Enlace al ejemplo**: [Generative Design P_2_0_02"](http://www.generative-gestaltung.de/2/sketches/?01_P/P_2_0_02)

- **¿Qué me llamó la atención?**  
  La generación automática de patrones geométricos a partir de interacciones simples.

- **¿Cómo está hecho?**  
  - Usa funciones como `beginShape()`, `vertex()`, `endShape()`.
  - Utiliza ciclos `for` para generar múltiples figuras.
  - Juega mucho con sin y cos

- **Modificación realizada**:  
  Agregué interacción con el mouse: cuando haces clic, se cambia la paleta de colores de los patrones.

- **Enlace a mi versión modificada**: [Mi versión modificada en p5.js](https://editor.p5js.org/supervejito80/sketches/CxZu60GT9)

---

#### **Ejemplo 3: p5.js Examples**

- **Enlace al ejemplo**: [3D Cube Sphere Example - p5.js](https://p5js.org/examples/3d-orbit-control/)

- **¿Qué me llamó la atención?**  
  Me pareció muy interesante cómo se crea una esfera usando únicamente cubos distribuidos en anillos mediante rotaciones en 3D. Además, la interacción con el mouse para girar la cámara le da una experiencia inmersiva.

- **¿Cómo está hecho?**  
  - Utiliza `WEBGL` como modo de renderizado 3D.
  - Usa `orbitControl()` para permitir el control de cámara con el mouse.
  - Utiliza `rotateZ()` y `rotateX()` en bucles anidados para posicionar los cubos en anillos.
  - Los cubos se colocan con `translate()` y se dibujan con `box()`.

- **Modificación realizada**:  
  Cambié el color de fondo y el color de los cubos, añadí una ligera rotación automática sobre el eje Y para que el objeto gire lentamente aunque el usuario no interactúe, y reduje la separación entre cubos para hacerlo más denso visualmente.

- **Enlace a mi versión modificada**: [Mi versión modificada en p5.js](https://editor.p5js.org/supervejito80/sketches/5AMEZ4guC)

