# El transformer por dentro

*La arquitectura detrás de casi todos los modelos de lenguaje, contada como un mecanismo — sin
una sola ecuación.*

## Piezas, no letras

Lo primero que hace el modelo con tu texto es picarlo en **tokens**: pedazos que a veces son
palabras enteras, a veces sílabas, a veces un espacio con letra incluida. "Interpretabilidad"
pueden ser tres tokens; "de" es uno. El modelo nunca ve letras — ve una secuencia de estas
piezas, y todo lo que sigue opera sobre ellas.

## Cada token es un punto en un mapa

Cada token se convierte en una **lista de miles de números** (un *vector*, si querés el nombre
técnico — pero pensalo como coordenadas). La imagen clave de todo este curso: cada estado
interno del modelo es **un punto en un mapa gigante** de miles de dimensiones. Significados
parecidos, puntos cercanos. Direcciones del mapa que significan cosas. Todo lo que viene
después — features, flechas, intervenciones — pasa en este mapa.

## El protagonista: el residual stream

Acá va el concepto más importante y menos famoso de la arquitectura. Dentro del modelo, cada
token tiene una especie de **documento compartido** que lo acompaña de principio a fin: el
**residual stream** (corriente residual). Arranca conteniendo poco más que "soy el token
'Italia'" y va acumulando información a medida que atraviesa las capas.

El modelo es una **pila de pisos** (las capas — decenas de ellas), y cada piso hace lo mismo:
**lee** el documento compartido, calcula algo, y **suma** su aporte al documento. No lo
reemplaza: lo *suma*. Por eso el estado en cualquier punto es, literalmente, la suma de todo lo
que los pisos anteriores fueron aportando.

Si vas a quedarte con una sola idea de esta página, que sea esta: **el residual stream es la
memoria de trabajo del modelo, y todos los pisos se comunican a través de él**. Cuando en la
página de [intervenciones](intervenciones.md) editemos "el pensamiento" del modelo, lo que
vamos a editar es esto.

## Los dos tipos de obrero

Cada piso tiene dos mecanismos, con trabajos muy distintos:

**La atención** mueve información **entre posiciones**. Cuando el modelo procesa el token final
de *"la capital de Italia es"*, la atención es lo que le permite ir a buscar "Italia" unas
posiciones atrás y traer esa información al documento del token actual. Sin atención, cada
token pensaría solo. Cada piso tiene varias "cabezas" de atención trabajando en paralelo, y —
esto se vuelve importante en la página de [circuitos](circuitos.md) — cabezas individuales
aprenden trabajos individuales reconocibles.

**El MLP** (una mini-red dentro de cada piso) trabaja **dentro de cada posición**: lee el
documento del token y le suma cosas nuevas. La evidencia sugiere que gran parte del
*conocimiento* del modelo — hechos, asociaciones, "la capital de Italia es Roma" — vive en
estos bloques, que funcionan como una especie de archivo consultable.

## El pensamiento se construye por pisos

Como cada piso suma su aporte, el "pensamiento" del modelo no aparece de golpe: **se
construye incrementalmente**. En los pisos bajos hay cosas básicas (qué palabra es, sintaxis);
en los pisos medios se arma la semántica de la tarea; los pisos altos preparan la respuesta
concreta. Hay un truco encantador llamado **logit lens**: en lugar de esperar al final, se
puede "espiar" en cada piso qué palabra diría el modelo si tuviera que responder ya — y ver
cómo la respuesta va tomando forma piso a piso.

Esto importa porque las preguntas de interpretabilidad casi siempre tienen la forma: **¿en qué
capa, en qué posición, vive tal información?** — y la respuesta suele ser "en un piso
sorprendentemente específico". (En [mi propio paper](../mi-investigacion.md), por ejemplo, la
estructura que estudiamos se *representa* temprano pero recién tiene *palanca causal* cerca del
final — el mismo objeto, distinto rol según el piso.)

## Jugá con uno de verdad

La mejor manera de fijar todo esto es verlo en movimiento:

<iframe src="https://poloclub.github.io/transformer-explainer/"
        title="Transformer Explainer (Georgia Tech)"
        style="width:100%;height:640px;border:1px solid #8884;border-radius:0.6rem"
        loading="lazy"></iframe>
*GPT-2 corriendo en tu navegador, con cada pieza de la arquitectura abierta e inspeccionable
(Georgia Tech / Polo Club — en inglés). Si el marco no carga,
[abrilo directo](https://poloclub.github.io/transformer-explainer/).*

Y si querés la versión 3D espectacular: [**LLM Visualization** de Brendan Bycroft](https://bbycroft.net/llm) —
un modelo completo dibujado como una máquina que podés recorrer.

!!! note "Honestidad técnica"
    Este dibujo está simplificado a propósito: no hablamos de normalizaciones, posiciones,
    varias variantes arquitecturales, ni del entrenamiento. Nada de eso cambia la imagen
    mental: un mapa de puntos, un documento compartido que se va sumando, atención que mueve
    información entre tokens y MLPs que consultan el archivo.

## Para profundizar

- [La serie de redes neuronales de 3Blue1Brown](https://www.3blue1brown.com/topics/neural-networks) —
  los capítulos 5 a 8 cubren GPT y atención con las mejores visualizaciones que existen. Los
  primeros capítulos están [doblados al español en el canal oficial](https://www.youtube.com/@3blue1brownespanol);
  los de transformers, en inglés con subtítulos.
- [A Mathematical Framework for Transformer Circuits](https://transformer-circuits.pub/2021/framework/index.html) —
  el paper que formalizó el residual stream como objeto central del campo (avanzado).
- [A Primer on the Inner Workings of Transformer-based Language Models](https://arxiv.org/abs/2405.00208) —
  survey técnico de entrada, primer autor hispanohablante (Ferrando, UPC Barcelona).

**Siguiente:** ¿y qué *hay* en ese mapa de miles de dimensiones?
[Features y superposición →](features.md)
