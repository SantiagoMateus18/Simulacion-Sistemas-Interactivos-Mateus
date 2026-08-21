# Unidad 3: Fuerzas

[Link local](http://localhost:5173/)
# Guion de interpretación — LesAlpx

## Antes de empezar (con la canción en pausa)

Estado por defecto al cargar la página (NO es cero):
- `radialStrength` = 2.20 (atracción)
- `vortexStrength` = 1.40 (giro)
- `dragCoefficient` = 0.12
- `wind` = apagado

1. Abre la página en modo LAB.
2. Pulsa `P` para pasar a PERFORMANCE (así se oculta el panel y controlas solo con teclado/mouse).
3. Ten el mouse quieto, cerca del centro de la pantalla.
4. Dale play a la canción y arranca el cronómetro al mismo tiempo.

**Regla de oro sobre el mouse:** el punto que sigue tu cursor es el "atractor" — el lugar hacia el cual atrae o repele todo el sistema. Muévelo despacio siempre, nunca de golpe (salvo que quieras un efecto brusco a propósito).

---

## TRAMO 1 · 0:00 – 0:20 (20 segundos) · "Ondas que suben"

| Cuándo | Tecla | Cuántas veces | Efecto |
|---|---|---|---|
| Seg 0 | `V` | 1 vez | Apaga el vórtice (queremos calma, sin giro todavía) |
| Seg 0–2 | `↓` | 12 veces (rápido, en 2 seg) | Baja `radialStrength` de 2.20 a ~1.0 — atracción más suave |
| Seg 3 | `W` | 1 vez | Enciende el viento |
| Seg 3–20 | `D` | 1 vez cada 1 segundo (17 veces en total) | Sube `wind.y` de 0 a ~1.7 — esto es literalmente "la ola subiendo" |

**Mouse:** quieto en el centro de la pantalla, sin moverlo.

**Qué deberías ver:** las partículas dejan de girar, se sueltan un poco de la atracción, y empiezan a derivar lentamente hacia arriba, cada vez más rápido.

---

## TRAMO 2 · 0:20 – 1:10 (50 segundos) · "Pulsaciones (parlante)"

| Cuándo | Tecla | Cuántas veces | Efecto |
|---|---|---|---|
| Seg 20 | `W` | 1 vez | Apaga el viento (ya cumplió su función) |
| Seg 20 | `A` | 17 veces (rápido) | Regresa `wind.y` a 0 (limpia el tramo anterior) |
| Cada ~4 segundos, desde el seg 20 hasta el 70 (≈12 pulsos) | `↑` x5 rápido, luego `↓` x5 rápido | 1 ciclo completo por pulso | Cada ciclo es un "latido": sube `radialStrength` ~0.5 y vuelve a bajar. Eso es la pulsación tipo parlante |

**Cómo hacer un "pulso" bien:** en menos de 1 segundo, toca `↑` cinco veces seguidas (sube de ~1.0 a ~1.5), espera medio segundo, toca `↓` cinco veces seguidas (vuelve a ~1.0). Repite este ciclo cada 4 segundos aprox., siguiendo el ritmo que escuches.

**Mouse:** puedes moverlo en círculos muy pequeños y lentos cerca del centro, casi sin desplazarte — le da un poco de vida sin romper la pulsación.

**Qué deberías ver:** el enjambre se "infla y desinfla" rítmicamente, como si respirara.

---

## TRAMO 3 · 1:15 – 1:50 (35 segundos) · "Estable: ondas y pulsaciones"

| Cuándo | Tecla | Cuántas veces | Efecto |
|---|---|---|---|
| Seg 0 (1:15) | `V` | 1 vez | Reactiva el vórtice |
| Seg 0–5 | `→` | 6 veces | Sube `vortexStrength` de 0 a ~0.6 — giro suave |
| Durante todo el tramo, cada ~6 seg (≈5 veces) | `↑` x3, luego `↓` x3 | 1 ciclo por pulso, más suave que el tramo 2 | Pulsaciones más discretas, conviviendo con el giro |

**Mouse:** movimientos circulares lentos y amplios (un círculo completo cada ~8 segundos) — esto alimenta visualmente el vórtice.

**Qué deberías ver:** el sistema gira suavemente Y sigue respirando un poco, sin que ninguna de las dos cosas domine.

---

## TRAMO 4 · 1:50 – 2:15 (25 segundos) · "División en dos extremos"

| Cuándo | Acción | Duración |
|---|---|---|
| Seg 0 (1:50) | Pulsa `V` para apagar el vórtice | instantáneo |
| Seg 0 | Mueve el mouse a una **esquina** de la pantalla (ej. arriba-izquierda) | — |
| Seg 1 | **Mantén presionada la barra `Espacio`** | sostenida por ~23 segundos |
| Mientras mantienes `Espacio` | Arrastra el mouse **lentamente, en diagonal, hacia la esquina opuesta** (abajo-derecha) | durante los 23 segundos que dura el tramo |
| Seg 24 | Suelta `Espacio` | — |

**Por qué esto crea "dos extremos":** al mantener `Espacio`, `radialStrength` se invierte a negativo (repulsión) — las partículas huyen del punto blanco (el atractor) en vez de acercarse. Como ese punto blanco sigue tu mouse, y tú lo estás arrastrando de una esquina a la otra, el "centro de fuga" se mueve por toda la pantalla, empujando el enjambre de un lado hacia el otro — el efecto visual de "partirse hacia extremos".

**Qué deberías ver:** el enjambre, antes compacto, se dispersa violentamente y parece huir del punto blanco mientras este cruza la pantalla.

---

## TRAMO 5 · 2:15 – 2:40 (25 segundos) · "Transición hacia el colapso" *(mi suposición — ajústala si querías otra cosa)*

| Cuándo | Tecla | Cuántas veces | Efecto |
|---|---|---|---|
| Seg 0 (justo al soltar Espacio) | Mueve el mouse de vuelta hacia el **centro**, despacio | durante todo el tramo | El atractor vuelve al centro, las partículas empiezan a converger otra vez |
| Seg 0–20 | `↑` | 1 vez cada 2 segundos (10 veces) | Sube `radialStrength` de ~1.0 a ~2.0, atracción regresando |
| Seg 0–20 | `→` | 1 vez cada 2.5 segundos (8 veces) | Sube `vortexStrength` de 0 a ~0.8, empieza a insinuarse el giro |

**Mouse:** movimiento lento y directo desde la esquina donde quedó, hacia el centro exacto de la pantalla.

**Qué deberías ver:** las dos nubes dispersas empiezan a ceder y converger de nuevo hacia el centro, ahora con un leve giro apareciendo.

---

## TRAMO 6 · 2:40 – 4:42 (≈122 segundos) · "Agujero negro girando y encogiéndose"

Esta es la parte más larga — hazlo en cámara lenta, muy gradual.

### Fase A: 2:40 a 4:20 (100 segundos) — crecimiento del colapso

| Tecla | Ritmo | Total de toques | Resultado al final de esta fase |
|---|---|---|---|
| `↑` | 1 toque cada 3 segundos | ~33 toques | `radialStrength` sube de ~2.0 a ~5.3 |
| `→` | 1 toque cada 3 segundos (alternando con el anterior) | ~33 toques | `vortexStrength` sube de ~0.8 a ~4.1 |

**Truco práctico:** alterna un toque de `↑` y uno de `→` cada 3 segundos (↑, espera 1.5s, →, espera 1.5s, ↑...). Así subes ambos parámetros parejo sin tener que contar dos ritmos distintos.

**Mouse:** fijo en el centro exacto de la pantalla, o haciendo un círculo diminuto (radio de 1-2 cm en pantalla) para que el giro se vea vivo pero estable, no errático.

### Fase B: 4:20 a 4:42 (22 segundos) — el cierre final

| Tecla | Ritmo | Total de toques | Resultado |
|---|---|---|---|
| `Z` | 1 toque cada 2 segundos | ~10 toques | `particleSize` baja de ~0.035 a ~0.015 — el "diámetro" visual se encoge |
| `E` | 1 toque cada 1.2 segundos | ~18 toques | `dragCoefficient` sube de 0.12 a ~0.3 — frena el sistema para que no explote, dando sensación de contracción controlada |

**Mouse:** completamente quieto en el centro, sin moverlo en absoluto durante estos últimos 22 segundos.

**Qué deberías ver:** un remolino denso, girando rápido, que se va comprimiendo visualmente hasta el final de la canción.

---

## Sobre las "pruebas de comportamiento" (botones 1-5 / teclas Digit1-5)

**No las uses durante la interpretación en vivo.** Cada una llama a `simulation.reset()`, que **teletransporta todas las partículas a posiciones aleatorias nuevas** — se ve como un corte brusco, no una transición.

Úsalas solo para:
- **Ensayar y entender** cada fuerza por separado antes del día de la presentación (eso es literalmente lo que pide la Actividad 02 del laboratorio).
- Como referencia de "a qué valores se ve bien" cada fuerza (ej. preset 5 te muestra cómo se ve `radialStrength=1.0` + `vortexStrength=3.0` juntos).

Si en algún momento decides que SÍ quieres un corte brusco a propósito (por ejemplo, un "reinicio" dramático justo antes del agujero negro), ahí sí podrías usar una tecla numérica como un efecto deliberado — pero eso ya sería una decisión tuya de diseño, no un accidente.

---

## Resumen de todo el mapa de teclas que vas a usar

| Tecla | Qué hace |
|---|---|
| `↑` `↓` | `radialStrength` (atracción/repulsión) |
| `←` `→` | `vortexStrength` (giro) |
| `A` `D` | `wind.y` |
| `W` | enciende/apaga viento |
| `V` | enciende/apaga vórtice |
| `Q` `E` | `dragCoefficient` (fricción) |
| `Z` `X` | `particleSize` |
| `Espacio` (mantener) | invierte atracción ↔ repulsión mientras la mantienes |
| Mouse | mueve el punto de atracción/repulsión por la pantalla |

## Recomendación final

Practícalo al menos 2-3 veces completo con la canción antes de la sustentación. Los tiempos exactos (cada 3 segundos, etc.) son una guía — en la práctica vas a ajustar por oído, no contando segundos con un cronómetro en la mano. Lo importante es la dirección del cambio (subir, bajar, cuándo) y la sensación, no el segundo exacto.

[Volver a la bitacora principal](../README.md)

