# Líneas de investigación abiertas

*Qué no sabemos todavía — con una referencia verificable por línea, al estado 2025–2026. Si
buscás proyecto, cualquiera de estas tiene versiones a escala de una persona con una GPU.*

El mapa general del campo está en
[Sharkey et al., *Open Problems in Mechanistic Interpretability*](https://arxiv.org/abs/2501.16496)
(2025, ~30 autores de todos los labs). Estas son las líneas que a mí me parecen más vivas:

## 1 · ¿Los SAEs sirven para algo, al final?

Los [sparse autoencoders](curso/sae.md) producen features hermosos — pero cuando se los compara
contra baselines simples en tareas concretas (probing, detección de conceptos), la ventaja a
veces desaparece. ¿Son la herramienta correcta o un desvío elegante? El campo está genuinamente
dividido. *Ref:* [Are Sparse Autoencoders Useful? (2025)](https://arxiv.org/abs/2502.16681).

## 2 · Grafos de atribución: escala y fidelidad

Los [attribution graphs](curso/sae.md) explican hoy una fracción de los prompts, en modelos
medianos. ¿Escalan a modelos frontera? ¿Y cómo verificamos que el grafo cuenta la historia
*verdadera* y no una racionalización plausible? *Refs:*
[Biology of an LLM](https://transformer-circuits.pub/2025/attribution-graphs/biology.html) ·
[el panorama comunitario de circuits](https://www.neuronpedia.org/graph/info).

## 3 · ¿El razonamiento en voz alta es el razonamiento real?

Los modelos "razonadores" escriben cadenas de pensamiento — pero hay evidencia de que el texto
no siempre refleja el cómputo interno que produjo la respuesta. Monitorear el razonamiento
*real* es quizás la aplicación de interp más importante para seguridad. *Ref:*
[Reasoning Models Don't Always Say What They Think (2025)](https://arxiv.org/abs/2505.05410).

## 4 · Universalidad: ¿todos los modelos piensan parecido?

¿Los mismos features y estructuras aparecen en modelos con distinto entrenamiento, distinta
empresa, distinta arquitectura? Cada caso de convergencia vuelve al hallazgo más interesante —
y hace la interp más transferible. *Ref:*
[The Platonic Representation Hypothesis (2024)](https://arxiv.org/abs/2405.07987).

## 5 · Interpretar los pesos, no (solo) las activaciones

Casi todo el campo estudia activaciones — el pensamiento en tránsito. Una línea nueva
descompone directamente los *parámetros*: encontrar los mecanismos escritos en los pesos.
*Ref:* [Attribution-based Parameter Decomposition (2025)](https://arxiv.org/abs/2501.14926).

## 6 · Steering aplicado a seguridad

Si los rasgos de comportamiento son [direcciones](curso/features.md), se pueden monitorear y
controlar: detectar cuándo un modelo se desliza hacia la adulación o la manipulación, y
corregirlo en el espacio de activaciones. *Ref:*
[Persona Vectors (2025)](https://arxiv.org/abs/2507.21509).

## 7 · Benchmarks: que los métodos compitan en serio

El campo produce métodos más rápido que maneras de compararlos. Sin evaluación estandarizada,
"mi método encuentra circuitos más lindos" no es ciencia. *Ref:*
[MIB: A Mechanistic Interpretability Benchmark (2025)](https://arxiv.org/abs/2504.13151).

## 8 · Introspección: ¿el modelo sabe qué le pasa adentro?

Si le inyectás un concepto al [residual stream](curso/transformer.md), ¿el modelo puede
*reportar* que se lo inyectaste? Los primeros experimentos dicen: a veces, de manera limitada
pero real. Un puente fascinante entre interp y la pregunta de qué "sabe" un modelo sobre sí
mismo. *Ref:*
[Emergent Introspective Awareness (Anthropic, 2025)](https://transformer-circuits.pub/2025/introspection/index.html).

## 9 · La mía: estructura composicional del residual stream

¿El estado interno factoriza en piezas reutilizables — *la cosa* y *la operación que se le
aplica* — que se pueden extraer, recombinar y reinsertar? [Mi paper](mi-investigacion.md)
muestra que sí para recuperación factual (en 3 modelos, con controles), y
[la página de futuro del sitio del paper](https://mpodeley.github.io/assembled-thought/future/)
lista nueve direcciones concretas: del model editing quirúrgico al diagnóstico causal de
errores en agentes. Conecta directo con las líneas 4 y 5 — y el siguiente paso mecanístico es
usar [circuit-tracer](https://github.com/safety-research/circuit-tracer) para encontrar *qué*
cabezas y MLPs implementan la recombinación.

---

*Los avances en estas líneas — míos y ajenos — van a ir apareciendo en el
[blog](blog/index.md).*
