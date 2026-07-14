---
date: 2026-07-14
slug: por-que-existe-este-sitio
categories:
  - Meta
---

# Por qué existe este sitio

Hace unos meses no sabía qué era un residual stream. La semana pasada envié mi primer paper de
interpretabilidad mecanicista a un workshop de EMNLP. Este sitio existe porque en el medio de
esas dos oraciones hay un camino que casi nadie documenta — y menos en español.

<!-- more -->

## El recorrido

Empecé como empieza casi todo el mundo en este campo: **intentando replicar el resultado de
otro**. Un paper afirmaba que cierta estructura era legible en el estado interno de un modelo;
armé el experimento, agregué los controles que me parecieron obvios (¿qué pasa con etiquetas
permutadas? ¿con direcciones aleatorias del mismo tamaño?)… y el resultado original **no
sobrevivió**. La réplica falló.

Eso pudo ser el final — un rato de aprendizaje y a otra cosa. Pero la pregunta buena apareció
justo ahí: si esta estructura no es real, ¿qué estructura *sí* sobrevive a todos los controles?
Meses de experimentos después, la respuesta era publicable: el estado interno de un modelo
pensando "la capital de Italia" **factoriza en piezas** — la cosa y la operación — que se pueden
extraer, recombinar y volver a escribir adentro del modelo, que entonces *dice la respuesta*.
El resultado, con sus 3 modelos, sus controles y sus dominios-donde-no-funciona, es
[el paper](../../mi-investigacion.md), y tiene
[un sitio interactivo](https://mpodeley.github.io/assembled-thought/) donde podés jugar con los
experimentos reales.

## Lo que aprendí que este sitio intenta transmitir

1. **El campo es entrable.** Todo lo que usé es público: modelos abiertos, una GPU modesta,
   papers gratis, librerías open source. La barrera real es el mapa — saber qué leer, en qué
   orden, y qué es señal versus ruido. Ese mapa es [el curso](../../curso/que-es.md) y
   [los recursos](../../recursos.md).
2. **Los controles son el producto.** La diferencia entre una anécdota y un resultado no está
   en el efecto — está en los experimentos diseñados para matarlo. Mi réplica fallida fue más
   valiosa que varios "éxitos" que tuve después, y le dedico
   [una sección entera del curso](../../curso/intervenciones.md).
3. **En español no había nada.** Cuando busqué material de interpretabilidad mecanicista en mi
   idioma encontré: una definición de diccionario y cobertura de diario. Para un campo que
   se declara cuello de botella de talento, eso es un desperdicio — hay demasiada gente que
   piensa en español como para que el material esté solo en inglés.

## Qué va a haber acá

- **Réplicas comentadas** de resultados del campo (con controles — siempre con controles).
- **Avances de mi propia agenda**: el siguiente paso es usar
  [circuit-tracer](https://github.com/safety-research/circuit-tracer) para encontrar qué
  cabezas y MLPs implementan la recombinación de piezas que mi paper demuestra por fuera.
- **Lecturas comentadas** de papers nuevos, cuando aporten algo al mapa.
- Y lo que el camino traiga. Podés seguirlo por
  [RSS](https://mpodeley.github.io/interpretabilidad-mecanicista/feed_rss_created.xml).

Si estás arrancando: [el curso empieza acá](../../curso/que-es.md). Si algo no se entiende,
[escribime](mailto:mpodeley@gmail.com) — que no se entienda es un bug de este sitio, no tuyo.
