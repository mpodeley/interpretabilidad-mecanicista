# Mi investigación

## El paper

**Operator–Operand Factorization in LLM Residual Streams: Causal Influence and Compositional
Sufficiency** — Matias Podeley, enviado a **BlackboxNLP 2026** (co-ubicado con EMNLP,
Budapest).

[:material-cube-outline: Sitio interactivo del paper](https://mpodeley.github.io/assembled-thought/){ .md-button .md-button--primary }
[:material-file-document: PDF](https://mpodeley.github.io/assembled-thought/assets/paper.pdf){ .md-button }
[:material-github: Código y reproducibilidad](https://github.com/mpodeley/jspace-qwen){ .md-button }

**En una frase:** el "pensamiento" de un modelo de lenguaje sobre un hecho — *la capital de
Italia* — está hecho de **piezas separables** (la cosa, y la pregunta que se le hace), y las
piezas alcanzan: se pueden extraer promediando, recombinar, escribir de vuelta adentro del
modelo… y el modelo **dice la respuesta** tan seguido como acierta normalmente. Con la pieza
"Francia" en lugar de "Italia", dice *París*.

**Por qué está bueno** (más allá del resultado): cada afirmación convive con el control
negativo que podría haberla matado — flechas aleatorias, etiquetas permutadas, dominios donde
la estructura *no* aparece (aritmética, lógica). De hecho el proyecto nació de una réplica que
**falló**: el resultado ajeno que quería reproducir no sobrevivió a los controles pareados, y
el paper salió de preguntar qué estructura sí sobrevivía. Esa historia está contada como
lección de rigor en [la página de intervenciones del curso](curso/intervenciones.md).

**Para jugar:** el [sitio del paper](https://mpodeley.github.io/assembled-thought/) tiene la
escena interactiva donde ensamblás un pensamiento desde sus piezas y leés la salida real del
modelo — nada simulado — más la evidencia completa, la explicación para cualquier persona, y
[las líneas que abre](https://mpodeley.github.io/assembled-thought/future/).

## Qué sigue

Lo que vaya investigando — el análisis con circuit-tracer de *qué* piezas implementan la
recombinación, extensiones a otros dominios, réplicas de resultados ajenos — va a ir
apareciendo en el [blog](blog/index.md), con código y datos. La [línea 9 de la página de
líneas](lineas.md) es el índice vivo de esta agenda.

## Citar

```bibtex
@misc{podeley2026operator,
  title  = {Operator--Operand Factorization in LLM Residual Streams:
            Causal Influence and Compositional Sufficiency},
  author = {Podeley, Matias},
  year   = {2026},
  url    = {https://mpodeley.github.io/assembled-thought/},
  note   = {Code: https://github.com/mpodeley/jspace-qwen}
}
```
