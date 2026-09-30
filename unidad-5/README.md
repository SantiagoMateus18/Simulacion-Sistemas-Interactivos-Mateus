## Unidad 5: Sistemas de partículas

**Proyecto:** presentación generativa para la charla “Relevo generacional: la ventaja que nadie está aprovechando”.  
**Cliente:** Centro de Eventos Fórum UPB.  
**Estado de esta entrada:** lectura y documentación de la versión presente en el workspace.

> Esta bitácora parte de lo que el proyecto ya permite observar. Las notas sobre decisiones describen la propuesta implementada; los espacios de reflexión quedan abiertos para registrar pruebas y aprendizajes personales a medida que avance el trabajo.

## Punto de partida

El encargo pide interpretar el guion suministrado sin alterar su secuencia y construir una presentación web para pantalla grande. El reto no consiste en añadir partículas como decoración, sino en dar significado a sus relaciones, movimientos y transformaciones.

La propuesta se titula **Potencial** y su idea central es que el potencial aparece en las conexiones: la experiencia y las nuevas generaciones no se presentan como fuerzas que se reemplazan, sino como grupos que pueden encontrarse y construir algo en común. La frase que resume el sistema es: **“El potencial está en las conexiones”**.

## Referentes y preguntas

- [Memo Akten, *Forms*](https://memo.tv/projects/2011/forms/): sirve como referencia conceptual para pensar cómo un movimiento puede extenderse y convertirse en estructura. La propuesta no busca copiar su estética.
- [ForumTEDTALK](https://github.com/juanferfranco/ForumTEDTALK) y [la presentación de referencia](https://juanferfranco.github.io/ForumTEDTALK/): ayudan a pensar cómo un discurso puede traducirse en comportamiento visual sin ilustrar literalmente cada frase.
- [Insumos del cliente](https://drive.google.com/drive/folders/1DoaP6OaAYheK7p3QUW_QAkjCA0l2aVBO?usp=sharing): base narrativa y documental del encargo.

Preguntas para observar los referentes: ¿qué relación sostiene la estructura?, ¿qué cambia a lo largo del discurso?, ¿cómo produce sentido ese cambio?

## Gramática visual

El campo está formado por **2.400 puntos persistentes**. Cada punto conserva su identidad mientras cambia de posición, tamaño y color para acercarse al objetivo que define cada escena. Así, las transiciones se leen como reorganizaciones del mismo sistema y no como una sucesión de imágenes independientes.

- **Relación:** los puntos se agrupan en masas, forman vínculos, se separan o convergen. La distancia entre grupos expresa encuentro, tensión o integración.
- **Movimiento:** las expansiones, impulsos y oscilaciones hacen visibles cambios en la organización. En las escenas de confianza, por ejemplo, un impulso acotado se propaga entre grupos con cierto retraso; en las escenas siguientes, las masas oscilan y cambian de escala.
- **Color:** azul, verde y amarillo distinguen grupos y momentos. En la escena de los tres sistemas, los colores corresponden visualmente a Academia, Industria y Ciudad. Más adelante, el contraste azul-verde ayuda a mantener diferenciadas las dos generaciones antes de su integración.
- **Forma:** el diamante funciona como forma común de inicio y cierre. Durante el relato se fragmenta en grupos, cuerpos y trayectorias, y al final vuelve a consolidarse.
- **Ritmo:** algunas configuraciones permanecen; otras siguen ciclos limitados. El cambio se reserva para acompañar una transformación del relato, no para mantener movimiento constante sin intención.

## Recorrido del discurso

La secuencia conserva los 13 momentos del guion. Esta lectura vincula cada texto con el comportamiento visible del sistema:

1. **Potencial oculto:** un diamante oscuro y compacto establece la forma inicial; algunos puntos claros anticipan lo que aún no se revela.
2. **“¿Un gran auditorio solo para hacer grados?”:** la forma se expande y deja aparecer un grupo de puntos claros; la pregunta abre el campo de posibilidades.
3. **La Universidad se encuentra con el mundo:** el diamante contiene grupos circulares y una separación que empieza a cerrarse.
4. **Academia + Industria + Ciudad:** tres diamantes de color organizan los tres sistemas nombrados en el guion.
5. **El impacto sí:** los tres grupos se aproximan y luego sus puntos se dispersan en trayectorias compartidas; el énfasis pasa del evento al efecto que produce.
6. **Una comunidad trae transformación:** pequeños grupos se distribuyen alrededor de una organización común y algunos puntos establecen vínculos entre ellos.
7. **El talento crece con confianza:** cuatro masas reciben impulsos sucesivos y acotados; el movimiento se propaga sin deshacer la estructura.
8. **Experiencia y nuevas rutas:** las masas oscilan en ciclos contenidos, diferenciando estabilidad y exploración.
9. **Una visión. Dos generaciones:** dos grupos de color se aproximan sin perder del todo su identidad.
10. **Trabajar juntas:** los grupos convergen hacia un centro compartido; el color cambia hacia el amarillo durante la integración.
11. **Los jóvenes son el presente:** desde la forma común, los puntos se distribuyen en unidades menores; la energía compartida se proyecta hacia nuevas posiciones.
12. **El futuro se construye:** esas unidades vuelven gradualmente a formar una estructura colectiva.
13. **Futuro consolidado:** el sistema recupera el diamante y reserva un espacio para el QR final.

Las seis fotografías locales acompañan algunos momentos como contexto documental. Se mantienen detrás del campo generativo para que el movimiento siga siendo parte de la estructura principal.

## Decisiones de implementación

- La presentación funciona localmente desde `index.html`, sin instalar dependencias ni necesitar conexión.
- El mismo conjunto de puntos se transforma entre escenas; las posiciones objetivo se calculan según la escena y el tiempo transcurrido.
- Las transiciones suavizan posición, tamaño y color, mientras que las escenas cíclicas usan movimientos acotados.
- La interfaz incluye avance y retroceso, indicador de progreso, modo de pantalla completa y ayuda por teclado. En pantallas pequeñas, la composición reubica el texto y el campo visual.
- El cierre reserva el espacio del QR, pero todavía es un contenedor vacío: falta insertar y probar el código definitivo.

## Registro de proceso

Esta primera entrada documenta el estado disponible, no reconstruye experimentos anteriores que no estén registrados. Para las siguientes versiones, anotar aquí qué se probó, qué cambió y por qué:

| Fecha / versión | Prueba o decisión | Evidencia | Aprendizaje / siguiente paso |
| --- | --- | --- | --- |
| Estado actual | Registro inicial construido a partir de la secuencia, los comportamientos de partículas y los controles presentes en el proyecto. | `app.js`, `index.html`, `styles.css` y las seis imágenes de `assets/`. | Probar la presentación en la pantalla de exposición y completar el QR. |
| Por completar |  |  |  |

## Reflexión personal

Completar después de probar la presentación en contexto:

- ¿Qué escena comunica con mayor claridad una relación entre generaciones? ¿Qué comportamiento lo logra?
- ¿Qué cambio visual resulta difícil de explicar o parece decorativo? ¿Cómo podría ajustarse?
- ¿Se entiende el recorrido del diamante, desde la forma inicial hasta la construcción colectiva, sin explicación verbal adicional?
- ¿Qué cambió al probar la presentación en pantalla completa y a distancia?
- ¿Qué decisión modificaría y qué evidencia motivaría ese cambio?

## Autoevaluación del proyecto

Cada criterio vale 25 puntos. Dejo el puntaje pendiente para completarlo después de la demostración, con evidencia de la versión final.

| Criterio | Puntaje / 25 | Evidencia que debo comprobar |
| --- | ---: | --- |
| Cumplimiento del encargo: interpreta el guion y funciona en pantalla completa. | 25 | Recorrer los 13 momentos y probar pantalla completa en el equipo de presentación. |
| Relaciones estructurales: puedo explicar qué relaciones organizan los elementos y qué significan. | 20 | Explicar la separación, propagación, aproximación e integración de los grupos. |
| Comportamiento y significado: relaciono los cambios de movimiento y composición con una intención comunicativa. | 25 | Justificar al menos una transformación concreta de la secuencia. |
| Explicación y demostración: presento la propuesta y puedo mostrar cómo construye sentido. | 25 | Ensayar el recorrido y la explicación del sistema funcionando. |

**Pregunta que guía la unidad:** ¿Cómo puede una estructura de elementos relacionados y en movimiento convertirse en un lenguaje visual capaz de construir el significado de un discurso?

[Volver a la bitacora principal](../README.md)
