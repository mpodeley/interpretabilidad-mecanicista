# Qué es la interpretabilidad mecanicista (y por qué importa)

*Primera parada del curso. Sin matemática, sin jerga — pero sin mentir.*

## Nadie escribió a ChatGPT

Los programas normales se **escriben**: una persona tipea reglas — "si pasa esto, hacé
aquello" — y el programa hace exactamente lo que dicen las reglas. Los modelos de lenguaje no
funcionan así. Un modelo como Claude, GPT o Gemini no se escribe: se **cultiva**. Se le muestra
una cantidad astronómica de texto y un proceso automático va ajustando miles de millones de
numeritos internos hasta que el sistema se vuelve bueno prediciendo la palabra siguiente.

El resultado es rarísimo: tenemos máquinas que traducen, programan, razonan y explican chistes,
y **nadie — ni la empresa que las hizo — sabe exactamente cómo lo hacen por dentro**. No hay
reglas para leer. Hay miles de millones de números ajustados, y de ellos *emerge* el
comportamiento. A eso se refiere la gente cuando dice que los modelos son una **caja negra**.

## El microscopio

La interpretabilidad mecanicista es el intento de abrir esa caja: hacer **ingeniería inversa**
de la red entrenada hasta entender *qué representa* y *qué algoritmos ejecuta* por dentro. La
analogía que más se usa es la **neurociencia** — estudiar un "cerebro" que nadie diseñó — pero
con tres ventajas que ningún neurocientífico tiene:

1. **Vemos todo.** Cada "neurona", cada conexión, cada estado intermedio, con precisión
   perfecta y sin abrir ningún cráneo.
2. **Podemos repetir.** El mismo pensamiento, mil veces, idéntico, cambiando una sola cosa
   por vez.
3. **Podemos intervenir.** Pausar el modelo a mitad de un pensamiento, editarle el estado
   interno, y ver qué cambia en lo que dice. Esta es la superpoder del campo, y le dedicamos
   [una página entera](intervenciones.md).

Lo de "mecanicista" no es decoración: la meta no es una intuición vaga tipo "el modelo prestó
atención a tal palabra", sino encontrar los **mecanismos** — piezas concretas haciendo trabajos
concretos que expliquen el comportamiento y sobrevivan a experimentos que intenten romperlos.

## El puente Golden Gate

El ejemplo más famoso de que esto funciona: en 2024, investigadores de Anthropic encontraron
dentro de Claude un patrón de actividad — un *feature* — que se prendía exactamente cuando el
tema era el puente Golden Gate de San Francisco. Después hicieron lo importante: **le subieron
el volumen**. El resultado fue [Golden Gate Claude](https://www.anthropic.com/news/golden-gate-claude),
un modelo obsesionado que metía el puente en cualquier conversación — le preguntabas cómo
gastar 10 dólares y te recomendaba pagar el peaje para cruzarlo.

Parece un chiste, pero es una demostración profunda: **encontraron una pieza del pensamiento,
la manipularon, y el comportamiento cambió como predijeron**. Eso es entender un mecanismo — no
mirar de afuera y adivinar.

## Por qué importa

- **Seguridad.** Los modelos se usan para decidir cosas cada vez más serias. Si no sabemos cómo
  deciden, no podemos anticipar cuándo van a fallar, mentir o ser manipulados. Entender el
  mecanismo es el camino para auditar de verdad, no solo testear de afuera.
- **Confianza calibrada.** No se trata de confiar más en la IA, sino de confiar *con
  fundamento* — y desconfiar con fundamento también.
- **Ciencia básica.** Es la primera vez en la historia que existe un sistema que produce
  lenguaje inteligente y se deja estudiar átomo por átomo. Lo que se descubra ahí adentro puede
  enseñarnos algo sobre el lenguaje y la computación en general.
- **Es un campo joven y accesible.** Los resultados centrales tienen menos de una década, hay
  problemas abiertos para regalar, y una laptop con GPU chica (o Colab gratis) alcanza para
  hacer experimentos reales. Es una de las pocas fronteras de la IA donde una persona
  independiente puede contribuir — este sitio es, en parte, la prueba.

## Qué NO es

No es lo mismo que la "explicabilidad" clásica (XAI), que suele producir mapas de calor de
"a qué le prestó atención el modelo" — descripciones correlacionales, de afuera. La
interpretabilidad mecanicista exige más: que la explicación identifique **piezas internas** y
sobreviva a la prueba de fuego de **intervenir** sobre ellas. Y tampoco promete milagros: hoy
entendemos fragmentos — features sueltos, circuitos chicos, resultados parciales en modelos
medianos — no "el pensamiento de la IA" completo. Este curso te cuenta exactamente qué se sabe
y qué no.

<div style="position:relative;padding-bottom:56.25%;height:0;overflow:hidden;border-radius:0.6rem;margin:1rem 0">
<iframe style="position:absolute;top:0;left:0;width:100%;height:100%;border:0"
src="https://www.youtube-nocookie.com/embed/fGKNUvivvnc"
title="Interpretability: Understanding how AI models think (Anthropic)"
allowfullscreen loading="lazy"></iframe>
</div>
*El equipo de interpretabilidad de Anthropic conversa sobre el estado del campo (en inglés,
subtítulos disponibles).*

## Para profundizar

- [Tracing the thoughts of a large language model](https://www.anthropic.com/research/tracing-thoughts-language-model) —
  el explicador accesible de Anthropic sobre su "microscopio" (inglés, sin matemática).
- [The moment we stopped understanding AI (Welch Labs)](https://www.youtube.com/watch?v=UZDiGooFs54) —
  la mejor puerta de entrada emocional al "por qué" de todo esto.
- [Golden Gate Claude](https://www.anthropic.com/news/golden-gate-claude) — el anuncio original.
- En español: [la definición de MIT Technology Review](https://technologyreview.es/article/interpretabilidad-mecanicista).

**Siguiente:** para entender los mecanismos, primero hay que conocer la máquina.
[El transformer por dentro →](transformer.md)
