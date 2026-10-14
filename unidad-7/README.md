# Bitácora — Unidad 7: Word as a Playable System

**Proyecto:** VANS — Off The Wall Sound  
**Autor:** Santiago Alejandro Mateus Arciniegas  
**Tecnologías:** p5.js, Matter.js, Tone.js, HTML5/CSS3  

---

## 1. Intención Semántica e Identidad

* **Empresa:** VANS (*footwear* y cultura urbana).
* **Atributo a comunicar:** **Resiliencia Elástica y Expresión Alternativa (Rock/Skate)**. Vans no es solo un zapato; es la suela de goma que soporta los impactos del escenario, el moshpit y la tabla de skate.
* **Público objetivo:** Músicos, skaters, jóvenes y seguidores de la escena alternativa (punk, emo, rock alternativo).
* **Contexto de uso:** *Hero section* / Portada web interactiva para una campaña digital de la marca ("Off The Wall Sound").

---

## 2. Referentes e Inspiración

* **Ji Lee — *Word as Image*:** El concepto de que la estructura gráfica de la letra comunica directamente la función del objeto.
* **Estética Cel Shading / Borderlands:** Contornos negros gruesos, colores planos (*pop-art*) y sombreado tipo cómic para reforzar el carácter caricaturesco de las letras.
* **Multi-track Stem Players:** Inspiración en videojuegos musicales (*Rock Band*) para desglosar una canción (*All The Small Things*) en 4 canales independientes.

---

## 3. Diseño Gráfico y Tipográfico

Las letras del nombre **V-A-N-S** fueron construidas como collages de instrumentos musicales específicos con transparencia en PNG:

* **V (Voz):** Formada por un ensamble de micrófonos de mano grises.
* **A (Guitarras):** Estructurada mediante ensamble de guitarras eléctricas rojas.
* **N (Bajo):** Compuesta por varios bajos eléctricos en tonos azules.
* **S (Batería):** Curvada utilizando tambores de batería.

**Ambiente visual:** Fondo estilo estudio fotográfico en tono rojo oscuro degradado con un patrón halftone (`#5a1e1e` a `#2a0b0b`) con sombra de piso en CSS y un panel flotante de interfaz estructurado como viñeta de cómic en contraste (amarillo y cyan).

---

## 4. Modelo Computacional y Reglas

### Sistema Físico (Matter.js + p5.js)
* **Cuerpos rígidos e impacto:** Cada letra posee un cuerpo físico rectangular con propiedades de fricción ($0.8$) y rebote/restitución ($0.7$).
* **Squash & Stretch:** La escala visual se deforma dinámicamente en p5.js según la velocidad vertical ($v_y$), simulando la elasticidad de la goma vulcanizada.
* **Límites cerrados:** Muros e infraestructuras invisibles de 500 px de grosor evitan que las letras salgan disparadas fuera del viewport.

### Sistema de Audio (Tone.js)
* **Sincronización:** Las 4 pistas (*stems*) inician simultáneamente al dar clic en el overlay inicial, manteniéndose en bucle perfecto en segundo plano.
* **Modulación por energía:** El volumen de cada pista decae progresivamente si la letra queda inactiva o abandona la interacción, y recupera su ganancia ($0\text{ dB}$) al ser manipulada o golpeada.

### Interacción y Controles
1. **Teclas `V`, `A`, `N`, `S`:** Funcionan como interruptores (*toggle*). Encienden/apagan la pista correspondiente y le aplican un impulso físico vertical.
2. **Arrastre con Mouse:** Permite agarrar, lanzar y hacer rebotar cualquier letra en la escena.
3. **Tecla `R` / Botón "Reset VANS":** Reorganiza las 4 letras instantáneamente a su posición original, alineación horizontal y rotación $0^\circ$.
4. **Tecla `H`:** Oculta o muestra la interfaz de controles estilo cómic.

---

## 5. Pruebas y Resultados de Interacción

* **Prueba de sincronización:** Se verificó que al activar múltiples letras en tiempos distintos no existen desfases de ritmo en la canción.
* **Prueba física:** Las letras responden elásticamente al mouse y a los comandos de teclado sin atravesar paredes ni perder su forma original tras los impactos.
* **Respuesta perceptiva:** Quienes interactúan con el sistema descubren que pueden "armar la mezcla" de la banda mientras juegan con la elasticidad de las letras.

---

## 6. Autoevaluación

| Criterio de Evaluación | Nota (0 - 25) | Sustentación con Evidencias | Comentarios Personales |
| :--- | :---: | :--- | :--- |
| **1. Cumplimiento del encargo** | **25 / 25** | El sistema utiliza una marca: VANS, funciona en tiempo real en la web (p5.js + Matter.js + Tone.js) y está hecho con base a ideales y marketing del producto original. | Me |
| **2. Comprensión y verificación del modelo** | **25 / 25** | hay parámetros físicos de rebote/fricción, el comportamiento de *Squash & Stretch*, y el control de volumen por disipación de sonido (*decay*). | Encantan |
| **3. Interacción e identidad** | **25 / 25** | Permite explorar la cultura rock/skate de Vans mediante la manipulación de pistas musicales de un "himno" de dicha cultura y la respuesta elástica de las letras representan la suela de goma presente en los zapatos. | Los zapatos |
| **4. Resolución tipográfica y experiencia** | **25 / 25** | Los collages de instrumentos en *Cel Shading*, la interfaz acorde a la filosofía de VANS, el reseteo con `R` y la visibilidad con `H` garantizan una lectura clara, jugable y con sentido sobre lo que representan los zapatos en la industria. | VANS |
| **NOTA FINAL SUSTENTADA** | **100 / 100** | **Valor total de la unidad:** **12.5%** de la nota final del curso. | La tabla fue hecha sin IA. Fue máximo esfuerzo!!!!! |
