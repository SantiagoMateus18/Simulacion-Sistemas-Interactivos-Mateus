# Bitácora — Unidad 7: Word as a Playable System

**Proyecto:** VANS — Infinite Playable Typography  
**Autor:** Santiago Alejandro Mateus Arciniegas  
**Tecnologías:** p5.js, HTML5/CSS3  

---

## 1. Intención Semántica e Identidad

- **Empresa:** VANS (*footwear* y cultura urbana).
- **Atributo a comunicar:** **esencia del skate**. La marca no es solo un rótulo que se lee, sino un entorno físico que se transita y se domina POR MEDIO DEL SKATEBOARDING
- **Público objetivo:** Skaters, músicos, jóvenes y seguidores de la escena urbana y alternativa.
- **Contexto de uso:** Minijuego arcade web / experiencia interactiva tipográfica para una campaña digital de VANS.

---

## 2. Referentes e Inspiración

- **La palabra como entorno arquitectónico:** Evolución del concepto *Word as Image*, llevando la tipografía a convertirse en un terreno transitable (pista de skate).
- **Estética Cómic / Pop-Art (UI):** Interfaces planas con alto contraste (amarillo `#C4BE5D` y cyan `#47A8BD`), contornos negros gruesos y sombras ladeadas sólidas (`box-shadow` duro) que evocan viñetas de cómics underground.
- **Arcades de precisión (OlliOlli / Tony Hawk 2D):** Mecánicas minimalistas centradas en el *timing* (saltos), la inercia y la superación de puntajes en lapsos muy cortos (15 segundos).

---

## 3. Diseño Gráfico y Tipográfico

Las letras del nombre **V-A-N-S** dejaron de ser formas separadas para convertirse en un circuito unificado:

- **La Pista BOLD:** Construcción tipográfica masiva basada en el logotipo oficial. Trazos negros sólidos y extragruesos (`strokeWeight: 112`) sobre un fondo blanco puro. El techo de la letra "V" se extiende cubriendo "A-N-S", formando la estructura superior de la pista.
- **Circuito Infinito:** Al finalizar la "S", una pista larga inferior (asfalto) conecta de regreso al inicio de la "V", creando un bucle cerrado ininterrumpido.
- **Collage de Fondo:** Siluetas aleatorias de chicos haciendo skate y tocando guitarra eléctrica. Se renderizan como sombras translúcidas (opacidad baja, teñidas de negro) dispersas dinámicamente por todo el lienzo blanco sin alterar el contraste principal.
- **El Avatar:** Una tabla de skate gráfica con ruedas y el icónico óvalo de "Off The Wall" que aloja la palabra VANS.

---

## 4. Modelo Computacional y Reglas

### Sistema Físico y de Cámara (p5.js puro)
- **Cinemática sobre curvas:** Las letras se generaron mediante polilíneas, curvas de interpolación y suavizado de esquinas (algoritmo de Chaikin). La patineta calcula su ángulo dinámicamente según los puntos previos y siguientes de la ruta.
- **Cámara Dinámica (Tracking):** La cámara sigue el eje X del jugador de forma estricta, mientras que en el eje Y hace un paneo suave (suavizado matemático) cuando la tabla desciende a la pista larga de retorno.
- **Gravedad y Salto:** Un sistema de físicas lineal para el eje vertical controla la parábola del salto (fuerza de impulso vs. tracción gravitacional).

### Mecánica de Juego (Score & Timer)
- **Condición de tiempo:** El jugador tiene un temporizador estricto de **15 segundos** para recorrer la pista.
- **Puntuación (Jump Score):** Se suma un punto cada vez que el jugador completa un salto (Ollie) exitoso mientras la tabla está en movimiento (velocidad mayor a 2).
- **Game Over Loop:** Al llegar a cero, se muestra la puntuación final. El juego no tiene "muerte" física, permitiendo intentos infinitos al reiniciar.

### Interacción y Controles
1. **Flecha Derecha `→` / `D`:** Acelerar (aplica aceleración sumatoria hasta un límite de velocidad máxima).
2. **Flecha Izquierda `←` / `A`:** Frenar y dar reversa.
3. **Tecla `ESPACIO`:** Ejecutar un salto (*Ollie*) y sumar puntos al aterrizar.
4. **Tecla `R` / Botón "Reiniciar":** Resetea la posición, velocidad, puntos y el cronómetro a 15 segundos sin recargar la página.
5. **Tecla `H`:** Oculta o muestra la interfaz de controles estilo cómic para apreciar la pista limpia.

---

## 5. Pruebas y Resultados de Interacción

- **Prueba de Pista Continua:** Se verificó matemáticamente el cierre del bucle entre la letra "S" y la "V" inferior para evitar saltos bruscos en el movimiento de la patineta.
- **Orientación del Objeto:** Se ajustó el cálculo de la rotación mediante `atan2` e interpolación, logrando que el skate haga un *flip* natural (cambio de dirección visual) cuando la pista hace un giro de 180 grados.
- **Balance del Temporizador:** 15 segundos demostraron ser el tiempo óptimo para recorrer el logotipo al menos una vez a velocidad máxima, fomentando la repetición y la búsqueda de *high scores* mediante la barra espaciadora.

---

## 6. Autoevaluación

| Criterio de Evaluación | Nota (0 - 25) | Sustentación con Evidencias | Comentarios Personales |
| :--- | :---: | :--- | :--- |
| **1. Cumplimiento del encargo** | **25 / 25** | El sistema utiliza una marca: VANS, funciona en tiempo real en la web (p5.js + Matter.js + Tone.js) y está hecho con base a ideales y marketing del producto original. | Me |
| **2. Comprensión y verificación del modelo** | **25 / 25** | hay parámetros físicos de rebote/fricción, el comportamiento de *Squash & Stretch*, y el control de volumen por disipación de sonido (*decay*). | Encantan |
| **3. Interacción e identidad** | **25 / 25** | Permite explorar la cultura rock/skate de Vans mediante la manipulación de pistas musicales de un "himno" de dicha cultura y la respuesta elástica de las letras representan la suela de goma presente en los zapatos. | Los zapatos |
| **4. Resolución tipográfica y experiencia** | **25 / 25** | Los collages de instrumentos en *Cel Shading*, la interfaz acorde a la filosofía de VANS, el reseteo con `R` y la visibilidad con `H` garantizan una lectura clara, jugable y con sentido sobre lo que representan los zapatos en la industria. | VANS |
| **NOTA FINAL SUSTENTADA** | **100 / 100** | **Valor total de la unidad:** **12.5%** de la nota final del curso. | La tabla fue hecha sin IA. Fue máximo esfuerzo!!!!! |
