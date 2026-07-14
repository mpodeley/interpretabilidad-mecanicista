# Intervenciones causales

*El superpoder del campo: no mirar el pensamiento — editarlo. Y la lección de rigor que viene
con el poder.*

## La trampa de mirar

Supongamos que encontrás una dirección del mapa que se activa siempre que el modelo procesa
preguntas sobre capitales. ¿Probaste que esa dirección *hace* el trabajo? **No.** Probaste que
*acompaña* al trabajo. Puede ser un eco, un subproducto, una correlación — como concluir que
los bomberos causan incendios porque siempre están donde hay fuego.

La neurociencia sufre esta trampa hace un siglo: ver que una zona del cerebro "se ilumina" no
dice qué función cumple. Pero acá estudiamos un cerebro artificial, y eso cambia todo: podemos
**pausar el modelo a mitad de un pensamiento, editarle el estado interno con precisión
quirúrgica, y ver qué cambia en lo que dice**. Correlación → causalidad. Estas son las
herramientas:

## Las tres herramientas

**Activation patching (trasplante).** Corré el modelo con la frase A y guardá su estado interno
en cierto piso y posición. Corrélo con la frase B, pero **trasplantándole** ese estado guardado.
Si el modelo ahora responde como si hubiera leído A, acabás de demostrar *dónde vive* la
información que distingue A de B — en qué capa, en qué posición. Es el bisturí del campo: se
usa para localizar información y para descubrir [circuitos](circuitos.md).

**Ablación.** Sacá una pieza — silenciá una cabeza de atención, borrá una dirección — y mirá
qué se rompe. Si tu explicación dice "esta cabeza hace tal trabajo", ablarla tiene que romper
exactamente ese trabajo, y nada más.

**Steering (dirigir).** Sumá una flecha al [residual stream](transformer.md) mientras el modelo
piensa, y el comportamiento se desplaza en la dirección del concepto:
[Golden Gate Claude](https://www.anthropic.com/news/golden-gate-claude) fue exactamente esto.
Es la prueba más contundente de que [las flechas](features.md) no son decoración — son palancas.

## Caso real: desarmar un pensamiento y volverlo a armar

Acá es donde te cuento [mi propio paper](../mi-investigacion.md) — no (solo) por orgullo, sino
porque es un ejemplo de punta a punta de cómo se usan estas herramientas, y porque podés
**jugar con los experimentos reales en tu navegador**.

La pregunta: cuando el modelo piensa *"la capital de Italia"*, ¿ese pensamiento es un bloque, o
son piezas separadas — la cosa (Italia) y la operación (capital-de)?

- **Steering:** mientras el modelo piensa *"la moneda de Italia es…"*, le restamos la flecha
  *moneda-de* y le sumamos la flecha *capital-de*. Su preferencia se invierte: deja de
  inclinarse por "euro" y se inclina por "Roma". Funciona en los 20 pares de operaciones
  probados, en 3 modelos de 2 empresas distintas.
- **Patching compositivo:** armamos el pensamiento **desde partes promediadas** — una base
  genérica + una parte "Italia" + una parte "capital-de" — y escribimos esa suma en una sola
  posición del residual stream. El modelo **dice "Roma"** tan seguido como acierta normalmente
  (52% contra su techo de 53%). Cambiá la parte "Italia" por "Francia" y dice "París". El
  pensamiento está hecho de partes, y las partes alcanzan para reconstruirlo.
- **La dosis importa:** con la flecha empujada 4× más fuerte de lo natural, el modelo balbucea
  en loops ("dollar dollar dollar…") — pero forzado a elegir entre las respuestas posibles,
  acierta el 80% de las veces. La sobredosis destruye la *fluidez*, no la *información*. Medio
  campo se había topado con este artefacto sin nombrarlo.

Todo esto se ve en vivo en [The Assembled Thought](https://mpodeley.github.io/assembled-thought/) —
la escena interactiva usa las salidas reales persistidas de los experimentos, nada simulado.

## La lección de rigor: los controles que podrían matarte el resultado

Y ahora la parte más importante de esta página. Intervenir es tan poderoso que **es fácil
engañarse**: metés mano adentro de un sistema de miles de millones de parámetros, algo va a
cambiar seguro. ¿Cómo sabés que tu efecto es real y no un empujón cualquiera? Con **controles
negativos** — experimentos diseñados para matar tu propio resultado:

- **Flecha aleatoria del mismo tamaño:** si cualquier empujón produjera el efecto, tu flecha no
  significa nada. (En nuestro caso: la flecha aleatoria no hace *nada*.)
- **Etiquetas permutadas:** reconstruí tus flechas con los rótulos mezclados — mismo
  procedimiento, significado destruido. Si el efecto sobrevive, tu procedimiento estaba
  midiendo otra cosa. (Efecto: cero.)
- **Piso equivocado, tarea equivocada, respuestas mezcladas:** cada variante ataca una
  explicación alternativa distinta.

Mi proyecto *nació* de esta disciplina: empezó como la réplica de un resultado ajeno que **no
sobrevivió** a los controles pareados. El hallazgo publicable apareció recién al preguntar qué
estructura *sí* sobrevivía a todos. Si te llevás una sola cosa de esta página: **una
intervención sin controles negativos es una anécdota, no un resultado.**

## Para profundizar

- [The Assembled Thought](https://mpodeley.github.io/assembled-thought/) — los experimentos de
  esta página, interactivos, con la evidencia y todos los controles enumerados.
- [Steering en Neuronpedia](https://www.neuronpedia.org) — subile el volumen a features reales
  y mirá qué pasa.
- [Persona vectors (Anthropic, 2025)](https://arxiv.org/abs/2507.21509) — steering aplicado a
  rasgos de personalidad: la misma idea, apuntada a seguridad.

**Siguiente:** con el bisturí en mano, se pueden encontrar los algoritmos completos.
[Circuitos →](circuitos.md)
