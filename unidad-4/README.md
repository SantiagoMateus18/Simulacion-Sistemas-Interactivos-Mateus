# Unidad 4: Oscilacion

Bitacora de trabajo de la Unidad 4 del curso de Simulacion.

# Bitácora de Desarrollo: "Resonancia en el Cementerio" (Unidad 4 - Oscilaciones)

**Creador:** Santiago Mateus  
**LINK:** [Al archivo P5.js](https://editor.p5js.org/SantiagoMateus18/sketches/EFZTj-3TJ)

**Proyecto:** Sistema Audiovisual Sonificado y Performativo  
**Modelo:** Sincronización de Fase de Kuramoto + Eventos Estocásticos (Rayos)

---

## 01. La Idea Central y el Concepto

La pregunta que me persiguió durante todo el proceso no fue cómo programar el algoritmo, sino esto:

> *¿Cómo lograr que la ecuación de Kuramoto no sea solo un gráfico que se mira, sino un ambiente sonoro fúnebre y ritual donde la física se combine con el azar del clima?*

Decidí alejarme de las interfaces de laboratorio tradicionales y construir un cementerio interactivo. En este sistema, **siete lápidas** actúan como osciladores independientes. Cada una lleva asignada una de las 7 notas musicales de la escala diatónica y genera un pulso audiovisual al completar su ciclo de fase. 

Para romper con la rutina de una simulación pura, introduje un elemento estocástico: **rayos atmosféricos** que caen cada ciertos segundos, alterando el acoplamiento global $K$ de forma aleatoria e impredecible.

---

## 02. Tropiezos, Rediseño y Golpes de Realidad

### El prototipo inicial (Y por qué lo descarté)
Empecé probando el modelo base de Kuramoto con esferas abstractas y tonos puros generados por código. Técnicamente funcionaba, pero **era frío y aburrido**. Los sonidos sonaban demasiado sintéticos y no había una narrativa clara que justificara por qué unos nodos se sincronizaban con otros.

[Volver a la bitacora principal](../README.md)
