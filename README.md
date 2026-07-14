# Interpretabilidad Mecanicista

Cómo piensan los modelos de lenguaje, por dentro — **en español**.

Un sitio didáctico sobre interpretabilidad mecanicista de LLMs: un curso corto en lenguaje
llano, recursos curados para aprender (videos, papers, cursos, herramientas), líneas de
investigación abiertas, y un blog donde publico lo que voy investigando.

No existe (hasta donde sabemos) ningún curso ni blog consolidado de interpretabilidad
mecanicista en español. Este sitio intenta llenar ese vacío.

Vivo: **https://mpodeley.github.io/interpretabilidad-mecanicista/**

Mi investigación: [The Assembled Thought](https://mpodeley.github.io/assembled-thought/)
(sitio interactivo del paper) · [jspace-qwen](https://github.com/mpodeley/jspace-qwen)
(código y reproducibilidad).

## Build & deploy

```bash
pip install -r requirements.txt
mkdocs serve            # preview local
mkdocs build --strict   # tiene que pasar limpio
mkdocs gh-deploy --force
```

MIT license · Matias Podeley · mpodeley@gmail.com
