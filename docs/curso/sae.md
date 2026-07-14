# SAEs y grafos de atribución

*Última parada: cómo se desenreda la superposición sin saber qué buscar, y los mapas de
pensamiento más ambiciosos dibujados hasta ahora.*

## El problema pendiente

En [features](features.md) quedó una deuda: si los conceptos viven **superpuestos** — millones
de flechas apretadas en miles de dimensiones, desalineadas de las neuronas — ¿cómo recuperás la
lista de conceptos activos en un momento dado? Peor: ¿cómo lo hacés **sin decirle al método qué
conceptos buscar**? Porque el punto es descubrir el vocabulario interno del modelo, no
confirmar el nuestro.

## Sparse autoencoders: el diccionario aprendido

La respuesta que definió los últimos años del campo es el **sparse autoencoder** (SAE,
autoencoder ralo). La idea, sin matemática:

Entrenás una red auxiliar chiquita con una sola consigna: *"reescribí el estado interno del
modelo como una suma de MUY POCAS entradas de un diccionario MUY GRANDE — y que la suma
reconstruya el estado original"*. El diccionario puede tener millones de entradas; la
restricción es que para cada pensamiento concreto se usen apenas un puñado.

Esa presión — diccionario enorme, uso ralo — es exactamente la inversa de la superposición, y
la deshace: las entradas del diccionario que emergen resultan ser, en una fracción enorme de
los casos, **monosemánticas** — cada una significa *una* cosa, verificable mirando qué textos
la activan. Features de "inseguridad en el código", de "adulación", de "puentes famosos"…
El [Golden Gate](que-es.md) se encontró así: era una entrada del diccionario de un SAE
entrenado sobre Claude ([Scaling Monosemanticity](https://transformer-circuits.pub/2024/scaling-monosemanticity/index.html),
2024).

Y no hace falta creerme: DeepMind publicó [**Gemma Scope**](https://www.neuronpedia.org/gemma-scope),
SAEs abiertos sobre sus modelos Gemma, con una demo interactiva en Neuronpedia donde podés
escribir texto y **ver qué features se prenden**, en vivo.

## De features a historias: attribution graphs

Los SAEs te dan el *vocabulario*. El paso siguiente es la *gramática*: ¿cómo se conectan esos
features entre sí para producir la respuesta? Los **grafos de atribución** (attribution graphs,
Anthropic 2025) automatizan justamente eso: para un prompt concreto, construyen el **grafo de
qué features activaron qué otros features**, capa a capa, hasta la respuesta — un
[circuito](circuitos.md) descubierto por algoritmo en lugar de por meses de trabajo manual.

El resultado insignia es [*On the Biology of a Large Language Model*](https://transformer-circuits.pub/2025/attribution-graphs/biology.html):
grafos trazados sobre un modelo de producción (Claude 3.5 Haiku) que muestran, entre otras
cosas, que el modelo **planifica rimas con versos de anticipación** cuando escribe poesía, que
suma con una mezcla de aproximación y tablas memorizadas, y que a veces su explicación verbal
de "cómo lo resolvió" **no coincide** con lo que el grafo muestra que hizo. Las herramientas
son [código abierto](https://github.com/safety-research/circuit-tracer) y hay
[grafos navegables en Neuronpedia](https://www.neuronpedia.org/graph).

!!! note "Honestidad técnica"
    Los SAEs tienen límites serios y activamente debatidos: la reconstrucción no es perfecta
    (algo del pensamiento queda afuera del diccionario), hay features que se parten o se
    fusionan según el tamaño del diccionario, y hay
    [evidencia mixta](https://arxiv.org/abs/2502.16681) sobre si ayudan en tareas prácticas
    más que métodos simples. Los grafos de atribución heredan estos límites y agregan los
    suyos (explican una fracción de los prompts intentados). Es la frontera — precisamente por
    eso hay [tanto para investigar](../lineas.md).

## El curso, en una pantalla

Terminaste el núcleo. El mapa completo:

| Pregunta | Respuesta del campo | Página |
|---|---|---|
| ¿Por qué hace falta esto? | Los modelos se cultivan, no se escriben — nadie sabe cómo deciden | [Qué es](que-es.md) |
| ¿Cómo es la máquina? | Un mapa de puntos + un documento compartido (residual stream) que las capas suman | [El transformer](transformer.md) |
| ¿En qué "idioma" piensa? | Features = direcciones; superpuestas porque no hay lugar | [Features](features.md) |
| ¿Cómo se prueba algo? | Interviniendo: patching, ablación, steering — más los controles que intentan matar tu efecto | [Intervenciones](intervenciones.md) |
| ¿Hay algoritmos legibles? | Sí: induction heads, IOI — carísimos de encontrar a mano | [Circuitos](circuitos.md) |
| ¿Cómo escala? | SAEs para el vocabulario, grafos de atribución para las historias | esta página |

**¿Y ahora?** Tres caminos: los [recursos curados](../recursos.md) para seguir aprendiendo (en
serio: hay un camino concreto ahí), las [líneas de investigación abiertas](../lineas.md) si te
pica hacer, y [mi investigación](../mi-investigacion.md) como ejemplo de que se puede entrar al
campo desde afuera.

## Para profundizar

- [Towards Monosemanticity](https://transformer-circuits.pub/2023/monosemantic-features/index.html) —
  el primer SAE que funcionó de verdad, y una lectura hermosa.
- [Scaling Monosemanticity](https://transformer-circuits.pub/2024/scaling-monosemanticity/index.html) —
  lo mismo a escala Claude 3, el paper del Golden Gate.
- [Gemma Scope en Neuronpedia](https://www.neuronpedia.org/gemma-scope) — para tocar features
  con las manos.
- [On the Biology of a Large Language Model](https://transformer-circuits.pub/2025/attribution-graphs/biology.html) —
  el estado del arte, con visualizaciones extraordinarias.
