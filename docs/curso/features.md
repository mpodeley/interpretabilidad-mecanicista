# Features, direcciones y superposición

*¿En qué "idioma" interno piensa el modelo? La respuesta corta: en flechas. La complicación:
están todas apretadas.*

## Qué es un feature

Un **feature** es una propiedad que el modelo representa internamente: *"esto está en
francés"*, *"esto es código Python"*, *"acá hay sarcasmo"*, *"se está hablando del puente
Golden Gate"*, *"este número es par"*. Son los **conceptos-átomo** del pensamiento del modelo —
lo que el modelo "anota" en su memoria de trabajo mientras lee.

La pregunta del millón: ¿cómo se escribe un feature en el
[mapa de miles de dimensiones](transformer.md) que ya conocés?

## La hipótesis de la representación lineal

La respuesta que domina el campo es sorprendentemente simple: **cada feature es una dirección
del mapa** — una flecha. Que un pensamiento tenga "mucho de francés" significa que su punto
está desplazado en la dirección-francés. Que aparezca el Golden Gate significa desplazamiento
en la dirección-Golden-Gate. El estado del modelo en un momento dado sería entonces una **suma
de flechas**: un poco de esta dirección, mucho de aquella, nada de esa otra.

Esto no es solo una metáfora linda — es una hipótesis que hace predicciones. Si los conceptos
son flechas que se suman, deberías poder *restar* un concepto, *sumar* otro, y obtener
comportamiento coherente. El famoso "rey − hombre + mujer ≈ reina" de los embeddings viejos era
la primera pista; los experimentos modernos de intervención — incluyendo
[los de mi paper](intervenciones.md) — son la versión con dientes.

## El problema: no hay lugar

Ahora, una cuenta incómoda. El mapa tiene miles de dimensiones — o sea, miles de flechas que
podrían apuntar cada una para un lado completamente independiente. Pero las cosas que un modelo
necesita representar — palabras, personas, lugares, estilos, sintaxis, hechos, tonos, tareas —
son **muchísimas más que miles**.

¿Cómo entran millones de conceptos en miles de dimensiones? El resultado teórico clave
([Toy Models of Superposition](https://transformer-circuits.pub/2022/toy_model/index.html),
Anthropic 2022) muestra que las redes hacen trampa de manera sistemática: como casi ningún
concepto aparece al mismo tiempo que casi ningún otro (hoy no estás pensando en el Golden Gate
*y* en recetas de sushi *y* en Beethoven), el modelo puede usar flechas **casi**
perpendiculares — muchísimas más flechas que dimensiones — y tolerar la pequeña interferencia
entre ellas. A esto se le llama **superposición**: los conceptos viven apretados, superpuestos
en el mismo espacio.

## La consecuencia: neuronas polisemánticas

La superposición explica una frustración vieja del campo. Lo natural era esperar que cada
**neurona** (cada coordenada individual del mapa) significara algo: la neurona del francés, la
neurona de los gatos. Pero cuando mirás neuronas reales, la mayoría son **polisemánticas**: la
misma neurona se activa con citas académicas, código en coreano y descripciones de tormentas.
No es que el modelo sea caótico — es que **las flechas con significado no están alineadas con
las neuronas**. La unidad natural del pensamiento del modelo es la dirección, no la neurona, y
las direcciones están inclinadas respecto de los ejes.

Podés verlo con tus propios ojos en [**Neuronpedia**](https://www.neuronpedia.org), un
"atlas" público donde se navegan features reales de modelos reales: cada feature con los textos
que lo activan, su dirección, y hasta la posibilidad de subirle el volumen
([steering](intervenciones.md)) para ver qué hace.

## Lo que esto le hace al campo

Dos consecuencias enormes:

1. **Mirar de a una neurona no alcanza.** Las herramientas tienen que buscar *direcciones* con
   significado, no coordenadas con significado.
2. **Hace falta desenredar.** Si los features viven superpuestos, necesitamos un método que,
   dado el estado del modelo, lo descomponga en su lista de conceptos activos — sin que nadie
   le diga de antemano qué conceptos buscar. Ese método existe, es la estrella de los últimos
   años del campo, y tiene [su propia página al final del curso](sae.md): los *sparse
   autoencoders*.

!!! note "Honestidad técnica"
    La hipótesis lineal es eso: una hipótesis. Funciona notablemente bien en muchísimos casos
    medidos, pero hay evidencia de estructura no-lineal también, y el propio campo discute sus
    límites. Como siempre acá: es la mejor imagen disponible, no un dogma.

## Para profundizar

- [Toy Models of Superposition](https://transformer-circuits.pub/2022/toy_model/index.html) —
  el paper que le puso teoría (y figuras hermosas) a todo esto.
- [Zoom In: An Introduction to Circuits](https://distill.pub/2020/circuits/zoom-in/) — el
  ensayo fundacional de Distill: features y circuitos en redes de visión, donde nació la
  agenda.
- [Neuronpedia](https://www.neuronpedia.org) — el atlas navegable de features.

**Siguiente:** basta de mirar — llegó la hora de tocar.
[Intervenciones causales →](intervenciones.md)
