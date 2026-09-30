# Unidad 6: Agentes autónomos
## Link: [Click Aquí para el Simulador](https://oilworkerpantheon.github.io/Stick_Stickly_Organism_Santiago_Mateus/index.html)
**Proyecto:** Stick Stickly — instrumento visual para interpretar una pieza musical en vivo.  
**Autor:** Santiago Mateus.  
**Pieza:** “Stick Stickly”, de Attack Attack!  
**Estado de esta entrada:** documentación de la versión presente en el workspace.

> Esta bitácora registra el prototipo actual y las decisiones que pueden observarse en el código. Los resultados que requieren una prueba presencial, como el rendimiento en el equipo de presentación o la comodidad de la interpretación completa, quedan marcados como pendientes.

## Propósito y punto de partida

La Unidad 6 propone diseñar un instrumento visual para interpretar una pieza musical usando agentes autónomos. La persona debe escuchar, observar lo que emerge y decidir cómo intervenir; el sistema no debe limitarse a reproducir una animación programada ni a convertir automáticamente el audio en una secuencia visual.

La propuesta **Stick Stickly** representa un organismo humano como un ecosistema fluorescente y contradictorio: una anatomía reconocible contiene circulación, impulsos nerviosos, tejido y rastros de crecimiento. La intención es que la música se sienta como una presión sobre un cuerpo vivo, mientras que los agentes producen la organización local del organismo.

La frase que resume el instrumento es: **“No conduzco cada partícula; conduzco las condiciones para que el organismo responda.”**

La pista local está en `assets/stick_stickly.mp3`. El botón **INICIAR ORGANISMO** reproduce el audio y activa el análisis espectral. La interpretación principal continúa siendo manual mediante `A`, `S`, `D`, `F` y el mouse.

## Referentes y preguntas

- [The Nature of Code — Autonomous Agents](https://natureofcode.com/autonomous-agents/): percepción limitada, estado interno y cálculo de acciones.
- [Steering Behaviors for Autonomous Characters — Craig Reynolds](https://www.red3d.com/cwr/papers/1999/gdc99steer.pdf): velocidad deseada, steering y combinación de comportamientos.
- [Flow Fields — Tyler Hobbs](https://www.tylerxhobbs.com/words/flow-fields): campos de dirección como estructura compositiva.
- [Birds — ejemplos de Three.js](https://threejs.org/examples/?q=birds): separación, alineación y cohesión en flocking.
- [Interactive Physarum — Bleuje](https://github.com/Bleuje/interactive-physarum): rastros locales y organización emergente.
- [Physarum explanation — Bleuje](https://bleuje.com/physarum-explanation/): referencia para entender sensores, depósito y seguimiento de feromonas.

Preguntas que orientan la exploración:

- ¿Qué puede percibir cada agente y qué información se le oculta?
- ¿Cómo se combinan las reglas locales para que aparezca un organismo legible?
- ¿Qué cambios controla la música y cuáles deben quedar bajo decisión de la persona?
- ¿Cómo puede una intervención breve producir una consecuencia que permanezca en el sistema?

## Gramática del instrumento

El cuerpo funciona como un límite compartido. Los agentes nacen dentro de la máscara anatómica, se mantienen dentro de ella y se dibujan sobre una textura y un contorno estáticos. La identidad visual combina hueso, tejido y colores fluorescentes que no pretenden imitar una anatomía real.

| Sistema | Qué percibe | Cómo actúa | Significado visual |
|---|---|---|---|
| **Flocking / circulación** | Vecinos cercanos, velocidad de vecinos, centro local, campo y mouse | Combina separación, alineación, cohesión y flujo; limita la velocidad y reubica el agente si sale del cuerpo | Sangre o células que forman una actividad colectiva sin líder |
| **Steering / impulsos nerviosos** | Un objetivo anatómico seleccionado y su distancia | Calcula una velocidad deseada hacia el objetivo, con wander e impulso variable | Señales que atraviesan el organismo y conectan zonas |
| **Flow field** | Posición dentro del cuerpo, tiempo, flujo, energía, beat y mouse | Consulta una dirección espacial turbulenta, con atracción hacia el corazón | Entorno común que orienta a varios sistemas sin imponer una trayectoria individual |
| **Physarum / crecimiento** | Tres muestras de rastro alrededor del agente | Elige la dirección con mayor rastro, deposita nueva señal y difunde el rastro en una cuadrícula | Redes, vasos, tejido o cicatrices que emergen de decisiones locales |

La música se incorpora como una condición adicional, no como un director automático. El análisis FFT obtiene energía de graves, medios y agudos; los golpes graves disparan contracciones breves y la energía general modula movimiento y brillo. El sistema no selecciona por sí solo el pasaje del score ni pulsa las teclas del intérprete.

## Controles e intervención humana

- `A` / **PULSE:** aumenta la agitación de la circulación y la respuesta al pulso.
- `S` / **FLOW:** intensifica el campo vectorial y la turbulencia.
- `D` / **IMPULSE:** lanza impulsos nerviosos hacia objetivos anatómicos.
- `F` / **GROWTH:** favorece el depósito y la expansión de las redes de Physarum.
- **Mouse o touch:** desplaza el campo de influencia; mantener presionado perturba con mayor fuerza el tejido.
- **Audio:** inicia la pieza y aporta energía espectral y detección de beats.
- `H`: oculta el panel para la presentación.
- `Space`: activa pantalla completa.
- `R` o doble clic: hace un reinicio suave para repetir un ensayo.

Los controles no cambian una imagen terminada: cambian parámetros comunes de las reglas. Cada agente sigue calculando su respuesta con su estado y su percepción local.

## Score visual

El score es una guía para escuchar y decidir, no un timeline automático. Los tiempos son referencias iniciales y deben verificarse con la versión exacta de la pista.

| Pasaje | Intención | Intervención humana | Resultado esperado |
|---|---|---|---|
| 0:00 Intro | Cuerpo dormido, vivo pero contenido | Ninguna o mouse lento | Circulación tenue y nervios discretos |
| 0:16 Acumulación | Tensión creciente | Abrir `S` gradualmente | El flujo se acelera y gana turbulencia |
| 0:30 Pre-chorus | Anticipación | Preparar `A` | El corazón y la actividad global ganan presencia |
| 0:33 Chorus | Explosión corporal | `A` + `S` | Circulación y tejido alcanzan alta actividad |
| 0:56 Verse | Volver a respirar | Soltar `A` | El organismo recupera espacio y silencio |
| 1:06 Bridge | Descarga nerviosa | `D` puntual | Impulsos brillantes atraviesan el cuerpo |
| 1:11 Breakdown | Descontrol corporal | `F` + `S` | Physarum prolifera y el flocking se densifica |
| 2:01 Chorus 2 | Máxima intervención | `A` + mouse | El cuerpo recibe una perturbación amplia e intensa |
| 2:23 Outro | Sobrevivir y dejar memoria | Soltar controles | Baja la actividad y quedan rastros residuales |

## Decisiones de implementación

- El prototipo funciona como una página web local sin npm ni librerías externas.
- El canvas usa una resolución limitada y ajusta el `devicePixelRatio` si el promedio de cuadros baja, para cuidar la presentación en tiempo real.
- Se usan 420 agentes de circulación, 120 nervios y 250 agentes de Physarum. Las cantidades son parámetros de una primera versión, no una medición de anatomía.
- La máscara `body_mask.png` define el espacio válido. Los agentes que salen son reubicados progresivamente dentro del cuerpo para conservar la lectura de organismo.
- El flocking usa vecinos limitados y combina separación, alineación y cohesión con el flow field, el crecimiento, la energía y la influencia del mouse.
- Los nervios usan steering hacia siete objetivos anatómicos posibles. `IMPULSE` aumenta la velocidad deseada y renueva los objetivos.
- Physarum mantiene una cuadrícula de rastros, consulta tres sensores angulares, elige el rastro más fuerte, deposita señal y aplica difusión/decaimiento.
- El audio se conecta mediante `AnalyserNode`. Los graves entre 20 y 120 Hz alimentan el detector de pulso; otras bandas modulan la energía de movimiento y la respuesta visual.
- La arquitectura conserva agentes persistentes: no se reemplaza la colonia por una imagen distinta cuando cambia el control.

## Registro de proceso

| Fecha / versión | Prueba o decisión | Evidencia | Aprendizaje / siguiente paso |
|---|---|---|---|
| Versión actual | Integrar cuatro comportamientos autónomos en un solo organismo | `index.html`: circulación, nervios, flow field y Physarum | La combinación permite distribuir funciones expresivas entre sistemas distintos |
| Versión actual | Mantener la intervención manual como centro del performance | Teclas `A`, `S`, `D`, `F`, mouse y score visible | Los parámetros comunes son legibles y pueden ensayarse por pasajes musicales |
| Versión actual | Añadir respuesta sutil al audio | `AnalyserNode`, energía de graves y detector de flux | El audio puede reforzar el pulso sin reemplazar las decisiones del intérprete |
| Pendiente | Ensayar una interpretación completa en pantalla grande | Aún no registrada en esta bitácora | Medir legibilidad, FPS, escala del cuerpo y fatiga de la interfaz |
| Pendiente | Ajustar el score a la escucha real | Tiempos iniciales en `SCORE.md` | Verificar entradas, duración de gestos y momentos en que conviene soltar |

## Reflexión personal

Esta reflexión queda abierta para completarse después del ensayo presencial:

- ¿El organismo se percibe como un sistema autónomo o como una animación que responde a botones?
- ¿Qué combinación produce una relación más clara entre música, cuerpo y emergencia: `A` + `S`, `D` o `F` + `S`?
- ¿Los rastros de Physarum se leen como memoria del gesto o como ruido visual?
- ¿Qué puede percibir realmente cada agente y qué parte de esa percepción debería limitarse más?
- ¿Qué cambia al ocultar el panel y observar la pieza a distancia?
- ¿Qué intervención puedo sostener con escucha y cuál exige demasiada atención a la interfaz?

## Autoevaluación del proyecto

Cada criterio vale 25 puntos. Los puntajes siguientes son provisionales hasta completar la presentación y deben sostenerse con capturas, pruebas o registro del ensayo.

| Criterio | Puntaje provisional / 25 | Evidencia actual y evidencia pendiente |
|---|---:|---|
| **Cumplimiento del encargo**: instrumento web, tiempo real e interpretación de una pieza | 23 | Página local, audio integrado, canvas en tiempo real y score. Falta probar la ejecución completa en el equipo de presentación. |
| **Comprensión y verificación**: explicar percepción, acciones y efectos de los parámetros | 23 | El código separa flocking, steering, flow field y Physarum, y los controles tienen consecuencias visibles. Falta registrar una prueba comparativa de cada parámetro. |
| **Diseño e intención**: justificar la combinación en relación con la música | 22 | El organismo, la paleta y el score relacionan circulación, descarga, crecimiento y memoria con pasajes musicales. Falta revisar si todas las metáforas se leen sin explicación verbal. |
| **Interpretación humana**: score y controles permiten conducir en vivo | 21 | Hay nueve momentos de guía, cuatro controles expresivos, mouse y reinicio. Falta ensayar la pieza completa y ajustar tiempos, ergonomía y transiciones. |
| **Total provisional** | **89 / 100** | Puntaje sujeto a la evidencia del ensayo y la demostración. |

## Próximos pasos

1. Servir el proyecto con Live Server y probar el audio, la pantalla completa y los controles.
2. Ensayar al menos 30–60 segundos con la pista exacta y anotar qué gestos son expresivos, tardíos o difíciles de coordinar.
3. Medir rendimiento y legibilidad en el computador y la pantalla de presentación.
4. Ajustar el score después de escuchar las entradas reales de la canción.
5. Completar la reflexión y reemplazar los puntajes provisionales por una autoevaluación sustentada.

[Volver a la bitacora principal](../README.md)
