# Recursos para aprender

*Curados a mano y con cada link verificado. Menos es más: esta no es una lista de todo lo que
existe, sino de lo que efectivamente conviene usar, en orden.*

Los niveles: <span class="chip ini">inicial</span> no pide matemática ni código;
<span class="chip med">medio</span> pide comodidad con Python y ganas;
<span class="chip avz">avanzado</span> son los papers fundacionales y las herramientas de
investigación.

## El camino corto (si no sabés por dónde empezar)

1. Hacé [el curso de este sitio](curso/que-es.md) (una tarde).
2. Mirá los capítulos de redes neuronales y GPT de **3Blue1Brown** (abajo).
3. Leé el **Getting Started** de Neel Nanda y hacé el capítulo 1 de **ARENA**.
4. Elegí un problema chico de los **200 Open Problems** o de [mis líneas](lineas.md), y hacé.

## Para arrancar (sin matemática)

- [**3Blue1Brown — serie de redes neuronales**](https://www.3blue1brown.com/topics/neural-networks)
  <span class="chip ini">inicial</span> — Las mejores visualizaciones que existen; los
  capítulos 5–8 cubren GPT, atención y transformers. Los primeros capítulos están
  [doblados al español en el canal oficial](https://www.youtube.com/@3blue1brownespanol); los
  de transformers, en inglés con subtítulos.
- [**Welch Labs — "The moment we stopped understanding AI"**](https://www.youtube.com/watch?v=UZDiGooFs54)
  <span class="chip ini">inicial</span> — 30 minutos que te hacen *sentir* por qué la
  interpretabilidad importa. [El canal](https://www.youtube.com/@WelchLabs) entero vale.
- [**Anthropic — Tracing the thoughts of a large language model**](https://www.anthropic.com/research/tracing-thoughts-language-model)
  <span class="chip ini">inicial</span> — El explicador sin matemática del "microscopio" de
  Anthropic; acompaña al paper más importante de 2025.
- [**Golden Gate Claude**](https://www.anthropic.com/news/golden-gate-claude)
  <span class="chip ini">inicial</span> — El experimento de steering más contable en un asado.
- [**Anthropic (video) — Interpretability: understanding how AI models think**](https://www.youtube.com/watch?v=fGKNUvivvnc)
  <span class="chip ini">inicial</span> — El equipo de interp de Anthropic conversando, sin
  filtro técnico.

## Fundamentos del campo

- [**Neel Nanda — Getting Started in Mechanistic Interpretability**](https://www.neelnanda.io/mechanistic-interpretability/getting-started)
  <span class="chip med">medio</span> — LA ruta de entrada opinionada, del referente pedagógico
  del campo. Complementos: su [glosario comprehensivo](https://www.neelnanda.io/mechanistic-interpretability/glossary)
  (el diccionario de facto) y su [canal de YouTube](https://www.youtube.com/@neelnanda2469) con
  walkthroughs de papers.
- [**200 Concrete Open Problems in Mechanistic Interpretability**](https://www.alignmentforum.org/s/yivyHaCAmMJ3CqSyj)
  <span class="chip med">medio</span> — Del 2022 y algo datada, pero sigue siendo el mejor
  generador de primeros proyectos.
- [**Distill — el hilo Circuits**](https://distill.pub/2020/circuits/) <span class="chip med">medio</span> —
  Donde nació la agenda del campo, empezando por
  [Zoom In](https://distill.pub/2020/circuits/zoom-in/). Prosa e ilustraciones ejemplares.
- [**A Mathematical Framework for Transformer Circuits**](https://transformer-circuits.pub/2021/framework/index.html)
  <span class="chip avz">avanzado</span> — El paper que formalizó el residual stream; denso y
  fundacional.
- [**In-context Learning and Induction Heads**](https://transformer-circuits.pub/2022/in-context-learning-and-induction-heads/index.html)
  <span class="chip avz">avanzado</span> — El circuito estrella (lo contamos [acá](curso/circuitos.md)).
- [**Toy Models of Superposition**](https://transformer-circuits.pub/2022/toy_model/index.html)
  <span class="chip avz">avanzado</span> — Por qué las neuronas son polisemánticas; la base
  conceptual de los SAEs.
- [**Towards Monosemanticity**](https://transformer-circuits.pub/2023/monosemantic-features/index.html) y
  [**Scaling Monosemanticity**](https://transformer-circuits.pub/2024/scaling-monosemanticity/index.html)
  <span class="chip avz">avanzado</span> — Los papers de los SAEs y del Golden Gate.
- [**On the Biology of a Large Language Model**](https://transformer-circuits.pub/2025/attribution-graphs/biology.html)
  <span class="chip avz">avanzado</span> — El insignia de 2025: grafos de atribución sobre un
  modelo de producción. [Los métodos](https://transformer-circuits.pub/2025/attribution-graphs/methods.html),
  aparte.

## Cursos y programas

- [**ARENA**](https://www.arena.education/curriculum) <span class="chip med">medio</span> — El
  curriculum práctico de referencia (transformers desde cero → interp → RL). Los materiales de
  auto-estudio viven en [learn.arena.education](https://learn.arena.education); el capítulo 1
  es interpretabilidad de transformers.
- [**BlueDot Impact**](https://bluedot.org) <span class="chip ini">inicial</span> — Cursos de
  AI safety (el ex "AI Safety Fundamentals") con cohortes facilitadas; buen marco general donde
  la interp es una pieza.
- [**MATS**](https://www.matsprogram.org) <span class="chip avz">avanzado</span> — El fellowship
  de investigación con mentores del campo (Neel Nanda entre ellos); el camino serio de
  "quiero dedicarme a esto".

## Surveys (para tener el mapa)

- [**Ferrando et al. — A Primer on the Inner Workings of Transformer-based Language Models**](https://arxiv.org/abs/2405.00208)
  <span class="chip med">medio</span> — El survey técnico de entrada; primer autor
  hispanohablante (UPC Barcelona).
- [**Sharkey et al. — Open Problems in Mechanistic Interpretability**](https://arxiv.org/abs/2501.16496)
  <span class="chip med">medio</span> — ~30 autores de todo el campo; el mejor mapa del estado
  del arte y de [lo que falta](lineas.md).
- [**Bereska & Gavves — Mechanistic Interpretability for AI Safety**](https://arxiv.org/abs/2404.14082)
  <span class="chip med">medio</span> — El survey con el ángulo de seguridad.

## Herramientas

- [**TransformerLens**](https://github.com/TransformerLensOrg/TransformerLens)
  <span class="chip med">medio</span> — LA librería para experimentos de interp en modelos
  chicos/medianos; [docs](https://transformerlensorg.github.io/TransformerLens/). Con esto se
  hizo [mi paper](mi-investigacion.md) (bueno — con hooks de PyTorch al estilo de esto).
- [**nnsight**](https://nnsight.net) <span class="chip med">medio</span> — Intervenciones sobre
  modelos locales o remotos (NDIF); tutoriales interactivos excelentes.
- [**Neuronpedia**](https://www.neuronpedia.org) <span class="chip ini">inicial</span> — El
  atlas navegable de features: buscá, mirá activaciones, hacé steering desde el navegador.
  [Docs y API](https://docs.neuronpedia.org). La demo de
  [Gemma Scope](https://www.neuronpedia.org/gemma-scope) es el mejor "tocar features" que
  existe.
- [**SAELens**](https://github.com/jbloomAus/SAELens) <span class="chip avz">avanzado</span> —
  Entrenar y analizar sparse autoencoders;
  [docs](https://decoderesearch.github.io/SAELens/).
- [**circuit-tracer**](https://github.com/safety-research/circuit-tracer)
  <span class="chip avz">avanzado</span> — Grafos de atribución open source
  ([anuncio](https://www.anthropic.com/research/open-source-circuit-tracing));
  [grafos navegables](https://www.neuronpedia.org/graph) en Neuronpedia.

## Comunidades

- [**AI Alignment Forum**](https://www.alignmentforum.org/w/interpretability-ml-and-ai) /
  [**LessWrong**](https://www.lesswrong.com/w/interpretability-ml-and-ai) — Donde el campo
  publica y discute entre papers; el tag de interpretabilidad concentra todo.
- **Open Source Mechanistic Interpretability Slack** — La comunidad de trabajo activa del área;
  el link de invitación rota, pero se mantiene actualizado en el
  [README de SAELens](https://github.com/jbloomAus/SAELens).
- [**BAISH — Buenos Aires AI Safety Hub**](https://baish.com.ar) 🇦🇷 — Comunidad de AI safety
  en Buenos Aires (UBA/Exactas): reading groups en español, cursos técnicos, becas. Si estás
  en Argentina, empezá por acá.

## En español

La razón de ser de este sitio: material *de* interpretabilidad mecanicista *en* español casi no
existe. Lo que hay:

- [**MIT Technology Review en español — "Interpretabilidad mecanicista"**](https://technologyreview.es/article/interpretabilidad-mecanicista)
  <span class="chip ini">inicial</span> — Definición divulgativa seria del término.
- [**Xataka — la cobertura del trabajo de Anthropic**](https://www.xataka.com/robotica-e-ia/ia-gran-caja-negra-que-nos-impedia-saber-como-pensaba-dentro-ahora)
  <span class="chip ini">inicial</span> — Lectura "de diario" sobre el microscopio.
- [**DotCSV**](https://www.youtube.com/@DotCSV) <span class="chip ini">inicial</span> — El
  mayor divulgador de IA en español; cubre las noticias del área (aunque no tiene, que
  sepamos, un video dedicado a interp mecanicista — todavía).
- [**3Blue1Brown Español**](https://www.youtube.com/@3blue1brownespanol)
  <span class="chip ini">inicial</span> — El doblaje oficial de la serie de redes neuronales.
- Y este sitio: [el curso](curso/que-es.md) y [el blog](blog/index.md), que es donde voy a ir
  agregando material nuevo en español.

---

*¿Falta algo que debería estar? [Escribime](mailto:mpodeley@gmail.com) — el criterio es
calidad sobre cantidad, pero la lista está viva.*
