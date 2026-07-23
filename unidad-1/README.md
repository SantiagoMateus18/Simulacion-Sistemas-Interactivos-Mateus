# Unidad 1: Aleatoriedad

Bitácora de trabajo de la Unidad 1 del curso de Simulación.

## Sesión 1 - Exploración y conceptos

- **Referentes revisados:** Ejemplos clásicos de *The Nature of Code* (Daniel Shiffman) sobre random walk (caminata aleatoria) y distribución gaussiana (`randomGaussian`).
- **Conceptos clave:**
  - **Caminata aleatoria (random walk):** un objeto se mueve paso a paso en direcciones elegidas al azar, acumulando su posición a lo largo del tiempo.
  - **Distribución normal / gaussiana:** valores que se concentran alrededor de una media, con una dispersión (desviación estándar) controlable.
  - **Ruido Perlin:** a diferencia del random puro, genera valores que cambian suavemente en el tiempo o el espacio (útil para texturas orgánicas y tendencias que no "saltan").
  - **Lévy flight:** un tipo de caminata aleatoria donde la mayoría de los pasos son pequeños, pero ocasionalmente ocurre un salto enorme (distribución de cola pesada) — modela eventos raros/excepcionales.
- **Reflexión:** `Estos modelos me sirven como la base para generar cosas a futuro. Son como los esqueletos de toda una experiencia artística generativa. xd`.

## Sesión 2 - Ejercicios guiados

Antes de construir el reto final, hice una serie de experimentos pequeños para entender cada concepto por separado, con ayuda de IA generativa (ver sección de uso de IA más abajo). El orden fue:

1. **Random walk básico con un objeto (`Walker`):** un punto que se mueve pixel a pixel en 4 direcciones (arriba/abajo/izquierda/derecha), elegidas con `floor(random(4))`.
2. **Cambio de figura:** reemplacé `circle()`/`stroke()` por `triangle()`, lo que me hizo entender que esta función necesita 6 argumentos (3 vértices), no 2 — mi primer error fue justamente no pasarle las coordenadas completas.
3. **Sesgo direccional:** modifiqué las probabilidades del `step()` para que dos de los 4 "casos" movieran hacia la derecha en vez de repartir la izquierda/derecha/arriba/abajo por igual — esto hizo que el walker "derivara" con una tendencia, en vez de moverse simétricamente.
4. **Wraparound (mundo toroidal):** agregué `if (this.x > width) this.x = 0;` para que el objeto reaparezca del lado opuesto al salir del canvas, en vez de perderse fuera de pantalla.
5. **Combiné random walk + distribución gaussiana:** en vez de que la gaussiana esté centrada en un punto fijo (`randomGaussian(320, 60)`), hice que el *centro* de la distribución (`mx`, `my`) se mueva con un random walk — así la "nube" de puntos migra por el canvas en vez de quedar fija.
6. **Rotación:** usé `translate()` + `rotate()` + `push()`/`pop()` para que la nube gaussiana tuviera forma elíptica (distinta desviación estándar en X y en Y) y rotara sobre su propio centro con el tiempo.
7. **Color y transparencia:** experimenté con `fill(r,g,b,alpha)` y `noStroke()` para lograr el efecto de "densidad acumulada" — muchas figuras semi-transparentes superpuestas generan zonas más opacas donde cae más "sedimento" y zonas más tenues donde cae menos.

- **Dificultades:**
  - Confundí `stroke()` con `triangle()` al copiar mal la sintaxis — aprendí que cada función de dibujo en p5.js tiene su propia cantidad de argumentos y no son intercambiables.
  - Al principio no entendía por qué la gaussiana "saltaba" a una posición nueva en cada frame sin memoria del frame anterior — la diferencia clave entre una variable local (se recrea cada `draw()`) y una variable de estado que persiste (`this.x` en una clase, o una variable global).
- **Soluciones:**
  - Verificar siempre la documentación de p5.js para la cantidad de argumentos de cada función de dibujo.
  - Sacar variables de posición a nivel de clase o global cuando necesito que persistan entre frames, en vez de declararlas dentro de `draw()`.

## Sesión 3 - Planteamiento del reto de diseño

- **Idea del reto:** "Navegar la incertidumbre" — en vez de simular tierra de forma literal, simular *procesos* geológicos (sedimentación, erosión, fractura) como sistema visual continuo, donde los 5 momentos de la unidad (posibilidad, tendencia, normalidad, excepción, influencia) coexisten todo el tiempo como capas del mismo sistema, en vez de estar separados en escenas distintas.
- **Bocetos / referencias:** Los experimentos de la Sesión 2 (walker con sesgo, wraparound, nube gaussiana rotante, transparencia acumulativa) funcionaron como boceto conceptual y técnico directo para el sketch final: cada pieza pequeña que probé se integró luego en una función específica del reto.

## Sesion 4 - Evaluacion y presentacion

| Momento | Comportamiento en el sistema |
|---|---|
| **Posibilidad** | Cada partícula de sedimento nace con un movimiento horizontal totalmente aleatorio (`random(-1, 1)` en `updateParticle`), sin dirección dominante. |
| **Tendencia** | Un sesgo direccional (`driftBias`) generado con ruido Perlin (`noise(frameCount * 0.0015)`) se mezcla gradualmente con el azar puro mediante `lerp()`; `biasStrength` crece muy lento (de 0 a 0.85) para que la tendencia se consolide sin saltos bruscos. |
| **Normalidad** | Cada 90 frames, `smoothTowardsMean()` empuja cada columna del terreno hacia el promedio general, con una perturbación gaussiana (`randomGaussian(0, 0.6)`) — el terreno tiende a un perfil "normal", parejo. |
| **Excepción** | Un click dispara `triggerLevyEvent()`: un salto tipo Lévy flight, con distribución de cola pesada (`pow(random(0.001,1), -1/alpha)`), casi siempre pequeño pero ocasionalmente enorme — una fractura repentina del terreno. |
| **Influencia** | La cercanía del mouse curva la trayectoria de las partículas (`influenceRadius`) — no las controla, las inclina probabilísticamente hacia o en contra de su posición. |

### Sistema generativo

- **Caminata aleatoria:** ajusta la velocidad horizontal de cada partícula frame a frame.
- **Distribución normal:** usada en `smoothTowardsMean()` para suavizar el terreno hacia un promedio.
- **Ruido Perlin:** controla la tendencia direccional (`driftBias`) y el bamboleo visual de cada depósito (`wob`), dando textura orgánica.
- **Lévy flight:** genera los eventos de excepción con saltos de magnitud mayormente pequeña pero ocasionalmente extrema.
- 
### Identidad visual

- **Paleta:** tonos cálidos y minerales (marrones, ocres, arenas), evocando estratos de tierra.
- **Textura:** orgánica y acumulativa, con leve distorsión de ruido en cada depósito.
- **Ritmo:** lento y "geológico" en la acumulación normal, interrumpido por destellos abruptos en los eventos de excepción.

### - Resultado final:
Sketch:
```js
/*
  RETO 07 — "Navegar la incertidumbre"
  Tema: sedimentación / terreno geológico infinito.

  Conceptos de la unidad usados:
  - Ruido Perlin       -> textura de fondo y ondulación de las capas
  - Caminata aleatoria  -> deriva horizontal de las partículas al caer
  - Distribución normal -> suavizado del terreno hacia un promedio (normalidad)
  - Lévy flight         -> fractura/desprendimiento que dispara el click (excepción)

  Los 5 momentos NO están en escenas separadas: coexisten todo el tiempo
  como capas de un mismo sistema. Lo que cambia es cuál predomina.
*/

// ---------- Configuración del lienzo 9:16 ----------
let W = 540;
let H = 960;
let scaleFactor = 1;

// ---------- Terreno ----------
let terrain;              // p5.Graphics: acumula la sedimentación (permanente)
let cols = 90;             // columnas del "mapa de alturas"
let surfaceHeight = [];    // altura acumulada por columna (desde abajo)
let colWidth;

// ---------- Partículas (sedimento cayendo) ----------
let particles = [];
const BASE_PARTICLE_RATE = 2; // cuántas partículas nuevas por frame en reposo

// ---------- Momento 2: Tendencia ----------
let driftBias = 0;        // sesgo direccional que se consolida lentamente
let biasStrength = 0;     // 0 = todavía todo es "posibilidad", 1 = tendencia fuerte

// ---------- Momento 4: Excepción (Lévy) ----------
let flashEvents = [];      // efectos visuales temporales de fracturas

// ---------- Momento 5: Influencia ----------
let influenceRadius = 140;

// ---------- Ciclo de pausa y reinicio ----------
let state = 'running';       // 'running' | 'resetting'
const RESET_HEIGHT_RATIO = 0.55; // a qué altura se congela y empieza el reinicio
const RESET_SHIFT = 10;          // velocidad del scroll durante el reinicio
let resetScrolled = 0;

// paleta de sedimento (tonos cálidos / minerales)
const PALETTE = [
  [64, 42, 33],
  [92, 58, 38],
  [122, 78, 45],
  [156, 104, 56],
  [184, 132, 74],
  [201, 164, 101],
];

function setup() {
  let cnv = createCanvas(W, H);
  cnv.parent(document.querySelector('main'));
  pixelDensity(1);
  fitCanvasToWindow();

  terrain = createGraphics(W, H);
  terrain.pixelDensity(1);
  terrain.noStroke();
  terrain.background(10, 8, 6);

  colWidth = W / cols;
  for (let i = 0; i < cols; i++) surfaceHeight[i] = random(6, 14);

  noStroke();
}

function windowResized() {
  fitCanvasToWindow();
}

function fitCanvasToWindow() {
  // mantiene el marco 9:16 dentro de cualquier pantalla (letterbox)
  let s = min(windowWidth / W, windowHeight / H);
  scaleFactor = s;
  let cnv = document.querySelector('canvas');
  if (cnv) {
    cnv.style.width = (W * s) + 'px';
    cnv.style.height = (H * s) + 'px';
  }
}

function draw() {
  if (state === 'running') {
    // ---------- 1) Actualiza la "tendencia" (Momento 2) ----------
    // Empieza cerca de cero (posibilidad total) y se va consolidando
    // muy lentamente con ruido Perlin: nunca es una decisión, es una deriva.
    driftBias = (noise(frameCount * 0.0015) - 0.5) * 2.4;
    biasStrength = constrain(biasStrength + 0.00025, 0, 0.85);

    // ---------- 2) Genera nuevas partículas de sedimento ----------
    let spawnRate = BASE_PARTICLE_RATE + (mouseIsInsideCanvas() ? 2 : 0);
    for (let i = 0; i < spawnRate; i++) spawnParticle();

    // ---------- 3) Actualiza y deposita partículas ----------
    for (let i = particles.length - 1; i >= 0; i--) {
      let p = particles[i];
      updateParticle(p);
      if (p.settled) {
        depositParticle(p);
        particles.splice(i, 1);
      } else if (p.pos.y > H + 20) {
        particles.splice(i, 1); // se perdió, no debería pasar casi nunca
      }
    }

    // ---------- 4) Cada tanto, "normalidad": suaviza el terreno ----------
    if (frameCount % 90 === 0) smoothTowardsMean();

    // ---------- 5) ¿Llegó al límite? Congela todo y empieza el reinicio ----------
    let maxH = Math.max(...surfaceHeight);
    if (maxH > H * RESET_HEIGHT_RATIO) {
      startReset();
    }
  } else if (state === 'resetting') {
    // nada cae, nada se genera: solo el scroll hasta quedar todo negro
    doResetStep();
  }

  // ---------- Dibuja ----------
  image(terrain, 0, 0);
  if (state === 'running') drawParticles();
  drawFlashEvents();
}

// =====================================================================
// PARTÍCULAS
// =====================================================================

function spawnParticle() {
  particles.push({
    pos: createVector(random(W), -random(20)),
    vx: 0,
    speed: random(1.2, 2.4),
    col: floor(random(PALETTE.length)),
    settled: false,
  });
}

function updateParticle(p) {
  // Momento 1 (Posibilidad): componente totalmente aleatoria, uniforme.
  let randomWalkStep = random(-1, 1);

  // Momento 2 (Tendencia): se mezcla con el sesgo consolidado driftBias.
  // biasStrength controla cuánto ya "pesa" la tendencia sobre el azar puro.
  let biased = lerp(randomWalkStep, driftBias, biasStrength);

  // Momento 5 (Influencia): la cercanía del visitante curva la caída
  // hacia (o en contra de) su posición, sin definirla del todo.
  let d = dist(p.pos.x, p.pos.y, mouseX, mouseY);
  let influence = 0;
  if (d < influenceRadius) {
    let strength = map(d, 0, influenceRadius, 0.9, 0);
    let dirSign = mouseX > p.pos.x ? 1 : -1;
    influence = dirSign * strength;
  }

  p.vx = lerp(p.vx, biased + influence, 0.08);
  p.pos.x += p.vx;
  p.pos.y += p.speed;
  p.pos.x = constrain(p.pos.x, 0, W - 1);

  let colIndex = floor(p.pos.x / colWidth);
  colIndex = constrain(colIndex, 0, cols - 1);
  let surfaceY = H - surfaceHeight[colIndex];

  if (p.pos.y >= surfaceY) {
    p.settled = true;
    p.colIndex = colIndex;
    p.landY = surfaceY;
  }
}

function depositParticle(p) {
  // el depósito es pequeño y aleatorio: la suma de muchos de estos
  // pequeños incrementos es lo que genera el perfil "normal" del terreno.
  let amount = random(0.4, 1.3);
  surfaceHeight[p.colIndex] += amount;

  let x = p.colIndex * colWidth;
  // modulo "seguro": nunca da negativo, incluso si surfaceHeight fuera negativo
  let raw = floor(surfaceHeight[p.colIndex] / 22) % PALETTE.length;
  let bandIndex = (raw + PALETTE.length) % PALETTE.length;
  let c = PALETTE[bandIndex];

  terrain.fill(c[0], c[1], c[2], 210);
  let wob = map(noise(x * 0.01, frameCount * 0.002), 0, 1, -2, 2);
  terrain.ellipse(x + colWidth / 2 + wob, p.landY, colWidth * 1.4, 4);
}

function drawParticles() {
  noStroke();
  for (let p of particles) {
    let c = PALETTE[p.col];
    fill(c[0] + 30, c[1] + 20, c[2] + 10, 230);
    circle(p.pos.x, p.pos.y, 3.2);
  }
}

// =====================================================================
// MOMENTO 3: NORMALIDAD
// =====================================================================

function smoothTowardsMean() {
  let mean = surfaceHeight.reduce((a, b) => a + b, 0) / cols;
  for (let i = 0; i < cols; i++) {
    // empuja suavemente cada columna hacia el promedio, con ruido
    // gaussiano: la mayoría de las columnas quedan cerca de lo habitual.
    let pull = randomGaussian(0, 0.6);
    surfaceHeight[i] = lerp(surfaceHeight[i], mean, 0.03) + pull;
    surfaceHeight[i] = max(surfaceHeight[i], 2);
  }
}

// =====================================================================
// MOMENTO 4: EXCEPCIÓN (Lévy flight) — disparado por click
// =====================================================================

function mousePressed() {
  if (state !== 'running') return;
  if (!mouseIsInsideCanvas()) return;
  triggerLevyEvent(mouseX, mouseY);
}

function triggerLevyEvent(x, y) {
  let centerCol = constrain(floor(x / colWidth), 0, cols - 1);

  // paso de Lévy: casi siempre pequeño, ocasionalmente enorme
  // (distribución de cola pesada, clásica de Lévy flight)
  let alpha = 1.5;
  let magnitude = pow(random(0.001, 1), -1 / alpha);
  magnitude = constrain(magnitude, 10, 220);
  let direction = random() < 0.5 ? 1 : -1;

  // afecta un rango de columnas alrededor del click, decayendo con la distancia
  let spread = 10;
  for (let i = -spread; i <= spread; i++) {
    let idx = centerCol + i;
    if (idx < 0 || idx >= cols) continue;
    let falloff = 1 - abs(i) / spread;
    surfaceHeight[idx] += direction * magnitude * falloff * random(0.3, 1);
    surfaceHeight[idx] = max(surfaceHeight[idx], 2);
  }

  // esto también puede torcer la tendencia futura: un evento raro
  // "descubre territorio nuevo" y reorienta el sesgo consolidado.
  driftBias = constrain(driftBias + direction * random(0.3, 0.8), -1, 1);

  // ráfaga de partículas emitidas desde el punto de fractura
  for (let i = 0; i < 40; i++) {
    let a = random(TWO_PI);
    let sp = random(1, 6);
    particles.push({
      pos: createVector(x, y),
      vx: cos(a) * sp,
      speed: abs(sin(a) * sp) + 0.6,
      col: floor(random(PALETTE.length)),
      settled: false,
    });
  }

  flashEvents.push({ x, y, r: 6, alpha: 255 });
}

function drawFlashEvents() {
  for (let i = flashEvents.length - 1; i >= 0; i--) {
    let f = flashEvents[i];
    noFill();
    stroke(230, 200, 150, f.alpha);
    strokeWeight(2);
    circle(f.x, f.y, f.r);
    f.r += 6;
    f.alpha -= 10;
    if (f.alpha <= 0) flashEvents.splice(i, 1);
  }
  noStroke();
}

// =====================================================================
// CICLO: PAUSA -> SCROLL HASTA NEGRO -> REINICIO
// =====================================================================

function startReset() {
  state = 'resetting';
  particles = [];       // se congela todo: nada sigue cayendo
  resetScrolled = 0;
}

function doResetStep() {
  let shift = RESET_SHIFT;
  terrain.copy(0, shift, W, H - shift, 0, 0, W, H - shift);
  terrain.noStroke();
  terrain.fill(10, 8, 6);
  terrain.rect(0, H - shift, W, shift);
  resetScrolled += shift;

  if (resetScrolled >= H) {
    // ya quedó completamente negro: reinicia el ciclo desde cero
    terrain.background(10, 8, 6);
    for (let i = 0; i < cols; i++) surfaceHeight[i] = random(6, 14);
    driftBias = 0;
    biasStrength = 0;
    state = 'running';
  }
}

// =====================================================================
// UTILIDAD
// =====================================================================

function mouseIsInsideCanvas() {
  return mouseX >= 0 && mouseX <= W && mouseY >= 0 && mouseY <= H;
}
```
Style.css:
```js
html, body {
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
  background: #0a0806;
}

main {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100vw;
  height: 100vh;
}

canvas {
  display: block;
  /* la sombra ayuda a que el "marco" 9:16 se lea como una pieza,
     incluso cuando la pantalla real tiene otra proporción */
  box-shadow: 0 0 60px rgba(0, 0, 0, 0.6);
}
```

- Enlace al prototipo: [Prototipo en P5.js](https://editor.p5js.org/SantiagoMateus18/sketches/tOxnf-Rwz)
- Reflexion final:

## Uso dado a la IA generativa

Usé IA generativa (Claude) como herramienta de exploración conceptual y depuración de código durante la Sesión 2, antes de construir el sketch final. El proceso documentado fue:

1. Empecé con un ejemplo base de *The Nature of Code* (un `Walker` con `stroke()`/`line()` y random walk de 4 direcciones).
2. Le pedí ayuda para reemplazar el dibujo por `triangle()` — la IA me explicó que esta función requiere 6 argumentos (3 vértices) y no 2, y me mostró cómo derivarlos a partir de un punto central y un "tamaño".
3. Pregunté cómo sesgar el random walk hacia una dirección — la IA propuso dos enfoques: duplicar un caso en el `if/else` (solución simple) o usar umbrales de probabilidad con `random(1)` (solución más flexible y escalable). **Decisión:** usé el enfoque de duplicar el caso, por simplicidad, entendiendo el trade-off de flexibilidad que eso implica.
4. Pedí agregar wraparound (mundo toroidal) — la IA propuso el chequeo `if (this.x > width) this.x = 0`, y señaló que también hacía falta cubrirlo en el eje Y, lo cual yo no había contemplado.
5. Pregunté cómo mover globalmente una nube de puntos generada con `randomGaussian` — la IA me explicó la diferencia entre una variable local (se recrea cada frame) y una variable de estado persistente, y propuso mover el *centro* de la distribución con un random walk en vez de mover cada punto individualmente.
6. Pedí que la nube rotara — la IA propuso usar `translate()` + `rotate()` + `push()`/`pop()`, con distintas desviaciones estándar en X e Y para lograr una forma elíptica que rota.
7. Pregunté cómo cambiar de círculos a triángulos dentro de ese sistema rotado, y luego cómo manejar color y transparencia con `fill()`/`noStroke()`/`stroke()`.

**Cambios realizados sobre las propuestas de la IA:** 
1. Estructura inicial del sketch
Después de decidir el tema (sedimentación/terreno) y los 5 momentos, le pedí que tradujera esas ideas a un sketch funcional con click como interacción principal (el disparador del momento de "Excepción").

2. Corrección de un bug de crasheo
Al probar el sketch, la consola arrojó un error cuando el terreno crecía demasiado. Le compartí el error y le pedí que lo solucionara; identificamos que era un problema de índices negativos en el arreglo de colores al hacer scroll, y se corrigió.

3. Ajuste del ritmo visual
Noté que el crecimiento del terreno y el ciclo de colores se sentían muy lentos, así que pedí ajustar las variables de ritmo (cantidad de partículas, velocidad de depósito, grosor de las capas de color) para que la pieza se sintiera más viva.

4. Rediseño del ciclo de reinicio
Decidí que, en vez de un scroll infinito continuo, quería que el sistema tuviera un ciclo más marcado: al llegar a cierto punto, todo se congela (nada cae, nada se genera), la pantalla se desplaza hasta quedar en negro total, y ahí reinicia desde cero. Le pedí implementar esa lógica de estados (running / resetting) y revertir los ajustes de ritmo anteriores a sus valores originales.

Es importante notar que el sketch final del Reto 07 (sistema de partículas, terreno acumulativo, Lévy flight, ciclo de reinicio) es una elaboración propia mucho más compleja que los ejercicios de exploración — estos últimos sirvieron como base conceptual y de sintaxis, no como código copiado directamente.
---

[Volver a la bitacora principal](../README.md)
