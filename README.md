# Análisis Bioinstrumental de la Zancada

Aplicación web desarrollada para la asignatura **Análisis Bioinstrumental del Movimiento Humano** de la carrera de Kinesiología.

## Objetivo

Analizar y comparar cuantitativamente dos ejecuciones de una **zancada hacia adelante (forward lunge)** a partir de videos grabados de perfil.

La aplicación utiliza estimación de pose para identificar puntos anatómicos y calcular el ángulo de la rodilla durante el movimiento.

## Variable analizada

La variable principal es el **ángulo interno de flexión de rodilla en grados**.

Para calcularlo se utilizan tres puntos anatómicos:

- Cadera
- Rodilla
- Tobillo

La rodilla corresponde al vértice del ángulo.

En esta medición:

- una rodilla cercana a la extensión presenta un ángulo próximo a 180°;
- al aumentar la flexión, el ángulo disminuye;
- el menor ángulo detectado corresponde al momento de máxima flexión de rodilla.

## Funcionalidades

La aplicación permite:

- Cargar dos videos para compararlos.
- Seleccionar la pierna derecha o izquierda de cada video.
- Reproducir los videos dentro de la página.
- Detectar cadera, rodilla y tobillo mediante estimación de pose.
- Dibujar los puntos anatómicos sobre el video.
- Dibujar las líneas cadera-rodilla y rodilla-tobillo.
- Mostrar el ángulo de rodilla sobre el video.
- Calcular el ángulo durante el movimiento.
- Obtener el ángulo mínimo.
- Obtener el ángulo máximo.
- Calcular el rango angular.
- Identificar el momento de máxima flexión.
- Comparar los resultados de ambos videos.
- Generar un gráfico de ángulo de rodilla versus tiempo.
- Mostrar el momento aproximado de máxima flexión de cada video.

## Tecnologías utilizadas

- HTML
- CSS
- JavaScript
- MediaPipe Pose Landmarker
- Chart.js
- Canvas API

La aplicación funciona directamente en el navegador y no requiere backend.

## Estimación de pose

Se utiliza **MediaPipe Pose Landmarker** para identificar puntos corporales en cada frame del video.

Para la pierna seleccionada se utilizan los landmarks correspondientes a:

### Pierna izquierda

- Cadera: 23
- Rodilla: 25
- Tobillo: 27

### Pierna derecha

- Cadera: 24
- Rodilla: 26
- Tobillo: 28

Si alguno de estos puntos no presenta una detección suficientemente confiable, ese frame se descarta del análisis.

No se utilizan valores inventados para reemplazar frames sin detección.

## Cálculo del ángulo de rodilla

Primero se forman dos vectores utilizando la rodilla como punto de origen:

```text
u = cadera - rodilla
v = tobillo - rodilla
